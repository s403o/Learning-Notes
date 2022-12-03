# INDEX

- [INDEX](#index)
  - [OOP](#oop)
    - [Object-Oriented Design Principles](#object-oriented-design-principles)
      - [Modularity Principle](#modularity-principle)
      - [Abstraction Principle](#abstraction-principle)
      - [Encapsulation Principle](#encapsulation-principle)
  - [Classes](#classes)
    - [The `self` Identifier](#the-self-identifier)
    - [constructor](#constructor)
    - [Python’s Built-In Classes](#pythons-built-in-classes)
    - [Operator and Function Overloading in Custom Python Classes](#operator-and-function-overloading-in-custom-python-classes)
    - [Class Methods](#class-methods)
    - [Attributes (Class Data Members)](#attributes-class-data-members)
  - [Inheritance](#inheritance)
    - [Abstract Base Classes](#abstract-base-classes)
  - [Encapsulation](#encapsulation)
  - [Shallow and Deep Copying](#shallow-and-deep-copying)

---

## OOP

**Object Oriented Programming**: is an approach to programming that involves modeling things into python objects. These objects can contain both `data` and `functionality` all wrapped-up together into a reusable component

The main “actors” in the object-oriented paradigm are called objects. Each object is an instance of a class. Each class presents to the outside world a concise and consistent view of the objects that are instances of this class

![instance](./img/oop-instance.png)

### Object-Oriented Design Principles

![oop principles](./img/oop-principles.png)

#### Modularity Principle

- Modern software systems typically consist of several different components that must interact correctly in order for the entire system to work properly. Keeping these interactions straight requires that these different components be well organized.
- Modularity refers to an organizing principle in which different components of a software system are divided into separate functional units (modules).
- This is particularly relevant in a study of **data structures**, which can typically be designed with sufficient abstraction and generality to be reused in many applications.

#### Abstraction Principle

- The notion of abstraction is to distill a complicated system down to its most fundamental parts. Typically, describing the parts of a system involves naming them and explaining their functionality.
- Applying the abstraction paradigm to the design of data structures gives rise to abstract data types (**ADTs**).
  - An ADT is a mathematical model of a data structure that specifies the type of data stored, the operations supported on them, and the types of parameters of the operations.
  - An ADT **specifies what each operation does, but not how it does it**.
- Python has a tradition of treating abstractions implicitly using a mechanism known as **"duck typing"**. As an interpreted and dynamically typed language, there is no “compile time” checking of data types in Python, and no formal requirement for declarations of abstract base classes. Instead programmers assume that an object supports a set of known behaviors, with the interpreter raising a run-time error if those assumptions fail.
  - > The description of this as “duck typing” comes from an adage attributed to poet James Whitcomb Riley, stating that “when I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck.”
- Python supports abstract data types using a mechanism known as an **abstract base class (ABC)**. An abstract base class cannot be instantiated (i.e., you cannot directly create an instance of that class), but it defines one or more common methods that all implementations of the abstraction must have. An ABC is realized by one or more concrete classes that inherit from the abstract base class while providing implementations for those method declared by the `ABC`.

#### Encapsulation Principle

- Different components of a software system should not reveal the internal details of their respective implementations.
- One of the main advantages of encapsulation is that it gives one programmer freedom to implement the details of a component, without concern that other programmers will be writing code that intricately depends on those internal decisions.
- It allows the implementation details of parts of a program to change without adversely affecting other parts, thereby making it easier to fix bugs or add new functionality with relatively local changes to a component.
- Python provides only loose support for encapsulation. By convention, names of members of a class (both data members and member functions) that start with a single underscore character (e.g., **`_secret`**) are assumed to be nonpublic and should not be relied upon.

---

## Classes

![class](./img/oop-class.png)

- Use meaningful names for identifiers:
  - Classes (other than Python’s built-in classes) should have a name that serves as a singular noun, and should be capitalized (e.g., `Date` rather than date or `Dates`). When multiple words are concatenated to form a class name, they should follow the so-called **“CamelCase” convention** in which the first letter of each word is capitalized (e.g., `CreditCard`).
  - Identifiers that represent a value considered to be a constant are traditionally identified using all capital letters and with underscores to separate words (e.g., `MAX_SIZE`).
  - identifiers in any context that begin with a single leading underscore (e.g., `_secret`) are intended to suggest that they are only for “internal” use to a class or module, and not part of a public interface.
  - Functions, including **member functions** of a class, should be lowercase. If multiple words are combined, they should be separated by underscores (e.g., `make_payment`). The name of a function should typically be a verb that describes its affect. However.
    - if the only purpose of the function is to `return` a value, the function name may be a noun that describes the value (e.g., `sqrt` rather than `calculate_sqrt`).

---

### The `self` Identifier

Each instance from a class must maintain its own properties & methods. Therefore, each instance stores its own instance variables to reflect its current state.

> **`self`** identifies the instance upon which a method is invoked

- when using a class-method that is called with one parameter, for example, as my `card.charge(200)`. The interpreter automatically **binds the instance upon which the method is invoked to the `self` parameter**.

---

### constructor

it initializes the data members of the class when an object of class is created by calling the specially-named `__init__` method that serves as the constructor of the class

- **"Dender" (double underScore) init method** `__init__()` which is a reserved method called when an object is created, It's responsible for establishing the **state** of a newly created instance object with appropriate instance variables

```py
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age
    self.hobbies = []
```

- The process of creating a new instance of a class is known as instantiation. In general, the syntax for **instantiating** an object is to invoke the `constructor` of a class.

  ```py
  # instantiating
  p1 = Person("John", 36) # Object definition
  ```

---

### Python’s Built-In Classes

- A class is **"immutable"** if each object of that class has a fixed value upon instantiation that cannot subsequently be changed. For example, the `float` class is immutable. Once an instance has been created, its value cannot be changed
- Commonly used built-in classes for Python:
  ![built-in-classes](./img/built-in-classes.png)

---

### Operator and Function Overloading in Custom Python Classes

![Operator and Function Overloading in Custom Python Classes](./img/Operator-and-Function-Overloading-in-Custom-Python-Classes_Watermarked.webp)

- If you’ve used the `+` or `*` operator on a `str` object in Python, you must have noticed its different behavior when compared to `int` or `float` objects:
- You might have wondered how the same built-in operator or function shows different behavior for objects of different classes. This is called `operator overloading` or `function overloading` respectively.
- By default, the `+` operator is undefined for a new class. However, the author of a class may provide a definition using a technique known as operator overloading. This is done by implementing a specially named method. In particular, the `+` operator is overloaded by implementing a method named `"__add__"` , which takes the right-hand operand as a parameter and which returns the result of the expression. That is, the syntax, `a+b`, is converted to a method call on object a of the form, "a.`__add__`(b)".

> When a binary operator is applied to two instances of different types, as in **3 \* "love me"** , Python gives deference to the class of the left operand. In this example, it would effectively check if the int class provides a sufficient definition for how to multiply an instance by a string, via the `__mul__` method. However, if that class does not implement such a behavior, Python checks the class definition for the right-hand operand, in the form of a special method named `__rmul__` (i.e., “right multiply”). This provides a way for a new user-defined class to support mixed operations that involve an instance of an existing class (given that the existing class would presumably not have defined a behavior involving this new class).

---

### Class Methods

- Adding a method: `get_full_name()` method is used to return string

  ```py
  class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age

    def get_full_name(self):
        return f'Person({self.first_name},{self.last_name},{self.age})'

    john = Person('John', 'Sam', 36)
    print(john.get_full_name())
  ```

- **Class Method**
  - here we use the decorator **"`@`"**
    ![class-methods](./img/class-methods.png)

---

### Attributes (Class Data Members)

As an object-oriented language, Python provides two scopes for attributes: **class attributes** and **instance attributes**.

- **class attribute**
  ![class-attribute](./img/class-attributes.png)
  - is a Python variable that belongs to a class rather than a particular object. It is shared between all the objects of this class and it is defined outside the constructor function, **init**(self,...), of the class.
  - all instances of the class will have the same value of that attribute
  - defined outside the constructor.
- **instance attribute**
  - is a Python variable belonging to one, and only one, object. This variable is only accessible in the scope of this object and it is defined inside the constructor function, `__init__(self,..)` of the class.
  - defined inside the constructor.

A `class-level data member` is often used when there is some value, such as a constant, that is to be shared by all instances of a class. In such a case, it would be unnecessarily wasteful to have each instance store that value in its instance namespace.

---

## Inheritance

A natural way to organize various structural components of a software package is in a **hierarchical** fashion, with similar abstract definitions grouped together in a level-by-level manner that goes from specific to more general as one traverses up the hierarchy. An example of such a hierarchy is shown in the Figure. Using mathematical notations, the set of `houses` is a **subset** of the set of buildings, but a **superset** of the set of `ranches`. The correspondence between levels is often referred to as an **“is a” relationship**, as a house is a building, and a `ranch` is a `house`.

![inheritance](./img/oop-inheritance3.png)

- In object-oriented programming, the mechanism for a modular and hierarchical organization is a technique known as **inheritance**.
- This allows a new class to be defined based upon an existing class as the starting point.
- In object-oriented terminology, the existing class is typically described as the **base class**, **parent class**, or **superclass**, while the newly defined class is known as the **subclass** or **child class**.
- There are two ways in which a subclass can differentiate itself from its superclass. A subclass may specialize an existing behavior by providing a new implementation that overrides an existing method. A subclass may also extend its superclass by providing brand new methods.
- The mechanism for calling the inherited constructor relies on the syntax, `super()`
  - it calls the `__init__` method that was inherited from the superclass

![inheritance](./img/oop-inheritance.png)
![inheritance](./img/oop-inheritance2.png)

---

### Abstract Base Classes

In classic object-oriented terminology, we say a class is an abstract base class if its only purpose is to serve as a base class through inheritance. More formally, an **"abstract base class"** is one that cannot be directly instantiated, while a **"concrete class"** is one that can be instantiated.

> Python’s collections module provides several abstract base classes that assist when defining custom data structures that share a common interface with some of Python’s built-in data structures. These rely on an object-oriented software design pattern known as the **template method pattern**

---

## Encapsulation

- it's grouping of variables and functions of a specific concept in a single component, named **class**
- in `c++`, `java`, this concept is more loaded with **hiding** things from outsiders
  - but `python` has another philosophy: **trust other programmers**
  - Python does not support formal access control, but names beginning with a `single underscore (_)` are conventionally akin to **protected**, while names beginning with a `double underscore (__)` (other than special methods) are akin to **private**.

---