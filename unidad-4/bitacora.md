# Evidencias para la unidad 4

## Código

Código para ofApp.h:

``` cpp
#pragma once
#include "ofMain.h"

// ====================== Nodo de la Cola ======================
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {}
};

// ====================== Clase BrushQueue (FIFO) ======================
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};

// ====================== Clase de la App ======================
class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo inicial = 50

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
```

Código para ofApp.cpp:

``` cpp
#include "ofApp.h"

// ====================== BrushQueue ======================

// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Agregar nodo al final
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);

    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    size++;

    // Eliminar el más antiguo si se supera el tamaño máximo
    if (size > maxSize) {
        dequeue();
    }
}

// Eliminar nodo más antiguo
void BrushQueue::dequeue() {
    if (!isEmpty()) {
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;

        if (front == nullptr) rear = nullptr;
    }
}

// Vaciar la cola
void BrushQueue::clear() {
    while (!isEmpty()) {
        dequeue();
    }
}

// Ver si está vacía
bool BrushQueue::isEmpty() {
    return size == 0;
}

// ====================== ofApp ======================

void ofApp::setup() {
    ofBackground(0);
    ofSetCircleResolution(50);
}

void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    // Agregar trazo si el mouse está presionado
    if (ofGetMousePressed()) {
        float x = ofGetMouseX();
        float y = ofGetMouseY();
        float radius = ofRandom(5, 20);
        ofColor color = ofColor::fromHsb(ofRandom(255), 200, 255);
        float opacity = ofRandom(80, 255);

        strokes.enqueue(x, y, radius, color, opacity);
    }
}

void ofApp::draw() {
    // Fondo dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // Dibujar los trazos de la cola
    Node* current = strokes.front;
    while (current != nullptr) {
        ofSetColor(current->color, current->opacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear(); // limpiar trazos
    }
    else if (key == 'a') {
        // Alternar entre 50 y 100
        strokes.maxSize = (strokes.maxSize == 50) ? 100 : 50;
        while (strokes.size > strokes.maxSize) {
            strokes.dequeue();
        }
    }
    else if (key == 's') {
        ofSaveScreen("screenshot.png");
    }
}

```

Código para main.cpp:
``` cpp
#include "ofApp.h"

// ====================== BrushQueue ======================

// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Agregar nodo al final
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);

    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    size++;

    // Eliminar el más antiguo si se supera el tamaño máximo
    if (size > maxSize) {
        dequeue();
    }
}

// Eliminar nodo más antiguo
void BrushQueue::dequeue() {
    if (!isEmpty()) {
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;

        if (front == nullptr) rear = nullptr;
    }
}

// Vaciar la cola
void BrushQueue::clear() {
    while (!isEmpty()) {
        dequeue();
    }
}

// Ver si está vacía
bool BrushQueue::isEmpty() {
    return size == 0;
}

// ====================== ofApp ======================

void ofApp::setup() {
    ofBackground(0);
    ofSetCircleResolution(50);
}

void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    // Agregar trazo si el mouse está presionado
    if (ofGetMousePressed()) {
        float x = ofGetMouseX();
        float y = ofGetMouseY();
        float radius = ofRandom(5, 20);
        ofColor color = ofColor::fromHsb(ofRandom(255), 200, 255);
        float opacity = ofRandom(80, 255);

        strokes.enqueue(x, y, radius, color, opacity);
    }
}

void ofApp::draw() {
    // Fondo dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // Dibujar los trazos de la cola
    Node* current = strokes.front;
    while (current != nullptr) {
        ofSetColor(current->color, current->opacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear(); // limpiar trazos
    }
    else if (key == 'a') {
        // Alternar entre 50 y 100
        strokes.maxSize = (strokes.maxSize == 50) ? 100 : 50;
        while (strokes.size > strokes.maxSize) {
            strokes.dequeue();
        }
    }
    else if (key == 's') {
        ofSaveScreen("screenshot.png");
    }
}
```

## Demostración:

[[Aquí está el video demostrativo de mi aplicación

<src="https://youtu.be/rmKRVZ1mLpc"></iframe>


### Link p5.js 
<src="https://editor.p5js.org/antonellavides/full/X62OG7hg0"></iframe>



