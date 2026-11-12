# Bitacora de prompts
 
Laboratorio 06: Fundamentos de Ingenieria de Prompts.
 
Herramienta de IA usada: Gemini
 
## Ejercicio 2: Tokens y ventana de contexto

| Texto | Caracteres | Tokens |
|-------|------------|--------|
| Los estudiantes programan en Java. | 34 | 7 |
| The students program in Java. | 29 | 6 |
| desafortunadamente | 18 | 4 |

En el mismo chat, Gemini respondio que mi aplicacion se llama TiendaTec y usa Java Swing, porque ese dato estaba dentro de su ventana de contexto.

En un chat nuevo respondio que no tenia registrada esa informacion: la ventana de contexto empieza vacia y el modelo nunca vio el dato.

## Ejercicio 3: Temperatura

| Temperatura | % de BiblioTec | Nombres en los 5 intentos |
|-------------|----------------|---------------------------|
| 0 | 100.0 % | BiblioTec, BiblioTec, BiblioTec, BiblioTec, BiblioTec |
| 0.5 | 65.3 % | LibroYa, BiblioTec, BiblioTec, BiblioTec, PrestaLibro |
| 1 | 44.5 % | LectoGo, LibroYa, BiblioTec, LibroYa, LibroYa |
| 1.8 | 32.2 % | PrestaLibro, NubeDeTinta, BiblioTec, LectoGo, LibroYa |

Al subir la temperatura, BiblioTec pierde probabilidad y aparecen nombres menos probables, como LectoGo o NubeDeTinta, y los intentos dejan de repetirse.
El simulador nunca inventa un nombre nuevo porque la temperatura solo reparte la probabilidad entre las opciones que ya existen: no le agrega conocimiento al modelo.
 
## Ejercicio 4: Prompt vago vs estructurado

| Criterio | Prompt vago | Prompt estructurado |
|----------|-------------|---------------------|
| Menciona el objetivo del sistema | Si | Si |
| Menciona a los usuarios principales | Si | Si |
| Tiene exactamente 3 funcionalidades | No | Si |
| Esta en 3 parrafos | No | No |
| Lo usaria en un informe real | No | Si |

El prompt vago genero un documento largo con muchos modulos y subsecciones, con una extension impredecible.
El estructurado respeto el rol, el objetivo, los usuarios y las 3 funcionalidades, pero presento las funcionalidades como lista numerada en lugar de un tercer parrafo: la IA no siempre sigue el formato al pie de la letra.
 
## Ejercicio 5: Anatomia de un prompt

Prompt final:

```text
Actua como desarrollador Java. Crea un programa en Java para gestionar los productos de una tienda usando una clase Producto con los atributos codigo, nombre, precio y stock. Explica primero la estructura de la clase y luego presenta el codigo Java. Usa este estilo para los metodos: getPrecio(), setPrecio(double precio).
```

| Componente | Texto de mi prompt |
|------------|--------------------|
| Rol | Actua como desarrollador Java. |
| Instruccion | Crea un programa en Java usando una clase Producto con los atributos codigo, nombre, precio y stock. |
| Contexto | para gestionar los productos de una tienda |
| Ejemplo | Usa este estilo para los metodos: getPrecio(), setPrecio(double precio). |
| Formato | Explica primero la estructura de la clase y luego presenta el codigo Java. |

Que cambio en cada nivel:

- **Nivel 1:** no sabia que crear; pidio mas detalles y dio un ejemplo generico de consola que calcula la edad.
- **Nivel 2 (+ Rol):** respondio como desarrollador Java, pero tampoco escribio codigo; ofrecio 4 tipos de aplicacion.
- **Nivel 3 (+ Contexto):** creo un sistema de productos con 3 clases, pero invento los atributos (uso id en lugar de codigo).
- **Nivel 4 (+ Instruccion):** uso exactamente codigo, nombre, precio y stock y fue directo al codigo.
- **Nivel 5 (+ Formato):** explico primero la estructura y luego el codigo, pero agrego metodos que no pedi (vender y reabastecer).
- **+ Ejemplo:** nombro todos los metodos con el estilo getPrecio() / setPrecio(double precio) y ya no agrego metodos extra.
