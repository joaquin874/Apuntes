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
