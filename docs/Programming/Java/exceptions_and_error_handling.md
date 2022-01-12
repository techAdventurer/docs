# Exceptions and error handling

## What is an exception?
> An *exception* is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions. (docs.oracle.com)

There are essentially three types of exceptions:
- Checked: This type of exception is (or should be) expected by the programmer (ie FileNotFoundException). The program won't compile if this type of exception is not handled.
- Unchecked: This type is not expected. It can be a programming mishap, an unexpected input, ...etc. The program can compile but unexpectedly crashes at runtime. Caring for it is not mandatory for the program to run (but can be useful if the program needs to be resilient).
- Errors: The error is an exception that is not expected and is external to the program. This can be because of a hardware malfunction (hard disk failure, ...etc).


## Try, catch, finally statements
The syntax to catch an exception is the following:
```java
try {
    // Code we expect to crash at some point
}
catch (ExceptionType name) {
    // What to do if it crashes because of ExceptionType
}
catch (AnotherExceptionType name) {
    // What to do if it crashes because of AnotherExceptionType
    // We can write as many catch statements as we can, from the
    // most precise exception type, to a broader one.
}
finally {
    // What to do regardless of everything happening (optional).
    // If the exception isn't of ExceptionType or AnotherExceptionType,
    // the program will execute this part of the code and then crash.
    // If everything happens as expected, without exceptions, this code
    // will still be executed. Useful to close sockets or a connexion to
    // a database.
}
```
Note that the `ExceptionType` must be a class that inherits from the `Throwable` class. The name of the exception isn't important, the "default" name is `e`.

## Throws keyword
Let's say we have a `readFile(String fileName)` method. We could handle the exception directly inside the method with a try/catch statement, but we might want to handle the exception someplace else, for example where we called the `readFile(String fileName)` method. To make sure we won't forget to handle the exception for the method later, we can declare the types of exceptions that the method could raise by adding the `throws` keyword added by the exceptions types to the method header:
```java
public static void readFile(String fileName) throws FileNotFoundException {
    // Read the file
}
```
As a consequence, the program won't compile until we have effectively handled the exception in the calling method, using a throw/catch statement or other:
```
java: unreported exception java.io.FileNotFoundException; must be caught or declared to be thrown
```

## Creating exceptions
Creating exceptions can be useful if there are some types of specific errors we need to handle (for example, a negative acceleration, or a value above the limit, ...etc).
We can either create a checked exception, or an unchecked exception.
> Rule of thumb, if a client can reasonably be expected to recover from an exceptio, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception. (LEPL1402 course, UCL)

### Creating a checked exception
```java
class NegativeAccelerationException extends Exception {
    public NegativeAccelerationException(String s) {
        // Call constructor of parent Exception
        super(s);
    }
}
```
In the code, we will write:
```java
if (acceleration < 0) {
    throw new NegativeAccelerationException("Acceleration is negative");
}
```

### Creating an unchecked exception
```java
class NegativeAccelerationException extends RuntimeException {
    public NegativeAccelerationException(String s) {
        // Call constructor of parent RuntimeException
        super(s);
    }
}
```
In the code, we will write:
```java
if (acceleration < 0) {
    throw new NegativeAccelerationException("Acceleration is negative");
}
```

