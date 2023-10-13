## Respuestas a las preguntas orientadoras

### 1. Describa brevemente las diferencias entre las familias de procesadores Cortex M0, M3 y M4.

Cortex M0: Es el procesador más básico de la familia Cortex M, diseñado para aplicaciones de bajo costo y bajo consumo de energía. Tiene una arquitectura de 32 bits, pero solo puede ejecutar código Thumb-2, que es un conjunto de instrucciones codificadas en 16 bits.
Cortex M3: Es un procesador más potente que el Cortex M0, con una arquitectura de 32 bits y la capacidad de ejecutar código Thumb-2 y Thumb. También tiene una unidad de división de hardware y un conjunto de instrucciones de aritmética de saturación.
Cortex M4: Es el procesador más potente de la familia Cortex M, con una arquitectura de 32 bits y la capacidad de ejecutar código Thumb-2, Thumb y Thumb-EE. También tiene una unidad de división de hardware, un conjunto de instrucciones de aritmética de saturación y una unidad de punto flotante opcional.
En resumen, el Cortex M0 es el procesador más básico y de menor costo, el Cortex M3 es un procesador intermedio más potente, y el Cortex M4 es el procesador más potente y versátil.

### 2. ¿Por qué se dice que el set de instrucciones Thumb permite mayor densidad de código? Explique

El set de instrucciones Thumb permite mayor densidad de código porque utiliza un formato de instrucción de 16 bits, en comparación con el formato de instrucción de 32 bits utilizado por el set de instrucciones ARM. Esto significa que cada instrucción Thumb ocupa la mitad de espacio que una instrucción ARM, lo que permite almacenar más código en la misma cantidad de memoria.

### 3. ¿Qué entiende por arquitectura load-store? ¿Qué tipo de instrucciones no posee este tipo de arquitectura?

Esto significa que los datos deben cargarse desde la memoria, procesarse y luego volver a escribirse en la memoria utilizando una serie de instrucciones independientes. Por ejemplo, para incrementar un valor de datos almacenado en la SRAM, el procesador necesita usar una instrucción para leer los datos de la SRAM y colocarlos en un registro dentro del procesador, una segunda instrucción para incrementar el valor del registro y luego una tercera instrucción para escribir el valor de nuevo en la memoria. Los detalles de los registros dentro de los procesadores se conocen comúnmente como el modelo de programador.

### 4. ¿Cómo es el mapa de memoria de la familia?

![alt](/images/memory-map.png)

### 5. ¿Qué ventajas presenta el uso de los “shadowed pointers” del PSP y el MSP?
### 6. Describa los diferentes modos de privilegio y operación del Cortex M, sus relaciones y como se conmuta de uno al otro. Describa un ejemplo en el que se pasa del modo privilegiado a no priviligiado y nuevamente a privilegiado.
### 7. ¿Qué se entiende por modelo de registros ortogonal? Dé un ejemplo
### 8. ¿Qué ventajas presenta el uso de intrucciones de ejecución condicional (IT)? Dé un ejemplo
### 9. Describa brevemente las excepciones más prioritarias (reset, NMI, Hardfault).
### 10. Describa las funciones principales de la pila. ¿Cómo resuelve la arquitectura el llamado a funciones y su retorno?
### 11. Describa la secuencia de reset del microprocesador.
### 12. ¿Qué entiende por “core peripherals”? ¿Qué diferencia existe entre estos y el resto de los periféricos?
### 13. ¿Cómo se implementan las prioridades de las interrupciones? Dé un ejemplo
### 14. ¿Qué es el CMSIS? ¿Qué función cumple? ¿Quién lo provee? ¿Qué ventajas aporta?
### 15. Cuando ocurre una interrupción, asumiendo que está habilitada ¿Cómo opera el microprocesador para atender a la subrutina correspondiente? Explique con un ejemplo
### 16. ¿Cómo cambia la operación de stacking al utilizar la unidad de punto flotante?
### 17.  Explique las características avanzadas de atención a interrupciones: tail chaining y late arrival.
### 18.  ¿Qué es el systick? ¿Por qué puede afirmarse que su implementación favorece la portabilidad de los sistemas operativos embebidos?
### 19.  ¿Qué funciones cumple la unidad de protección de memoria (MPU)?
### 20.  ¿Cuántas regiones pueden configurarse como máximo? ¿Qué ocurre en caso de haber solapamientos de las regiones? ¿Qué ocurre con las zonas de memoria no cubiertas por las regiones definidas?
### 21.  ¿Para qué se suele utilizar la excepción PendSV? ¿Cómo se relaciona su uso con el resto de las excepciones? Dé un ejemplo
### 22.  ¿Para qué se suele utilizar la excepción SVC? Expliquelo dentro de un marco de un sistema operativo embebido.

## ISA
### 1. ¿Qué son los sufijos y para qué se los utiliza? Dé un ejemplo
### 2. ¿Para qué se utiliza el sufijo ‘s’? Dé un ejemplo
### 3. ¿Qué utilidad tiene la implementación de instrucciones de aritmética saturada? Dé un ejemplo con operaciones con datos de 8 bits.
### 4. Describa brevemente la interfaz entre assembler y C ¿Cómo se reciben los argumentos de las funciones? ¿Cómo se devuelve el resultado? ¿Qué registros deben guardarse en la pila antes de ser modificados?
### 5. ¿Qué es una instrucción SIMD? ¿En qué se aplican y que ventajas reporta su uso? Dé un ejemplo.

