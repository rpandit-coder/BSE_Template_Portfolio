# Fingerprint ID and Keypad Lockbox
This safe is unique to only the user, using fingerprint and keypad technology! Through a series of 
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Rhea P| Trinity School | Neuroscience/Bioengineering | Rising Junior

![Headstone Image](https://bluestampengineering.com/wp-content/uploads/2016/05/improve.jpg)
 
 <details>
<summary>Bill of Materials</summary>
<br>
 Servos
Safe box thing
Fingerprint scanner
Keypad
Arduino UNO
LEDs
Research RGB leds to see how it might turn red or green
Wires 
LCD screen 
Power source 
</details>

# Final Milestone
My final milestone is ...

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My second milestone is ...
[![Second Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1625232439/video_to_markdown/images/youtube--Q9LxzEajmmc-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/Q9LxzEajmmc "Second Milestone"){:target="_blank" rel="noopener"}
# First Milestone
My first milestone was getting the keypad and RGB LED up and running with the Arduino! So I first tinkered around to make create a code that worked with the keypad. Each number or letter button on the 4 x 4 keypad was expressed by the input of two different pins on the Arduino. I used an array for the rows, using 4 pins on the Arduino, and another array to express the 4 columns of the keypad. Using arrays, in this project was especially useful for making a specific code to punch into the keypad. I created an array with my desired code, and then an array with "null" numbers represent the last 4 numbers pressed into the keypad. If the last 4 numbers pressed onto the keypad are the same as the correct code, then the RGB LED light turns green, and the serial monitor prints "CORRECT". And if the wrong code is pressed, then the LED turns "red", and the serial monitor reads "INCORRECT". 
<details>
<summary>First Milestone Code: With the Keypad and RGB LED</summary>
<br>

#include <Keypad.h> 

#include <Password.h> 

const byte ROWS = 4;
const byte COLS = 4;

char hexaKeys[ROWS][COLS] = {
  {'1', '2', '3', 'A'},
  {'4', '5', '6', 'B'},
  {'7', '8', '9', 'C'},
  {'*', '0', '#', 'D'}};

char keypressed;                 //Where the keys are stored it changes very often
char code[4] = {'1', '5', '9', '0'};
char lastpressedkeys[4] = {'\0', '\0', '\0', '\0'};

short a = 4, i = 0, s = 0, j = 0; //Variables used later

byte rowPins[ROWS] = {13, 12, 11, 10};
byte colPins[COLS] = {9, 8, 7, 4};

Keypad Mykeypad = Keypad(makeKeymap(hexaKeys), rowPins, colPins, ROWS, COLS);
char customKey = Mykeypad.getKey();

int redPin = 6;
int greenPin = 5;
int bluePin = 3;

void setup() {
  Serial.begin(9600);

  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
  //int myPins[5] = {'1', '5', '9', '0'};
}
 
void ReadCode() {                 //Getting code sequence
  i = 0;                    //All variables set to 0
  a = 0;
  j = 0;

  while (keypressed != 'A') {                                   //The user press A to confirm the code otherwise he can keep typing
    

  }
  keypressed = NO_KEY;
}
void setColor(int red, int green, int blue)
{
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);  
}
void loop() {

  char customKey = Mykeypad.getKey();

  if (customKey) {
    Serial.println(customKey);
  }

  if (customKey == '*') {                    // * to turn on LED
    Serial.println("TestingCode");

    
    bool correctcodeentered = true;
    for (int index = 0; index < 4; index++) {
      if (code [index] != lastpressedkeys[index]) {
        correctcodeentered = false;

      }
      Serial.print("Index: "); Serial.print(index); Serial.print(". Last pressed: "); Serial.print(lastpressedkeys[index]); Serial.print(" correct code"); Serial.println(code[index]);
    }

    if (correctcodeentered) {       //The ReadCode function assign a value to a (it's correct when it has the size of the code array)
      Serial.println("CORRECT");
      //digitalWrite(2, HIGH);
      setColor(0, 255, 0);
        delay(3000);
       setColor(0, 0, 0);  
    }
    //Open lock function if code is correct
    else {
      Serial.println("INCORRECT");
      //digitalWrite(2, LOW);
      setColor(255, 0, 0);
      delay(3000);
       setColor(0, 0, 0);  
    }
  }
  else if (customKey != NO_KEY) {
    for (int index = 0; index < 3; index++) {
      lastpressedkeys[index] = lastpressedkeys[index + 1];
    }
    lastpressedkeys[3] = customKey; //lastpressedkeys always shows last 4 keys we pressed

  }



}


//once we hit customKey then it checks each recorded pin //

</details>

[![First Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1625232636/video_to_markdown/images/youtube--18KGtm8ud0g-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/18KGtm8ud0g "First Milestone")
