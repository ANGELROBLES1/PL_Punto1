# Lenguaje CRUD NoSQL - Punto 1
## Descripción

En este punto se diseñó e implementó una gramática para un lenguaje orientado a operaciones CRUD sobre una base de datos No relacional.

## Archivos del proyecto

El proyecto está compuesto por los siguientes archivos:

- ANT.g4: Define la gramática del lenguaje en ANTLR
- main.py: Ejecuta el parser y valida las instrucciones
- ejemplos.txt: Contiene las instrucciones de prueba

## Operaciones del lenguaje

El lenguaje implementa las siguientes operaciones:

| Comando | Función         |
| ------- | --------------- |
| PUSH    | Inserta datos   |
| PULL    | Consulta datos  |
| SHIFT   | Actualiza datos |
| DROP    | Elimina datos   |

## Estructura del lenguaje

Cada instrucción sigue una estructura definida. Ejemplo:
``
PUSH usuarios WITH [ nombre => "Ana", edad => 20 ]
PULL usuarios FILTER edad > 18
SHIFT usuarios REPLACE [ edad => 25 ] FILTER nombre == "Ana"
DROP usuarios FILTER edad < 18
``

Cada línea es evaluada de forma independiente por el parser.

## Gramática utilizada

La gramática fue definida en el archivo ANT.g4:

``
start : stmt+ EOF ;

stmt
    : pushStmt
    | pullStmt
    | shiftStmt
    | dropStmt ;
``

## Ejecución del programa
1. Abrir terminal
2. Navegar a la carpeta del proyecto
3. Generar el parser
``
antlr4 -Dlanguage=Python3 ANT.g4
``
Este comando genera automáticamente los archivos necesarios para el análisis léxico y sintáctico.
4. Ejecutar el programa
``
python3 main.py
``
Salida del programa

El programa analiza cada línea del archivo ejemplos.txt y muestra:
Linea X: VALIDA
Linea X: ERROR

## Prueba con entradas válidas

- Ejemplo de entrada:

``
PUSH usuarios WITH [ nombre => "Ana", edad => 20 ]
``

Salida esperada:

Linea 1: VALIDA

Esto indica que la instrucción cumple completamente con la gramática definida.

- Prueba con errores

Se introdujo una instrucción incorrecta:
``
PUSH usuarios WITH nombre => "Ana"
``
Error: Falta la estructura [ ]

Salida:

Linea X: ERROR

Cuando una instrucción no cumple la gramática:

El parser no puede construir el árbol sintáctico
Se detecta una inconsistencia en la estructura
Se marca la línea como inválida

Esto permite validar que el lenguaje no solo acepta entradas correctas, sino que también detecta errores de sintaxis.
<img width="808" height="248" alt="image" src="https://github.com/user-attachments/assets/efa7e711-4d87-48fd-bcb7-48b62ef79eea" />
