--- 
title: Aprendizaje básico
summary: Sintaxis básica.
authors:
    - Revisión autorizada
    - Jose Robledano
date: 2026-09-11
---
# Sintaxis básica del lenguaje Python

Python es un lenguaje de programación sencillo y legible. El código fuente se
escribe mediante instrucciones que el intérprete ejecuta en orden.

## Código fuente y texto normal

El código Python debe escribirse entre comillas invertidas para distinguirlo
del texto normal.

Por ejemplo, la siguiente instrucción muestra un mensaje:

````python
print("Hola, mundo")
````

El resultado de ejecutar la instrucción es:

````text
Hola, mundo
````

Los nombres de funciones, variables y palabras reservadas forman parte del
código fuente. Los comentarios comienzan con el carácter `#` y no se ejecutan:

````python
# Este es un comentario
print("Mensaje mostrado por Python")
````

## Uso de Python en un fichero

El código Python se puede guardar en un fichero con extensión `.py`. Por
ejemplo, el fichero `saludo.py` puede contener:

````python
nombre = "Ana"
print(f"Hola, {nombre}")
````

Para ejecutar el fichero desde la terminal de Windows:

````powershell
python saludo.py
````

También puede ser necesario utilizar el lanzador `py`:

````powershell
py saludo.py
````

La salida será:

````text
Hola, Ana
````

### Variables y tipos de datos

Una variable almacena un valor. Python determina automáticamente su tipo:

````python
nombre = "Ana"       # Cadena de texto
edad = 25            # Número entero
altura = 1.68        # Número decimal
es_estudiante = True # Valor booleano
````

Los tipos más habituales son:

- `str`: texto.
- `int`: números enteros.
- `float`: números decimales.
- `bool`: valores `True` o `False`.

El tipo de un valor puede consultarse con `type()`:

````python
print(type(nombre))
print(type(edad))
````

### Operadores básicos

Python permite realizar operaciones matemáticas:

````python
suma = 3 + 2
resta = 3 - 2
producto = 3 * 2
division = 3 / 2
potencia = 3 ** 2
resto = 3 % 2
````

También se pueden comparar valores:

````python
print(edad >= 18)
print(nombre == "Ana")
````

Los operadores lógicos principales son `and`, `or` y `not`:

````python
puede_acceder = edad >= 18 and es_estudiante
````

### Entrada y salida

La función `input()` permite solicitar datos al usuario. El resultado siempre
es texto, por lo que puede ser necesario convertirlo:

````python
nombre = input("Escribe tu nombre: ")
edad = int(input("Escribe tu edad: "))

print(f"{nombre} tiene {edad} años.")
````

### Condicionales

Las instrucciones `if`, `elif` y `else` permiten ejecutar código dependiendo
de una condición. La indentación es obligatoria:

````python
edad = 20

if edad >= 18:
    print("Es mayor de edad")
else:
    print("Es menor de edad")
````

### Bucles

El bucle `for` recorre una secuencia:

````python
for numero in range(1, 4):
    print(numero)
````

El bucle `while` se repite mientras se cumpla una condición:

````python
contador = 0

while contador < 3:
    print(contador)
    contador += 1
````

### Listas

Una lista almacena varios valores:

````python
frutas = ["manzana", "pera", "uva"]

print(frutas[0])
frutas.append("naranja")

for fruta in frutas:
    print(fruta)
````

Los índices comienzan en `0`.

### Funciones

Una función agrupa instrucciones reutilizables:

````python
def saludar(nombre):
    return f"Hola, {nombre}"

mensaje = saludar("Ana")
print(mensaje)
````

## Uso de Python en la consola interactiva

La consola interactiva permite ejecutar instrucciones inmediatamente. Se inicia
desde PowerShell con:

````powershell
python
````

También puede utilizarse:

````powershell
py
````

A continuación se pueden introducir instrucciones directamente:

````python
>>> 2 + 3
5
>>> print("Hola desde la consola")
Hola desde la consola
````

Para salir de la consola:

````python
>>> exit()
````

En Windows también se puede pulsar `Ctrl+Z` y después `Enter`.

La consola es útil para realizar pruebas rápidas y consultar el funcionamiento
de expresiones sencillas.

## Uso de Python en un cuaderno Jupyter Notebook

Jupyter Notebook permite combinar texto, código y resultados en un documento
interactivo. Para instalarlo:

````powershell
python -m pip install notebook
````

Para iniciar Jupyter Notebook:

````powershell
jupyter notebook
````

También puede iniciarse mediante:

````powershell
python -m notebook
````

En un cuaderno, el código se escribe en celdas. Una celda de código puede
contener:

````python
nombre = "Ana"
print(f"Hola, {nombre}")
````

Al ejecutar la celda se muestra:

````text
Hola, Ana
````

Las celdas de texto utilizan Markdown. Por ejemplo:

````markdown
# Título

Este es un texto explicativo.

- Primer elemento
- Segundo elemento
````

Los cuadernos suelen guardarse con la extensión `.ipynb`.

### Orden de ejecución

Las variables de un cuaderno permanecen disponibles después de ejecutar una
celda. Por ejemplo, primero se puede ejecutar:

````python
numero = 10
````

Y posteriormente:

````python
print(numero * 2)
````

Si las celdas se ejecutan en un orden diferente, pueden producirse errores o
resultados inesperados. Cuando sea necesario, se puede reiniciar el núcleo
del cuaderno y ejecutar todas las celdas de nuevo.

## Recomendaciones iniciales

- Utilizar nombres descriptivos para las variables.
- Mantener una indentación de cuatro espacios.
- Escribir comentarios cuando ayuden a comprender el código.
- Ejecutar pequeñas partes del programa para detectar errores.
- Guardar los ficheros Python con extensión `.py`.
- Usar celdas Markdown en Jupyter para documentar los ejemplos.
