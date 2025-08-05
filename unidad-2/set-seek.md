# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 1

**Lenguaje ensamblador:**

```asm

@SCREEN
M=1

```

**Traducido a c++**

```c++
screeen=1; 
```
<img width="2000" height="2000" alt="Screenshot 2025-07-29 082615" src="https://github.com/user-attachments/assets/f5594217-edae-4330-af29-2cd0f0cd8cd2" />
<img width="2000" height="2000" alt="Screenshot 2025-07-29 082632" src="https://github.com/user-attachments/assets/a12d501c-b968-4a2f-8c70-eb7c3c4eb9a4" />

### Actividad 2

**Lenguaje ensamblador:**

```asm

@SCREEN
M=-1

```

**Traducido a c++**

```c++
c++
screen = -1;

```
<img width="2000" height="2000" alt="Screenshot 2025-07-29 083107" src="https://github.com/user-attachments/assets/d502246d-b55e-46f6-82b2-41942bd70e26" />
<img width="2000" height="2000" alt="Screenshot 2025-07-29 083121" src="https://github.com/user-attachments/assets/ad5c4087-6728-4772-94b4-822e695dd69e" />

### Actividad 3

**Lenguaje ensamblador:**

```asm

@SCREEN
M=-1
@CONTADOR
M=0


(LEER)
@KDB
D=M
@100
D=D-A
@DERECHA
D;JEQ

@KDB
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)

//BORRO POSICION ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

//
@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A
M=-1

@LEER


(IZQUIERDA)

@CONTADOR
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER 
0;JMP

```

**Traducido a c++**

```c++

SCREEN=-1;
contador=0;

//CICLO
INT TMP;
WHILE(1)

// CICLO
{
IF (TMP ==100){
//DERECHA
}
ELSE IF (TMP == 105)
//IZQUIERDA
}

// MEMORIA

[CONTADOR+VALORBASESCREEN]= 0;

CONTADOR=CONTADOR+1;

MEMORIA[CONTADOR+screen]=-1;

```

### Actividad 4

**Lenguaje ensamblador:**

```asm

@I
M=1

@SUM
M=0

(WHILE)
@I
D=M
@100
D=D-A
@END
D;JGT // LA CONDICION DEL WHILE SON TODAS ESTAS OPERACIONES

@I
D=M 
@sum
M=D+M 
@I
M=M+1
@LOOP
0;JMP
@END
0;JMP

```

**Conclusiones:**

Ambos programas hacen lo mismo pero escritos diferente. Al pasarlos a ensamblador, se ve que el while y el for terminan siendo prácticamente iguales, porque en ese lenguaje todo se hace con saltos y condiciones. Lo importante es entender la lógica, no tanto la forma.

### Actividad 5

```asm

@10
d=a
@a
m=d

//calcular la direccion en p, en D se guarda la direccion de A, para saber la direccion de A se pone @A
@a
d=a
@p
m=d

//cambiando valor de a a traves de p, EN A HAY QUE TENER LA DIRECCION DE LA VARIABLE A, LEER CONTENIDO DEL PUNTERO @P, PUNTERO DIRECCION DE LA VARIABLE, MODIFICACION DE LA VARIABLE A TRAVES DEL PUNTERO
@20
D=A
@P //LEYENDO CONTENIDO DE P GUARDAR EN A
A=M
A=
M=D

```

```asm

@10
D=A
@a
M=D

@5
D=A
@b
M=D

@0
D=A
@p
M=D

@p
A=M
D=M
@b
M=D

```








