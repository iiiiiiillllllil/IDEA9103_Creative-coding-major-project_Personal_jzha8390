# IDEA9103_Creative coding major project_Personal_jzha8390
 Personal work
Thank you for reading this README file.

I've already written comments in the code on what each piece of code does, so here I think I need to go into some technical detail.

# Topic Selection
I choose time-based animation effects, the effect is that the theme color will switch every second after 5 seconds.

Wait 5 seconds for the animation to start, the color will be switched once every second, and colorful balls will be generated continuously from the middle.

## Coding
I added the following code to my individual assignments：
```
if(frameCount>300&&frameCount%60==0){
  //Switching once per second after 5s
     palette = []
    createComposition();
      for (let i = 0; i < 12; i++) {
    let randomColor = '#' + Math.floor(Math.random()*16777215).toString(16); // Generate random hexadecimal colors
   palette.push(randomColor); // Add the generated color to the array
  }
  mainCol = '#' + Math.floor(Math.random()*16777215).toString(16)
    allColors = [...palette.slice(1), mainCol]
  }
  
  
  class Ball
{
  constructor(diam_, _angle)
  {
    this.center = createVector(width/2, height/2); 
    this.dir = createVector(cos(_angle), sin(_angle));
  this.pos = this.center.copy().add(this.dir.mult(1));
    this.diam = diam_;
  this.col = color(map(this.dir.heading(), -PI, PI, 0, 100), 90, 100);
  }
  
  move()
  {
  this.pos.add(this.dir);
  const d = dist(this.pos.x,this.pos.y, this.center.x,this.center.y);
  const s = min(width,height);
  
  if(d > s*0.4)this.diam = map(d,s*0.4,s*0.45,s*0.04,0,true);
  else if(d > s*0.3)this.diam = map(d,s*0.3,s*0.4,s*0.023,s*0.042,true);
  else this.diam = map(d,0,s*0.1,0,s*0.021,true);
  }
   
  display()
  {
  noStroke();
  fill(this.col);
    ellipse(this.pos.x, this.pos.y, this.diam, this.diam);
  }
  
  isDead()
  {
    if (dist(this.pos.x,this.pos.y, this.center.x,this.center.y) > min(width,height)) return true;
    else return false;
  }
 
}
```
#### Technical Notes
# Part 1
If the number of frames exceeds 300 and every 60 frames, the code regenerates the color palette (palette) and the main color (mainCol) and calls the createComposition() function to regenerate the composition pattern. Detial:
>if(frameCount>300&&frameCount%60==0){
  //Switching once per second after 5s
     palette = []
# Part 2
In the createComposition() function, some random small squares are first generated and added to the rectangle array until a certain number is reached. Then, a circle of small squares is generated at the edges and they are added to the rectangle array.
Next, assign internal colors to some of the cubes. The colors come from the color palette(palette) and the (mainCol). Detials:
>createComposition();
      for (let i = 0; i < 12; i++) {
    let randomColor = '#' + Math.floor(Math.random()*16777215).toString(16); // into random hexadecimal colors
   palette.push(randomColor); // The generated color is added to the array
  }
  mainCol = '#' + Math.floor(Math.random()*16777215).toString(16)
    allColors = [...palette.slice(1), mainCol]
  }
# Part 3
 The rectanglesIntersect() function is used to determine whether two rectangles intersect.
generateRectangle() function is used to generate random rectangles.
The drawRectangle() function is used to draw a rectangle with an inner color. It uses a loop to draw the boundaries of the rectangle and fills the boundaries with a randomly chosen color.
A steady stream of colored blobs are generated from the middle , the
The constructor of the ball accepts two parameters: the diameter of the ball and the initial angle.
In the constructor, the center point, direction of motion, position, diameter and color of the ball are initialized.
# Part 4 
The move() method:
The move() method is used to control the movement of the ball.
Updates the position of the ball according to the direction of its movement.
According to the distance between the ball and the center point, dynamically adjust the ball's diameter size.
display() method:
The display() method is used to display the ball on the canvas.
Sets the fill color and draws a filled circle to represent the ball.
isDead() method:
The isDead() method is used to check if the ball has moved out of the canvas range.
Returns true if the ball is outside the canvas boundaries, false otherwise. 
##### Acknowledgement
The code uses some functions from the p5.js library, such as createVector(), dist(), map(), etc., to handle operations such as vectors, distance calculations, and value mapping.
With map() function, the color is mapped according to the angle of the direction of motion of the sphere, so that the color of the sphere changes with the direction of motion.