## Flask
3rd party Python library.
[Flask Documentation](https://flask.palletsprojects.com/en/2.2.x/api/?highlight=session#flask.session)

{% highlight Python linenos %}
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")

def index():
	name = request.args["name"]
	return render_template("index.html")
	
{% endhighlight %}

{% highlight HTML linenos %}
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        hello, {{ name }}
    </body>
</html>
{% endhighlight %}

### Jinja
a language for Flask to use placeholders in html pages.
[Jinja Documentation](https://jinja.palletsprojects.com/en/3.1.x/)

{% highlight Python linenos %}
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")

def index():
	name = request.args["name"]
	return render_template("index.html", placeholder=name)
	
{% endhighlight %}

{% highlight HTML linenos %}
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        hello, {{ placeholder }}
    </body>
</html>
{% endhighlight %}

a list can cause of problem, so use .get

{% highlight Python linenos %}
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")

def index():
							#reaquest, default
	name = request.args.get("name", "world")
	return render_template("index.html", placeholder=name)
	
{% endhighlight %}

Using a form is more standard.

{% highlight HTML linenos %}
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        <form action="/greet" methd="get">
			<input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
			<button type="submit">Greet</button>
		</form>
    </body>
</html>
{% endhighlight %}

Use Jinja to create an .html template. (*Could have used this last week instead of jQuery*)

{% highlight HTML linenos %}
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
{% endhighlight %}

{% highlight HTML linenos %}
{% extends "layout.html" %}

{% block body %}

    <form action="/greet" method="get">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>

{% endblock %}
{% endhighlight %}

### Post
{% highlight HTML linenos %}
{% extends "layout.html" %}

{% block body %}

    <form action="/greet" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>

{% endblock %}
{% endhighlight %}
Hides the special requests sent in the URL

{% highlight Python linenos %}
# Uses a single route

from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        return render_template("greet.html", name=request.form.get("name", "world"))
    return render_template("index.html")
{% endhighlight %}


### SQL integration
{% highlight Python linenos %}
# Implements a registration form, storing registrants in a SQLite database, with support for deregistration

from cs50 import SQL
from flask import Flask, redirect, render_template, request

app = Flask(__name__)

db = SQL("sqlite:///froshims.db")

SPORTS = [
    "Basketball",
    "Soccer",
    "Ultimate Frisbee"
]


@app.route("/")
def index():
    return render_template("index.html", sports=SPORTS)


@app.route("/deregister", methods=["POST"])
def deregister():

    # Forget registrant
    id = request.form.get("id")
    if id:
        db.execute("DELETE FROM registrants WHERE id = ?", id)
    return redirect("/registrants")


@app.route("/register", methods=["POST"])
def register():

    # Validate submission
    name = request.form.get("name")
    sport = request.form.get("sport")
    if not name or sport not in SPORTS:
        return render_template("failure.html")

    # Remember registrant
    db.execute("INSERT INTO registrants (name, sport) VALUES(?, ?)", name, sport)

    # Confirm registration
    return redirect("/registrants")


@app.route("/registrants")
def registrants():
    registrants = db.execute("SELECT * FROM registrants")
    return render_template("registrants.html", registrants=registrants)
{% endhighlight %}

{% highlight HTML linenos %}
#INDEX
{% extends "layout.html" %}

{% block body %}
    <h1>Register</h1>
    <form action="/register" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        {% for sport in sports %}
            <input name="sport" type="radio" value="{{ sport }}"> {{ sport }}
        {% endfor %}
        <button type="submit">Register</button>
    </form>
{% endblock %}
{% endhighlight %}

{% highlight HTML linenos %}
#REGISTRANTS
{% extends "layout.html" %}

{% block body %}
    <h1>Registrants</h1>
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Sport</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            {% for registrant in registrants %}
                <tr>
                    <td>{{ registrant.name }}</td>
                    <td>{{ registrant.sport }}</td>
                    <td>
                        <form action="/deregister" method="post">
                            <input name="id" type="hidden" value="{{ registrant.id }}">
                            <button type="submit">Deregister</button>
                        </form>
                    </td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
{% endblock %}
{% endhighlight %}

## Sessions
{% highlight HTML linenos %}
Set-Cookie: session=value

Cookie: session=value
{% endhighlight %}

{% highlight Python linenos %}
from flask import Flask, redirect, render_template, request, session
from flask_session import Session

# Configure app
app = Flask(__name__)

# Configure session
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)


@app.route("/")
def index():
    return render_template("index.html", name=session.get("name"))


@app.route("/login", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        session["name"] = request.form.get("name")
        return redirect("/")
    return render_template("login.html")


@app.route("/logout")
def logout():
    session.clear()
    return redirect("/")
{% endhighlight %}

### Shopping Cart
{% highlight Python linenos %}
from cs50 import SQL
from flask import Flask, redirect, render_template, request, session
from flask_session import Session

# Configure app
app = Flask(__name__)

# Connect to database
db = SQL("sqlite:///store.db")

# Configure session
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)


@app.route("/")
def index():
    books = db.execute("SELECT * FROM books")
    return render_template("books.html", books=books)


@app.route("/cart", methods=["GET", "POST"])
def cart():

    # Ensure cart exists
    if "cart" not in session:
        session["cart"] = []

    # POST
    if request.method == "POST":
        book_id = request.form.get("id")
        if book_id:
            session["cart"].append(book_id)
        return redirect("/cart")

    # GET (?) gets from []
    books = db.execute("SELECT * FROM books WHERE id IN (?)", session["cart"])
    return render_template("cart.html", books=books)
{% endhighlight %}

### Shows / SQL searching
{% highlight Python linenos %}
# Searches for shows using LIKE

from cs50 import SQL
from flask import Flask, render_template, request

app = Flask(__name__)

db = SQL("sqlite:///shows.db")


@app.route("/")
def index():
    return render_template("index.html")


@app.route("/search")
def search():
    shows = db.execute("SELECT * FROM shows WHERE title LIKE ?", "%" + request.args.get("q") + "%")
    return render_template("search.html", shows=shows)
{% endhighlight %}

## Ajax
asynchronies query and response to create responsive searching from the database as the user types.

### API
functions as an API to the local "*server*".

#### JSON
the most likely form of implementation. Formatted and standardized.

