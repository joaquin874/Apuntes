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