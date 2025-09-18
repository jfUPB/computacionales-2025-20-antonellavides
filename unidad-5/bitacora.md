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

### 1. PREGUNTA: ¿Qué hace exactamente la aplicación de fuegos artificiales en openFrameworks y cómo organiza el código las diferentes explosiones y partículas?

### 2. HIPOTESIS:

Creo que la aplicación crea partículas que primero suben como “cohetes” y luego explotan en patrones

### 3. EXPERIMENTO

Revisé el código fuente (ofApp.cpp y las clases de partículas).

Corrí la aplicación en openFrameworks para observar su funcionamiento.

Probé interacciones:

Clic con el mouse → lanza un cohete.

Barra espaciadora → lanza varios cohetes.

Tecla s → guarda una captura de pantalla.

### 4. HALLAZGO

Confirmé que cada explosión está encapsulada en una clase distinta (CircularExplosion, SquareExplosion, StarExplosion).

Vi que las clases manejan sus propias partículas, pero todas comparten una misma interfaz (draw, update).

El uso del mouse y teclado permite comprobar la interacción en tiempo real.

El programa demuestra los tres conceptos de POO:

Encapsulamiento: cada explosión gestiona sus partículas sin que ofApp tenga que saber cómo.

Herencia: todas las explosiones derivan de una clase base común.

Polimorfismo: al llamar explosion->draw(), el programa decide en ejecución si dibuja círculo, cuadrado o estrella.

Llamada polimorfica:
```
for(auto& explosion : explosions) {
    explosion->update();
    explosion->draw();
}

```
### 5. REFLEXION

El análisis me permitió ver cómo se estructura una aplicación interactiva usando POO. Entendí que los fuegos artificiales no son “efectos mágicos” sino objetos bien organizados que heredan comportamientos y redefinen métodos según su forma. Me parece interesante que con pocas líneas en ofApp se puedan manejar diferentes explosiones gracias al polimorfismo.

### CICLO B

### 1. PREGUNTA: ¿Qué pasa en la memoria del computador cuando se crean objetos como ofApp, CircularExplosion o StarExplosion? ¿Cómo puedo comprobarlo con el depurador?

### 2. HIPOTESIS:

Pienso que cada objeto guarda sus datos en memoria de forma ordenada, como una caja que tiene compartimientos: primero los atributos de la clase base y después los de la clase hija. Tal vez con el depurador puedo ver esa estructura y comprobar qué valores tiene cada atributo en tiempo real.

### 3. EXPERIMENTO

Abrí el proyecto en Visual Studio con el depurador activo.

Coloqué puntos de interrupción (breakpoints) en:

El constructor de CircularExplosion.

El momento en que se crea un StarExplosion.

Inspeccioné las variables en la ventana del depurador:

Vi la instancia de ofApp.

Revisé la lista explosions y exploré cada objeto con el mouse.

Observé que cada explosión tenía sus atributos (posición, color, partículas) además del nombre heredado.

### 4. HALLAZGO

Confirmé que los objetos en memoria están organizados jerárquicamente: primero lo heredado de Explosion y luego lo específico de CircularExplosion o StarExplosion.

Pude ver cómo cambian los valores cuando la animación avanza (por ejemplo, el radio del círculo aumentaba con cada frame).

Me quedó claro que el depurador no solo sirve para corregir errores, sino también para entender cómo se representa un objeto en memoria.

### 5. REFLEXION

Usar el depurador fue clave para pasar de la teoría a lo concreto. Antes pensaba en herencia y objetos de forma abstracta, pero ahora vi directamente cómo se guardan y cambian en memoria. Eso me ayuda a confiar más en el código y entender cómo se conecta la POO con el funcionamiento real del computador.























