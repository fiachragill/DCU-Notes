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

## Polymorphism

- Base Animal class:

````java
public class Animal {
	private String name;
	private String colour;

	public void eat() {
		System.out.println("munch");
	}

	public String getName() {
		return name
	}

	public void setName(String name) {
		this.name = name;
	}
}
````

- Dog class (an extension of the animal class)

````java
public class Dog extends Animal {
	private String breed; // adds new attribute (3 attributes now: name, colour and breed)

	@Override //good practice to mark override.
	public void eat() { // overrides eat function as seen in output.
		System.out.println("bark bark");
	}

	public String getBreed {
		return breed
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public void jump() {
		super.eat(); // the use of the super keyword will call eat from parent(Animal class)
		// i.e it's state prior to being overridden.
	}
}
````

- Testing class

````java

public class TestPolymorphism {
	public static main(String[] args) {

		Animal myAnimal = new Animal();
		myAnimal.eat();

		Dog myDog = new Dog();
		myDog.eat();
	}
}
````

````txt
Output:
========
"munch"
"bark bark"
````