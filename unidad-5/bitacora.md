# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

### PARTE 1

### ¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.

Es lo que nos permite controlar si los atributos de una clase son accesibles o no. Los tres tipos son: público, privado y protegido. Me ha servido, por ejemplo, para proteger datos sensibles (por ejemplo una contrasena) y que no se cambien directamente.

### ¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.

Es cuando una clase hija toma atributos y métodos de una clase padre. Sirve para no repetir código y aprovechar lo que ya está hecho. Ejemplo: una clase PERRO puede heredar de ANIMAL y solo agregar lo que es propio del perro.

### ¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.

Es cuando un mismo método puede comportarse de distintas formas según el objeto. Por ejemplo, hacerSonido() en un gato significa maullar y en un perro significa ladrar.

### PARTE 2

### Encapsulamiento:
Un ejemplo es:

```cs
private string nombre;
public string Nombre { get; protected set; }
```
Esto es encapsulamiento porque el campo nombre está oculto y solo se accede a través de la propiedad. Se hace private para evitar que cualquiera lo cambie directamente; con la propiedad se controla mejor y se evitan errores o valores inválidos.

### Herencia:
Se ve en public class Circulo : Figura. Eso significa que Circulo hereda todo lo de Figura. Entonces, además de su atributo Radio, también guarda Nombre porque viene de la clase base.

### Polimorfismo:
En el foreach, aunque la variable es de tipo Figura, cuando se llama a Dibujar() se ejecuta el método correcto según si es un Circulo o un Rectangulo. Yo creo que por debajo el programa tiene como una tabla que guarda qué método usar según el tipo real del objeto.

### PARTE 3

### Memoria y herencia:

Me imagino que el objeto se guarda como un bloque donde primero están los datos de la clase padre (por ejemplo, Nombre) y luego los de la clase hija (como Base y Altura en el rectángulo).

### El mecanismo del polimorfismo:

Creo que el programa, al ejecutar, mira qué tipo real tiene el objeto y busca en una especie de tabla cuál versión de Dibujar() debe llamar.

### La barrera del encapsulamiento: 

Pienso que el compilador es el que revisa que no se pueda acceder a un campo private. O sea, la protección funciona más en el momento de escribir el código que en la ejecución, aunque de alguna manera esa información también queda guardada en el programa.

## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

### CICLO A 

### 1. PREGUNTA: ¿Qué significa el encapsulamiento en C# y cómo se ve aplicado en el código de la clase Figura?

### 2. HIPOTESIS:

Revisé el código:

```
private string nombre;

public string Nombre
{
    get { return nombre; }
    protected set { nombre = value; }
}
```

Intenté ejecutar el programa, pero me salió un error de linker en Visual Studio.

<img width="400" height="400" alt="error" src="https://github.com/user-attachments/assets/df6597bc-9488-4b05-bcc8-355875332399" />

### 3. EXPERIMENTO

Vi que aunque el programa no corrió por completo, sí identifiqué cómo el atributo nombre está protegido por ser private, y solo se controla con la propiedad pública Nombre.

### 4. HALLAZGO

Vi que aunque el programa no corrió por completo, sí identifiqué cómo el atributo nombre está protegido por ser private, y solo se controla con la propiedad pública Nombre.

### 5. REFLEXION

El encapsulamiento evita que cualquiera cambie directamente el nombre de la figura. Me di cuenta de que es útil cuando se quieren proteger datos, incluso aunque el código no compile bien.
