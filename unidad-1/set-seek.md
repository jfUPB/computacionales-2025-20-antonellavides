# Unidad 1

## 🔎 Fase: Set + Seek

- [x] Actividad 01
- [x] Actividad 02
      
### Actividad 01

#### ¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?

La RAM es la memoria que usa el computador mientras estás trabajando, como cuando abres programas o juegos. Es rápida pero se borra cuando apagas todo. En cambio, la ROM tiene info que el computador necesita para encender, como las instrucciones básicas, y esa no se borra. La RAM se puede escribir y cambiar todo el tiempo, pero la ROM casi no se toca.

#### Observación de experimentos

**Experimento 1: Ejecutar el program.asm**

Cuando corrí el programa en el simulador, vi que funcionaba bien y no se trababa. En la dirección de memoria 16 quedó guardado un valor (en mi caso era como 123). Supongo que ese número es el resultado de alguna operación que hace el programa y por eso lo guarda ahí. En cada paso, el simulador va leyendo una instrucción, la interpreta y la ejecuta (lo típico de Fetch-Decode-Execute). Vi que los registros A y D van cambiando según lo que hace el programa, y también va cambiando un poco la memoria. Todo se ejecutó sin errores y el programa terminó bien.

**Experimento 2: Suma de 5 + 10 y guardar en la dirección 20**

Escribí un mini programa en ensamblador para que sumara 5 y 10. Cuando lo ejecuté, al final se guardó el 15 en la dirección de memoria 20, así que salió bien. El simulador muestra cómo va paso por paso: primero carga el 5, luego el 10, los suma, y luego guarda el resultado en la memoria. Mientras se ejecuta, los registros también van cambiando. En resumen, el programa hizo lo que tenía que hacer y no se enredó.

### Actividad 02

#### Identifica una instrucción que use la ALU y explica qué hace

Una que usa la ALU es D=D+A. Ahí lo que pasa es que se suman los valores que están en los registros D y A, y el resultado queda guardado otra vez en D. Básicamente le está diciendo: “suma esto con esto otro y guárdalo”.

#### ¿Para qué sirve el registro PC?

El PC es como el que lleva la cuenta de qué instrucción toca ejecutar. Va uno por uno, y si el programa hace un salto, el PC se mueve a esa otra línea. Si no, simplemente sigue derecho.

#### ¿Cuál es la diferencia entre @i y @READKEYBOARD?

@i es una variable que uno crea, o sea una dirección de memoria cualquiera donde uno guarda algo. En cambio, @READKEYBOARD ya viene con el sistema y se usa para saber si alguien presionó una tecla. Es como la diferencia entre tu cuaderno y el teclado del computador.

#### Describe qué se necesita para leer el teclado y mostrar información en la pantalla

Para leer el teclado, uno tiene que ir a la dirección READKEYBOARD y revisar si ahí hay un número distinto de cero (eso quiere decir que se presionó algo). Para mostrar cosas en pantalla, toca escribir en la memoria a partir de SCREEN, que es donde vive la imagen. Entonces necesitas escribir en esas direcciones especiales.

#### Identifica un bucle en el programa y explica su funcionamiento

Un bucle se ve como esto:

``` asm
(LOOP)
  // cosas que hace
  @LOOP
  0;JMP
```


Eso hace que el programa vuelva una y otra vez a repetir lo mismo. Sirve para que algo siga pasando hasta que tú decidas romper ese ciclo con una condición.

#### Identifica una condición en el programa y explica su funcionamiento

Una condición puede ser algo como:

``` asm
@i
D=M
@FIN
D;JEQ
```

Ahí lo que se hace es revisar si lo que hay en i es cero. Si sí, el programa salta a la etiqueta FIN. Si no, sigue derecho. Es como decir: “si ya llegamos a cero, termina; si no, seguimos”.


  
