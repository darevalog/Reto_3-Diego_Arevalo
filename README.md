|# Inheritance and Classes in Python

This repository contains Python classes that demonstrate inheritance and class concepts.

## Repository Structure

- **classes/**: Contains the implementations of the classes.
   - `class point`: Point class to represent coordinates.
   - `class rectangle`: Rectangle class with methods to calculate area, perimeter and interference.
   - `class square`: Square class that inherits from Rectangle and adds functionality.

## Use

The "color" class was added for the sole purpose of highlighting the subtitles and ordering the data output:

```python
import os

#Limpiar la consola
os.system("cls")

class color:
    Purple = "\033[95m"
    Cyan = "\033[96m"
    Darkcyan = "\033[36m"
    Blue = "\033[94m"
    Green = "\033[92m"
    Yellow = "\033[93m"
    Red = "\033[91m"
    Bold = "\033[1m"
    Underline = "\033[4m"
    End = "\033[0m"

    def print_title(title):
        print(f"{color.Red}{color.Bold}{title.upper()}{color.End}")

    def print_subtitle(subtitle):
        print(f"{color.Cyan}{color.Bold}{subtitle}{color.End}")


class point:
    def __init__(self, x, y):
        self.x = x
        self.y = y


class Rectangle(point):
    def __init__(self, width, height, center, method):
        self.width = width
        self.height = height
        self.center = center

        if method == 1:
            self.center = point(center.x - width/2, center.y - height/2)
            self.width = width
            self.height = height
        elif method == 2:
            self.center = center
            self.width = width
            self.height = height
        elif method == 3:
            self.bottom_left = point(center.x - width/2, center.y - height/2)
            self.upper_right = point(center.x + width/2, center.y + height/2)
            self.width = (center.x + width/2) - (center.x - width/2)
            self.height = (center.y + height/2) - (center.y - height/2)

    def compute_area(self):
        print(f"\nArea: {self.width * self.height}")
    
    def compute_perimeter(self):
        print(f"\nPerimeter: {2 * (self.width + self.height)}")

    def compute_interference_point(self, point):
        if (self.center.x - self.width/2 <= point.x <= self.center.x + self.width/2) and (self.center.y - self.height/2 <= point.y <= self.center.y + self.height/2):
            print(f"\nThe point {point.x, point.y} is inside the polygon.\n")
        else:
            print(f"\nThe point {point.x, point.y} is outside the polygon.\n")


class Square(Rectangle):
    def __init__(self, side, center, method):
        super().__init__(side, side, center, method)
        self.side = side


#Creación de rectángulo con datos del usuario
color.print_title("\nCreación de rectángulo con datos del usuario")
width = float(input("\nEnter the width of the rectangle: "))
height = float(input("\nEnter the height of the rectangle: "))
x = float(input("\nEnter the x coordinate of the center: "))
y = float(input("\nEnter the y coordinate of the center: "))
method = int(input("\nEnter the method to create the rectangle (1, 2 or 3): "))
center = point(x, y)
r = Rectangle(width, height, center, method)
r.compute_area()
r.compute_perimeter()
if method == 1:
    print(f"\nLower corner: {r.center.x , r.center.y}\n")
elif method == 2:
    print(f"\nCenter point: {r.center.x , r.center.y}\n")
elif method == 3:
    print(f"\nOpposite corners: Lower corner = {r.bottom_left.x , r.bottom_left.y} and upper corner = {r.upper_right.x , r.upper_right.y}\n")

#Punto de interferencia con datos del usuario para rectangulo
color.print_title("\nPunto de interferencia con datos del usuario")
x = float(input("\nEnter the x coordinate of the point: "))
y = float(input("\nEnter the y coordinate of the point: "))
p = point(x, y)
r.compute_interference_point(p)

#Creación de cuadrado con datos del usuario
color.print_title("\n\n\n\nCreación de cuadrado con datos del usuario")
side = float(input("\nEnter the side of the square: "))
x = float(input("\nEnter the x coordinate of the center: "))
y = float(input("\nEnter the y coordinate of the center: "))
method = int(input("\nEnter the method to create the square (1, 2 or 3): "))
center = point(x, y)
s = Square(side, center, method)
s.compute_area()
s.compute_perimeter()
if method == 1:
    print(f"\nLower corner: {s.center.x , s.center.y}\n")
elif method == 2:
    print(f"\nCenter point: {s.center.x , s.center.y}\n")
elif method == 3:
    print(f"\nOpposite corners: Lower corner = {s.bottom_left.x , s.bottom_left.y} and upper corner = {s.upper_right.x , s.upper_right.y}\n")

#Punto de interferencia con datos del usuario para cuadrado
color.print_title("\nPunto de interferencia con datos del usuario")
x = float(input("\nEnter the x coordinate of the point: "))
y = float(input("\nEnter the y coordinate of the point: "))
p = point(x, y)
s.compute_interference_point(p)
```

> :shipit: Diego Alejandro Arévalo Guevara. February 27, 2024.
