Práctica 1

Integrantes:
Quiroz Castañeda Edgar
Soto Corderí Sandra del Mar


Preguntas:
1. ¿Como se da cuenta un thread que su stack se desbordó?

A los threads se les asigna en su estructura un valor constante aleatorio conocido como 'magic' que si el proceso detecta que cambia, se considera hay un stack overflow.

2. Describe el proceso de booting (inicialización) de Pintos.

Al terminar el BIOS(UEFI) el reconocimiento de hardware, el PC se pone en 0.

En esa dirección de memoria se encunetra un programa en ensamblador que contiene
el proceso de booting.

Este realiza varios pasos importantes.

Primero, se carga en memoria desde el disco duro el kernel del sistema 
operativo.

Luego, se reserva espacio para la pila de ejecución y se transifiere el control
a programa de inicialización del kernel.

Este configura el procesador para que funcione con memoria virtual para que 
todos los procesos puedan usarla. Y manda a llamar lo que será el primer hilo 
del sistema operativo, que en pintOS es un programa en C.

Este inicializa más funcionalidades del kernel, y crea y configura un PCB 
para sí mismo. Usa una interfaz de ensamblador para asignarse espacio en la 
pila de ejecución.

Después de crear el PCB, este programa se transforma en el primer hilo. El 
sistemo operativo está inicializado.




3. En Pintos cada thread utiliza un bloque de 4KB, en el cual se almacena su PCB y el stack del thread. ¿Dónde se almacenan las variables globales?

Se guardan directamente en la memoria RAM, pues son referencias estáticas con 
tamaño conocido en tiempo de ejecución.


4. ¿Qué función tiene el thread idle de Pintos?

El thread idle se ejecuta cuando ningún otro proceso está listo para ejecutarse. Se coloca inicialmente en la lista lista por thread_start (). Es devuelto por next_thread_to_run () como un caso especial cuando la lista lista está vacía.
