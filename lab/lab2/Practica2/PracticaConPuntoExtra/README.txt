Práctica 2

Integrantes:
Quiroz Castañeda Edgar
Ruiz Melo Jean Paul
Soto Corderí Sandra del Mar

1. En términos de la arquitectura Intel x86 ¿Qué significa que un thread
o proceso está en ejecución?

Significa que un hilo tiene control del procesador, y puede hacer cualquier
accion que tenia que hacer.

2. La función switch_threads es la encargada de cambiar de ejecución un
hilo por otro. En resumen, la función sustituye los valores de ciertos
registros. El registro EIP (Instruction Pointer o Program Counter) guarda
el valor de la siguiente instrucción a ejecutar. ¿Por qué la función
switch_threads no sustituye dicho registro?

En pintOS, todos los procesos hacen una llamada a la misma función para ser 
bloqueados.

Así que al momento de ser bloqueados y desbloqueados, todos los procesos 
tiene exactamente las mismas instrucciones, hasta el fin de la llamada a la 
función de bloqueo.
Por lo que el EIP de todas es exactamente igual en ese momento.

Las llamadas a funciones se almacenan en la pila de cada proceso. Así que 
independietemente de que proceso llame a la función de bloqueo, al terminar la
llamada, el procesador volverá a donde esté apuntando la pila del proceso 
actual.

3. De las dos técnicas para implementar el calendarizador de prioridades:
mantener la lista ordenada o buscar el máximo. ¿Cúal es más factible utilizar?
y ¿Por qué?

En necesario hacer dos operaciones con la lista de procesos listo. 

Primero hay que insertar procesos, lo cual toma lugar en el método de 
desbloqueo. Después de hacerlo, los procesos desbloqueados esperan a ser
ejecutados. Mateniendo la lista ordenada esto toma tiempo lineal. Buscando el 
máximo toma tiempo constante.

Y hay que consultar el próximo proceso a ser ejecutado. Al hacer esto, 
inmediatamente se tiene que cambiar al proceso. Mateniendo la lista ordenada 
esto toma tiempo constante. Buscando el máximo toma tiempo linela.

Esto último debe tomar el menor tiempo posible, mientras que lo primero no 
generaría problema se tarda un poco más.

Así que es más conventiene mantener la lista ordenada.