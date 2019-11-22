/*
  Description: Processing Assignment Two
 Author: Mihir Kachroo
 Date of last edit: November 18
 */

float moveBirdY;

boolean darkMode;

int currentScore, topScore;

void settings() {
  size(950, 650);
}

void setup() { 
  textAlign(CENTER);

  moveBirdY=0;
  darkMode=true;
  
  currentScore=0;
  
  //Creates the background
  for (int i=0; i<height; i+=1) {
    if (darkMode==true) {
      stroke(61-i/15, 80, i/5+90);
    } 
    else {
      stroke(76, 188, 252);
    }
    line(0, i, width, i);
  }

  if (darkMode==true){
    createWhiteDots();
    createStars();
  }
}

void draw() {

  //Flappy Bird
  stroke(0);
  strokeWeight(1.7);
  fill(240, 190, 83);
  ellipse(200, 300+moveBirdY, 43, 35); //Yellow body
  fill(245);
  ellipse(210, 292.5+moveBirdY, 20, 19); //White eye
  fill(230);
  rect(175, 298+moveBirdY, 18, 10, 8); //White wing
  fill(253, 104, 74);
  rect(207, 300+moveBirdY, 20, 6, 100); //Upper lip
  rect(207, 306+moveBirdY, 17, 6, 100); //Lower lip
  triangle(207, 301+moveBirdY, 202, 306+moveBirdY, 207, 311+moveBirdY); //Side of lip
  strokeWeight(0);
  triangle(209, 303.5+moveBirdY, 203, 306+moveBirdY, 209, 310+moveBirdY); //Covers the join between the upper, lower and side lip
  strokeWeight(5.8);
  point(214, 292.5+moveBirdY); //Black eye pupil

  //use for loop for dark to light mode

  //The pale ground
  noStroke();
  fill(230, 180, 120);
  rect(0, height, 950, -45);

  //The green track
  createGreenTrack();

  //Gold Point
  fill(220, 185, 9);
  ellipse(200, 200, 25, 25);
  fill(250);
  textSize(20);
  text(5, 200, 206);

  //Current Score
  textSize(50);
  fill(250);
  text(5, width/2, 75);
}

void keyPressed() {
  if (key==' ' || keyCode==UP) {
    moveBirdY-=1;
  }
}
void createWhiteDots() {
  for (int i=0; i<19; i+=1) {
    fill(255);
    ellipse(random(width), random(-10, 400), 3, 3);
  }
}

void createStars() {
  for (int i=0; i<15; i+=1) {
    noStroke();
    if (i%3==0) {
      fill(70, 100, 160);
    } else {
      fill(255, 246, 0);
    }
    rect(random(width), random(10, 300), 0, 0, -6);
  }
}
int x;
void createGreenTrack() {
  for (int i=0; i<90000; i+=40) {
    strokeWeight(2);
    stroke(10);
    fill(118, 190, 51);
    rect(i-x+1, height-47, 40, 10, 3);

    noStroke();
    fill(152, 218, 91);
    rect(i-x+3, height-44.5, 15, 6.5, 1);
  }
  x+=1;
}

void startScreen(){
  //Information box
  stroke(0);
  strokeWeight(6);
  fill(220,213,135);
  rect(275,250,400,100);
  
  //Start Game text
  textSize(55);
  fill(251, 150, 72);
  text("Start Game", 480, 215);
  
  textSize(27);
  
  //Current Score and Top Score Text
  text("Current Score", 490, 285);
  text("Top Score", 472, 331);
  
  //Displays Current Score and Top Score Numbers
  fill(255);
  text(currentScore, 330, 285);
  text(topScore, 330, 331);

    //Highlights (by changing the colour) the option which the user is hovering over
    if (mouseX<405 && mouseX>275 && mouseY<430 && mouseY>380) {
      fill(49);
    } 
    else {
      fill(0); //The default colour if the user is not hovering over the option
    }

    //Creates the left rectangle
    stroke(255);
    strokeWeight(4);
    rect(275, 380, 130, 50);

    //Highlights (by changing the colour) the option which the user is hovering over
    if (mouseX<675 && mouseX>545 && mouseY<430 && mouseY>380) {
      fill(190);
    } else {
      fill(255); //The default colour if the user is not hovering over the option
    }

    //Creates the right rectangle
    stroke(0);
    rect(545, 380, 130, 50);

    if (mousePressed) {
      if (mouseX<405 && mouseX>275 && mouseY<430 && mouseY>380) { //If the user selects the play option
       println("h");
      }
      
      else if (mouseX<675 && mouseX>545 && mouseY<430 && mouseY>380) { //If the user selects the quit option
        exit(); //Exits program
      }
    }

    //Writes the text for the options of playing or quitting
    textAlign(CENTER);
    fill(0, 102, 153);
    textSize(25);
    text("Play", 340, 413);
    text("Quit", 610, 413);
}
