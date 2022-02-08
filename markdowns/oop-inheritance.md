<a name='0'></a>

# Object Oriented Programming(OOP) - Inheritance

Contents:

- [How to Create a Child Class from a Parent Class](#1)
- [Addind New Data and Methods to a Child Class](#2)
- [Method Overriding](#3)
- [Checking if Child Class Belongs to Parent Class](#4)
- [Class Methods, Class Attributes, Static Methods](#5)
- [Final Notes¶](#6)
    

Real world objects that are in the same class/category share similar behaviors. OOP classes can also have things in common where rather than creating new classes, classes can be inherited from other class.

Also, similar to how we write a normal functions once and reuse them multiple times without having to recreate them again, we can inherit methods and attributes of the parent class using inheritance. 


Inheritance is an OOP based techniques that refers to `parent-child relationship` where a child class can be inherited from the parent class. The child class will have the access of data and methods of the parent class (but not the other way).

Inheritance is essentially deriving a new class(child class) from an existing class(parent class). A parent class is also called base class or super class, while the child class is called derived class.

<a name='1'></a>

## 1. How to Create a Child Class from a Parent Class

When deriving a child class, you simply define the parent class in the child class. Below is a syntax for inheritance:


```python
class ChildClassName(ParentClassName):
    .
    .
    .
    .
    .
    .
    .
    
    <statements>
```

If you simply want the child class to inherit all data and method attributes without adding or overriding any method of the parent class, simply do the following:


```python
class ChildClassName(ParentClassName):
    pass
```

Let's take a real example. But we will create a parent class first.


```python
class Vehicle:
    
    def __init__ (self, brandmaker, model, speed):
        
        self.brandmaker = brandmaker
        self.model = model
        self.speed = speed
        
    def speed_up(self, add_speed):
        
        new_speed = self.speed + add_speed
        
        return new_speed
    
    def vehicle_info(self):
        
        print(f"Vehicle Info:\n \
            Current Speed: {self.speed}\n \
            Vehicle Model: {self.model}\n \
            Vehicle Maker: {self.brandmaker}")
```

From the `Vehicle` class, we can derive a new child class `Bicycle`. If we only want to inherit all data and method attributes, all we have to do is to `pass`.


```python
class Car(Vehicle):
    pass
```


```python
car = Car('Tesla', 'Model S', 40)
car.vehicle_info()
```

    Vehicle Info:
                 Current Speed: 40
                 Vehicle Model: Model S
                 Vehicle Maker: Tesla


A child class inherited from the parent class will have an access to all parent class data and method attributes but if the child class have its own data and methods attributes, they can not be accessed in the parent class. It's only one direction.

<a name='2'></a>

## 2. Adding New Data and Methods to a Child Class

In addition to the inherited data and method attributes, it's possible to add new data and methods to the class.

To automatically get the access to the data and methods of the parent class, we can use the `super()` function. Below we use `super` for accessing the initialized parent class data through `__init__` method, but it can be used for almost any method.


```python
class Car(Vehicle):
    
    def __init__(self, brandmaker, model, speed): #__init__ method is overriden: more on method overriding later
        super().__init__(brandmaker, model, speed) #use super() to automatically get the data and methods of parent class
    
    def speed_down(self, down_speed): #speed_down is a new method, down_speed is a new data/variable
        
        speed = self.speed + down_speed
        
        return speed
```


```python
car = Car('Tesla', 'Model S', 40)
car.speed_down(20)
```




    60



<a name='3'></a>

## Method Overriding

A derived or child class inherits all methods of the parent class or base class. But there are times you may want to override the methods of the parent class in child class. All you have to do is to define the methods that have the same name as the parent class. Such method will be overriden!

We saw that for __init__ method but let's demonstrate it for normal method.


```python
class Bicycle(Vehicle):
    
    def vehicle_info(self):
        
        print(f"Bicycle Info:\n \
            Current Speed: {self.speed}\n \
            Bicycle Model: {self.model}\n \
            Bicycle Maker: {self.brandmaker}")
```


```python
bicycle = Bicycle('Bike Manufacturer', 'Model XXXX', 20)
bicycle.vehicle_info()
```

    Bicycle Info:
                 Current Speed: 20
                 Bicycle Model: Model XXXX
                 Bicycle Maker: Bike Manufacturer


You can see that the method `vehicle_info()` was overriden. A one caveat to make here is that the things we are using are only just examples that demonstrate the concepts. In the real world, inheritance is more about code reuse than following hierachies. 

<a name='3'></a>

## 3. Checking if Child Class Belongs to Parent Class

We can check if an object is a type of a given class with `isinstance()` built-in function. It will return `True` if the object belong to the class, and otherwise `False`.


```python
isinstance(car, Vehicle)
```




    True




```python
isinstance(bicycle, Vehicle)
```




    True




```python
class TempClass:
    print('Hello world')
    
class TempChild(TempClass):
    pass
```

    Hello world



```python
temp_obj = TempChild()
isinstance(temp_obj, TempClass)
```




    True




```python
isinstance(temp_obj, Vehicle)
```




    False



There is another built-in function `issubclass()` that can be used to check if the a particular child class is a subclass of a given parent class. The first argument in `issubclass()` must be a subclass and the later argument must be the parent class.


```python
issubclass(Car, Vehicle)
```




    True




```python
issubclass(Bicycle, Vehicle)
```




    True




```python
issubclass(TempChild, Vehicle)
```




    False



<a name='4'></a>

## 4. Multiple Inheritance

Python being a very unique programming language supports multiple inheritance where a new child class can be inherited from multiple parent classes.


Below is the template for inheriting from several number of parent classes:

```python

class ChildClass(ParentClass1, ParentClass2, ParentClass3, ParentClass4):
    
    #Statements
    
```

It's rare that you will need to inherit from multiple classes, but if you happen to do, check the Python [doc](https://docs.python.org/3/tutorial/classes.html#multiple-inheritance) for more. 

<a name='5'></a>

## 5. Class Methods, Class Attributes, Static Methods

Class methods are type of methods that are very specific to the class instead of the objects of the class. Class methods are represented by `@classmethod` decorator above `def` definition. The first parameter of methods is `cls` that stands for `class`.

Class methods can not access regular class methods or attributes.

Here is a template of class method:

```python

class ClassName:
    
    def regular_method(self):
        #statements
        
    @classmethod
    def class_method(cls):
        #statements
        
```

Class methods can be called without creating the object of the class.

```python
ClassName.class_method()
```

Just like class methods, class attributes are variables that are specific to the class not the objects of the class. Class attributes are like global variables, they are defined above all methods and they are not initialized in `__init_() method`.

Here is a template for class attributes:

```python
class ClassName:
    num = 0
    
    # statements
 ```

Static methods are type of methods that don't have `self` or `cls` parameter and have `@staticmethod` decorator above `def` definition. Just like class methods, static methods can not access the class methods and attributes(variables).

Below is a template for static methods:

```python
class ClassName:
    
    @staticmethod
    def static_method_name():
        #statements
        
```
Static methods are not widely used in Python. They are common in languages like Java and C++.

Inheritance, class methods and attributes, and static methods are rarely used. But it's good to know them so that you can be able to read the codes of those who still use them. Most frameworks also use them in their codebases, so it's good to know them!

<a name='6'></a>

## 6. Final Notes

Inheritance is all about code reuse and OOP is about representing the real world complex systems into software objects. Classes are extremely helpful for organizing large piece of codes but they are probably not the right option when you are building something you just want to use once, normal functions are away better and simpler option.

>Fun fact:
Python language has 250 classes. That means that most Python programs should use fewer or no class at all. Interesting [watch](https://www.youtube.com/watch?v=o9pEzgHorH0) on why you should not use class!!

### [BACK TO TOP](#0)


```python

```
