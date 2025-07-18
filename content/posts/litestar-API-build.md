+++
tags = ['API', 'Litestar', 'Build Notes', 'Python', 'SQL']
title = 'Litestar & SQLAlchemy REST API'
date = 2025-07-18T10:40:07+01:00
draft = false
+++

**REPO:** [https://github.com/pbrazeale/litestar_REST_API](https://github.com/pbrazeale/litestar_REST_API)

This project is a simple To-Do List REST API built with the [Litestar](https://litestar.dev/) and [SQLAlchemy 2.0](https://www.sqlalchemy.org/). It serves as a practical example for understanding core concepts like dependency injection, database transaction management, and Dockerization in a modern Python web application.

This project was originally based on the excellent [Litestar tutorial by Teclado](https://www.youtube.com/watch?v=o8gWK1wqro0) and has been expanded to highlight key development patterns and lessons learned.

## Features

- **Create To-Do Items**: `POST /todo`
- **List All To-Do Items**: `GET /todos`
- **Async First**: Built with `asyncio` and `asyncpg` / `aiosqlite`.
- **Database Integration**: Uses SQLAlchemy 2.0 ORM with Litestar's plugin.
- **Data Validation**: Leverages Litestar's DTOs, built on Pydantic.
- **Containerized**: Fully configured to run with Docker.
- **Interactive API Docs**: Automatic Swagger UI at `/schema/swagger`.

## Lessons Learned & Key Concepts

This project demonstrates several important patterns for building robust APIs.

### 1. Explicit vs. Implicit Transaction Management

A critical part of a database application is managing transactions (commit/rollback). The Litestar SQLAlchemy plugin offers two ways to do this, and using both simultaneously will cause an error.

- **Implicit Method (Plugin-driven):** The plugin can automatically commit the session before sending a response using the `autocommit_before_send_handler`. This is simple but hides the transaction logic.
- **Explicit Method (Dependency-driven):** You can define a dependency that wraps your handler in a transaction block (`async with db_session.begin():`). This is more verbose but makes the transaction boundaries clear and explicit in your code.

**This repository uses the explicit method, as it is generally preferred for clarity and easier debugging.**

The `provide_transaction` dependency manages the session lifecycle. Note how it also includes `try...except` to catch specific database errors and convert them into a clean HTTP response.

```python
# app.py

async def provide_transaction(
    db_session: AsyncSession,
) -> AsyncGenerator[AsyncSession, None]:
    try:
        # This block starts a transaction and automatically
        # commits it if the block succeeds, or rolls it back
        # if an exception occurs.
        async with db_session.begin():
            yield db_session
    except IntegrityError as exc:
        # Catches database integrity errors (e.g., duplicate primary key)
        # and returns a user-friendly HTTP 409 Conflict error.
        raise ClientException(
            status_code=HTTP_409_CONFLICT,
            detail=str(exc),
        ) from exc

# To make this work, we MUST remove the autocommit handler from the plugin config.
# This prevents a "double commit" error.

db_config = SQLAlchemyAsyncConfig(
    connection_string="sqlite+aiosqlite:///db.sqlite",
    # ...
    # before_send_handler=autocommit_before_send_handler, # <-- THIS LINE IS REMOVED
)

app = Litestar(
    # ...
    dependencies={"transaction": provide_transaction},
    # ...
)
```

### 2. Data Transfer Objects (DTOs)

Litestar uses DTOs to control how data is serialized (outgoing responses) and deserialized (incoming requests). In this project, `WriteDTO` prevents a client from being able to specify the `id` of a new To-Do item, as the database should generate it.

```python
# app.py

class WriteDTO(SQLAlchemyDTO[ToDo]):
    # This config tells the DTO to ignore the 'id' field
    # when processing incoming data for creating a new ToDo.
    config = SQLAlchemyDTOConfig(exclude={"id"})

@post("/todo", dto=WriteDTO)
async def create_todo(data: ToDo, transaction: AsyncSession) -> ToDo:
    # 'data' is an instance of the ToDo model, created from
    # the request payload, with the 'id' field excluded.
    transaction.add(data)
    await transaction.flush() # Flushes to the DB to get the generated ID
    return data
```
