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

### Que esta haciendo el codigo de la aplicacion:

El código es una simulación de fuegos artificiales en openFrameworks. Primero crea partículas que suben desde la parte de abajo y cuando llegan a cierta altura explotan. De la explosión salen más partículas que forman distintos patrones: círculos, cuadrados al azar o estrellas. Con el mouse se lanza una partícula y con la barra espaciadora se lanzan muchas al mismo tiempo. También se puede guardar una imagen con la tecla s.

## 2.  **La pregunta inicial**

¿Cómo se implementan en memoria y en tiempo de ejecución el polimorfismo, la herencia y el encapsulamiento en C++ (y qué relación tienen con lo que ya conozco de C#)?

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

### CICLO A 

### 1. PREGUNTA: ¿Cómo identificar en el código de Figura, Circulo y Rectangulo ejemplos claros de encapsulamiento, herencia y polimorfismo?

### 2. HIPOTESIS:

Encapsulamiento: los campos privados se exponen solo a través de propiedades (Nombre).

Herencia: se da cuando una clase declara : Figura.

Polimorfismo: ocurre en el foreach (Figura fig in misFiguras) porque llama a Dibujar() sin saber el tipo concreto.

### 3. EXPERIMENTO

```cs
private string nombre;   // Encapsulamiento: campo privado
public string Nombre { get { return nombre; } protected set { nombre = value; } } // Encapsulación controlada
```
```
public class Circulo : Figura {  // Herencia
    public override void Dibujar() { ... }  // Polimorfismo (sobrescribe)
}
```
```
foreach (Figura fig in misFiguras) {
    fig.Dibujar();  // Polimorfismo dinámico
}
```

### 4. HALLAZGO

Sí se cumple:

El encapsulamiento está en private string nombre más la propiedad.

La herencia en la declaración de clases derivadas.

El polimorfismo en la llamada fig.Dibujar(), que ejecuta la versión adecuada.

### 5. REFLEXION

El diseño permite manipular diferentes figuras de manera genérica. Esto es la base de cómo después en ofApp manejamos std::vector<Particle*> sin importar el tipo concreto de partícula.

```
           ┌─────────────┐
           │   Figura    │
           │─────────────│
           │ - nombre    │   (campo privado)
           │ + Nombre{}  │   (propiedad: encapsulamiento)
           │ + Dibujar() │   (método virtual)
           └──────┬──────┘
                  │
   ┌──────────────┴───────────────┐
   │                              │
┌─────────────┐             ┌─────────────┐
│  Circulo    │             │ Rectangulo  │
│─────────────│             │─────────────│
│ + Dibujar() │ (override)  │ + Dibujar() │ (override)
└─────────────┘             └─────────────┘
```

Encapsulamiento en el campo privado nombre, herencia con la flecha desde Figura hacia Circulo y Rectangulo, polimorfismo en que cada uno sobrescribe Dibujar().

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
