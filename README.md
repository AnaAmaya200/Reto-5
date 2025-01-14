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
Notese el método de importación entre ellos 

```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
```python

```
