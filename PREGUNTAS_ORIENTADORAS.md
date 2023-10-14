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

El stack es una estructura de datos fundamental en la programación y en la arquitectura de microcontroladores. Se utiliza para almacenar datos y registros importantes durante la ejecución del programa, especialmente cuando se trata del llamado a funciones y su retorno.

Funciones principales del stack

- Almacenamiento temporal: el stack se utiliza para almacenar de manera temporal datos y registros importantes durante la ejecución del programa. Esto incluye la preservación de registros antes de realizar llamadas a funciones para que se puedan restaurar después de que la función retorne.
- Gestión de llamadas a funciones: Cuando se llama a una función, la dirección de retorno y otros valores necesarios se almacenan en el stack. Esto permite a la función su ejecución y que luego pueda regresar al punto de llamada cuando termine.
- Anidamiento de llamadas: Cuando una función llama a otra función, la dirección de retorno y los registros de la función actual se almacenan en el stack. Esto permite que se realice otra llamada antes de que la función actual haya terminado.
- Almacenamiento de variables locales: Podemos guardar las variables locales de una función en el stack. Esto asegura que las variables locales estén disponibles solo dentro del contexto de la función y se liberen automáticamente cuando la función regresa.

### 11. Describa la secuencia de reset del microprocesador.


La secuencia de reset de los procesadores Cortex-M es la siguiente:

- El controlador de reset inicializa el procesador.
- El procesador lee las dos primeras palabras de la memoria (la tabla de vectores).
- El procesador configura el MSP y el Contador de Programa (PC) con los valores de las dos primeras palabras de la tabla de vectores.
- El procesador ejecuta el programa a partir de la dirección especificada en el vector de reset.

![alt](/images/reset-seq.png)

### 12. ¿Qué entiende por “core peripherals”? ¿Qué diferencia existe entre estos y el resto de los periféricos?

Los "core peripherals" son los periféricos integrados en el núcleo del procesador Cortex-M. Estos periféricos son esenciales para el funcionamiento del procesador y no requieren hardware adicional para funcionar. Algunos ejemplos de core peripherals son:

- MSP: El MSP es un puntero al stack principal del procesador. El stack se utiliza para almacenar datos temporales, como registros y direcciones de retorno.
- Contador de programa (PC): El PC es un registro que contiene la dirección de la instrucción que se está ejecutando actualmente.
- Controlador de interrupciones (NVIC): El NVIC es un controlador que gestiona las interrupciones del procesador.
- Controlador de memoria (MMU): La MMU es un controlador que gestiona la memoria del procesador.

Los demás periféricos son periféricos externos que no están integrados en el núcleo del procesador. Estos periféricos requieren hardware adicional para funcionar, como memoria, puertos GPIO o controladores de comunicaciones.

### 13. ¿Cómo se implementan las prioridades de las interrupciones? Dé un ejemplo

Las prioridades de las interrupciones se implementan mediante registros de prioridad, con un ancho de 3 a 8 bits.

Cuantos más bits se implementen, más niveles de prioridad estarán disponibles. Sin embargo, más bits de prioridad también pueden aumentar el número de puertas y, por lo tanto, el consumo de energía de los diseños de silicio. Para la arquitectura ARMv7-M, el número mínimo de anchos de registro de prioridad implementados es 3 bits (ocho niveles). En los procesadores Cortex-M3 y Cortex-M4, todos los registros de nivel de prioridad tienen un valor de reinicio de 0.

### 14. ¿Qué es el CMSIS? ¿Qué función cumple? ¿Quién lo provee? ¿Qué ventajas aporta?


CMSIS es un estándar de software desarrollado por ARM que proporciona una API común para acceder a los periféricos y funciones de los microcontroladores Cortex-M.

CMSIS facilita el desarrollo de software para microcontroladores Cortex-M, proporcionando una API común para todos los dispositivos.

CMSIS es proporcionado por ARM, pero está disponible de forma gratuita para todos los desarrolladores.

Ventajas:

Portabilidad: permite a los desarrolladores escribir código que se pueda ejecutar en diferentes dispositivos.
Eficiencia: proporciona código optimizado para acceder a los periféricos y funciones del procesador.
Facilidad de uso: proporciona una API sencilla y fácil de usar.

### 15. Cuando ocurre una interrupción, asumiendo que está habilitada ¿Cómo opera el microprocesador para atender a la subrutina correspondiente? Explique con un ejemplo

Cuando un periférico o hardware necesita servicio del procesador, normalmente se produce la siguiente secuencia:

- El periférico genera una solicitud de interrupción al procesador.
- El procesador suspende la tarea que se está ejecutando actualmente.
- El procesador ejecuta una rutina de servicio de interrupción (ISR) para atender al periférico y, opcionalmente, borrar la solicitud de interrupción por software si es necesario.
- El procesador reanuda la tarea previamente suspendida.

```assembly
// Define la dirección de la ISR
.global _timer_irq_handler

// ISR de interrupción de timer
_timer_irq_handler:

  // Salva el estado del procesador
  push {r0-r3,lr}

  beq _handle_timer_irq

  // vuelve a la tarea que se estaba ejecutando
  bx lr
  ```


### 16. ¿Cómo cambia la operación de stacking al utilizar la unidad de punto flotante?


La operación de stacking cambia al utilizar la unidad de punto flotante de la siguiente manera:

- Los registros de punto flotante se apilan en el stack de la misma manera que los registros de propósito general.
- Los registros de punto flotante se apilan en orden inverso, comenzando por el registro de punto flotante menos significativo.
- El valor de retorno de una función de punto flotante se almacena en el registro de punto flotante más significativo.

![alt](/images/stack%20floating%20point.png)

### 17.  Explique las características avanzadas de atención a interrupciones: tail chaining y late arrival.

#### tail chaining
Es una técnica que se utiliza para reducir el tiempo que tarda el procesador en manejar una excepción cuando ya está manejando otra excepción de la misma o mayor prioridad. La latencia de la cadena de cola funciona omitiendo los pasos de unstacking y stacking de registros, lo que permite al procesador entrar en el handler de excepciones de la excepción pendiente lo antes posible.

#### late arrival

Cuando se produce una excepción, el procesador acepta la solicitud de excepción e inicia la operación de stacking. Si durante esta operación de stacking se produce otra excepción de mayor prioridad, la excepción de llegada tardía de mayor prioridad se atenderá primero.


### 18.  ¿Qué es el systick? ¿Por qué puede afirmarse que su implementación favorece la portabilidad de los sistemas operativos embebidos?

El SysTick es un temporizador integrado en los procesadores Cortex-M. Está integrado como parte del NVIC y puede generar la excepción SysTick (excepción #15). El temporizador SysTick es un simple temporizador de decremento de 24 bits y puede funcionar con la frecuencia del reloj del procesador o con la frecuencia del reloj de referencia.

La implementación del SysTick favorece la portabilidad de los sistemas operativos embebidos porque todos los procesadores Cortex-M tienen el mismo temporizador SysTick. Esto significa que un sistema operativo escrito para un microcontrolador Cortex-M3/M4 puede reutilizarse en otros microcontroladores Cortex-M3/M4.


### 19.  ¿Qué funciones cumple la unidad de protección de memoria (MPU)?

La MPU es un dispositivo programable que puede utilizarse para definir permisos de acceso a la memoria (por ejemplo, solo acceso privilegiado o acceso completo) y atributos de la memoria (por ejemplo, almacenable en búfer, almacenable en caché) para diferentes regiones de memoria. La MPU de los procesadores Cortex-M3 y Cortex-M4 puede soportar hasta ocho regiones de memoria programables, cada una con sus propias direcciones de inicio, tamaños y ajustes programables. También admite una función de región de fondo.

La MPU puede utilizarse para hacer que un sistema embebido sea más robusto y, en algunos casos, puede hacer que el sistema sea más seguro al:

- Evitar que las tareas de la aplicación corrompan el stack o la memoria de datos utilizada por otras tareas y el núcleo del sistema operativo.
- Evitar que las tareas sin privilegios accedan a determinados periféricos que pueden ser críticos para la fiabilidad o la seguridad del sistema.
- Definir el espacio SRAM o RAM como no ejecutable (eXecute Never, XN) para evitar ataques de inyección de código.
- También puede utilizar la MPU para definir otros atributos de la memoria, como la capacidad de almacenamiento en caché, que pueden exportarse a la unidad de caché del sistema o a los controladores de memoria.

### 20.  ¿Cuántas regiones pueden configurarse como máximo? ¿Qué ocurre en caso de haber solapamientos de las regiones? ¿Qué ocurre con las zonas de memoria no cubiertas por las regiones definidas?

El número de regiones de memoria que se pueden configurar en la MPU de un Cortex-M depende del microcontrolador específico. El fabricante define el número máximo de regiones que se pueden configurar.

Cuando se configuran regiones que se solapan, es importante comprender cómo se comporta la MPU y cómo se resuelven estos solapamientos. Aquí se describen las consideraciones clave:

- Prioridad de región: La MPU suele dar prioridad a las regiones con permisos más restrictivos en caso de solapamiento. Esto significa que, si dos regiones se solapan y una de ellas tiene permisos más restrictivos que la otra, los permisos más restrictivos prevalecerán.
- Permisos de acceso: Los permisos de acceso también son importantes en la resolución de solapamientos. Si dos regiones se solapan pero tienen permisos de acceso diferentes, la MPU aplicará los permisos específicos de cada región a las direcciones correspondientes.
- Región más específica: En algunos casos, si una dirección de memoria está dentro de dos regiones que se solapan, se aplicarán los permisos de la región más específica o la región con una dirección de inicio más baja.
- Verificación por hardware: La resolución de solapamientos generalmente es manejada por hardware en la MPU. El hardware de la MPU verifica las direcciones de memoria en tiempo real y aplica los permisos adecuados según las reglas configuradas.
- Configuración cuidadosa: Para evitar problemas de solapamiento, es importante configurar las regiones de manera cuidadosa y coherente. Los desarrolladores deben considerar las necesidades específicas de la aplicación y definir las regiones de manera que no se generen conflictos no deseados.
- Validación y pruebas: Después de configurar las regiones, es aconsejable realizar pruebas exhaustivas para garantizar que los permisos y los solapamientos se comporten como se espera en la aplicación.

![alt](/images/regiens.png)

### 21.  ¿Para qué se suele utilizar la excepción PendSV? ¿Cómo se relaciona su uso con el resto de las excepciones? Dé un ejemplo

En los sistemas operativos embebidos, PendSV es una excepción que se utiliza para cambiar de tarea. Se diferencia de otras excepciones, como las de interrupción, en que puede usarse para programar la ejecución de tareas específicas en momentos oportunos.

¿Cómo funciona PendSV?

Cuando una tarea necesita ceder el control a otra, puede invocar PendSV. PendSV entonces suspende la tarea actual y cambia al contexto de la nueva tarea. Este proceso se denomina cambio de contexto.

Un ejemplo

Imaginemos un sistema operativo embebido que maneja dos tareas: una tarea que actualiza datos y otra tarea que muestra información en pantalla. Cuando la tarea de actualización de datos termina, puede invocar PendSV para ceder el control a la tarea de visualización. PendSV entonces cambia al contexto de la tarea de visualización, que luego puede mostrar la información actualizada.

### 22.  ¿Para qué se suele utilizar la excepción SVC? Expliquelo dentro de un marco de un sistema operativo embebido.

La excepción SVC (Supervisor Call) se utiliza en sistemas operativos embebidos para solicitar servicios al supervisor del sistema, como el kernel del sistema operativo. Es una forma de comunicación entre las aplicaciones de usuario y el núcleo del sistema operativo. Por ejemplo, si una tarea de usuario necesita realizar una operación privilegiada, como acceder a un recurso protegido o realizar una acción que requiere privilegios especiales, puede llamar a una rutina SVC para solicitar permisos al kernel. El kernel verifica si la solicitud es válida y luego realiza la operación solicitada.

## ISA
### 1. ¿Qué son los sufijos y para qué se los utiliza? Dé un ejemplo
### 2. ¿Para qué se utiliza el sufijo ‘s’? Dé un ejemplo
### 3. ¿Qué utilidad tiene la implementación de instrucciones de aritmética saturada? Dé un ejemplo con operaciones con datos de 8 bits.
### 4. Describa brevemente la interfaz entre assembler y C ¿Cómo se reciben los argumentos de las funciones? ¿Cómo se devuelve el resultado? ¿Qué registros deben guardarse en el stack antes de ser modificados?
### 5. ¿Qué es una instrucción SIMD? ¿En qué se aplican y que ventajas reporta su uso? Dé un ejemplo.

