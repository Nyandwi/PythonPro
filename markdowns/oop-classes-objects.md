# Object Oriented Programming (OOP) - Classes and Objects

Object Oriented Programming(OOP) is a programming paradigm or feature that allows developers to structure programs into classes and objects. OOP gives the developers the ability to design programs around data.

Classes are new data type that you can create yourself. Objects can be created from the Class. A typical class has two components: `fields` (or variables) that store data and `methods`(or functions) that operate on those data. Python [glossary](https://docs.python.org/3/glossary.html) defines class as a template for creating user defined objects and object
as any data with state(attribute or value) and defined behavior(methods).

With the simplicity of Python and the thousands of features it provides that can be used on the fly, the majority of Python developers doesn't need to use OOP. However, it is important to understand OOP so that you can understand when and when not to use it. OOP provides modularity and reusability. Take an example: Python list is a built-in object. Imagine how many time you(and other millions of coders) use list with different data!! That's extreme reusability!!

When should you use class or function? This is a hard questions, but generally if you found yourself using a number of functions over and over on same data, then you should consider using class for reusability. If on the otherhand you are creating a class with methods that you will use once, it's probably better to use normal functions. Here is a great talk about that: [Stop Using Classes ](https://www.youtube.com/watch?v=o9pEzgHorH0) by Jack Diederich. You can also learn more about the critism of OOP [here](https://en.wikipedia.org/wiki/Object-oriented_programming#Criticism).

Also, if you plan to build an API(Application Protocol Interface) one day, it's very likely that you will need to structure data and methods in a systematic way. So, OOP is an important thing to know. 

In Python, everything is an `object` and has a `type`. OOP gives us the power to create our custom object of a given data type that can be manipulated. Below is an example of how everything in Python is an object of a certain type.


```python
# In Python, everything is an object of a given type

my_list = [1, 2, 3, 4]

type(my_list)
```




    list



The type of Python `list` is a `type` too. This is the same thing for other objects such as `str` and  `dict`. The `type` of `type` object is a `type` too :)


```python
type(list)
```




    type




```python
type(str)
```




    type




```python
type(type)
```




    type



There is a popular notion that OOP allows developers to represent real world objects into software objects. To some extent, this is true. Real world objects contain state and behavior. Take an example of a car object: The state of a car might be price, model, car maker, speed while the behavior might be changing the gear, applying the brake, etc...). 

Software objects provide an abstraction of the real world objects. Software objects store their states in data attributes(or variables), and they expose their behaviors through method attributes(or functions). Methods act on the state of the objects. Java documentation has a great explaination of class and objects in  the contexts of the real world objects. For more, check it [here](https://docs.oracle.com/javase/tutorial/java/concepts/object.html).


Let's see how to create a class in Python.

### Creating a Class in Python

Classes are user defined objects. That signal that there are built-in classes that we use day to day contained in some [standard libraries](https://docs.python.org/3/tutorial/stdlib.html). Take an example for a `list`. A list is a class. When we create a list object, we can manipulate it in different ways.


```python
# Creating a list object, 
# The data [1,2,3] is an instance of the list

my_list = [1, 2, 3]

# We can manipulate the list object

my_list.append(4)

print(my_list)
```

    [1, 2, 3, 4]


Below is a simple user defined class:

```python
class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'
```

When creating a new class:
* We specity its class name. It is common to use Capital letters for defining the class like `ClassName`. This style is called `CamelCase`. 

```python

class ClassName:
    ## Class attributes
    
```

* We define the class attributes(data and methods). Data attributes are data (or variables) that makes up the class and the methods are like functions that operate on data. Methods only work with class. 

* We use a special method `__init__` to initialize the data attributes. `__init__` method starts and ends with double underscore(`__`). When passing data to the init method, the first paremeter must be `self`. There are other special methods beyond `__init__`.

```python

class ClassName:
    
    def __init__(self, x, y):
```
    

* We use `self` as the first parameter for any method that we define in the class. With the exception of `self` parameter, methods are similar to normal functions. `self` parameter allows the method to use the class data attributes.

* To access the data attribute and method of an object, we use `. operator`.


```python

class ClassName:
    
    def __init__(self, var1, var2):
        self.var1 = var1
        self.var2 = var2
        
    def method_1(self, var3):
        """
        DOCSTRING
        self points to the data attributes, 
        function can take new data attribute like var3
        """
        
        #statements
        
```
Now that we understand what makes a class, let's create a real class.


```python
class Car:
    
    def __init__(self, speed, gear, model, maker):
        
        self.speed = speed
        self.gear = gear
        self.model = model
        self.maker = maker
        
    def speed_up(self, add_speed):
        
        speed = self.speed + add_speed
        
        return speed
        
    def apply_brake(self, decre_speed):
        speed = self.speed - decre_speed
        
        return speed
        
    def change_gear(self, new_gear):
        gear = new_gear
        
        return gear
    
    def car_info(self):
        
        print(f"Car Info:\n \
            Speed: {self.speed}\n \
            Model: {self.model}\n \
            Maker: {self.maker}")
```

That's an example of class. In the next section, let's see how to use the class we created.

### Using a Class

To create the instance of the object, we simply call class we created with the values of the data fields. Note that we don't pass `self` when calling the class.


```python
my_car = Car(45, 2, 'Model S', 'Tesla')
```


```python
# Accessing the data attributes

my_car.gear
```




    2




```python
my_car.speed
```




    45




```python
my_car.maker
```




    'Tesla'



To use the methods we defined in class, we do as we always do with built-in objects (ex: `my_list.append(2)`). We use `. operator` and we pass the variables that make up a particular method. Note that we don't use `self` when calling the methods defined in the class.


```python
my_car.apply_brake(10)

# Should return speed - 10 = 45 - 10 = 35
```




    35




```python
my_car.speed_up(20)
```




    65




```python
my_car.change_gear(4)
```




    4




```python
my_car.car_info()
```

    Car Info:
                 Speed: 45
                 Model: Model S
                 Maker: Tesla


When you print `my_car` object(created from class `Car`), you don't see the information about the class other than that it is an object. 


```python
print(my_car)
```

    <__main__.Car object at 0x10371c2b0>


To choose what will be diplayed when we print the object, we can define a `__str__` method inside the class. The `__str__` method must return a string. Otherwise, you will get an error.


```python
class Car:
    
    def __init__(self, speed, gear, model, maker):
        
        self.speed = speed
        self.gear = gear
        self.model = model
        self.maker = maker
        
    def speed_up(self, add_speed):
        
        speed = self.speed + add_speed
        
        return speed
        
    def apply_brake(self, decre_speed):
        speed = self.speed - decre_speed
        
        return speed
        
    def change_gear(self, new_gear):
        gear = new_gear
        
        return gear
    
    def car_info(self):
        
        print(f"Car Info:\n \
            Speed: {self.speed}\n \
            Model: {self.model}\n \
            Maker: {self.maker}")
    def __str__(self):
        
        return f"This is the object created from class Car. The car model {self.model} was made by {self.maker}"
```


```python
my_car = Car(45, 2, 'Model X', 'Tesla')
print(my_car)
```

    This is the object created from class Car. The car model Model X was made by Tesla


The methods `__str__` and `__init__` are examples of special or magic methods. Python special methods allows us to overload(or to imitate) built-in operators so that we can use them in our objects just like built-in data types. Magic methods are unique to Python and they are not found in other OOP languages such as Java and C++. We will learn more about magic methods later. 

You can find all magics methods on [Python Documentation](https://docs.python.org/3/reference/datamodel.html#basic-customization).

One last thing: we can use `isinstance()` to check if the object `my_car` is a Car type.


```python
isinstance(my_car, Car)
```




    True



### Final Notes and Further Learning

The central idea of OOP is creating user-defined objects. With OOP, you can create structured and systematic programs. OOP provides modularity and code reusability which are essential ingredients for building large scale programs.

In the next parts, we will learn about inheritance and special or magic methods.

You can learn more about OOP and classes and Objects at:

* OOP, Lecture 8 of [MIT 6.0001 Introduction to Computer Science and Programming in Python](https://www.youtube.com/watch?v=-DP1i2ZU9gk)
* [Python Doc](https://docs.python.org/3/tutorial/classes.html)
* [Wikipedia, OOP](https://en.wikipedia.org/wiki/Object-oriented_programming)
* [Stop Using Classes](https://www.youtube.com/watch?v=o9pEzgHorH0)


```python

```
