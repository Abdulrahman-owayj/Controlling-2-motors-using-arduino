# Controlling-2-motors-using-arduino

**Project discription**

I used an Arduino as a controller and 9V battery as a supply and L239D driver to control 2 motors of the robot, also included 4 buttons to control the robot movements and a variable resistance to set the speed initially.

Circuit diagram on tinkercad: https://www.tinkercad.com/things/7Id1rZ4bsQd-daring-fulffy/editel?tenant=circuits

**Diagram preview:**

![control 2 motors diagram](https://user-images.githubusercontent.com/5675794/123260871-c1045380-d4fe-11eb-832a-3799a32160dd.png)


The code of the project 

```ruby
// difine the pin numbers
int enable = 13;
int input1 = 9;
int input2 = 10;
int input3 = 6;
int input4 = 5;
int buttonForward = 2;
int buttonBackward = 7;
int buttonRight = 3;
int buttonLeft = 4;

void setup()
{
  // define the pin modes
  pinMode(buttonForward, INPUT);
  pinMode(buttonBackward, INPUT);
  pinMode(buttonLeft, INPUT);
  pinMode(buttonRight, INPUT);
  pinMode(input1, OUTPUT);
  pinMode(input2, OUTPUT);
  pinMode(input3, OUTPUT);
  pinMode(input4, OUTPUT);
  pinMode(enable, OUTPUT);
  
}

void loop()
{

  // condition to move forward  
  if (digitalRead(buttonForward) == HIGH)
  {
    int motorSpeed = speed();          // get the motor speed set by user
    digitalWrite(enable, HIGH);        // enable the two input of the driver
    digitalWrite(input1, LOW);         // Put this terminal to ground
    analogWrite(input2, motorSpeed);   // use pmw to move the motor with spicific speed
    digitalWrite(input3, LOW);         // Put this terminal to ground
    analogWrite(input4, motorSpeed);   // use pmw to move the motor with spicific speed
  }
  
  // condition to move backward  
   else if (digitalRead(buttonBackward) == HIGH)
   {
   int motorSpeed = speed();        // get the motor speed set by user
   digitalWrite(enable, HIGH);      // enable the two input of the driver
   analogWrite(input1 ,motorSpeed); // use pmw to move the motor with spicific speed
   digitalWrite(input2, LOW);       // set the other terminal to LOW (Ground)
   analogWrite(input3, motorSpeed); // use pmw to move the motor with spicific speed
   digitalWrite(input4, LOW); 
   }
     
    // condition to move Right
   else if (digitalRead(buttonRight) == HIGH)
   {
   int motorSpeed = speed();        // get the motor speed set by user
   digitalWrite(enable, HIGH);      // enable the two input of the driver
   digitalWrite(input1 ,LOW);        
   analogWrite(input2, motorSpeed);
   analogWrite(input3, motorSpeed);
   digitalWrite(input4, LOW); 
   }
  
    // condition to move Left
   else if (digitalRead(buttonLeft) == HIGH)
   {
   int motorSpeed = speed();        // get the motor speed set by user
   digitalWrite(enable, HIGH);      // enable the two input of the driver
   analogWrite(input1 ,motorSpeed); 
   digitalWrite(input2, LOW);      
   digitalWrite(input3, LOW);
   analogWrite(input4, motorSpeed);
   } 
     
   // if no button is pressed the motors will stop
  else
      digitalWrite(enable, LOW);
  
}

// difinition of (speed) function that return the speed set by user
int speed(){
 int a = analogRead(A0);
 a = map(a, 0,1023, 0 , 255);
 
  return a ;       // return the specified speed 
}

```
