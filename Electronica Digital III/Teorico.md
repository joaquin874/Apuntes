### Introduccion

ARM CORTEX M3
- Arquitectura ARMv.7M
- No Chace - No MMU
- La tabla de vectores contiene direcciones y no instrucciones
- Instrucción DIV
- Interrupciones salvan y restauran en estado automáticamente
- Mapa de Memoria FIJO
- Bit-Banding : Manipulación de los bits como una dirección de memoria propia
- Interrupción no enmascarable (NMI)
- Núcleo compatible con Thumb-2
- Utiliza Tecnologia ARM Thumb-2:
- Intrucciones de 16 bits (Thumb)
- Intrucciones de 32 bits ARM
- Compilador "C" usa ambas

El microcontrolador ARM soporta los siguentes tipos de instrucciones:
* Codigo ARM: todas las instrucciones, con todas las opciones y todos los modos de direccionamiento
* Codigo Thumb: instrucciones de 16 bits mas "compactas", tiene la ventaja de tener programas mas cortos, pero el problema es que se vuelve mas lento en la ejecucion del mismo.
* Thumb2: combina los dos anteriores de forma que no sea necesario poner instrucciones para pasar de un modo a otro. No es necesario que las instrucciones este alineadas a palabra.

![[Pasted image 20230905191756.png]]

### Registros

* La MCU cuenta con 16 registros (que a diferencia del PIC que contiene 1), con ellos se pueden hacer instrucciones e direccionamiento inmediato, operaciones, etc.
* Registros de R0 al R12 son registros de proposito general, enfocados prinipalmente para hacer operaciones.
* Registros de Propósito especifico R13, R14 y R15
* R13 Stack Pointer, apuntador de la pila (para hacer subrutinas)
* R14 Link register, instrucciones (Push y Pop)
* R15 Program Counter (contador de programa), usado para direccionar a la memoria de codigo.

![[Pasted image 20230905191835.png]]
### Modulos LPC1769 NXP (Del modelo especifico, no ARM)

![[Pasted image 20230905191846.png]]
#### Analog

- ADC 12bit - 8 CH
- DAC 10bit
#### Motor Control

- Motor Control PWM (Pulse Width Modulation)
- Quadrature Encoder Interface
#### Timers

#### Interfaces

- NVIC (Nested Vectored Interrupt Controller): es responsable de controlar las interrupciones y asegurarse que se cumplan en el orden apropiado. Utiliza un sistema de prioridades para determinar que interrupción se manejara primero. Cada interrupción está asociado con una dirección de memoria especifica donde se encuentra la rutina de interrupción correspondiente.
- UART (Universal Asynchronous Receiver-Transmitter): es el componente de hardware que se encarga de la conversion entre el fromato de datos paralelos y el formato de datos seriales. Maneja la sincronizacion de bits y la deteccion de inciio y final de la trama en las comunicaciones seriales.

## SysTick

![[Pasted image 20230830105607.png]]

El SysTick es un temporizador de sistema (System Timer) integrado en el microcontrolador. Se utiliza para tareas de temporizacion y para generar interrupciones periódicas en el sistema.

Tiene las siguientes características:
* Temporizador de cuenta descendiente: El temporizador cuanta desde un valor inicial hacia cero y luego se reinicia. Cuando alcanza cero, puede generar una interrupción y reiniciar el contador con un valor predefinido.
* Contador configurable: Se puede configurar el valor inicial del contador para controlar la duración de las interrupciones periódicas.
* Interrupción Generada: Cuando el temporizador alcanza cero, se puede configurar para generar una interrupción, lo que permite ejecutar una función o código especifico en respuesta a la interrupción del temporizador.
* Fuente de reloj configurable: El temporizador puede utilizar diferentes fuentes de reloj, como el reloj principal del microcontrolador o un divisor del reloj principal.
* Contador de 24 bits: En la mayoría de las implementaciones, el temporizador SysTick tiene un contador de 24 bits, lo que significa que puede contar hasta 2^(24-1) antes de reiniciarse.
* Modo de un solo disparo o periódico: Puedes configurar el temporizador SysTick para que genere una interrupción después de contar hasta cero una vez o para que genere interrupciones periódicas cada vez que alcance cero.

![[Pasted image 20230830110125.png]]

**El triangulo al interior del bloque hace referencia a que el bloque responderá a un flanco descendiente o ascendente**

## Clase Sep 6

### ADC

* A diferencia del PIC que tiene un ADC  de 10 bits (aproximaciones sucesivas), la LPC1769 tiene un ADC de 12 bits.
* Multiplexado de entrada entre 8 pines.
* Modo de Apagado (Bajo consumo).
* Rango de medición VREFN a VREFP (tipicamente 3V, sin exeder el nivel de voltaje VDDA)
* Tasa de Conversion de 12 bits de 200 KHz
* Para entrada digital 5V y para entrada analogica 3V
* Modo de conversion de rafaga para entradas simple o multiples (Modo BURST).
* Conversion opcional en la transiscion en el pin de entrada o la senial de coincidencia del temporizador.

Usar cualquier dispositivo periférico implica tres pasos principales:
1. Encender el periférico
2. Configurando el reloj periférico
3. Configurar las funciones pin

Para configurar el ADC se utiliza el registro PCONP(Registro de control de Potencia para Perfiericos) y tambien configurar un reloj periferico con el registro PCLKSEL0

![[Pasted image 20230906163515.png]]
*CAN1 y CAN2 es un protocolo de comunicacion utilizado en aplicaciones industriales y automotrices.

* La LPC permite usar fuentes externas como voltaje de referncia para evitar el ruido que produce la fuente interna de la LPC 
### Registros del ADC

![[Pasted image 20230906164907.png]]

![[Pasted image 20230906165509.png]]

*B (Burst) y E (Edge)
* Cuando se habilita el bit de Burst (bit 16) queda inhabilitado los pines de Start, ya que comienza a convertir en el momento que se habilita de bit de Burst
![[Pasted image 20230906165932.png]]

OVERRUN avisa si el ADC sigue convirtiendo