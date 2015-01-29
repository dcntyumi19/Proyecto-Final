# Proyecto-Final

//Creación del objeto martillo
Martillo martillo1 = new Martillo(10, 10);
//Declaracíon de variables globales para moviento del zombie
float posX = 300; 
float posY = 300;
int lastMillis = 0;
int cont = 0;
//Switch pa condicion start de iniciar juego 
int start = 0;
//Declaración de parametro para importar imágen
PImage img;

void setup() {
  size(800, 600);
  imageMode(CENTER);
  //Asignación de la imágen a la variable img
  img = loadImage("monster.png");
}

void draw() {
  background(255); 

  if (start == 0) {
    fill(0, 0, 255);
    rect(width/2 - 50, height/2, 100, 50);
    fill(255);
    textSize(20);
    text("INICIAR", width/2 - 35, height/2 + 35);
  }
  if (start == 1) {
    //Despliegue de la imágen con parametros de posicion y escala
    image(img, posX, posY, img.width/5, img.height/5);
    //despliegue del martillo en el escenario con funcion display()  
    martillo1.display();
    changePosRectangle();
    fill(255, 0, 0);
    textSize(30);
    text(cont, width/2, 50);
    }
  }
  void mouseClicked() {
    start = 1;
  }
  //Función del mouse para intereactuar con el zombie (objeto)
  void mousePressed() {

    if (mouseY <= posY) {
      cont = cont + 1;
      if (cont == 5) {
        background(255);
        textSize(50);
        fill(0, 0, 255);
        text("GANASTE", 300, 500);
        fill(255, 0, 0);
        stop();
      }
      println("PUM");
    }
    println("FALLASTE");
  }

  //Funcion para controlar el tiempo 
  void changePosRectangle() {
    int thisMillis = millis();
    if (thisMillis-lastMillis>700) {
      posX=random(0, width);
      posY=random(0, height);
      lastMillis = thisMillis;
    }
  }

  //Declaración de la clase martillo con parametros de posicion para "tracking" con el mouse
  class Martillo {
    int x;
    int y;
    PImage imgMartillo;
    Martillo(int x_, int y_) {
      x = x_;
      y = y_;
    }
    //Declaracion de la funcion display para desplegar martillo en el escenario y traking con el mouse
    void display() {
      imgMartillo = loadImage("martillo.png");
      image(imgMartillo, mouseX, mouseY, img.width/5, img.height/5);
    }
  }
