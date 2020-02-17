Práctica 1

Integrantes:
Quiroz Castañeda Edgar
Soto Corderí Sandra del Mar


Preguntas:
1. ¿Como se da cuenta un thread que su stack se desbordó?

A los threads se les asigna en su estructura un valor constante aleatorio conocido como 'magic' que si el proceso detecta que cambia, se considera hay un stack overflow.

2. Describe el proceso de booting (inicialización) de Pintos.



3. En Pintos cada thread utiliza un bloque de 4KB, en el cual se almacena su PCB y el stack del thread. ¿Dónde se almacenan las variables globales?



4. ¿Qué función tiene el thread idle de Pintos?

El thread idle se ejecuta cuando ningún otro proceso está listo para ejecutarse. Se coloca inicialmente en la lista lista por thread_start (). Es devuelto por next_thread_to_run () como un caso especial cuando la lista lista está vacía.
