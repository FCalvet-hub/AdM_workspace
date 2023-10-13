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

Los procesadores Cortex-M tienen dos punteros de stack: el puntero de stack principal (MSP) y el puntero de stack del procesador (PSP). El MSP se utiliza para el kernel del sistema operativo y los manejadores de interrupciones, mientras que el PSP se utiliza para las tareas de la aplicación.

Esta disposición tiene varias ventajas:

- Si una tarea de aplicación encuentra un problema que conduce a una corrupción del stack, es probable que el stack utilizado por el kernel del sistema operativo y otras tareas siga intacta, lo que ayuda a mejorar la fiabilidad del sistema.
- El espacio de stack para cada tarea solo necesita cubrir el uso máximo del stack más un nivel de marco de stack. El espacio de stack necesario para la ISR y la gestión de interrupciones anidadas se asigna solo en el stack principal.
- Facilita la creación de un sistema operativo eficiente para los procesadores Cortex-M.
- Un sistema operativo también puede utilizar la unidad de protección de memoria (MPU) para definir la región de stack que puede utilizar una tarea de aplicación. Si una tarea de aplicación tiene un problema de desbordamiento de stack, la MPU puede activar una excepción de fallo de gestión de memoria e impedir que la tarea sobrescriba regiones de memoria fuera del espacio de stack asignado para esta tarea.

### 6. Describa los diferentes modos de privilegio y operación del Cortex M, sus relaciones y como se conmuta de uno al otro. Describa un ejemplo en el que se pasa del modo privilegiado a no priviligiado y nuevamente a privilegiado.

Los procesadores Cortex-M tienen dos modos de privilegio, el modo Thread y el modo Handler. El modo Thread es el modo predeterminado en el que se ejecuta el código de usuario. El modo Handler es el modo que se utiliza para manejar excepciones.

Para cambiar de un modo de privilegio a otro, se utiliza la instrucción **<MSR CONTROL, #value>**. El valor en **value** especifica el nuevo modo de privilegio.

El modo Thread tiene acceso a todos los recursos del sistema, incluyendo la memoria, los periféricos y los registros de control. El modo Handler tiene acceso limitado a los recursos del sistema. No puede acceder a la memoria del núcleo, a los periféricos de alto rendimiento o a los registros de control.

El cambio de modo de privilegio se produce cuando se ejecuta una instrucción SVC o cuando se produce una excepción.

### 7. ¿Qué se entiende por modelo de registros ortogonal? Dé un ejemplo

Se refiere a un diseño de arquitectura en el cual los registros son utilizados de manera uniforme y consistente, esto significa que los registros pueden ser usados indistintamente para una variedad de propósitos. Es decir, en un modelo de registros ortogonal, no hay restricciones que limiten el uso de un registro específico para ciertas operaciones o tipos de datos. Esto brinda flexibilidad y eficiencia en el uso de registros y forma de programación.

Ejemplo

El registro R0 es un registro de propósito general que se puede utilizar para almacenar un valor de datos o un puntero de memoria. El registro CPSR es un registro de propósito especial que almacena el estado del procesador. El registro LR es un registro de estado que almacena la dirección de retorno de la instrucción anterior.

```S
add $t0, $t1, $t2
sub $t2, $t2, $t1
```

### 8. ¿Qué ventajas presenta el uso de intrucciones de ejecución condicional (IT)? Dé un ejemplo

Ejecución condicional (instrucción IF-THEN)

Además de las ramificaciones condicionales, los procesadores Cortex-M3 y Cortex-M4 también admiten la ejecución condicional. Después de ejecutar una instrucción IT (IF-THEN), se pueden ejecutar condicionalmente hasta cuatro de las instrucciones siguientes en función de la condición especificada por la instrucción IT y el valor de APSR.

Un bloque de instrucciones IT consta de una instrucción IT, con detalles de ejecución condicional, seguida de una a cuatro instrucciones de ejecución condicional. Las instrucciones de ejecución condicional pueden ser instrucciones de procesamiento de datos o instrucciones de acceso a memoria. La última instrucción de ejecución condicional en el bloque IT también puede ser una instrucción de bifurcación condicional.

La declaración de instrucción IT contiene el código de operación de instrucción IT con hasta tres sufijos opcionales adicionales de "T" (entonces) y "E" (si no), seguidos de la condición a verificar, que es la misma que el símbolo de condición para bifurcaciones condicionales.

Ejemplo

```S
CMP R0, #1 ; Comparar R0 con 1
ITE EQ ; La siguiente instrucción se ejecuta si Z está establecida (EQ),
; la siguiente después se ejecuta si Z está desactivado (NE)
MOVEQ R3, #2 ; Establecer R3 a 2 si EQ
MOVNE R3, #1 ; Establecer R3 a 1 si no EQ (NE)
```
Tener en cuenta que cuando se utiliza el sufijo "E", la condición de ejecución para la instrucción correspondiente en el bloque IT debe ser la inversa de la condición especificada por la instrucción IT.

Son posibles diferentes combinaciones de secuencia "T" y "E":

Solo una instrucción de ejecución condicional: IT
Dos instrucciones de ejecución condicional: ITT, ITE
Tres instrucciones de ejecución condicional: ITTT, ITTE, ITET, ITEE
Cuatro instrucciones de ejecución condicional: ITTTT, ITTTE, ITTET, ITTEE, ITETT, ITETE, ITEET, ITEEE

### 9. Describa brevemente las excepciones más prioritarias (reset, NMI, Hardfault).

#### reset
Después del reinicio y antes de que el procesador comience a ejecutar el programa, los procesadores Cortex-M leen las dos primeras palabras de la memoria. El principio del espacio de memoria contiene la tabla de vectores, y las dos primeras palabras de la tabla de vectores son el valor inicial del Puntero de Pila Principal (MSP) y el vector de reinicio, que es la dirección de inicio del manejador de reinicio. Después de que el procesador lee estas dos palabras, el procesador configura el MSP y el Contador de Programa (PC) con estos valores.

#### NMI

NMI significa Non-Maskable Interrupt (Interrupción no enmascarable). Las interrupciones NMI son las interrupciones de mayor prioridad en los microcontroladores Cortex-M. No se pueden deshabilitar, por lo que se pueden utilizar para manejar eventos críticos del sistema, como fallas de hardware o eventos externos importantes.

#### Hard Fault

Cuando ocurre una falla de hardware, el procesador Cortex-M genera una excepción de falla de hardware. La excepción de falla de hardware es la excepción de mayor prioridad en los microcontroladores Cortex-M y no se puede deshabilitar.

### 10. Describa las funciones principales del stack. ¿Cómo resuelve la arquitectura el llamado a funciones y su retorno?
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
### 4. Describa brevemente la interfaz entre assembler y C ¿Cómo se reciben los argumentos de las funciones? ¿Cómo se devuelve el resultado? ¿Qué registros deben guardarse en el stack antes de ser modificados?
### 5. ¿Qué es una instrucción SIMD? ¿En qué se aplican y que ventajas reporta su uso? Dé un ejemplo.

