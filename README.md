# Basic Class and Object Creation
class Book:
    pass

b1 = Book()

# Adding Attributes and Methods
class book:
    def __init__(self, title):
        self.title = title

b1 = book('Brave new world')
b2 = book('War and peace')
print(b1)
print(b1.title)
print(b2.title)

# Adding More Instance Attributes and Methods
class book:
    def __init__(self, title, author, pages, price):
        self.title = title
        self.author = author
        self.pages = pages
        self.price = price
        self.__secret = "this is a secret attribute."
    
    def getprice(self):
        if hasattr(self, "_discount"):
            return self.price - (self.price * self._discount)
        else:
            return self.price
    
    def setdiscount(self, amount):
        self._discount = amount

b1 = book('Brave new world', 'JD', 234, 29.95)
b2 = book('War and peace', 'LT', 1225, 39.95)
print('price before discount', b1.getprice())
b1.setdiscount(0.30)
print('price after discount', b1.getprice())
print(b1._discount)
print(b1._book__secret)

# Comparing Object Types
class book:
    def __init__(self, title):
        self.title = title
        
class newspaper:
    def __init__(self, name):
        self.name = name

b1 = book('The book')
b2 = book('Another book')
n1 = newspaper('Newspaper 1')
n2 = newspaper('Newspaper 2')
print(type(b1))
print(type(b2))
print(type(n1))
print(type(n2))
print(type(b1) == type(b2))
print(type(b1) == type(n2))
print(isinstance(b1, book))
print(isinstance(n1, book))
print(isinstance(n1, newspaper))
print(isinstance(b1, object))
print(isinstance(n1, object))

# Class and Static Methods
class book:
    book_types = ('hardcover', 'paperback', 'ebook')
    __booklist = None
    
    @classmethod
    def getbooktypes(cls):
        return cls.book_types
    
    @staticmethod
    def getbooklist():
        if book.__booklist is None:
            book.__booklist = []
        return book.__booklist
    
    def __init__(self, title, book_type):
        self.title = title
        if book_type not in book.book_types:
            raise ValueError(f'{book_type} is not a valid book type')
        else:
            self.book_type = book_type

print(book.getbooktypes())
b3 = book("Title 2", "paperback")
thebooks = book.getbooklist()
thebooks.append(b3)
print(thebooks)

# Inheritance
class publication:
    def __init__(self, title, price):
        self.title = title
        self.price = price

class periodical(publication):
    def __init__(self, title, price, period, publisher):
        super().__init__(title, price)
        self.period = period
        self.publisher = publisher

class book(publication):
    def __init__(self, title, author, pages, price):
        super().__init__(title, price)
        self.pages = pages
        self.author = author

class magazine(periodical):
    def __init__(self, title, publisher, price, period):
        super().__init__(title, price, period, publisher)

class newspaper(periodical):
    def __init__(self, title, publisher, price, period):
        super().__init__(title, price, period, publisher)

b1 = book('Brave new world', 'AH', 311, 29.0)
n1 = newspaper('NY Times', 'NYTC', 6.0, 'Daily')
m1 = magazine('Nature', 'Springer', 5, 'Monthly')
print(b1.author)
print(n1.price)
print(m1.publisher)

# Abstract Base Class
from abc import ABC, abstractmethod

class graphic_shape(ABC):
    def __init__(self):
        super().__init__()
    
    @abstractmethod
    def calcArea(self):
        pass

class circle(graphic_shape):
    def __init__(self, radius):
        self.radius = radius
    
    def calcArea(self):
        return 3.14 * (self.radius ** 2)

class square(graphic_shape):
    def __init__(self, side):
        self.side = side
    
    def calcArea(self):
        return self.side * self.side

c = circle(10)
print(c.calcArea())

s = square(12)
print(s.calcArea())
