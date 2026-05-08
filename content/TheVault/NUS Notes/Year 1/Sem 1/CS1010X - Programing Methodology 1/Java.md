---
Title: Java
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Java
---

## Table of Content
- [[#Differences between Java and Pythion|Differences between Java and Pythion]]
- [[#Function Declaration|Function Declaration]]
- [[#Type Conversion|Type Conversion]]
	- [[#Type Conversion#Promotion (Widening)|Promotion (Widening)]]
	- [[#Type Conversion#Demotion (Narrowing)|Demotion (Narrowing)]]
- [[#Conditional Statements|Conditional Statements]]
- [[#Flow Control (While and For)|Flow Control (While and For)]]
- [[#Array|Array]]
	- [[#Array#Creating an Array|Creating an Array]]
	- [[#Array#Looping Through an Array|Looping Through an Array]]
	- [[#Array#Array-List|Array-List]]
- [[#Scanner Class|Scanner Class]]
- [[#Print-f|Print-f]]
- [[#Classes In Java|Classes In Java]]
	- [[#Classes In Java#Features of OO Language|Features of OO Language]]
	- [[#Classes In Java#Accessibility|Accessibility]]
	- [[#Classes In Java#Creating a Class|Creating a Class]]
	- [[#Classes In Java#"This"|"This"]]
	- [[#Classes In Java#Dynamic Polymorphism|Dynamic Polymorphism]]
- [[#Interfaces|Interfaces]]
---
<div style="page-break-after: always;"></div>

## Differences between Java and Pythion
---
- Better for object orientation programming
- Need to declare the type for the variable and the type cannot be changed
- all lines of code ends with a ;
- { } is used to enclose the body for the functions

```Java
public float expt(float x, int n)
{
	if (n == 0)
	{
		return 1;
	}
	
	else
	{
		return x * expt(x, n-1);
	}
}
```
<div style="page-break-after: always;"></div>

## Function Declaration
---
Sample Java code as shown above

```Java
public static float expt (float x, int n){
	pass
}

/*
The first word is the access modifier private means can only be accessed within the class while public can be accessed outside the class

static means that there is only one instances of the function and it is owned
by the class and not an instance of the class. Without the static word you need an object to access it 

return type must be stated for each function, void means that it returns nothing. The return type must be followed
*/

private void expt (float x, int n){
	pass
}

//The following code is special function, when code is executed it will find the main function. This is where the program begins*

public static void main(String [] args){

}
```
<div style="page-break-after: always;"></div>

## Type Conversion
---
When dealing with different operands of different types;
1. If one is a `double`, convert the other to a `double`
2. Else, if one is a `float`, convert the other to a `float`
3. Else, if one is a `long`, convert the other to a `long`
4. Else, convert both into an `int`

### Promotion (Widening)

Promotion of a variable means that the system will auto convert a variable if the value has a smaller range compared to the variable.
```Java
int x = 12;
double d;

d = i/10; // d = 1.0 instead of 1.2 since i and 10 are both integers
```

### Demotion (Narrowing)
Do type casting to manually change the variable type, usually done when the value has a larger range compared to the variable.
```Java
double d;
int i;

d = 1.2;
i = (int) d; // I will be 1 since we cast the value of d into a int
```
<div style="page-break-after: always;"></div>

## Conditional Statements
---
**If & Else**
```Java
int time = 22;

if (time < 10){
	System.out.println("Good morning");
}
else if (time < 20){
	System.out.println("Good day.");
}
else{
	System.out.println("Good evening");
}

// OR

int time = 20;

String result = (time < 18) ? "Good day" : "Good evening"; // ? is like if : is like else
System.out.println(result);
```

**Switches**

Is another way to write if else statements based on a variable's value.
```Java
public static void main(string[], args){
	char Grade = "B";
	switch (Grade){
		case "A": // If Grade == A
			System.out.printLn("You are Grade A Employee: Bonus = " + 2000)
			break; # Have to use break to get out of the switch
		case "B":
			System.out.println("You are Grade A Employee: Bonus = " + 1000)
			break;
		case "C":
			System.out.println("You are Grade A Employee: Bonus = " + 500)
			break;
		case "D":
			System.out.println("You are Grade A Employee: Bonus = " + 100)
			break;
	}
}
```
<div style="page-break-after: always;"></div>

## Flow Control (While and For)
---
**While**

```Java
while (a > b) {
	// Body
}
// OR
do {
	//body
} while (a > b)

/*
Both are acceptable, however the latter will execute the code once before doing the conditional check, the former will check before executing the code
*/
```

**For**

```java
for (int i = 0; i < 10; i++){ 
// Declare loop controle variable, checking condition and incrementing loop control variable
	// Body
}
for (int i = 0; i < 10; i--){
	// Body
}
```

**Increments**

`++i`, is a pre-increment operator where it increments the value of `i` by 1 and returns the incremented value.

`i++`, is a post-increment operator which also does increment `i` by 1 but returns the original value (Pre-Incremented).

```Java
class Increment{
	public static void main(String[] args) { 
		int i = 1;
		System.out.println(i++); // 1
		System.out.println(++i); // 3
	}
}
```
<div style="page-break-after: always;"></div>

## Array
---

An array is like a list however it has a fixed length.
To change the length of the length, a new array needs to be created.

### Creating an Array

```java
// 1D Array
int [] intarray = new int[] {10,20,30,40}

// Multidiemtional array
int [][] multiintarray = new int[][] {{1,2,3,4},{5,6,7,8}}

// Creating a empty array
int [] new_array = new int[5]; // It makes a empty array of size 5
```

### Looping Through an Array

```Java
int [] intarray = new int[] {10,20,30,40}

int length = intarray.length; // Get the length of an array

// Using indexes
for (int i = 0; i < length. i++){
	System.out.println(intarray[i])
}

// Using values
for (int i : intarray){
	System.out.println(i)
}
```
<div style="page-break-after: always;"></div>

### Array-List

An array list acts like a python list where the length is not fixed.

For an array list if you don't specify the variable type stored, java will not know what inside the array list and will return a object type.

We can add an element into a undefined variable type array list, by putting it straight into the ()

```Java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    cars.set(0, "Opel"); // Set the index of the arraylist to another value
    cars.remove(0); // Remove an item based on index
    cars.size(); // Get the length of the array list
    cars.clear(); // Empty the array list
    
    System.out.println(cars.get(0)); // Get an item based on index
```
<div style="page-break-after: always;"></div>

## Scanner Class
---
The scanner class is used to get inputs from users and use it in the program.

```Java
import java.util.Scanner;

class Temperature {
	public static void main(String[], args){
		double fahrenheit, celcius;
		Scanner = myScanner = new Scanner(System.in);

		// Requests an input from the user
		System.out.printLn("Enter temperature in Fahrenheit: ");
		// Sets the input into a variable
		fahrenheit = myScanner.nextDouble();

		celcius = (5.0/9) * (fahrenheit - 32)
		System.out.println("Celcius: " + celcius);
	}
}
```

## Print-f
---
Its a method to format string outputs in Java.

```Java
public static void main(String[], args){
	System.out.printf("PI = %.6f\n", PI) // For 6 decimal points
}
```

**Different types of formatting with print-f**

| Symbol |   Type    |
|:------:|:---------:|
|   %c   | Character |
|   %d   |  Decimal  |
|   %f   |   Float   |
|   %i   |  Integer  |
|   %s   |  String   |
<div style="page-break-after: always;"></div>

## Classes In Java
---

Java as an OO language is easier to design and easy to maintain as it is modular and extensible.

However, it is less efficient as its removed from low level execution and the program is usually longer with high design overhead.

### Features of OO Language

**Encapsulation**
-  Group data and associated functionalities into a single package
-  Hide internal details from outsider

**Inheritance**

-  A method of extending current implementation
-  Introduce logical relationship between packages
-  Functions will be searched in the subclass, followed by the superclass

**Polymorphism**

-  Behavior of the functionality changes according to the actual type of data
-  Allows the same function name to have different inputs based on the class requirements


### Accessibility

**Public**
- Anyone can access the variable or function
- Intended for functions only

**Private**
- Only can be access within the class or functions in the class
- This is recommended for attributes
- Static methods cannot access private objects unless an instance of the object is passed into the function.
<div style="page-break-after: always;"></div>

**Protected**

- Is a more relaxed version of the private accessibility level
- Can be access by the same class, its children classes and classes in the same java package
- Recommended for things that are common in the "Family"

**None**
-  Only accessible to classes in the same Java package
-  Known as the package private visibility


### Creating a Class

**Sample Code for making a Class**

Below displays a-lot of OOP concepts in Java such as
1. Inheritance
2. Encapsulation
3. Polymorphism
4. Substitution
5. Overriding 

```java
class BankAccount {

	// The reason we are using protected is because we have a sub class which
	// Needs access to the parent class attribute
	protected int _acctNum;
	protected double _balance;

	/*
	Constructors are use to create the object, it is public so it can be used
	outside of the class. It has no return value. If there is no constructor
	Java will auto create one with no input and all attributes will be 0
	The name of the consturctor must be the same name as the class
	*/

	// Constructor with no parameters
	public BankAccount() {
		// Initialize all attributes to 0
	}

	// Constructor with parameters
	public Bankaccount(int aNum, double bal) {
		//initalize attributes with uer provided values
		_acctNum = aNum;
		_balance = bal;
	}

	public boolean withdraw (double amount) {
	
		if (balance < ammount)
			return false;

		_balance -= amount;
		return true;
	}

	public void deposit (double amount) {
	
		if (amount <= 0)
			return;
			
		_balance += amount;
	}

	public void print() {
		System.out.println ("Account Number: " + _acctNum);
		System.out.println ("Balance: $%.2f\n" + _balance);
	}
}

// The below is an exmaple of a subclass
class SavingAcct extends BankAcct {

	protected double _rate;

	public SavingAcct (int aNum, dobule bal, double rate) {

		super(aNum, bal); // Call the superclass constructor
		_rate = rate;
	}

	public void print () {

		super.print(); // This will call the superclass print function
		System.out.printf("Interest: %.2f \n", _rate);
	}

}

// The class for the compliler
class CodeRuner {

	// The below function works for SavingsAcct or any subclass of BankAcct
	// As all functions that work with the superclass works with the subclass
	public ststic void transfer (BankAcct fromacct, BankAcct toAcct, double amt) {
		// Some code

		// This function transfer works for both Bankaccount and SavingsAcct
	}

	public static void main (String[] args) {
		
	}
}
```

```Java
class TestBankAcct{
	public static void main (String[] args) {
		BankAcct bal1 = new BankAcct();

		bal1.deposit(1000); // Balance = 1000 as we used the default constructor with no parameter

		bal1.balance += 1000 // Error will arise as the accessibility of the attribute is only with in the class BankAcct
	}
}
```

**Reference Data Type**

```Java
class TestBankAcct{
	public static void main (String[] args) {
		BankAcct bal1 = new BankAcct(); // This is a reference to a BankAccount object
		BankAcct bal2; // This is just creating a variable name with refrence to the BankAcct class, its a Null pointer as it is assigned with nothing
		
		bal2 = bal1
		bal1.deposit(1000)
		bal2.print() // Will print Account Name 0 and Balance: 1000
	}
}
```
<div style="page-break-after: always;"></div>

### "This"

The keyword `this`, is used as a reference to call the object.

```Java
// Without using the keyword this
public void deposit (double amount) {
	
		if (amount <= 0)
			return;
			
		_balance += amount;
}

// Using the keyword this
public void deposit (double amount) {
	
		if (amount <= 0)
			return;
			
		this._balance += amount;

/*
Using the key word this is a good practice as if there are 2 objects with the same class, we will need to indicate which object attribute to access.
*/
}
```

### Dynamic Polymorphism

A superclass reference can refer to an object of a subclass

```Java
public static void main (String[] args) {
		SavingAcct bal1 = new SavingAcct(2, 1000.0, 0.03); 
		BankAcct bal2;
		
		bal2 = bal1
		bal2.print() // Will also print out the interest rate. It will use the SavingAccct print() function.

		bal2.payInterest(); // Will raise a compilation error as BankAcct does not have a function called payInterest. This is because it does not check the variable type of the actual object.
}
```

This works because `bal2`, is a reference to an object `bal1`. When a method is called, it will find the function that is <mark style='background:#fa8231'>associated to the referenced object</mark>, `bal1`. If its not found it will search in the Superclass of `bal1`.
<div style="page-break-after: always;"></div>

## Interfaces
---
It is another way to achieve abstraction where a class an **implement** an abstract class.

For a class to inherit from a interface, use the keyword `impliments`. The difference between `impliments` and `extend` is that a class can implement from multiple interfaces while it can extend from on one superclass only.

```Java
interface Test1{
	public void function_1(); // The functions in the interface MUST HAVE NO BODY
}

interface Test2{
	public int function_2(int i);
}

class Testing impliments Test1, Test2 {
	public void function_1(){
		System.out.println("Yes this is function 1")
	}
	public int function_2(int i){
		return i + 1
	}
}
```