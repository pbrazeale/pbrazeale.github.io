+++
tags = ['LLM', 'AI', 'Python', 'Articles']
title = 'ChatGPT Technical Tutor'
date = 2025-02-18T16:34:07+01:00
draft = false
+++

I've been slowly figuring out the best way to approach learning with ChatGPT that's not just give code, get back fixed code.

While that no doubt is quick and efficient, it does little toward helping me progress my own knowledge base. However, finding a way to get back sourced information--that I don't have to skim the documentation for myself--is a win!

Over the past week, I've noticed a massive improvement in the quality of feedback. Not sure if it's model upgrades on the server side, better prompting on my part, or a mixture of both.

This is by far the best result I've gotten yet!

## Prompting

**Priming Question:**
Are you familiar with the turtle module for python?

**Response:**
Yes! The `turtle` module in Python is a standard library module used for creating simple graphics and animations. It provides a way to control a turtle (a graphical pen) that moves around the screen, drawing shapes, lines, and patterns. It's often used for teaching programming concepts, especially in an interactive and visual way.

Would you like help with a specific `turtle` project or issue?

### Core Question:

Current code:

```python
import turtle as T

screen = T.Screen()
timmy = T.Turtle()


def move_forward():
    global timmy
    timmy.forward(10)


def move_backward():
    global timmy
    timmy.backward(10)


def clockwise():
    global timmy
    timmy.right(36)


def counter_clockwise():
    global timmy
    timmy.left(36)


def clear_screen():
    global screen
    screen.clear()
    main()


def main():
    global timmy, screen
    screen.listen()
    screen.onkey(key="w", fun=move_forward)
    screen.onkey(key="s", fun=move_backward)
    screen.onkey(key="d", fun=clockwise)
    screen.onkey(key="a", fun=counter_clockwise)
    screen.onkey(key="c", fun=clear_screen)

    screen.exitonclick()

main()
```

my `clear_screen()` doesn't restart with the arrow in the center of the screen. How should I go about fixing this? Please used detailed explanations and site source documentation.

### Takeaways:

1. Using a priming question to load relevant information.
2. Provide context (_whole code snippet_).
3. Explain your concern/issue `my clear_screen() doesn't restart with the arrow in the center of the screen.`
4. Ask for guidance, **not answer** `How should I go about fixing this?`
5. `Please used detailed explanations and site source documentation.`
   1. Reiterate explanation for learning purposes.
   2. `Site Sources` will keep it focused on the original priming material.

## Excellent Answer!

Your issue arises because calling `screen.clear()` only clears the screen—it does not reset the turtle's position, orientation, or reinitialize the `Turtle` instance. Additionally, calling `main()` after `clear_screen()` does not recreate the `Turtle` object, which means `timmy` is lost when `screen.clear()` is called.

## **Why Doesn’t `clear_screen()` Work as Expected?**

6. **`screen.clear()` removes everything, including the `Turtle` object.**

   - The documentation for [`clear()`](https://docs.python.org/3/library/turtle.html#turtle.clear) states that it clears the drawings but does **not** reset the turtle’s position or heading.
   - However, [`screen.clear()`](https://docs.python.org/3/library/turtle.html#turtle.Screen.clear) clears **everything** from the screen, including all turtles.

7. **The `timmy` object is lost after `screen.clear()`.**

   - Since `timmy` is created at the start of `main()`, it needs to be reinitialized after clearing the screen.

8. **The event listeners (`onkey`) may be lost after clearing the screen.**

   - `screen.clear()` removes event listeners, so `main()` needs to reassign them.

---

## **Solution: Reset the Turtle After Clearing**

Instead of calling `screen.clear()`, you can:

- Reset the turtle’s position manually.
- Reset its heading (orientation).
- Clear only the drawings (`timmy.clear()`) instead of clearing the entire screen.

### **Fixed Code:**

```python
import turtle as T

screen = T.Screen()
timmy = T.Turtle()

def move_forward():
    timmy.forward(10)

def move_backward():
    timmy.backward(10)

def clockwise():
    timmy.right(36)

def counter_clockwise():
    timmy.left(36)

def clear_screen():
    """Clears the screen and resets the turtle to the center."""
    timmy.clear()  # Clears the drawing
    timmy.penup()  # Lifts the pen to avoid drawing while moving
    timmy.home()   # Moves turtle to (0,0) and sets heading to default (East)
    timmy.pendown()  # Puts the pen down to resume drawing

def main():
    """Sets up the screen and key bindings."""
    screen.listen()
    screen.onkey(key="w", fun=move_forward)
    screen.onkey(key="s", fun=move_backward)
    screen.onkey(key="d", fun=clockwise)
    screen.onkey(key="a", fun=counter_clockwise)
    screen.onkey(key="c", fun=clear_screen)

    screen.exitonclick()

main()
```

---

## **Explanation of Fixes**

9. **Using `timmy.clear()` Instead of `screen.clear()`**

   - `screen.clear()` removes everything, but `timmy.clear()` **only clears the turtle's drawings** while keeping it active.
   - [`clear()` documentation](https://docs.python.org/3/library/turtle.html#turtle.clear) states:
     "Delete the turtle’s drawings from the screen. Do not move turtle."

10. **Using `timmy.home()` Instead of Recreating the Turtle**

    - `home()` moves the turtle to the center (`0,0`) and resets its heading to the default (east).
    - [`home()` documentation](https://docs.python.org/3/library/turtle.html#turtle.home) states:
      "Move turtle to the origin – coordinates (0,0) – and set its heading to its start orientation (east)."

11. **Using `timmy.penup()` and `timmy.pendown()` to Avoid Unwanted Drawing**

    - `penup()` prevents the turtle from drawing while repositioning.
    - `pendown()` resumes drawing once it's reset.
    - [`penup()` documentation](https://docs.python.org/3/library/turtle.html#turtle.penup) states:
      "Pull the pen up – no drawing when moving."

---

## **Alternative: If You Want a Full Reset**

If you truly need to **reset the entire screen**, you must **recreate the turtle** after clearing it:

```python
def clear_screen():
    """Fully resets the screen, including event bindings."""
    global timmy
    screen.reset()  # Resets everything (screen, turtles, events)

    timmy = T.Turtle()  # Recreate the turtle
    timmy.speed("normal")  # Optional: Set turtle speed

    main()  # Rebind keys
```

- [`screen.reset()`](https://docs.python.org/3/library/turtle.html#turtle.Screen.reset) clears the screen **and reinitializes everything**, but you must **recreate the turtle and event bindings** afterward.

---

## **Which Solution Should You Use?**

- **Use `timmy.clear()` and `timmy.home()` if you only want to clear the drawing and reset the turtle.**
- **Use `screen.reset()` if you want to completely reset the environment.**

Would you like to customize the behavior further? 😊
