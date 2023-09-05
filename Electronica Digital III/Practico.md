# Clase 3 (24 de Agosto)
El siguiente programa es un ejemplo que prende un led del pin 22
```
#include "LPC17xx.h"

void retardo(void);
int main(){
	LPC_PINCON->PINSEL1 &= ~(ob11<<12);
	LPC_GPIO0->FIODIR |= (1<<22);
	while(1){
		LPC_GPIO0->FIOCLR |= (1<<22);
		retardo();
		LPC_GPIO0->FIOSET |= (1<<22);
		retardo();
	}
}

void retardo(void){
	uint32_t contador;
	for(contador = 0; contador < 6000000; contador++){};
}
```

La función **retardo(void)** se ocupa de dar un delay para que se pueda ver como se prende y apaga el led (en este caso un led integrado en el LPC) 

# Clase 4 (31 de Agosto)
* Para no modificar un registro entero y solo un bit, se usa **|** **OR** o **& ~** **AND EXCLUSIVA**
* Los vectores de interrupcion se encuentran en los primeras direcciones de la memoria de programa
* Existen 33 niveles de prioridad para las interrupciones
* A diferencia del PIC16F887 que tiene 1 interrupcion externa (RB0), la LPC1769 contiene 4 interrupciones externas 
* Se puede activar las interrupciones por flanco ascendente (0), descendente (1) o ambas al mismo tiempo. (**Table 103 GPIO Interrupt register map**)
* 