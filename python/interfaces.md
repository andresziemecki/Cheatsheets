# Python Interfaces

Interfaces in Python are handled differently than in most other languages, and they can vary in their design complexity

At a high level, an interface acts as a blueprint for designing classes. Like classes, interfaces define methods. Unlike classes, these methods are abstract. An `abstract method` is one that the interface simply defines. It doesn’t implement the methods. This is done by classes, which then implement the interface and give concrete meaning to the interface’s abstract methods.

Python’s approach to interface design is somewhat different when compared to languages like Java, Go, and C++. These languages all have an interface keyword, while Python does not. Python further deviates from other languages in one other aspect. It doesn’t require the class that’s implementing the interface to define all of the interface’s abstract methods.

# Informal Intercaces

In certain circumstances, you may not need the strict rules of a formal Python interface. Python’s dynamic nature allows you to implement an informal interface. An informal Python interface is a class that defines methods that can be overridden, but there’s no strict enforcement.

``` python
class InformalParserInterface:
    def load_data_source(self, path: str, file_name: str) -> str:
        """Load in the file for extracting text."""
        pass

    def extract_text(self, full_file_name: str) -> dict:
        """Extract text from the currently loaded file."""
        pass
```

As you can see, `InformalParserInterface` looks identical to a standard Python class. You rely on duck typing to inform users that this is an interface and should be used accordingly.

To use your interface, you must create a concrete class. A concrete class is a subclass of the interface that provides an implementation of the interface’s methods.

To check if a class accomplish an interface we can use the following:

``` python
issubclass(className, InterfaceName)
```

Checking the method resolution order (MRO) of classes interface implementation tells you the superclasses of the class in question, as well as the order in which they’re searched for executing a method. You can view a class’s MRO by using the dunder method `cls.__mro__`

``` python
className.__mro__
(__main__.className, __main__.InterfaceName, object) 
# order of execution of its method, if in className doesnt exist, will execute the interfaceName (which do nothing)
```

Such informal interfaces are fine for small projects where only a few developers are working on the source code.

# Metaclasses

Ideally, you would want issubclass(EmlParser, InformalParserInterface) to return False when the implementing class doesn’t define all of the interface’s abstract methods. And add this to the testing phase.

To do this, you’ll create a metaclass and overriding two dunder methods:

``` python
.__instancecheck__()
.__subclasscheck__()
```

Like the following:

``` python
class ParserMetaclass(type):
    """A Parser metaclass that will be used for parser class creation.
    """
    def __instancecheck__(cls, instance):
        return cls.__subclasscheck__(type(instance))

    def __subclasscheck__(cls, subclass):
        return (hasattr(subclass, 'method1') and 
                callable(subclass.method1) and 
                hasattr(subclass, 'method2') and 
                callable(subclass.method2))


class classInterface(metaclass=ParserMetaclass):
    """This interface is used for concrete classes to inherit from.
    There is no need to define the ParserMeta methods as any class
    as they are implicitly made available via .__subclasscheck__().
    """
    pass
```

Running issubclass() on your concrete classes will produce the desire output.

If we have a look at the MRO:

``` python
className.__mro__
(<class '__main__.className'>, <class 'object'>)
```
As you can see, `classInterface` is a superclass of `className`, but it doesn’t appear in the MRO. This unusual behavior is caused by the fact that `classInterface` is a virtual base class of `className`.

## Using Virtual Base Classes

I didn't understand a shit -> [link](https://realpython.com/python-interface/)

# Formal Interfaces

We have seen informal interface. In order to create a formal Python interface, you’ll need a few more tools from Python’s abc module.

## Using abc.ABCMeta

To enforce the subclass instantiation of abstract methods, you’ll utilize Python’s builtin ABCMeta from the abc module.

Rather than create your own metaclass, you’ll use abc.ABCMeta as the metaclass. Then, you’ll overwrite .__subclasshook__() in place of .__instancecheck__() and .__subclasscheck__(), as it creates a more reliable implementation of these dunder methods.

``` python
import abc

class FormalParserInterface(metaclass=abc.ABCMeta):
    @classmethod
    def __subclasshook__(cls, subclass):
        return (hasattr(subclass, 'load_data_source') and 
                callable(subclass.load_data_source) and 
                hasattr(subclass, 'extract_text') and 
                callable(subclass.extract_text))

class PdfParserNew:
    """Extract text from a PDF."""
    def load_data_source(self, path: str, file_name: str) -> str:
        """Overrides FormalParserInterface.load_data_source()"""
        pass

    def extract_text(self, full_file_path: str) -> dict:
        """Overrides FormalParserInterface.extract_text()"""
        pass

class EmlParserNew:
    """Extract text from an email."""
    def load_data_source(self, path: str, file_name: str) -> str:
        """Overrides FormalParserInterface.load_data_source()"""
        pass

    def extract_text_from_email(self, full_file_path: str) -> dict:
        """A method defined only in EmlParser.
        Does not override FormalParserInterface.extract_text()
        """
        pass
```

If you run issubclass() on PdfParserNew and EmlParserNew, then issubclass() will return True and False, respectively.

## Using abc to Register a Virtual Subclass

Didn't understand a shit

## Using Subclass Detection With Registration

Didn't understand a shit

# Using Abstract Method Declaration

Finally, this is the last and the most important one.

An abstract method is a method that’s declared by the Python interface, but it may not have a useful implementation. The abstract method must be overridden by the concrete class that implements the interface in question.

``` python
import abc

class FormalParserInterface(metaclass=abc.ABCMeta):
    @classmethod
    def __subclasshook__(cls, subclass):
        return (hasattr(subclass, 'load_data_source') and 
                callable(subclass.load_data_source) and 
                hasattr(subclass, 'extract_text') and 
                callable(subclass.extract_text) or 
                NotImplemented)

    @abc.abstractmethod
    def load_data_source(self, path: str, file_name: str):
        """Load in the data set"""
        raise NotImplementedError

    @abc.abstractmethod
    def extract_text(self, full_file_path: str):
        """Extract text from the data set"""
        raise NotImplementedError

class PdfParserNew(FormalParserInterface):
    """Extract text from a PDF."""
    def load_data_source(self, path: str, file_name: str) -> str:
        """Overrides FormalParserInterface.load_data_source()"""
        pass

    def extract_text(self, full_file_path: str) -> dict:
        """Overrides FormalParserInterface.extract_text()"""
        pass

class EmlParserNew(FormalParserInterface):
    """Extract text from an email."""
    def load_data_source(self, path: str, file_name: str) -> str:
        """Overrides FormalParserInterface.load_data_source()"""
        pass
```

In the above example, you’ve finally created a formal interface that will raise errors when the abstract methods aren’t overridden

``` python
>>> pdf_parser = PdfParserNew()
>>> eml_parser = EmlParserNew()
Traceback (most recent call last):
  File "real_python_interfaces.py", line 53, in <module>
    eml_interface = EmlParserNew()
TypeError: Can't instantiate abstract class EmlParserNew with abstract methods extract_text
```

