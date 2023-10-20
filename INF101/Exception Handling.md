Exception handling in Java involves managing exceptional conditions that occur during the execution of code. Exceptions can be system-generated or manually generated. The Java exception handling mechanism utilizes five keywords: try, catch, throw, throws, and finally.

The try block contains the code that is monitored for exceptions. If an exception occurs, it is thrown. The catch blocks catch and handle specific types of exceptions. Multiple catch blocks can be used to handle different types of exceptions.

The throw keyword is used to manually throw an exception, while the throws keyword specifies that a method may throw a specific type of exception.

The finally block is used to define code that must be executed after the try block completes, regardless of whether an exception occurred or not.

The general form of an exception-handling block includes the try block, one or more catch blocks to handle specific exceptions, and a finally block for code that should always be executed.

The text provides an overview of the Java exception handling mechanism, introducing the keywords and their basic usage. It sets the foundation for understanding and applying exception handling in Java code.

This is the general form of an exception-handling block:
```Java
try {
// block of code to monitor for errors
}
catch (ExceptionType1 exOb) {
// exception handler for ExceptionType1
}
catch (ExceptionType2 exOb) {
// exception handler for ExceptionType2
}
// ...
finally {
// block of code to be executed after try block ends
}
```

## Exception Types
In Java, all exception types are subclasses of the built-in class Throwable, which is at the top of the exception class hierarchy. The exception class hierarchy is divided into two branches.

The first branch is headed by the Exception class. It is used for exceptional conditions that user programs should catch. This class can be subclassed to create custom exception types. Within the Exception branch, there is a subclass called RuntimeException, which includes exceptions that are automatically defined for the programs you write. Examples of RuntimeExceptions include division by zero and invalid array indexing.

The second branch is headed by the Error class. Exceptions of type Error are not expected to be caught under normal circumstances by your program. They are used by the Java runtime system to indicate errors related to the runtime environment itself. Examples of Error exceptions include stack overflow. This chapter does not cover Error exceptions because they usually represent catastrophic failures that cannot be handled by the program.

This text provides an overview of the exception types in Java. It explains the hierarchy with Throwable at the top, the distinction between Exception and Error subclasses, and the purpose of RuntimeExceptions for user programs. It clarifies the different branches and their roles in handling exceptions.
![[Pasted image 20230522181042.png]]

## Uncaught Exceptions
When exceptions are not handled in a Java program, they are considered uncaught exceptions. We will demonstrates what happens when an exception is not handled using a program that intentionally causes a divide-by-zero error.

This smaller program includes an expression that intentionally causes a divide-by-zero error:
```Java
class Exc0 {
	public static void main(String[] args) {
		int d = 0;
		int a = 42 / d;
	}
}
```

When running this script, the java run-time system detects the attempt to divide by zero, it constructs a new exception object and then *throws* this exception. By doing this, the ``Exc0`` execution stops, because a exception was thrown, and it must be caught by an exception handler and dealt with as soon as possible.
In the small code example we have not provided any exception handlers, so the exception is caught by the default handler provided by the Java run-time system.
- Any exception that is not caught by your program will ultimately be processed by the default handler.
The default handler displays a string describing the exception, prints a stack trace
from the point at which the exception occurred, and terminates the program.Here is the exception generated when this example is executed:
```
java.lang.ArithmeticException: / by zero
at Exc0.main(Exc0.java:4)
```
- Notice: the class name, ``Exc0;`` the method name, ``main;`` the filename, ``Exc0.java;`` and the line number, 4, are all included in the simple stack trace. Also, notice that the type of exception thrown is a subclass of ``Exception`` called ``ArithmeticException``, which more specifically describes what type of error happened.
- Java supplies several built-in exception types that match the various sorts of run-time errors that can be generated.

The stack trace will always show the sequence of method invocations that led up to the error. For example, here is another version of the preceding program that introduces the same error but in a method separate from ``main()``:
```Java
class Exc1 {
	static void subroutine() {
		int d = 0;
		int a = 10 / d;
	}
	public static void main(String[] args) {
	Exc1.subroutine();
	}
}
```
- The resulting stack trace from the default exception handler shows how the entire call stack is displayed:
```
java.lang.ArithmeticException: / by zero
	at Exc1.subroutine(Exc1.java:4)
	at Exc1.main(Exc1.java:7)
```
- As you can see, the bottom of the stack is main’s line 7, which is the call to subroutine( ), which caused the exception at line 4. The call stack is quite useful for debugging, because it pinpoints the precise sequence of steps that led to the error.

## Using Try and Catch
- The try-catch block is a fundamental construct in Java used for exception handling. It allows you to catch and handle exceptions that may occur during the execution of your code. The basic syntax of the try-catch block consists of a try block followed by one or more catch blocks.

- Within the try block, you place the code that may potentially throw an exception. If an exception occurs within the try block, it is "thrown" or raised. The catch blocks come immediately after the try block and are used to catch and handle specific types of exceptions.

- Each catch block specifies the type of exception it can handle. If an exception of that type is thrown within the try block, the corresponding catch block is executed. This allows you to provide custom handling code for specific exceptions.

- It's important to note that catch blocks are evaluated sequentially from top to bottom. So if multiple catch blocks are present, only the first one whose exception type matches the thrown exception will be executed. The remaining catch blocks will be skipped.

- By using the try-catch block, you can prevent your program from terminating abruptly when an exception occurs. Instead, you can gracefully handle the exceptional situation, perform error recovery, or display meaningful error messages to the user. This helps in improving the robustness and reliability of your code.

- Additionally, you can include a finally block after the catch blocks. The finally block contains code that is always executed, regardless of whether an exception is thrown or not. It is typically used to release resources or perform cleanup operations.

- The try-catch block provides a structured and organized way to handle exceptions, ensuring that your program can recover from errors and continue execution. It is an essential tool for effective error handling and maintaining the stability of Java applications.

There are several benefits with handling the exceptions yourself, by allowing is to fix the error faster, and preventing the program from automatically terminate when an exception is thrown. 
For this we will put the code we want to monitor inside a ``try`` block. The ``try`` block is followed by the ``catch`` clause that is specified by us, on what exception type we wish to catch. 

Here's an example:
```Java
class Exc2 {
	public static void main(String[] args) {
		int d, a;
		
		try { // monitor a block of code.
			d = 0;
			a = 42 / d;
			System.out.println("This will not be printed.");
		} catch (ArithmeticException e) { // catch divide-by-zero error
			System.out.println("Division by zero.");
		}
		System.out.println("After catch statement.");
	}
}
```
- This program uses an try-catch block to check if there is any exceptions of the type ``ArithmicException`` generated by a division-by-zero error.
- The program outputs this:
```
Division by zero.
After catch statement.
```
- **Notice:** the call to`` println()`` inside the ``try`` block is never executed. Once an exception is thrown, program control transfers out of the ``try`` block into the ``catch`` block.
- Catch is not “called,” so execution never “returns” to the try block from a catch.
	- Thus, the line "This will not be printed." is not displayed. Once the catch statement has executed, program control continues with the next line in the program following the entire try / catch mechanism.
- A try and its catch statement form a unit. The scope of the catch clause is restricted to those statements specified by the immediately preceding try statement. A catch statement cannot catch an exception thrown by another try statement (except in the case of nested try statements).
- The statements that are protected by try must be surrounded by curly braces. (That is, they must be within a block.) You cannot use try on a single statement.
- The goal of most well-constructed catch clauses should be to resolve the exceptional condition and then continue on as if the error had never happened.

Example program:
in the next program each iteration of the for loop obtains two random integers. Those two integers are divided by each other, and the result is used to divide the value 12345. The final result is put into a. If either division operation causes a divide-by-zero error, it is caught, the value of a is set to zero, and the program continues.
```Java
// Handle an exception and move on.
import java.util.Random;

class HandleError {
	public static void main(String[] args) {
		int a=0, b=0, c=0;
		Random r = new Random();
		
		for(int i=0; i<32000; i++) {
			try {
				b = r.nextInt();
				c = r.nextInt();
				a = 12345 / (b/c);
			} catch (ArithmeticException e) {
				System.out.println("Division by zero.");
				a = 0; // set a to zero and continue
			}
			System.out.println("a: " + a);
		}
	}
}
```

### Displaying a Description of an Exception
**Throwable** overrides the **toString()** method so that it returns a string containing a description of the exception. You can display this description in a **println()** statement by simply passing the exception as an argument. We can for example change the example above by rewriting the catch block like this:
```Java
catch (ArithmeticException e) {
	System.out.println("Exception: " + e);
	a = 0; // set a to zero and continue
}
```
- In this version, when the program is run, each divide-by-zero error displays this message: 
	- ``Exception: java.lang.ArithmeticException: / by zero``
- While it is of no particular value in this context, the ability to display a description of an exception is valuable in other circumstances—particularly when you are experimenting with exceptions or when you are debugging.

## Multiple catch Clauses
In Java, it is possible for a single piece of code to raise multiple exceptions. To handle such situations, you can use multiple catch clauses, each targeting a different type of exception. When an exception is thrown, each catch statement is evaluated in order, and the first one whose type matches the exception is executed. Once a catch statement executes, the remaining catch statements are skipped, and the program continues after the try-catch block. 

Here's a example program that traps two different exception types:
```Java
// Demonstrate multiple catch statements.
class MultipleCatches {
	public static void main(String[] args) {
		try {
			int a = args.length;
			System.out.println("a = " + a);
			int b = 42 / a;
			int[] c = { 1 };
			c[42] = 99;
		} catch(ArithmeticException e) {
			System.out.println("Divide by 0: " + e);
		} catch(ArrayIndexOutOfBoundsException e) {
			System.out.println("Array index oob: " + e);
		}
		System.out.println("After try/catch blocks.");
	}
}
```
- The example program "MultipleCatches" demonstrates this concept. It performs division and array access operations that may throw ArithmeticException and ArrayIndexOutOfBoundsException respectively. The catch blocks in the program handle these exceptions separately, displaying appropriate error messages. The output of the program varies based on the input provided.
- It will survive the division if you provide a command line argument, setting a to something larger than zero.  But it will cause an ``ArrayIndexOutOfBoundsException``, since the int array ``c`` has a length of 1, yet the program attempts to assign a value to c[42].
- The output of the program:
```
C:\>java MultipleCatches
a = 0
Divide by 0: java.lang.ArithmeticException: / by zero
After try/catch blocks.
C:\>java MultipleCatches TestArg
a = 1
Array index oob: java.lang.ArrayIndexOutOfBoundsException:
Index 42 out of bounds for length 1
After try/catch blocks.
```

When using multiple catch statements, it is important to arrange them in the correct order. Subclass-specific catch statements should precede their superclass counterparts. This is because a catch statement targeting a superclass will also catch exceptions of its subclasses. Placing a subclass catch statement after its superclass catch statement will result in unreachable code, which is an error in Java.

Here's a program example:
```Java
/* This program contains an error.

	A subclass must come before its superclass in
	a series of catch statements. If not,
	unreachable code will be created and a
	compile-time error will result.
*/
class SuperSubCatch {
	public static void main(String[] args) {
		try {
			int a = 0;
			int b = 42 / a;
		} catch(Exception e) {
			System.out.println("Generic Exception catch.");
		}
		/* This catch is never reached because
		ArithmeticException is a subclass of Exception. */
		catch(ArithmeticException e) { // ERROR – unreachable
			System.out.println("This is never reached.");
		}
	}
}
```
This program "``SuperSubCatch``" serves as an example of the error caused by improper ordering of catch statements. The second catch statement, targeting ``ArithmeticException``, becomes unreachable since the first catch statement catches all exceptions derived from Exception, including ``ArithmeticException``. To resolve this, the catch statements should be reordered, placing the subclass catch before the superclass catch.

Understanding the order of catch statements is crucial for proper exception handling in Java programs, ensuring that exceptions are handled appropriately and avoiding compile-time errors due to unreachable code.

## Nested Try Statements
The try statement in Java can be nested, allowing one try block to be placed inside the block of another try statement. Each time a try statement is entered, the context of the exception is pushed onto the stack. If an inner try block does not have a catch handler for a specific exception, the stack is unwound, and the catch handlers of the next try statement are evaluated. This process continues until a catch statement matches the exception or all nested try statements have been examined. If no catch statement is found, the Java run-time system handles the exception.

The example program "NestTry" demonstrates the use of nested try statements. It contains an outer try block that encompasses an inner try block. The program performs division and array access operations that may generate exceptions. If an exception occurs within the inner try block and is not caught, it is propagated to the outer try block for handling. The program produces different output based on the number of command-line arguments provided.
```Java
// An example of nested try statements.
class NestTry {
	public static void main(String[] args) {
		try {
			int a = args.length;
			/* If no command-line args are present,
			the following statement will generate
			a divide-by-zero exception. */
			int b = 42 / a;
			System.out.println("a = " + a);
			try { // nested try block
			/* If one command-line arg is used,
			then a divide-by-zero exception
			will be generated by the following code. */
			
				if(a==1) a = a/(a-a); // division by zero
				
			/* If two command-line args are used,
			then generate an out-of-bounds exception. */
				if(a==2) {
					int[] c = { 1 };
					c[42] = 99; // generate an out-of-bounds exception
				}
			} catch(ArrayIndexOutOfBoundsException e) {
				System.out.println("Array index out-of-bounds: " + e);
			}
		} catch(ArithmeticException e) {
			System.out.println("Divide by 0: " + e);
		}
	}
}
```

The program "MethNestTry" shows another example of nested try statements using method calls. In this case, a try block is placed inside a method called "nesttry()". The method is invoked within the main try block. The nested try block inside the method is still considered to be nested within the outer try block. The program exhibits the same exception handling behavior as the previous example.
```Java
/* Try statements can be implicitly nested via
calls to methods. */

class MethNestTry {
	static void nesttry(int a) {
		try { // nested try block
			/* If one command-line arg is used,
			then a divide-by-zero exception
			will be generated by the following code. */
			
			if(a==1) a = a/(a-a); // division by zero
			
			/* If two command-line args are used,
			then generate an out-of-bounds exception. */
			
			if(a==2) {
				int[] c = { 1 };
				c[42] = 99; // generate an out-of-bounds exception
			}
		} catch(ArrayIndexOutOfBoundsException e) {
		System.out.println("Array index out-of-bounds: " + e);
	}
}
	public static void main(String[] args) {
		try {
			int a = args.length;
			/* If no command-line args are present,
			the following statement will generate
			a divide-by-zero exception. */
			int b = 42 / a;
			System.out.println("a = " + a);
			nesttry(a);
		} catch(ArithmeticException e) {
		System.out.println("Divide by 0: " + e);
		}
	}
}
```
Nesting try statements allows for more complex exception handling scenarios, especially when method calls are involved. By nesting try blocks, you can handle exceptions at different levels of the program and propagate them as needed to ensure appropriate handling of exceptional conditions.

## Throw
In Java, it is possible for your program to explicitly throw an exception using the throw statement. The throw statement has the general form "throw ThrowableInstance;", where ThrowableInstance is an object of type Throwable or a subclass of Throwable. Primitive types and non-Throwable classes cannot be used as exceptions. You can obtain a Throwable object either by using a parameter in a catch clause or by creating a new instance with the new operator.

When a throw statement is encountered, the flow of execution immediately stops, and subsequent statements are not executed. The nearest enclosing try block is examined to see if it has a catch statement that matches the type of exception. If a match is found, control is transferred to that catch statement. If no match is found, the next enclosing try statement is inspected, and so on. If no matching catch is found, the default exception handler halts the program and prints the stack trace.

```Java
// Demonstrate throw.
class ThrowDemo {
	static void demoproc() {
		try {
			throw new NullPointerException("demo");
		} catch(NullPointerException e) {
			System.out.println("Caught inside demoproc.");
			throw e; // rethrow the exception
		}
	}
	public static void main(String[] args) {
		try {
			demoproc();
		} catch(NullPointerException e) {
			System.out.println("Recaught: " + e);
		}
	}
}
```

This program "ThrowDemo" serves as an example of creating and throwing an exception. The demoproc() method throws a NullPointerException explicitly and catches it within the method. It then rethrows the exception to the outer handler in the main() method. The program demonstrates how multiple exception handling contexts can be used to deal with the same error. The output shows that the exception is caught inside demoproc() and then recaught in the main() method.

Creating a standard exception object is illustrated in the line "throw new NullPointerException("demo");". The new keyword is used to construct an instance of NullPointerException with a descriptive string argument. This string provides a description of the exception and can be displayed using print() or println() or obtained through the getMessage() method defined by Throwable.

## Throws
In Java, if a method has the potential to cause an exception that it does not handle, it must indicate this behavior by including a throws clause in its declaration. The throws clause specifies the types of exceptions that the method might throw. All exceptions, except those of type Error or RuntimeException and their subclasses, must be declared in the throws clause. Failure to declare these exceptions will result in a compile-time error.

The general form of a method declaration with a throws clause is:
```Java
type method-name(parameter-list) throws exception-list {
    // body of method
}
```
Here, exception-list is a comma-separated list of the exceptions that the method may throw.

If a method attempts to throw an exception without declaring it in the throws clause, a compilation error will occur. The text provides an example program, "ThrowsDemo," which tries to throw an IllegalAccessException without specifying it in the throws clause. The program will not compile until the necessary changes are made.

Example of incorrect program that tries to throw an exception that it does not catch. Because the program does not specify a throws clause to declare this fact, the program will not compile.
```Java
// This program contains an error and will not compile.
class ThrowsDemo {
	static void throwOne() {
		System.out.println("Inside throwOne.");
		throw new IllegalAccessException("demo");
	}
public static void main(String[] args) {
	throwOne();
	}
}
```

To make this program compile, we declare that **throwOne()** throws **IllegalAccessException**, and **main()** must define a try/catch statement that catches this exception.
Here is a correct example:
```Java
// This is now correct.
class ThrowsDemo {
	static void throwOne() throws IllegalAccessException {
		System.out.println("Inside throwOne.");
		throw new IllegalAccessException("demo");
	}
	public static void main(String[] args) {
		try {
			throwOne();
		} catch (IllegalAccessException e) {
			System.out.println("Caught " + e);
		}
	}
}
```

Here is the output generated by running this example program:
```
inside throwOne
caught java.lang.IllegalAccessException: demo
```
To fix the program, two changes are required. First, the method "throwOne()" needs to declare that it throws IllegalAccessException by adding it to the throws clause. Second, the "main()" method must include a try/catch statement to handle this exception. Once the corrections are made, the program will compile and run successfully.

The corrected program, "ThrowsDemo," demonstrates the proper usage of the throws clause. When executed, it prints "Inside throwOne" before throwing the IllegalAccessException. The catch block in the "main()" method catches the exception and displays "Caught" followed by the exception message.

By using the throws clause, methods can inform callers of the potential exceptions that might occur during the method's execution, allowing the callers to handle those exceptions appropriately.

## Finally
In Java, the "finally" keyword is used to create a block of code that will be executed after a try/catch block, regardless of whether an exception is thrown or not. The "finally" block ensures that certain code is executed, even if an exception occurs, and it is executed just before a method returns to the caller.

The "finally" block is optional, but each try statement must have at least one catch or a finally clause. It is commonly used to handle resource cleanup tasks, such as closing file handles or releasing allocated resources.

The program "FinallyDemo" demonstrates the usage of "finally" in various scenarios. It defines three methods: procA(), procB(), and procC().
- In procA(), an exception is thrown within the try block. Regardless of the exception, the finally block is executed before the method exits.
- In procB(), the method returns within the try block. Again, the finally block is executed before the method returns.
- In procC(), the try block executes normally without any exceptions. Still, the finally block is executed as expected.

```Java
// Demonstrate finally.
class FinallyDemo {
// Throw an exception out of the method.
	static void procA() {
		try {
			System.out.println("inside procA");
			throw new RuntimeException("demo");
		} finally {
			System.out.println("procA's finally");
		}
	}
// Return from within a try block.
	static void procB() {
		try {
			System.out.println("inside procB");
			return;
		} finally {
			System.out.println("procB's finally");
		}
	}
// Execute a try block normally.
	static void procC() {
		try {
			System.out.println("inside procC");
		} finally {
			System.out.println("procC's finally");
		}
	}
	public static void main(String[] args) {
		try {
			procA();
		} catch (Exception e) {
			System.out.println("Exception caught");
		}
		procB();
		procC();
	}
}
```
In the main() method, procA() is called within a try block, and any caught exception is handled. Then, procB() and procC() are called without try/catch blocks, but their finally blocks are still executed before the methods finish.

The "finally" block provides a way to ensure that critical cleanup tasks are performed, even in exceptional scenarios, and helps maintain the expected behavior of methods that allocate resources.

## Java's Build-in Exception:
In Java, the standard package java.lang includes various exception classes that are used to handle different types of errors and exceptional situations. These exception classes are categorized into two types: unchecked exceptions and checked exceptions.

- The unchecked exceptions are [[Classes#Subclasses|subclasses]] of the ``RuntimeException`` class. They are called unchecked because the compiler does not enforce the requirement for methods to handle or declare them in the throws clause. These exceptions do not need to be explicitly listed in the throws list of a method. Some examples of unchecked exceptions from java.lang include ``NullPointerException``,`` ArithmeticException``, and ``ArrayIndexOutOfBoundsException``.
- On the other hand, the checked exceptions, also defined in java.lang, must be included in the throws list of a method if that method can potentially generate one of these exceptions and does not handle it internally. These exceptions are checked by the compiler, and the method must either catch them or declare them in the throws clause. Examples of checked exceptions from java.lang include ``IOException``, ``ClassNotFoundException``, and ``InterruptedException``.
- In addition to the exceptions defined in java.lang, Java also defines additional exceptions that are specific to its other standard packages. These exceptions allow developers to handle errors and exceptional conditions specific to those packages.
- Understanding the distinction between checked and unchecked exceptions is important for writing robust and reliable code. Checked exceptions require explicit handling, while unchecked exceptions can be handled or left to propagate through the call stack.
- *List of Exceptions:*
- ![[Pasted image 20230522193630.png]]
- ![[Pasted image 20230522193650.png]]

## Creating Your Own Exception Subclasses
In Java, you have the flexibility to create your own exception subclasses to handle specific situations in your applications. To create a custom exception subclass, you simply define a class that extends the Exception class, which is itself a subclass of Throwable. The existence of these subclasses allows you to use them as exceptions in your code.

- When creating your own exception subclasses, you don't need to implement any specific methods because the Exception class inherits the methods defined by Throwable. These methods, such as getMessage(), printStackTrace(), and toString(), are available to all exception subclasses, including the ones you create. You can also choose to override these methods in your custom exception classes if needed.
- The Exception class provides four public constructors. Two of them support chained exceptions, which allow one exception to be associated with another. The other two constructors allow you to create an exception with or without a description. It's common to provide a description for the exception by overriding the toString() method inherited from Throwable. This allows you to customize the output of the exception and provide a more meaningful description.
![[Pasted image 20230522193952.png]]
- In the provided example, a custom exception subclass called MyException is created. It includes a constructor to initialize a detail variable and overrides the toString() method to display a carefully tailored description of the exception. The ExceptionDemo class demonstrates how to use the MyException subclass by throwing it within the compute() method. The main() method sets up an exception handler and calls the compute() method with both a legal and an illegal value to demonstrate the different paths through the code and the handling of the exception.
```Java
// This program creates a custom exception type.
class MyException extends Exception {
	private int detail;
	
	MyException(int a) {
		detail = a;
	}
	
	public String toString() {
		return "MyException[" + detail + "]";
	}
}

class ExceptionDemo {
	static void compute(int a) throws MyException {
		System.out.println("Called compute(" + a + ")");
		if(a > 10)
			throw new MyException(a);
		System.out.println("Normal exit");
	}
	
	public static void main(String[] args) {
		try {
			compute(1);
			compute(20);
		} catch (MyException e) {
			System.out.println("Caught " + e);
		}
	}
}
```
- By creating your own exception subclasses, you can effectively handle specific error conditions or exceptional situations in your applications and provide meaningful information about the encountered exceptions.

## Chained Exceptions
Chained exceptions, introduced as a feature in the exception subsystem of Java, allow you to associate one exception with another, describing the cause of the first exception. This feature is particularly useful when there are multiple layers of exceptions and you want to provide information about the underlying cause of an exception.

- To support chained exceptions, two constructors and two methods were added to the ``Throwable`` class. The constructors allow you to specify the cause exception while creating an exception object, either with or without a description. The ``getCause()`` method returns the exception that caused the current exception, and the ``initCause()`` method associates a cause exception with the invoking exception.
- In this example provided, the ``ChainExcDemo`` class demonstrates the mechanics of handling chained exceptions. A ``NullPointerException`` is created as the top-level exception, and an ``ArithmeticException`` is added as the cause exception using the ``initCause()`` method. When the exception is thrown from ``demoproc()``, it is caught in the main() method. The top-level exception and the underlying cause exception are then displayed using the ``getCause()`` method.
```Java
  // Demonstrate exception chaining.
class ChainExcDemo {
	static void demoproc() {
		
		// create an exception
		NullPointerException e =
			new NullPointerException("top layer");
	// add a cause
		e.initCause(new ArithmeticException("cause"));
		throw e;
	}
	
	public static void main(String[] args) {
		try {
			demoproc();
		} catch(NullPointerException e) {
			// display top level exception
			System.out.println("Caught: " + e);
			// display cause exception
			System.out.println("Original cause: " +
								e.getCause());
		}
	}
}
```
- Chained exceptions can be nested to any required depth, allowing the cause exception to have its own cause. However, it's important to consider the design and avoid excessively long chains of exceptions, as they may indicate poor design.
- While not every program requires chained exceptions, they provide an elegant solution in cases where knowledge of the underlying cause is valuable and can help in understanding and handling exceptions effectively.

## Additional Exception Features
Since JDK 7, the exception system in Java has introduced three additional features that enhance exception handling. These features are the try-with-resources statement, multi-catch, and more precise rethrow.

- The try-with-resources statement automates the process of releasing system resources, such as files, by automatically closing them when they are no longer needed. This feature is explained in Chapter 13 of the Java documentation.
- The multi-catch feature allows multiple exceptions to be caught by a single catch clause. Instead of duplicating code for each exception type, a single catch clause can handle multiple exceptions by separating each exception type with the OR operator (|). The multi-catch parameter is implicitly final, meaning it cannot be assigned a new value.
- In the example provided, the ``MultiCatch`` class demonstrates the multi-catch feature in action. It attempts to perform a division by zero, which throws an ``ArithmeticException``, and if that line is commented out, it generates an ``ArrayIndexOutOfBoundsException``. The single catch statement is able to catch both exceptions.
```Java
// Demonstrate the multi-catch feature.
class MultiCatch {
	public static void main(String[] args) {
		int a=10, b=0;
		int[] vals = { 1, 2, 3 };
		try {
			int result = a / b; // generate an ArithmeticException
			// vals[10] = 19; // generate an ArrayIndexOutOfBoundsException
			// This catch clause catches both exceptions.
		} catch(ArithmeticException | ArrayIndexOutOfBoundsException e) {
			System.out.println("Exception caught: " + e);
		}
		System.out.println("After multi-catch.");
	}
}
```
- The more precise rethrow feature allows for the re-throwing of checked exceptions that are not handled by preceding catch clauses, and that are either a sub-type or supertype of the catch parameter. This feature ensures that only specific types of exceptions are rethrown. To enable this feature, the catch parameter must be effectively [[Classes#Final Classes|final]] or explicitly declared as [[Classes#Final Classes|final]].
- Although the more precise rethrow feature may not be needed frequently, it provides a useful capability in certain situations where fine-grained control over the rethrown exceptions is required.

## Using Exceptions
Exception handling provides a powerful mechanism for controlling complex programs that
have many dynamic run-time characteristics. It is important to think of try, throw, and
catch as clean ways to handle errors and unusual boundary conditions in your program’s
logic. Instead of using error return codes to indicate failure, use Java’s exception handling
capabilities. Thus, when a method can fail, have it throw an exception. This is a cleaner way
to handle failure modes.
One last point: Java’s exception-handling statements should not be considered a general
mechanism for nonlocal branching. If you do so, it will only confuse your code and make it
hard to maintain.