# Tarea: Mi prompt profesional

Herramienta de IA usada: Gemini (modelo Flash), cada version en un chat nuevo.

## Funcionalidad elegida

**Control de inventario de un almacen de materiales.** Un programa de consola en Java que permita registrar materiales, registrar sus entradas y salidas, y mostrar el stock actual. Lo elegi porque se parece a un control que hoy se lleva en Excel en el almacen de una empresa minera.

## Version 1: prompt basico

```text
Haz un programa de inventario.
```

**Que paso:** Gemini eligio por su cuenta el lenguaje (**Python**, no Java), guardo los datos en un archivo JSON y agrego atributos que nunca pedi, como el precio unitario.

**Que falta:** no dije el lenguaje, ni el tipo de inventario, ni que datos manejar. La IA tuvo que adivinar todo.

## Version 2

```text
Actua como desarrollador Java. Crea un programa de consola en Java para controlar el inventario de un almacen de materiales de una empresa minera. Debe registrar entradas y salidas de materiales y mostrar el stock actual.
```

**Que cambie y por que:** agregue un **rol** (desarrollador Java), **contexto** (almacen de materiales de una empresa minera) y una **instruccion** concreta (entradas, salidas y stock) para que la IA dejara de adivinar.

**Que mejoro:** ahora genero el programa en **Java** con programacion orientada a objetos, una clase `Material` con codigo, nombre, unidad de medida y stock, y validaciones para evitar stock negativo.

**Que falta:** siguio decidiendo cosas por su cuenta: uso un `HashMap` y nombres de atributos propios (`unidadMedida`), y paso directo al codigo sin explicar la estructura. No le indique el formato de la respuesta.

## Version 3: prompt final

```text
Actua como desarrollador Java con experiencia en sistemas de almacen.

Contexto: trabajo en el almacen de una empresa minera pequena y registro en Excel las entradas y salidas de materiales (por ejemplo cascos, guantes y barrenos). Quiero pasar ese control a un programa sencillo.

Instruccion: crea un programa de consola en Java que permita registrar materiales, registrar entradas y salidas, y mostrar el stock actual de cada material. Usa una clase Material con los atributos codigo, nombre, unidad y stock, y una clase Almacen que gestione la lista de materiales.

Restricciones: no uses librerias externas ni base de datos, solo Java estandar con ArrayList. No permitas que una salida deje el stock en negativo; en ese caso muestra un mensaje de error.

Ejemplo de como debe verse el reporte de stock:
CODIGO | MATERIAL | UNIDAD | STOCK
M001 | Casco de seguridad | und | 25

Formato: primero explica en una lista breve las clases y sus metodos, luego presenta el codigo completo en un solo bloque y al final muestra un ejemplo de ejecucion.
```

**Que cambie y por que:** agregue los componentes que faltaban: **contexto real** (de donde vienen los datos), **atributos y clases exactos**, **restricciones** (sin librerias externas, solo `ArrayList`, sin stock negativo), un **ejemplo** del reporte y el **formato** de la respuesta.

**Que mejoro:** Gemini primero explico la estructura del programa: la clase `Material` con `codigo`, `nombre`, `unidad` y `stock`; la clase `Almacen` con un `ArrayList<Material>` y los metodos `registrarMaterial`, `registrarEntrada`, `registrarSalida` y `mostrarReporteStock`; y una clase principal con un menu en consola. Recien despues presento el codigo.

## Componentes del prompt final

| Componente | Texto de mi prompt |
|:-----------|:-------------------|
| Rol | Actua como desarrollador Java con experiencia en sistemas de almacen. |
| Instruccion | Crea un programa de consola en Java que permita registrar materiales, registrar entradas y salidas, y mostrar el stock actual de cada material. Usa una clase Material con los atributos codigo, nombre, unidad y stock, y una clase Almacen que gestione la lista de materiales. |
| Contexto | Trabajo en el almacen de una empresa minera pequena y registro en Excel las entradas y salidas de materiales (por ejemplo cascos, guantes y barrenos). |
| Ejemplos | CODIGO \| MATERIAL \| UNIDAD \| STOCK / M001 \| Casco de seguridad \| und \| 25 |
| Formato | Primero explica en una lista breve las clases y sus metodos, luego presenta el codigo completo en un solo bloque y al final muestra un ejemplo de ejecucion. |
| Restricciones | No uses librerias externas ni base de datos, solo Java estandar con ArrayList. No permitas que una salida deje el stock en negativo. |

## Evaluacion del resultado

| Criterio | Version 1 | Version 3 |
|:---------|:---------:|:---------:|
| Esta escrito en Java | No | Si |
| Usa las clases Material y Almacen con los atributos pedidos | No | Si |
| Usa solo Java estandar con ArrayList | No | Si |
| Impide que el stock