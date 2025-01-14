# Reto-5
Cree un paquete con todo el código de la clase Shape, este ejercicio debe realizarse de dos maneras: 
- Un módulo único dentro del paquete Shape. 
- Los módulos individuales que importan Shape heredan de él.

Para esto iniciamos generando un esquema que nos permita enteneder como vamos a realizar el paquete

## Parte 1

```
Reto 5.1/
│
├── main.py
│
└── paquete/
    │
    ├── __init__.py
    │
    └── shape.py

```
siguiendo este esquema empezamos con el código.
En shape metemos el código del reto anterior (no lo copiaremos en esta ocasión)

lo que cambia es el main. Sin embargo todo el código está disponible en el Zip reto 5.1 disponible en este repositorio.
Note el cambio importante en como se importa el paquete yadefinido de shape:
```python
import math
import paquete.shape as shape


bottom_left_corner_rect = shape.Point(0, 0)
upper_right_corner_rect = shape.Point(4, 3)
    
bottom_left_corner_square = shape.Point(0, 0)
upper_right_corner_square = shape.Point(3, 3)
    

rect = shape.Rectangle(bottom_left_corner_rect, upper_right_corner_rect)
square = shape.Square(bottom_left_corner_square, upper_right_corner_square)

print(f"El rectángulo tiene área de {rect.compute_area():.2f} y perímetro de {rect.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {rect.compute_inner_angles()}")
    
print ("\n")

print(f"El cuadrado tiene área de {square.compute_area():.2f} y perímetro de{square.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {square.compute_inner_angles()}")

print ("\n")

p1 = shape.Point(0, 0)
p2 = shape.Point(4, 0)
p3 = shape.Point(2, 4)
p4 = shape.Point(3, 0)
p5 = shape.Point(3, 3)

triangle = shape.Triangle(p1, p2, p3)
isosceles = shape.Isosceles(p1, p2, p3)
equilateral = shape.Equilateral(p1, shape.Point(4, 0), shape.Point(2, math.sqrt(12)))
scalene = shape.Scalene(p1, p4, p5)
trirectangle = shape.Trirectangle(p1, p2, shape.Point(4, 3))

 

print(f"El triangulo inicial tiene un perímetro de {triangle.compute_perimeter():.2f}")

print ("\n")

print(f"El triangulo isosceles tiene un área de {isosceles.compute_area():.2f}, un perímetro de {isosceles.compute_perimeter():.2f}")

print(f"Sus ángulos internos son {isosceles.compute_inner_angles()}")
    
print ("\n")
print(f"El triangulo equilátero tiene un área de {equilateral.compute_area():.2f}, un perímetro de {equilateral.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {equilateral.compute_inner_angles()}")

print ("\n")

print(f"El triangulo escaleno tiene un área de {scalene.compute_area():.2f}, un perímetro de  {scalene.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {scalene.compute_inner_angles()}")

print ("\n")
print(f"El triangulo rectángulo tiene un área de {trirectangle.compute_area():.2f}, un perímetro de {trirectangle.compute_perimeter():.2f}")

```
## Resultado
```python
El rectángulo tiene área de 12.00 y perímetro de 14.00
Sus ángulos internos son [90, 90, 90, 90]


El cuadrado tiene área de 9.00 y perímetro de12.00
Sus ángulos internos son [90, 90, 90, 90]


El triangulo inicial tiene un perímetro de 12.94


El triangulo isosceles tiene un área de 35.98, un perímetro de 12.94
Sus ángulos internos son [53.15748233594751, 63.42125883202625, 63.42125883202623]


El triangulo equilátero tiene un área de 6.93, un perímetro de 12.00
Sus ángulos internos son [60, 60, 60]


El triangulo escaleno tiene un área de 4.50, un perímetro de  10.24
Sus ángulos internos son [45.035650716454285, 45.035650716454285, 89.92869856709143]


El triangulo rectángulo tiene un área de 10.00, un perímetro de 12.00
```

## Parte 2

```
Reto 5.2/
│
├── main.py
│
└── paquete/
    │
    ├── __init__.py
    │
    ├── Point.py
    │
    ├── Line.py
    │
    ├── Rectangle.py
    │
    ├── Triangle.py
    │
    ├── Shape.py
    │
    ├── RectangleTypes/
    │   ├── __init__.py
    │   └── Square.py
    │
    └── TriangleTypes/
        ├── __init__.py
        ├── Isosceles.py
        ├── Scalene.py
        ├── Trirectangle.py
        └── Equilateral.py

```
Ahora, en esta sección es más importante la jerarquía del código y como lo vamos planteando, especialmente la importación de los módulos. a continuación encontrará cada uno de los módulos por separado y al final el máin que los ejecuta.
Esta estructura de distribución está disponible en el Zip Reto 5.2 disponible en el repositorio.
Notese el método de importación entre ellos:

```python
#Point.py
class Point:
  def __init__(self, x=0.0, y=0.0):
    self.x = float(x) 
    self.y = float(y)
  def compute_distance(self, point:"Point"):
    return ((self.x - point.x)**2+(self.y - point.y)**2)**(0.5)

```
```python
#Line.py
from paquete.Point import Point
class Line:
  def __init__(self,start: Point,end: Point):
    self.start = start
    self.end = end
  def compute_length(self):
    self.length = (round(Point.compute_distance(self.start, self.end),2))
    return self.length
```
```python
#Shape.py

class Shape:
  def __init__(self):
    self.is_regular = None
    self.vertices = []
    self.edges = []
    self.inner_angles = []
  def compute_area(self):
    pass
  def compute_perimeter(self):
    pass
  def compute_inner_angles(self):
    pass


```
```python
#Triangle.py
from paquete.Shape import Shape
from paquete.Line import Line


class Triangle(Shape):
  def __init__(self, Bottom_left_corner, Bottom_right_corner, Upper_corner):
    super().__init__()
    self.is_regular = False
    self.vertices.append(Bottom_left_corner)
    self.vertices.append(Bottom_right_corner)
    self.vertices.append(Upper_corner)
    self.edges.append(Line(Bottom_left_corner,Bottom_right_corner))
    self.edges.append(Line(Bottom_right_corner,Upper_corner))
    self.edges.append(Line(Upper_corner,Bottom_left_corner))
  def compute_perimeter(self):
    return Line.compute_length(self.edges[0]) + Line.compute_length(self.edges[1]) + Line.compute_length(self.edges[2])
  
```
```python
#Rectangle.py
from paquete.Shape import Shape
from paquete.Line import Line
from paquete.Point import Point

class Rectangle(Shape):
    def __init__(self, bottom_left_corner, upper_right_corner):
        super().__init__()
        self.is_regular = False
        bottom_right_corner = Point(upper_right_corner.x, bottom_left_corner.y)
        upper_left_corner = Point(bottom_left_corner.x, upper_right_corner.y)
        self.vertices.append(bottom_left_corner)
        self.vertices.append(upper_left_corner)
        self.vertices.append(upper_right_corner)
        self.vertices.append(bottom_right_corner)
        self.edges.append(Line(bottom_left_corner, upper_left_corner))
        self.edges.append(Line(upper_left_corner, upper_right_corner))
        self.edges.append(Line(upper_right_corner, bottom_right_corner))
        self.edges.append(Line(bottom_right_corner, bottom_left_corner))
    
    def compute_area(self):
        return self.edges[0].compute_length() * self.edges[1].compute_length()

    def compute_perimeter(self):
        return (2 * self.edges[0].compute_length()) + (2 * self.edges[1].compute_length())

    def compute_inner_angles(self):
        self.inner_angles = [90] * 4
        return self.inner_angles



```
```python
#Square.py
from paquete.Rectangle import Rectangle

class Square(Rectangle):
  def __init__(self, Bottom_left_corner, Upper_right_corner):
    super().__init__(Bottom_left_corner, Upper_right_corner)
    self.is_regular = True
  def compute_area(self):
    return super().compute_area()
  def compute_inner_angles(self):
    return super().compute_inner_angles()

```
```python
#Equilateral.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle


class Equilateral(Triangle):
  def __init__(self, Bottom_left_corner, Bottom_right_corner, Upper_corner):
    super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
    self.is_regular = True

  def compute_area(self):
    return (((Line.compute_length(self.edges[0]))**2)*math.sqrt(3))/4
  
  def compute_perimeter(self):
    return super().compute_perimeter()
  
  def compute_inner_angles(self):
    self.compute_inner_angles = [60]*3
    return self.compute_inner_angles 

```
```python
#Isosceles.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle

class Isosceles(Triangle):
  def __init__(self, Bottom_left_corner, Bottom_right_corner, Upper_corner):
    super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)

  def compute_area(self):
    h = ((Line.compute_length(self.edges[1]))**2+(Line.compute_length(self.edges[0])**2))**1/2
    return (Line.compute_length(self.edges[0])*h)/2
  
  def compute_perimeter(self):
    return super().compute_perimeter()
  
  def compute_inner_angles(self):
        
        A = math.degrees(math.acos(((Line.compute_length(self.edges[1]))**2 + (Line.compute_length(self.edges[2]))**2 - (Line.compute_length(self.edges[0]))**2) / (2 * (Line.compute_length(self.edges[1])) * (Line.compute_length(self.edges[2])))))
        B = math.degrees(math.acos(((Line.compute_length(self.edges[0]))**2 + (Line.compute_length(self.edges[2]))**2 - (Line.compute_length(self.edges[1]))**2) / (2 * (Line.compute_length(self.edges[0])) * (Line.compute_length(self.edges[2])))))
        C = 180 - A - B
        
        self.inner_angles.append(A) 
        self.inner_angles.append(B) 
        self.inner_angles.append(C) 
 
        return self.inner_angles

```
```python
#Scalene.py
import math
from paquete.Line import Line
from paquete.Triangle import Triangle



class Scalene(Triangle):
  def __init__(self, Bottom_left_corner, Bottom_right_corner, Upper_corner):
    super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)
  
  def compute_perimeter(self):
    return super().compute_perimeter()
  
  def compute_area(self):
        s = self.compute_perimeter() / 2 
        c = Line.compute_length(self.edges[2])
        return math.sqrt(s * (s - Line.compute_length(self.edges[0])) * (s - (Line.compute_length(self.edges[1]))) * (s - (Line.compute_length(self.edges[2]))))
    
  def compute_inner_angles(self):

        
        A = math.degrees(math.acos(((Line.compute_length(self.edges[1]))**2 + (Line.compute_length(self.edges[2]))**2 - (Line.compute_length(self.edges[0]))**2) / (2 * (Line.compute_length(self.edges[1])) * (Line.compute_length(self.edges[2])))))
        B = math.degrees(math.acos(((Line.compute_length(self.edges[0]))**2 + (Line.compute_length(self.edges[2]))**2 - (Line.compute_length(self.edges[1]))**2) / (2 * (Line.compute_length(self.edges[0])) * (Line.compute_length(self.edges[2])))))
        C = 180 - A - B
        
        self.inner_angles.append(A)
        self.inner_angles.append(B)
        self.inner_angles.append(C)
        return self.inner_angles

```
```python
#Trirectangle.py
import math
import paquete.Line as Line
from paquete.Line import Line
from paquete.Triangle import Triangle


class Trirectangle(Triangle):
  def __init__(self, Bottom_left_corner, Bottom_right_corner, Upper_corner):
    super().__init__(Bottom_left_corner, Bottom_right_corner, Upper_corner)

  def compute_perimeter(self):
    return super().compute_perimeter()
  
  def compute_area(self):
    if self.vertices[1].y == self.vertices[2].y :
      return (Line.compute_length(self.edges[0])* Line.compute_length(self.edges[1]))/2
    else:
      return (Line.compute_length(self.edges[0])* Line.compute_length(self.edges[2]))/2
    
  def compute_inner_angles(self):
    a = 90
    if self.vertices[1].y == self.vertices[2].y :
      b = math.atan(Line.compute_length(self.edges[1])/ Line.compute_length(self.edges[0]))
    else:
      b = math.atan(Line.compute_length(self.edges[2])/ Line.compute_length(self.edges[0]))
    c = a - b
    self.inner_angles.append(a)
    self.inner_angles.append(b)
    self.inner_angles.append(c)
```
Ahora el main que lo ejecuta todo.
Notese las importaciones, aquí es donde más se ve el uso de paquetes
```python
#main.py
import math
import paquete.Point as Point
import paquete.Rectangle as Rectangle
import paquete.Triangle as Triangle
import paquete.RectangleTypes.Square as Square
import paquete.TriangleTypes.Equilateral as Equilateral
import paquete.TriangleTypes.Isosceles as Isosceles
import paquete.TriangleTypes.Scalene as Scalene
import paquete.TriangleTypes.Trirectangle as Trirectangle


bottom_left_corner_rect = Point.Point(0, 0)
upper_right_corner_rect = Point.Point(4, 3)
    
bottom_left_corner_square = Point.Point(0, 0)
upper_right_corner_square = Point.Point(3, 3)
    

rect = Rectangle.Rectangle(bottom_left_corner_rect, upper_right_corner_rect)
square = Square.Square(bottom_left_corner_square, upper_right_corner_square)

print(f"El rectángulo tiene área de {rect.compute_area():.2f} y perímetro de {rect.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {rect.compute_inner_angles()}")
    
print ("\n")

print(f"El cuadrado tiene área de {square.compute_area():.2f} y perímetro de{square.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {square.compute_inner_angles()}")

print ("\n")

p1 = Point.Point(0, 0)
p2 = Point.Point(4, 0)
p3 = Point.Point(2, 4)
p4 = Point.Point(3, 0)
p5 = Point.Point(3, 3)

triangle = Triangle.Triangle(p1, p2, p3)
isosceles = Isosceles.Isosceles(p1, p2, p3)
equilateral = Equilateral.Equilateral(p1, Point.Point(4, 0), Point.Point(2, math.sqrt(12)))
scalene = Scalene.Scalene(p1, p4, p5)
trirectangle = Trirectangle.Trirectangle(p1, p2, Point.Point(4, 3))

 

print(f"El triangulo inicial tiene un perímetro de {triangle.compute_perimeter():.2f}")

print ("\n")

print(f"El triangulo isosceles tiene un área de {isosceles.compute_area():.2f}, un perímetro de {isosceles.compute_perimeter():.2f}")

print(f"Sus ángulos internos son {isosceles.compute_inner_angles()}")
    
print ("\n")
print(f"El triangulo equilátero tiene un área de {equilateral.compute_area():.2f}, un perímetro de {equilateral.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {equilateral.compute_inner_angles()}")

print ("\n")

print(f"El triangulo escaleno tiene un área de {scalene.compute_area():.2f}, un perímetro de  {scalene.compute_perimeter():.2f}")
print(f"Sus ángulos internos son {scalene.compute_inner_angles()}")

print ("\n")
print(f"El triangulo rectángulo tiene un área de {trirectangle.compute_area():.2f}, un perímetro de {trirectangle.compute_perimeter():.2f}")
print(f"Sus ángulos internos son de {trirectangle.compute_inner_angles()}")


```
##RESULTADO
```python
El rectángulo tiene área de 12.00 y perímetro de 14.00
Sus ángulos internos son [90, 90, 90, 90]


El cuadrado tiene área de 9.00 y perímetro de12.00
Sus ángulos internos son [90, 90, 90, 90]


El triangulo inicial tiene un perímetro de 12.94


El triangulo isosceles tiene un área de 35.98, un perímetro de 12.94
Sus ángulos internos son [53.15748233594751, 63.42125883202625, 63.42125883202623]


El triangulo equilátero tiene un área de 6.93, un perímetro de 12.00
Sus ángulos internos son [60, 60, 60]


El triangulo escaleno tiene un área de 4.50, un perímetro de  10.24
Sus ángulos internos son [45.035650716454285, 45.035650716454285, 89.92869856709143]


El triangulo rectángulo tiene un área de 10.00, un perímetro de 12.00
```

