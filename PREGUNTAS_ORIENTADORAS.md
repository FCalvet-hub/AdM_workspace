## Respuestas a las preguntas del trabajo práctico

### 1. Describa brevemente las diferencias entre las familias de procesadores Cortex M0, M3 y M4.

Cortex M0: Es el procesador más básico de la familia Cortex M, diseñado para aplicaciones de bajo costo y bajo consumo de energía. Tiene una arquitectura de 32 bits, pero solo puede ejecutar código Thumb-2, que es un conjunto de instrucciones codificadas en 16 bits.
Cortex M3: Es un procesador más potente que el Cortex M0, con una arquitectura de 32 bits y la capacidad de ejecutar código Thumb-2 y Thumb. También tiene una unidad de división de hardware y un conjunto de instrucciones de aritmética de saturación.
Cortex M4: Es el procesador más potente de la familia Cortex M, con una arquitectura de 32 bits y la capacidad de ejecutar código Thumb-2, Thumb y Thumb-EE. También tiene una unidad de división de hardware, un conjunto de instrucciones de aritmética de saturación y una unidad de punto flotante opcional.
En resumen, el Cortex M0 es el procesador más básico y de menor costo, el Cortex M3 es un procesador intermedio más potente, y el Cortex M4 es el procesador más potente y versátil.

### 2. ¿Por qué se dice que el set de instrucciones Thumb permite mayor densidad de código? Explique

El set de instrucciones Thumb permite mayor densidad de código porque utiliza un formato de instrucción de 16 bits, en comparación con el formato de instrucción de 32 bits utilizado por el set de instrucciones ARM. Esto significa que cada instrucción Thumb ocupa la mitad de espacio que una instrucción ARM, lo que permite almacenar más código en la misma cantidad de memoria.

### 3. ¿Qué entiende por arquitectura load-store? ¿Qué tipo de instrucciones no posee este tipo de arquitectura?

Esto significa que los datos deben cargarse desde la memoria, procesarse y luego volver a escribirse en la memoria utilizando una serie de instrucciones independientes. Por ejemplo, para incrementar un valor de datos almacenado en la SRAM, el procesador necesita usar una instrucción para leer los datos de la SRAM y colocarlos en un registro dentro del procesador, una segunda instrucción para incrementar el valor del registro y luego una tercera instrucción para escribir el valor de nuevo en la memoria. Los detalles de los registros dentro de los procesadores se conocen comúnmente como el modelo de programador.

### 4. Mapa de memoria de la familia Cortex M

