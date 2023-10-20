Lambda expressions are a key feature introduced in Java that involves two main components: lambda expressions themselves and functional interfaces.

A lambda expression is an unnamed method that is used to implement a method defined by a functional interface. It can be thought of as an anonymous class. Lambda expressions are also commonly known as closures.

A functional interface is an interface that contains exactly one abstract method. This method represents the intended purpose of the interface and typically defines a single action. For example, the ``Runnable`` interface is a functional interface with its single method, run(), representing the action to be performed.

A functional interface serves as the target type for a lambda expression. It specifies the type of object that the lambda expression can be assigned to. It is important to note that a lambda expression can only be used in a context where its target type is explicitly specified.

Functional interfaces are sometimes referred to as SAM types, where SAM stands for Single Abstract Method. This term emphasizes that a functional interface must have only one abstract method.

In summary, lambda expressions provide a concise way to define and use anonymous methods, while functional interfaces define the contract and target type for lambda expressions. They enable the implementation of functional programming paradigms in Java.

## Lambda Expression Fundamentals
Lambda expressions introduced a new syntax element and operator in Java, known as the lambda operator or arrow operator (``->``). The lambda expression is divided into two parts: the parameter list on the left side and the lambda body on the right side.
-  The −> can be verbalized as “becomes” or “goes to.”
There are two types of lambda bodies in Java: single-expression bodies and block bodies. This part focuses first on lambda expressions with single-expression bodies.
- One consists of a single expression, and the other type consists of a block of code.


A lambda expression with an empty parameter list, such as:
- ``() -> 123.45 ``
takes no parameters and returns a constant value. It is similar to a method with no parameters, such as:
- ``double myMeth() { return 123.45; }``.
The method defined by a lambda expression does not have a name. A slightly more interesting lambda expression is shown here:
- ``() -> Math.random() * 100``
- obtains a pseudo-random value from Math.random() and multiplies it by 100 before returning the result.
When a lambda expression requires a parameter, it is specified in the parameter list on the left side of the lambda operator. 
- For example, ``(n) -> (n % 2) == 0`` returns true if the value of parameter ``n`` is even. 
In many cases, the type of the parameter can be inferred, and explicit type specification is not necessary.

Lambda expressions can have multiple parameters, similar to named methods. The number and types of parameters can be adjusted as needed to suit the specific requirements of the lambda expression.

## Functional Interfaces
A functional interface in Java is an interface that specifies only one abstract method. Prior to JDK 8, all interface methods were implicitly abstract, but with JDK 8, default implementations, private methods, and static methods were introduced.

- An interface method is considered abstract only if it doesn't provide an implementation. Non-default, non-static, and non-private interface methods are implicitly abstract, so there's no need to use the abstract modifier explicitly.
- A functional interface example is shown with the MyNumber interface, which declares the implicitly abstract method getValue(). It is the only method in the interface, making MyNumber a functional interface.
- A lambda expression is not executed on its own but instead serves as the implementation of the abstract method defined by the functional interface. Lambda expressions can be used in contexts where a target type is defined, such as being assigned to a functional interface reference, variable initialization, return statements, and method arguments.
- In the example, a lambda expression is assigned to the MyNumber interface reference, creating an instance of a class that implements MyNumber with the lambda expression defining the behavior of the getValue() method. When getValue() is called through the reference, the lambda expression is executed, resulting in the value 123.45 being displayed.
```Java
interface MyNumber {
	double getValue();
}
// Create a reference to a MyNumber instance.
MyNumber myNum;
// Use a lambda in an assignment context.
myNum = () -> 123.45;
// Call getValue(), which is implemented by the previously assigned
// lambda expression.
System.out.println(myNum.getValue());
```
- For a lambda expression to be used in a target type context, the types and number of its parameters must be compatible with the [[Abstraction|abstract method's]] parameters. The return types must also be compatible, and any exceptions thrown by the lambda expression must be acceptable to the method.

## Some Lambda Expression Examples
With the preceding discussion in mind, let’s look at some simple examples that illustrate the
basic lambda expression concepts. The first example puts together the pieces shown in the
foregoing section.
```Java
// Demonstrate a simple lambda expression.
// A functional interface.
interface MyNumber {
	double getValue();
}

class LambdaDemo {
	public static void main(String[] args)
	{
		MyNumber myNum; // declare an interface reference
		
		// Here, the lambda expression is simply a constant expression.
		// When it is assigned to myNum, a class instance is
		// constructed in which the lambda expression implements
		// the getValue() method in MyNumber.
		myNum = () -> 123.45;
		
		// Call getValue(), which is provided by the previously assigned
		// lambda expression.
		System.out.println("A fixed value: " + myNum.getValue());
		
		// Here, a more complex expression is used.
		myNum = () -> Math.random() * 100;
		
		// These call the lambda expression in the previous line.
		System.out.println("A random value: " + myNum.getValue());
		System.out.println("Another random value: " + myNum.getValue());
		// A lambda expression must be compatible with the method
		// defined by the functional interface. Therefore, this won't work:
		// myNum = () -> "123.03"; // Error!
	}
}
```
- Sample output from the program:
```
A fixed value: 123.45
A random value: 88.90663650412304
Another random value: 53.00582701784129
```

A lambda expression must be compatible with the abstract method that it is intended to implement. For this reason, the commented-out line at the end of the preceding program is illegal because a value of type String is not compatible with double, which is the return type required by ``getValue()``.
The next example shows the use of a parameter with a lambda expression:
```Java
// Demonstrate a lambda expression that takes a parameter.
// Another functional interface.
interface NumericTest {
	boolean test(int n);
}

class LambdaDemo2 {
	public static void main(String[] args)
	{
		// A lambda expression that tests if a number is even.
		NumericTest isEven = (n) -> (n % 2)==0;
		
		if(isEven.test(10)) System.out.println("10 is even");
		if(!isEven.test(9)) System.out.println("9 is not even");
		
		// Now, use a lambda expression that tests if a number
		// is non-negative.
		NumericTest isNonNeg = (n) -> n >= 0;
		
		if(isNonNeg.test(1)) System.out.println("1 is non-negative");
		if(!isNonNeg.test(-1)) System.out.println("-1 is negative");
	}
}
```
The output from this program is shown here:
```
10 is even
9 is not even
1 is non-negative
-1 is negative
```

This program demonstrates a key fact about lambda expressions that warrants close
examination. Pay special attention to the lambda expression that performs the test for
evenness. It is shown again here:
- ``(n) -> (n % 2) == 0``
Notice that the type of n is not specified. Rather, its type is inferred from the context. In this
case, its type is inferred from the parameter type of test( ) as defined by the NumericTest
interface, which is int. It is also possible to explicitly specify the type of a parameter in a
lambda expression. For example, this is also a valid way to write the preceding:
- ``(int n) -> (n % 2) == 0``
Here, ``n`` is explicitly specified as ``int``. Usually it is not necessary to explicitly specify the type,
but you can in those situations that require it.
Beginning with JDK 11, you can also use var to explicitly indicate local variable type inference for a lambda expression parameter.
This program demonstrates another important point about lambda expressions:
- A functional interface reference can be used to execute any lambda expression that is compatible with it. Notice that the program defines two different lambda expressions that are compatible with the ``test()`` method of the functional interface ``NumericTest``.
- The first, called ``isEven``, determines if a value is even.
- The second, called ``isNonNeg``, checks if a value is non-negative.
- In each case, the value of the parameter ``n`` is tested. Because each lambda expression is compatible with ``test()``, each can be executed through a ``NumericTest`` reference.
When a lambda expression has only one parameter, it is not necessary to surround the parameter name with parentheses when it is specified on the left side of the lambda operator. For example, this is also a valid way to write the lambda expression used in the program:
- ``n -> (n % 2) == 0``

This program demonstrates a lambda expression that takes two parameters. In this
case, the lambda expression tests if one number is a factor of another.
```Java
// Demonstrate a lambda expression that takes two parameters.
interface NumericTest2 {
	boolean test(int n, int d);
}

class LambdaDemo3 {
	public static void main(String[] args)
	{
	// This lambda expression determines if one number is
	// a factor of another.
	NumericTest2 isFactor = (n, d) -> (n % d) == 0;
	if(isFactor.test(10, 2))
		System.out.println("2 is a factor of 10");
	if(!isFactor.test(10, 3))
		System.out.println("3 is not a factor of 10");
	}
}
```

The output of the program:
```
2 is a factor of 10
3 is not a factor of 10
```

In this program, the functional interface ``NumericTest2`` defines the ``test()`` method:
```
boolean test(int n, int d);
```
In this version, ``test()`` specifies two parameters. Thus, for a lambda expression to be
compatible with ``test()``, the lambda expression must also specify two parameters. Notice
how they are specified:
```
(n, d) -> (n % d) == 0
```
The two parameters, **n** and **d**, are specified in the parameter list, separated by commas. This
example can be generalized. Whenever more than one parameter is required, the parameters
are specified, separated by commas, in a parenthesized list on the left side of the lambda
operator.
Here is an important point about multiple parameters in a lambda expression: If you
need to explicitly declare the type of a parameter, then all of the parameters must have
declared types. For example, this is legal:
```
(int n, int d) -> (n % d) == 0
```
But this is not:
```
(int n, d) -> (n % d) == 0
```


## Block Lambda Expression
