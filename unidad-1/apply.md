# Unidad 1

## 🛠 Fase: Apply

### Actividad 3
 
 Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

 (LOOP) // O (START)

@5
D=M 77CARGANDO EN D LO DE LA POSICION 5
@10
D=D-A //LEER DIRECCION DE MEMORIA 5 Y RESTARLO A D10 ARA SABER SI ES MAYOR O MENOR QUE 10 

@MENOR
D;JLT //INSTRUCCION DE SALTO GENERA UN VALOR EN EL REGRSTRO D, SALTA A MENOR


(MAYOREQ) // SIGO DERECHO
@7
M=0
@LOOP
0;JMP


(MENOR)
@7
M=1
@LOOP
0;JMP
