# Unidad 1

## 🛠 Fase: Apply

- [x] Actividad 03
- [ ] Actividad 04

## Actividad 03
 
### Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

 (LOOP) -> o tambien (START)

@5
D=M 77 -> Cargando en D lo de la posicion 5
@10
D=D-A -> Leer direccion de memoria 5 y restarlo a D10 para saber si es mayor o menor que 10

@MENOR
D;JLT -> Instruccion de salto genera un valor en registro D, salta a menor

(MAYOREQ) -> Sigo derecho
@7
M=0
@LOOP
0;JMP

(MENOR)
@7
M=1
@LOOP
0;JMP

## Actividad 04

@1       -> Inicializa contador en 1
D=A
@i
M=D

@0       -> Inicializa acumulador en 0
D=A
@sum
M=D

(LOOP)
  @i     -> Cargar contador
  D=M
  @sum
  M=D+M  -> sum = sum + i

  @i
  M=M+1  -> i = i + 1

  @i
  D=M
  @6     -> condición: si i == 6, termina
  D=D-A
  @END
  D;JEQ

  @LOOP
  0;JMP

(END)
  @sum
  D=M
  @12
  M=D   -> Guardar resultado en la dirección 12

(END2)
  @END2
  0;JMP

### Paso a paso

- Veo que la variable i empieza en 1 y sum en 0.
- El bucle se repite 5 veces, sumando 1+2+3+4+5.
- Cuando i llega a 6, se cumple la condición y se salta al final.
- El valor 15 queda guardado en la dirección de memoria 12.

---------------

- El registro D cambia constantemente para cargar valores temporales.
- i se va incrementando de uno en uno.


