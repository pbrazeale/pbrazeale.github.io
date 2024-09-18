## OOP (Object-Oriented Programming)
### Step 1 of creating an OOP
{% highlight python linenos %}
def main():
    name = get_name()
    house = get_house()
    print(f"{name} from {house}")


def get_name():
    return input("Name: ")


def get_house():
    return input("House: ")


if __name__ == "__main__":
    main()
{% endhighlight %}
Where the name and house variables are now defined by using separate functions, and those functions could be used again in the future. 

### Tuple
*"A tuple is a sequences of values. Unlike a list, a tuple can’t be modified. In spirit, we are returning two values."*
{% highlight python linenos %}
def main():
    student = get_student()
    print(f"{student[0]} from {student[1]}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return (name, house)


if __name__ == "__main__":
    main()
{% endhighlight %}

### List
For when you want to allow yourself to change the values.
{% highlight python linenos %}
def main():
    student = get_student()
    if student[0] == "Padma":
        student[1] = "Ravenclaw"
    print(f"{student[0]} from {student[1]}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return [name, house]


if __name__ == "__main__":
    main()
{% endhighlight %}

### Dictionary
Has a key value pair.
{% highlight python linenos %}
def main():
    student = get_student()
    if student["name"] == "Padma":
        student["house"] = "Ravenclaw"
    print(f"{student['name']} from {student['house']}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return {"name": name, "house": house}


if __name__ == "__main__":
    main()
{% endhighlight %}

## Classes
*"Classes are a way by which, in object-oriented programming, we can create our own type of data and give them names.
A class is like a mold for a type of data – where we can invent our own data type and give them a name.
We can modify our code as follows to implement our own class called Student:"*
{% highlight python linenos %}
class Student:
    ...


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    student = Student()
    student.name = input("Name: ")
    student.house = input("House: ")
    return student


if __name__ == "__main__":
    main()
{% endhighlight %}

Convention is to make custom classes Uppercase.
### Object
Classes create an Object.

### Better way to use the Student class
{% highlight python linenos %}
class Student:
    def __init__(self, name, house):
        self.name = name
        self.house = house


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    student = Student(name, house)
    return student


if __name__ == "__main__":
    main()
{% endhighlight %}

### Raise
*"Object-oriented program encourages you to encapusulate all the functionality of a class within the class definition. What if something goes wrong? What if someone tries to type in something random? What if someone tries to create a student without a name? Modify your code as follows:"*
{% highlight python linenos %}
class Student:
    def __init__(self, name, house):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self.name = name
        self.house = house


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return Student(name, house)


if __name__ == "__main__":
    main()
{% endhighlight %}

### str
*"`__str__` is a built-in method that comes with Python classes. It just so happens that we can create our own methods for a class as well! Modify your code as follows:"*
{% highlight python linenos %}
class Student:
    def __init__(self, name, house, patronus=None):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        if patronus and patronus not in ["Stag", "Otter", "Jack Russell terrier"]:
            raise ValueError("Invalid patronus")
        self.name = name
        self.house = house
        self.patronus = patronus

    def __str__(self):
        return f"{self.name} from {self.house}"

    def charm(self):
        match self.patronus:
            case "Stag":
                return "🐴"
            case "Otter":
                return "🦦"
            case "Jack Russell terrier":
                return "🐶"
            case _:
                return "🪄"


def main():
    student = get_student()
    print("Expecto Patronum!")
    print(student.charm())


def get_student():
    name = input("Name: ")
    house = input("House: ")
    patronus = input("Patronus: ") or None
    return Student(name, house, patronus)


if __name__ == "__main__":
    main()
{% endhighlight %}

### Properties
@poperty
#### Decorators
{% highlight python linenos %}
    # Getter for house
    @property
    def house(self):
        return self._house

    # Setter for house
    @house.setter
    def house(self, house):
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self._house = house

{% endhighlight %}
*"Notice how we’ve written `@property` above a function called `house`. Doing so defines `house` as a property of our class. With `house` as a property, we gain the ability to define how some attribute of our class, `_house`, should be set and retrieved. Indeed, we can now define a function called a “setter”, via `@house.setter`, which will be called whenever the house property is set—for example, with `student.house = "Gryffindor"`. Here, we’ve made our setter validate values of `house` for us. Notice how we raise a `ValueError` if the value of `house` is not any of the Harry Potter houses, otherwise, we’ll use `house` to update the value of `_house`. Why `_house` and not `house`? `house` is a property of our class, with functions via which a user attempts to set our class attribute. `_house` is that class attribute itself. The leading underscore, `_`, indicates to users they need not (and indeed, shouldn’t!) modify this value directly. `_house` should _only_ be set through the `house` setter. Notice how the `house` property simply returns that value of `_house`, our class attribute that has presumably been validated using our `house` setter. When a user calls `student.house`, they’re getting the value of `_house` through our `house` “getter”."*

Python has no private variables, which is why `_variable` is used by convention to express not to touch it, and `__variable` means for real, under no circumstance, should you touch/change the variable.

### Inheritance
- *Inheritance is, perhaps, the most powerful feature of object-oriented programming.*
- *"t just so happens that you can create a class that “inherits” methods, variables, and attributes from another class.*
- *In the terminal, execute `code wizard.py`. Code as follows:*
{% highlight python linenos %}
# by creating the wizard class, we can control inheritance being passed into Student and Professor.
class Wizard:
    def __init__(self, name):
        if not name:
            raise ValueError("Missing name")
        self.name = name

    ...


class Student(Wizard):
    def __init__(self, name, house):
	    # this is what creates the inheritance.
        super().__init__(name)
        self.house = house

    ...


class Professor(Wizard):
    def __init__(self, name, subject):
        super().__init__(name)
        self.subject = subject

    ...


wizard = Wizard("Albus")
student = Student("Harry", "Gryffindor")
professor = Professor("Severus", "Defense Against the Dark Arts")
...
{% endhighlight %}

*"Notice that there is a class above called `Wizard` and a class called `Student`. Further, notice that there is a class called `Professor`. Both students and professors have names. Also, both students and professors are wizards. Therefore, both `Student` and `Professor` inherit the characteristics of `Wizard`. Within the “child” class `Student`, `Student` can inherit from the “parent” or “super” class `Wizard` as the line `super().__init__(name)` runs the `init` method of `Wizard`. Finally, notice that the last lines of this code create a wizard called Albus, a student called Harry, and so on."*


### Inheritance and Exceptions

- *While we have just introduced inheritance, we have been using this all along during our use of exceptions.*
- *It just so happens that exceptions come in a heirarchy, where there are children, parent, and grandparent classes. These are illustrated below:*

{% highlight %}
BaseException
 +-- KeyboardInterrupt
 +-- Exception
      +-- ArithmeticError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- KeyError
      +-- NameError
      +-- SyntaxError
      |    +-- IndentationError
      +-- ValueError
 ...
{% endhighlight %}

- *You can learn more in Python’s documentation of [exceptions](https://docs.python.org/3/library/exceptions.html).*

### Operator Overloading
*Some operators such as + and - can be “overloaded” such that they can have more abilities beyond simple arithmetic.*
{% highlight python linenos %}
class Vault:
    def __init__(self, galleons=0, sickles=0, knuts=0):
        self.galleons = galleons
        self.sickles = sickles
        self.knuts = knuts

    def __str__(self):
        return f"{self.galleons} Galleons, {self.sickles} Sickles, {self.knuts} Knuts"

	# this is what overwrites the operand and allows overloading.
    def __add__(self, other):
        galleons = self.galleons + other.galleons
        sickles = self.sickles + other.sickles
        knuts = self.knuts + other.knuts
        return Vault(galleons, sickles, knuts)


potter = Vault(100, 50, 25)
print(potter)

weasley = Vault(25, 50, 100)
print(weasley)

total = potter + weasley
print(total)
{% endhighlight %}

*You can learn more in Python’s documentation of [operator overloading](https://docs.python.org/3/reference/datamodel.html#special-method-names).*
