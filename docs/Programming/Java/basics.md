# Basics

## Start
```java
public class BasicsOfJava {
    static public void main(String[] args){
        System.out.println("Hello, World!");
    }
}
```
**public**: Means the method (or class) can be called from outside. For example, if the method `goUp()` inside the `Helicopter` class is public, it will be possible to call `Helicopter.goUp()` from outside the class. On the other hand, a non-public function like `convertKnotsToMetric()` will not be callable through `Helicopter.convertKnotsToMetric()` from outside the class. The method `goUp()` could however still call `convertKnotsToMetric`. The main function must always be public since it is the entrypoint of the program.

**static**: Means the value or method doesn't need to be part of an instanciated class (an object) to be accessed or executed. This is mostly used to store "constants" (but for this we can also use the keyword `final`).

**void**: Means the method returns nothing (but it doesn't mean it *does* nothing). Usually, the main method doesn't return anything.

**String[] args**: Makes possible the usage of command-line arguments. `args` can be renamed, but it's best to follow convention. It is then possible to access the arguments as a `String` array (ie `args[0]`). Unlike bash, the first argument is at position `args[0]`. The command used to call the programm isn't in the arguments' array.

## Arrays
### 1D Arrays
```java
int [] myArray;
myArray = new int[10];
```
Creating a new array can also be done in one step:
```java
int [] myArray = new int[10];
```
### nD Arrays (or "Arrays of arrays")
```java
int [][] matrix;
matrix = new int[3][4];
```
When initializing an array with `new int[3][4]`, the last number represents the values the deepest array can contain. In this example, each 3 arrays contained in matrix[][] will be able to hold 4 values:
{
    {1, 2, 3, 4},
    {1, 2, 3, 4},
    {1, 2, 3, 4}
}

`new int[5][4][3][2]` will look like this:
```java
{
    {
        // 1
        {
            // 1.1
            {1, 2}, // 1.1.1
            {1, 2}, // 1.1.2
            {1, 2}  // 1.1.3
        },

        {
            // 1.2
            {1, 2}, // 1.2.1
            {1, 2}, // 1.2.2
            {1, 2}  // 1.2.3
        },

        {
            // 1.3
            {1, 2}, // 1.3.1
            {1, 2}, // 1.3.2
            {1, 2}  // 1.3.3
        },

        {
            // 1.4
            {1, 2}, // 1.4.1
            {1, 2}, // 1.4.2
            {1, 2}  // 1.4.3
        }
    },

    {
        // 2
        {
            // 2.1
            {1, 2}, // 2.1.1
            {1, 2}, // 2.1.2
            {1, 2}  // 2.1.3
        },

        {
            // 2.2
            {1, 2}, // 2.2.1
            {1, 2}, // 2.2.2
            {1, 2}  // 2.2.3
        },

        {
            // 2.3
            {1, 2}, // 2.3.1
            {1, 2}, // 2.3.2
            {1, 2}  // 2.3.3
        },

        {
            // 2.4
            {1, 2}, // 2.4.1
            {1, 2}, // 2.4.2
            {1, 2}  // 2.4.3
        }
    },

    // Repeated until 5
}
```

## Conditionals

### If/else
```java
if(nb == 0){
    System.out.prinln("nb is null");
}
else if(nb > 0){
    System.out.println("nb is positive");
}
else {
    System.out.println("nb is negative");
}
```
### Switch
```java
int nb = 4;

switch (nb) {
    case 1:
        System.out.println("The number is one");
        break;
    case 2:
        System.out.println("The number is two");
        break;
    case 3:
        System.out.println("The number is three");
        break;
    default:
        System.out.println("The number is not one, two or three.");
}
```

## Loops

### For
```java
for(int i = 0; i < myArray.length; i++){
    System.out.println(myArray[i]);
}
```
### For-each
```java
String[] daysOfTheWeek = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};

for(String i : daysOfTheWeek) {
    System.out.println(i);
}
```
This can also be done with 2D arrays:
```java
for (int[] line : matrix) {
    for (int value : line) {
        System.out.println(value);
    }
}
```

### While
```java
int nb = 0;
while(nb < 20){
    keepPushing();
    nb ++;
}
```

### Do While
```java
do {
    putHandsInTheAir();

} while (isTheMusicgood());
```

### Keywords for Loops
#### Continue
`continue;` is used to pass an iteration of the loop, and start the next iteration.

#### Break
`break;` is used to break out of the loop entirely, and execute the rest of the program.

## Operators

### Comparison Operators

#### == (EQUAL TO) and != (NOT EQUAL TO) (reference testing)
It is **essential** to know that `==` may not have the same behaviour depending on wether we want to compare primitives or objects.
- For primitive types (byte, short, **int**, long, float, **double**, **boolean**, **char**), `==` compares their __**values**__.
- For objects, `==` compares their __**references**__. This means that comparing two objects containing the same values, even if one is copied from the other, will almost always return `FALSE`.

For example, the following code will return `FALSE`:
```java
public class EqualityTesting {
    public static void main(String[] args){
        Integer nb1 = 9756;
        Integer nb2 = 9756;
        System.out.println(nb1 == nb2);
    }
}
```
Note that because of *caching* (true for Integers lower than 128) or *String constant "interning"*, comparing two objects might return `TRUE`. This is because for some reasons, Java uses the same **reference**. Since those are exceptions, it's best not to count on it.

To compare the *logical* values of two objects, it is better to use a user-defined .equals method.

### Logical Operators
#### && (AND)
```java
if (isItSunny() && isItWarm() && amIFree()) {
    System.out.println("Time to go to the beach!");
}
```
Using `&&`, the first `FALSE` to return from a function will stop the comparison and return `FALSE`. The operator `&` is used if it is necessary to execute every function before the comparison even returns a boolean. In the example above, if it is not sunny, `&&` will return `FALSE` after `isItSunny()`. `isItWarm()` and `amIFree()` will not even be executed. If we use `&`, all the functions will be executed before the comparison returns `FALSE`.

#### || (OR)
```java
if (isHungry() || isThursty()){
    openFridge();
}
```

## Objects

An object is an instance of a class. This object is "callable" through a **reference** ("a variable that refers to something else and can be used as an alias for that something else").

To create a new object in Java, we first write the class and it's constructor:
```java
public class Sailboat {
    int size;
    int weight;
    int sailArea;
    int maxSpeed;
    String name;
    String port;

    Sailboat(int size, int weight, int sailArea, int maxSpeed, String name, String port) {
        this.size = size;
        this.weight = weight;
        this.sailArea = sailArea;
        this.maxSpeed = maxSpeed;
        this.name = name;
        this.port = port;
    }
}
```
Note about **constructors**: "A constructor in Java is a special method that is used to initialize objects. The constructor is called when an object of a class is created. It can be used to set initial values for object and attibutes" (W3schools).

Then, we create an instance of this object:
```java
Sailboat mySailboat = new Sailboat(10, 6000, 171, 18, "Sunny", "Oostende");
```

We can also split the line like this:
```java
Sailboat mySailboat;
mySailboat = new Sailboat(10, 6000, 171, 18, "Sunny", "Oostende");
```

