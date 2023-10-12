## Respuestas a las preguntas del trabajo práctico

### 1. Diferencias entre las familias Cortex M0, M3 y M4

| Característica | Cortex M0 | Cortex M3 | Cortex M4 |
|---|---|---|---|
| Conjunto de instrucciones | Reducido | Completo | Completo + punto flotante |
| Número de registros | 16 | 32 | 32 |
| Modos de operación | Un solo modo | Un solo modo | Un solo modo |
| Prioridades de interrupción | 4 | 8 | 8 |
| Unidad de punto flotante | No | No | Sí |
| Consumo de energía | Bajo | Bajo | Medio |
| Rendimiento | Bajo | Medio | Alto |

### 2. Densidad de código del set de instrucciones Thumb

El set de instrucciones Thumb permite mayor densidad de código que el set de instrucciones ARM. Esto se debe a que las instrucciones Thumb son de longitud de 16 bits, mientras que las instrucciones ARM son de longitud de 32 bits.

**Explicación:**

Las instrucciones ARM se componen de dos palabras de 16 bits, una para el código de operación y otra para los operandos. Las instrucciones Thumb, por otro lado, se componen de una sola palabra de 16 bits que contiene tanto el código de operación como los operandos.

Esto significa que las instrucciones Thumb requieren la mitad de la memoria que las instrucciones ARM. Como resultado, los programas escritos en Thumb suelen ser más pequeños y eficientes que los programas escritos en ARM.

### 3. Arquitectura load-store

Una arquitectura load-store es un modelo de arquitectura de memoria en el que las operaciones de carga y almacenamiento son las únicas que pueden acceder a la memoria principal.

**Tipos de instrucciones que no posee este tipo de arquitectura:**

* Instrucciones de aritmética e indirección
* Instrucciones de control de flujo
* Instrucciones de coma flotante

### 4. Mapa de memoria de la familia Cortex M

