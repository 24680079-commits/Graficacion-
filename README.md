# Graficacion-

#  Introducción a Blender y uso de Scripting

Este repositorio contiene mis primeros apuntes y prácticas de la materia Graficación.
Durante estas prácticas se aprendió el uso básico de Blender, trabajando únicamente dentro del programa, tanto en la manipulación de objetos como en el uso de scripting con Python para la creación de figuras geométricas.

⸻

#  Sistema Operativo
	•	macOS

⸻

#   Herramienta Utilizada
	•	Blender
	•	Lenguaje de scripting integrado: Python (bpy)

Todo el trabajo se realizó directamente dentro de Blender, sin utilizar editores de código externos.

⸻

#  Instalación de Blender

Para realizar las prácticas fue necesario instalar Blender desde su sitio oficial.

Pasos realizados:

	1.	Ingresé al sitio oficial de Blender:
https://www.blender.org

	2.	Entré a la sección Download.
  
	3.	Descargué la versión compatible con macOS.
  
	4.	Ejecuté el instalador.
  
	5.	Finalicé la instalación.

<img width="1792" height="1120" alt="Captura de pantalla 2026-02-09 a la(s) 20 02 41" src="https://github.com/user-attachments/assets/3ffe11c0-d65a-419b-b702-b36da1383e08" />

 Interfaz inicial de Blender

Al abrir Blender, aparece una escena predeterminada que incluye:
	•	Un cubo
	•	Una cámara
	•	Una luz

Estos elementos forman la escena inicial de trabajo.

<img width="1792" height="1120" alt="Captura de pantalla 2026-02-09 a la(s) 20 04 47" src="https://github.com/user-attachments/assets/59f32867-2754-4af2-8018-f60ba0ba844b" />

Eliminación del objeto predeterminado

El profesor explicó cómo eliminar el cubo inicial de la escena.

Métodos utilizados:
	•	Seleccionar el cubo y presionar la tecla X
	•	Seleccionar el cubo y presionar Delete

Ambos métodos permiten borrar el objeto seleccionado.

<img width="534" height="315" alt="Captura de pantalla 2026-02-09 a la(s) 20 05 32" src="https://github.com/user-attachments/assets/6ba96871-73ed-4cd2-8671-78df79a628bc" />

Uso de la sección Scripting en Blender

Posteriormente se trabajó en la sección Scripting, la cual forma parte de la interfaz de Blender.

En esta sección se puede:
	•	Ejecutar instrucciones línea por línea desde la consola.
	•	Escribir código en el Text Editor.
	•	Ver los cambios reflejados directamente en la escena.

  Creación de figuras desde la consola

Desde la consola integrada en Scripting, se aprendió a:
	•	Agregar una figura
	•	Modificar su tamaño
	•	Visualizar los cambios en tiempo real

Esto permitió comprender cómo Blender responde a instrucciones escritas en Python.


  ![IMG_6645](https://github.com/user-attachments/assets/53984a1e-64c4-45da-a766-945fc00680d8)

# Creación de un polígono 2D mediante código

Finalmente, se utilizó el Text Editor dentro de la sección Scripting para escribir código en Python que permite crear un polígono en 2D.
⸻
# codigo 

```bash
import bpy
import math

#Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

def crear_poligono_2d(nombre, lados, radio):
    # Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)

    # Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)

    vertices = []
    aristas = []

    # Cálculo de vértices usando coordenadas polares a cartesianas
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))  # Z = 0 para mantenerlo en 2D

    # Definir las conexiones (aristas) entre los vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))

    # Definir la cara del polígono
    caras = [list(range(lados))]

    # Cargar los datos en la malla
    malla.from_pydata(vertices, aristas, caras)
    malla.update()
    
#Llamada a la función: Un hexágono de radio 5

crear_poligono_2d("Poligono2D", lados=8, radio=10)

```
⸻

•	Se usa la librería bpy, integrada en Blender.
	•	Se define una función para crear un polígono en 2D.
	•	Los vértices se calculan matemáticamente usando seno y coseno.
	•	El número de lados y el radio pueden modificarse.
	•	El eje Z se mantiene en 0 para conservar la figura en 2D.
	•	Como ejemplo, se genera un hexágono.
  
<img width="1792" height="1120" alt="Captura de pantalla 2026-02-09 a la(s) 20 11 58" src="https://github.com/user-attachments/assets/ee83d7eb-5703-475b-93f0-d40024009633" />

  # Conclusión

Con esta práctica se aprendió:

	•	A instalar y usar Blender.
  
	•	A trabajar con la interfaz gráfica.
  
	•	A manipular objetos en los ejes X y Y.
  
	•	A usar la sección Scripting.
  
	•	A crear figuras geométricas mediante código en Python dentro de Blender.

Este repositorio representa mis primeros trabajos en la materia de Graficación.


#  Practica 2

# Construcción de Patrón Circular (Flor de la Vida)

En esta práctica trabajé con Blender y Python (bpy) para generar una figura basada en la distribución geométrica de círculos utilizando coordenadas polares.

El objetivo fue comprender:

Conversión de coordenadas polares a cartesianas.

Distribución angular uniforme.

Uso de estructuras de control (while).

Automatización de patrones geométricos.

1. Base Matemática

Para posicionar los círculos alrededor del círculo central no utilicé coordenadas X e Y directamente.

En su lugar, utilicé coordenadas polares (r, θ) y después las convertí a coordenadas cartesianas usando:

𝑥
=
𝑟
⋅
𝑐
𝑜
𝑠
(
𝜃
)
x=r⋅cos(θ)
𝑦
=
𝑟
⋅
𝑠
𝑖
𝑛
(
𝜃
)
y=r⋅sin(θ)

En Python, como las funciones math.cos() y math.sin() trabajan en radianes, utilicé:

```bash

math.radians(angulo_actual)
```

Esto convierte los grados a radianes.

 2. Limpieza de Escena

Antes de generar la figura, limpié la escena para evitar que los objetos se encimaran en cada ejecución:
```
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```
Esto garantiza que cada vez que ejecute el script, la escena esté vacía.
<img width="1792" height="1120" alt="Captura de pantalla 2026-02-14 a la(s) 22 36 29" src="https://github.com/user-attachments/assets/5fd491da-54e0-4489-b03c-c79b7ba35895" />

 3. Definición de Parámetros

Definí las variables principales:

radio = 3
angulo_actual = 0
paso_angular = 20

radio: Tamaño del círculo.

angulo_actual: Ángulo inicial.

paso_angular: Cantidad de grados que se suman en cada iteración.

⚠ Nota: En el documento el ejemplo menciona 60°, pero en mi práctica utilicé 20° para generar mayor densidad de círculos y un patrón más complejo.

4. Creación del Círculo Central

Primero generé el círculo base en el origen:

bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

Este círculo sirve como referencia para posicionar los demás.

<img width="1792" height="1120" alt="Captura de pantalla 2026-02-14 a la(s) 22 37 46" src="https://github.com/user-attachments/assets/7fe30b61-3f0c-4d1c-88c5-a9a4de672f76" />


5. Construcción Manual Inicial

Para comprender mejor la lógica, primero generé los primeros dos círculos manualmente:
```
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
```
Después incrementé el ángulo:

angulo_actual += paso_angular

Y repetí el procedimiento.

Esto me permitió entender cómo el ángulo afecta la posición del nuevo círculo.

 6. Automatización con While

Después de entender la lógica, implementé una estructura while para evitar repetir el código manualmente.
```
while angulo_actual < 360:

```
 Lógica del ciclo:

Verifica que el ángulo sea menor a 360°.

Calcula la nueva posición (x, y).

Crea el círculo en esa posición.

Incrementa el ángulo.

Repite hasta completar la circunferencia.

Código:
```
while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0),
        vertices=64
    )
    
    angulo_actual += paso_angular
```
 # Importancia de Incrementar el Ángulo

Esta línea es crítica:

angulo_actual += paso_angular

Si no se incrementa el ángulo:

El ciclo nunca terminaría.

Se generaría un bucle infinito.

Blender podría congelarse.

 7. Resultado Final

Al finalizar la ejecución del script se genera un patrón circular distribuido uniformemente alrededor del círculo central.

Como utilicé un paso de 20°, el patrón tiene más círculos que el ejemplo tradicional de 6 círculos (60°).

<img width="1792" height="1120" alt="Captura de pantalla 2026-02-14 a la(s) 22 40 51" src="https://github.com/user-attachments/assets/f5d75aad-eb26-4cb5-8da0-2dc9eb930d49" />

CODIGO: 
```
  import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 20  # Cada 60 grados para obtener 6 círculos alrededor

# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

# --- INICIO DEL PATRÓN REPETITIVO ---

# Círculo 1 (Manual)
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)

# Círculo 2 (Manual)
angulo_actual += paso_angular
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x2, y2, 0), vertices=64)

# --- CONTINUACIÓN AUTOMÁTICA CON WHILE ---

angulo_actual += paso_angular

while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    
    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0),
        vertices=64
    )
    
    angulo_actual += paso_angular
```
