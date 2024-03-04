# Reto #3 // Diego Arévalo

This repository contains Python classes that demonstrate inheritance and class concepts.

## Repository Structure

- **classes/**: Contains the implementations of the classes.
   - `class point`: Point class to represent coordinates.
   - `class rectangle`: Rectangle class with methods to calculate area, perimeter and interference.
   - `class square`: Square class that inherits from Rectangle and adds functionality.
   - `class color`: The "color" class was added for the sole purpose of highlighting the subtitles and ordering the data output.
   - `class line`: The line class creates a line from given points.

## Rectangle and square code

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

class line:
    def __init__(self, start, end):
        self.start = start
        self.end = end

class Rectangle(line):
    def __init__(self, width, height, center, method):
        super().__init__(center, center)
        self.width = width
        self.height = height
        self.center = center

        if method == 1:
            self.center = point(center.x , center.y)
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
        elif method == 4:
            self.lines = []
            self.lines.append(line(point(center.x - width/2, center.y - height/2), point(center.x + width/2, center.y - height/2)))
            self.lines.append(line(point(center.x + width/2, center.y - height/2), point(center.x + width/2, center.y + height/2)))
            self.lines.append(line(point(center.x + width/2, center.y + height/2), point(center.x - width/2, center.y + height/2)))
            self.lines.append(line(point(center.x - width/2, center.y + height/2), point(center.x - width/2, center.y - height/2)))
            
        
            

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
while True:
    method = int(input("\nEnter the method to create the rectangle (1, 2, 3 or 4): "))
    if method == 1 or method == 2 or method == 3 or method == 4:
        break
    else:
        print("\nInvalid method. Please enter a number between 1 and 4.")
        continue
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
elif method == 4:
    print(f"\nLine 1: {r.lines[0].start.x, r.lines[0].start.y} - {r.lines[0].end.x, r.lines[0].end.y}\n")
    print(f"Line 2: {r.lines[1].start.x, r.lines[1].start.y} - {r.lines[1].end.x, r.lines[1].end.y}\n")
    print(f"Line 3: {r.lines[2].start.x, r.lines[2].start.y} - {r.lines[2].end.x, r.lines[2].end.y}\n")
    print(f"Line 4: {r.lines[3].start.x, r.lines[3].start.y} - {r.lines[3].end.x, r.lines[3].end.y}\n")
    

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
while True:
    method = int(input("\nEnter the method to create the square (1, 2, 3 or 4): "))
    if method == 1 or method == 2 or method == 3 or method == 4:
        break
    else:
        print("\nInvalid method. Please enter a number between 1 and 4.")
        continue
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
elif method == 4:
    print(f"\nLine 1: {s.lines[0].start.x, s.lines[0].start.y} - {s.lines[0].end.x, s.lines[0].end.y}\n")
    print(f"Line 2: {s.lines[1].start.x, s.lines[1].start.y} - {s.lines[1].end.x, s.lines[1].end.y}\n")
    print(f"Line 3: {s.lines[2].start.x, s.lines[2].start.y} - {s.lines[2].end.x, s.lines[2].end.y}\n")
    print(f"Line 4: {s.lines[3].start.x, s.lines[3].start.y} - {s.lines[3].end.x, s.lines[3].end.y}\n")

#Punto de interferencia con datos del usuario para cuadrado
color.print_title("\nPunto de interferencia con datos del usuario")
x = float(input("\nEnter the x coordinate of the point: "))
y = float(input("\nEnter the y coordinate of the point: "))
p = point(x, y)
s.compute_interference_point(p)
```

## Line code
```python
import os
import math

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

class point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

class line(point):
    def __init__(self, start, end):
        self.start = start
        self.end = end


    def compute_length(self, start, end):
         length = ((end.x - start.x)**2 + (end.y - start.y)**2)**0.5
         rounded_length = round(length, 2)
         print(f"\nThe length of the line is: {rounded_length} unidades.")

    def compute_slope(self, start, end):
        slope = math.degrees(math.atan((end.y - start.y) / (end.x - start.x))).__round__(2)
        print(f"\nThe slope of the line from the horizontal is: {slope} degrees.")

    def compute_horizontal_cross(self, start, end):
        if start.y >= 0 and end.y <= 0 or start.y <= 0 and end.y >= 0:
            print(f"\nThe line crosses the x-axis.")
        else:
            print(f"\nThe line does not cross the x-axis.")

    def compute_vertical_cross(self, start, end):
        if start.x >= 0 and end.x <= 0 or start.x <= 0 and end.x >= 0:
            print(f"\nThe line crosses the y-axis.\n")
        else:
            print(f"\nThe line does not cross the y-axis.\n")


# Creación de línea con datos del usuario

color.print_title("\nLine crated with user data")
start_x = float(input("\nEnter the x coordinate of the start point: "))
start_y = float(input("\nEnter the y coordinate of the start point: "))
end_x = float(input("\nEnter the x coordinate of the end point: "))
end_y = float(input("\nEnter the y coordinate of the end point: "))
start = point(start_x, start_y)
end = point(end_x, end_y)
l = line(start, end)
print(f"\nStart point: {l.start.x, l.start.y}")
print(f"\nEnd point: {l.end.x, l.end.y}")
l.compute_length(start, end)
l.compute_slope(start, end) 
l.compute_horizontal_cross(start, end)
l.compute_vertical_cross(start, end)
```
## Restaurant scenario code
```python
import os
os.system("cls")

class menuitem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class  appetizer(menuitem):
    def __init__(self, name, price, calories):
        super().__init__(name, price)
        self.calories = calories

    def __str__(self):
        return f"{self.name}: ${self.price} ({self.calories} cal)"
    
class main_course(menuitem):
    def __init__(self, name, price, calories, protein):
        super().__init__(name, price)
        self.calories = calories
        self.protein = protein

    def __str__(self):
        return f"{self.name}: ${self.price} ({self.calories} cal, {self.protein} g)"

class beverage(menuitem):
    def __init__(self, name, price, volume):
        super().__init__(name, price)
        self.volume = volume

    def __str__(self):
        return f"{self.name}: ${self.price} ({self.volume} ml)"
    
class order(menuitem):
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)

    def calculate_total(self):
        total = 0
        for item in self.items:
            total += item.price
        return total

    def apply_discount(self):
        discount = 0.1
        total = self.calculate_total()
        discounted_total = total - (total * discount)
        return discounted_total

# Creación de menú
appetizer1 = appetizer("Guacamole", 5.50, 150)
appetizer2 = appetizer("Nachos", 6.50, 200)
appetizer3 = appetizer("Queso fundido", 7.50, 250)
appetizer4 = appetizer("Tostadas", 4.50, 100)
main_course1 = main_course("Tacos", 12.50, 300, 20)
main_course2 = main_course("Burrito", 10.50, 400, 25)
main_course3 = main_course("Enchiladas", 11.50, 350, 22)
main_course4 = main_course("Quesadillas", 9.50, 250, 18)
beverage1 = beverage("Margarita", 8.50, 250)
beverage2 = beverage("Tequila", 7.50, 200)
beverage3 = beverage("Soda", 2.50, 500)
beverage4 = beverage("Water", 1.50, 500)

a = "MENU"
b = a.center(50, "-")
print(b)
print("\nAppetizers:")
print(appetizer1)
print(appetizer2)
print(appetizer3)
print(appetizer4)
print("\nMain courses:")
print(main_course1)
print(main_course2)
print(main_course3)
print(main_course4)
print("\nBeverages:")
print(beverage1)
print(beverage2)
print(beverage3)
print(beverage4)
print()


# Creación de orden por input del cliente
c = "ORDERS"
d = c.center(50, "-")
print(d)

order1 = order()
order1.add_item(appetizer1)
order1.add_item(main_course1)
order1.add_item(beverage1)
print("\nORDER 1")
for item in order1.items:
    print(item)
print(f"\nTotal: ${order1.calculate_total()}\n")
print(f"Total with discount: ${order1.apply_discount()} (10% of discount)\n")

order2 = order()
order2.add_item(appetizer2)
order2.add_item(main_course2)
order2.add_item(beverage2)
print("\nORDER 2")
for item in order2.items:
    print(item)
print(f"\nTotal: ${order2.calculate_total()}\n")
print(f"Total with discount: ${order2.apply_discount()} (10% of discount)\n")

order3 = order()
order3.add_item(appetizer4)
order3.add_item(main_course4)
order3.add_item(beverage1)
print("\nORDER 3")
for item in order3.items:
    print(item)
print(f"\nTotal: ${order3.calculate_total()}\n")
print(f"Total with discount: ${order3.apply_discount()} (10% of discount)\n")
```
> :shipit: Diego Alejandro Arévalo Guevara. February 27, 2024.
