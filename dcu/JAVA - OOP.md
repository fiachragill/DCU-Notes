# Getting Started

- Write code in a filename of {name}. java
- Filename ***MUST*** be same as class 

### Example HelloWorld.java:
````java
public class HelloWorld {

    public static void main(String[] args){

        System.out.println("Hello world");

    }

}
````

## How to compile a Java file

````
javac HelloWorld.java // enter to compile 
java HelloWorld // run program
````

## Visibility Options

![[Pasted image 20230202171117.png]]

- Java has 'visibilty' options to control what orther code can see and access it.

## Variables 

````java
int myNum = 5;
float myFloatNum = 5.99f;
char myLetter = 'D';
boolean myBool = true;
String myText = "Hello";
Double myDoubleNum = 3.1415926535897;
````

- General Assignment goes as follows:

````java
type variableName = value;
````

### Final Variables

- You can add the final keyword if you do not want you or other potential developers to overwrite existing values.
- This can be achived as follows

````java
final Double PI = 3.1415926535897;
// following line will generate an error as assignment is impossible
PI = 420.69;
````

### Data Assignment Rules

- Java is very strict about data types in assignment statements, Java only puts into a vraiable a value of the appropriate type.
- For example only expressions having an integer value can map to an Integer variable.

````java
int i;
double x = 3.0;
i = 10.3 * x; // this statement is illgeal
// 10.3 * x results in a float therefore i cannot be mapped.
````

### Conversion between Data types

- Type casting is when you assign a value of one primitve data type to another type. The cast operation let's you explicityly convert one type to another.

````java
// You can typecast to convert a variable of one data type to another. 
// Wide Casting converts small data types to larger ones. 
// Narrow Casting converts large data types to smaller ones. 
// Java can automatically Wide Cast. 
// Java will throw an error when trying to automatically Narrow Cast. 
// This is because data is often lost when Narrow Casting. 
// Narrow Casting must be done manually. 
//Wide Cast: 
int SomeNumber = 5; 
double WideCastedNumber = (double)SomeNumber; 
//Narrow Cast: 
double SomeNumber = 5.39; 
int NarrowCastedNumber = (int)SomeNumber; 
//Note: The data that holds the decimal places will be lost!
````

## Increment/Decrement

````java
x = x + 1; //is equivalent to:
x++;
//and likewise
x--;
````

## Arrays

- Arrays can be defined as follows

````java
int[] scores; //array of ints
scores = new int[7]; // scores can hold 7 ints

int[] scores = {1, 2, 3, 4, 5, 6, 7};
scores[0] // = 1
scores[1] // = 2
//ect.
````
