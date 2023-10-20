In Java, a class is a blueprint or template that defines the properties (data) and behaviors (methods) that objects of that class will possess. It serves as a fundamental building block of object-oriented programming (OOP) and allows for the creation of objects based on that blueprint.

Classes in OOP are used to model real-world entities or concepts. They encapsulate related data and behaviors, providing a way to organize and structure code. Objects are instances of classes, and they can be created and manipulated based on the defined class.

## Abstract Classes
[[Abstraction|Abstract]] classes in Java are classes that cannot be instantiated directly and serve as a blueprint for other classes. They are designed to be extended by subclasses, which provide concrete implementations for abstract methods defined in the abstract class. 

Here are some key points about abstract classes:
1. Declaration and Usage:
    - An abstract class is declared using the `abstract` keyword before the `class` keyword.
    - Abstract classes can have abstract methods (methods without a body) as well as regular methods with implementations.
    - Abstract classes can have instance variables, constructors, and any other features of a regular class.
2. Abstract Methods:
    - Abstract methods are declared without a body and are meant to be implemented by concrete subclasses.
    - Abstract methods are marked with the `abstract` keyword and end with a semicolon instead of a method body.
    - Subclasses that extend an abstract class must provide an implementation for all abstract methods inherited from the abstract class.
3. Concrete Methods:
    - Abstract classes can also have concrete (non-abstract) methods with implementations.
    - These methods can be used directly by the subclasses without overriding them.
    - Concrete methods in an abstract class can access abstract methods, instance variables, and other concrete methods.
4. Purpose and Benefits: 
    - Abstract classes provide a way to define common behavior and attributes among related classes.
    - They enable code reuse and promote code organization and maintainability.
    - Abstract classes can establish a contract or an interface that must be followed by subclasses.
    - They help achieve abstraction and polymorphism, allowing objects of different concrete subclasses to be treated uniformly through their abstract superclass.
5. Relationship with Subclasses:
    - Abstract classes are meant to be extended by subclasses.
    - Subclasses of an abstract class must either provide an implementation for all inherited abstract methods or be declared as abstract classes themselves.
    - Subclasses can also extend other non-abstract classes while implementing an abstract class simultaneously.
6. Instantiation and Usage: 
    - Abstract classes cannot be directly instantiated with the `new` keyword.
    - However, they can be used as reference types to refer to objects of their concrete subclasses.
    - Abstract classes can be used to define variables, method parameters, and return types.

Abstract classes provide a way to define common behavior and enforce a structure among related classes, while allowing subclasses to provide their own specific implementations. They play a crucial role in achieving abstraction, encapsulation, and code reusability in object-oriented programming.

## Subclasses
a subclass is a class that is derived from another class, known as the superclass. Subclasses inherit properties and behaviors from their superclass, allowing them to extend or specialize the functionality of the superclass. Subclasses are an essential concept in object-oriented programming, enabling code reuse, modularity, and hierarchical organization of classes.

Additional information about subclasses:
1.  Inheritance Relationship:
    - Subclasses have an "is-a" relationship with their superclass. This means that a subclass is a more specific type of the superclass.
    - The superclass provides a common set of attributes and behaviors, while subclasses can add or modify these inherited elements to suit their specific requirements.
2.  Access to Superclass Members:
    - Subclasses have access to the public and protected members (methods and variables) of their superclass.
    - Private members of the superclass are not accessible in subclasses.
3.  Overriding Methods:
    - Subclasses can override methods defined in the superclass, providing their own implementation.
    - Method overriding allows for polymorphism, where a method call on a superclass reference can execute the appropriate implementation in the subclass.
4.  Extending Functionality:
    - Subclasses can add additional attributes, methods, or behaviors to the ones inherited from the superclass.
    - This allows for specialization and customization, making subclasses more specific or tailored to certain use cases.
5.  Creating Subclass Instances:
    - Subclass instances can be created using the `new` keyword, just like instances of the superclass.
    - The subclass can inherit and utilize the constructors of the superclass or define its own constructors.
6.  [[Inheritance]] Hierarchy:
    - Subclasses can have their own subclasses, forming an inheritance hierarchy or tree-like structure.
    - This hierarchy allows for multiple levels of specialization and abstraction.

### Example of subclasses
```Java 
class Vehicle {
    void start() {
        System.out.println("Starting the vehicle...");
    }
}

class Car extends Vehicle {
    void accelerate() {
        System.out.println("Accelerating the car...");
    }
}

class SportsCar extends Car {
    void turboBoost() {
        System.out.println("Activating turbo boost!");
    }
}

```

In this example, `Vehicle` is the superclass, `Car` is a subclass of `Vehicle`, and `SportsCar` is a subclass of `Car`. Each subclass inherits the properties and behaviors of its superclass. The subclasses `Car` and `SportsCar` add their own specific methods (`accelerate()` and `turboBoost()`) to extend the functionality.

Subclasses provide a powerful mechanism for creating more specialized and modular code in Java. They allow for code reuse, customization, and hierarchical organization, making object-oriented programming more flexible and scalable.

## Superclasses
In Java, a superclass is a class that serves as a base or parent class from which other classes, called subclasses, are derived. Superclasses provide a common set of properties and behaviors that can be inherited by subclasses. They are a fundamental concept in object-oriented programming and facilitate code reuse, modularity, and abstraction.

Additional information about superclasses:

1. Inheritance Relationship:
    - Superclasses have an "is-a" relationship with their subclasses. This means that a superclass represents a more general or abstract category, and subclasses are more specific or specialized types within that category.
    - Superclasses define the common attributes and behaviors that can be shared by multiple subclasses.
2. Inherited Members:
    - Subclasses inherit the public and protected members (methods and variables) of their superclass.
    - Private members of the superclass are not directly accessible in subclasses.
3. Defining Common Behavior:
    - Superclasses provide a way to define common behavior that can be shared among multiple subclasses.
    - By [[Encapsulation|encapsulating]] shared functionality in the superclass, code redundancy is reduced, and changes can be made in a centralized manner.
4. Overridden Methods:
    - Superclasses may define methods that can be overridden by subclasses.
    - Subclasses can provide their own implementation of these methods, customizing the behavior to suit their specific requirements.
    - Method overriding allows for polymorphism, where a superclass reference can be used to invoke the appropriate implementation in the subclass.
5. [[Inheritance]] Hierarchy:
    - Superclasses can have their own superclasses, creating an inheritance hierarchy or tree-like structure.
    - This hierarchy allows for the organization and categorization of classes based on their common characteristics.

### Example of Superclasses
```Java
class Animal {
    void eat() {
        System.out.println("The animal is eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog is barking...");
    }
}

```

In this example, `Animal` is the superclass, and `Dog` is a subclass of `Animal`. The `Dog` class inherits the `eat()` method from `Animal` and adds its own method, `bark()`. The `Animal` class provides common behavior that can be shared among different types of animals.

Superclasses are a crucial element in object-oriented programming as they provide a foundation for creating hierarchies of classes and defining shared behavior. They enable code reuse, [[encapsulation]] of common functionality, and facilitate the creation of specialized subclasses.

### Using Super to call Superclass Constructors
A [[Classes#Subclasses|subclass]] can call a constructor defined by its superclass by use of the following form of super: ``super(arg-list);``
Here, ``arg-list`` specifies any arguments needed by the constructor in the superclass. [Super()](https://docs.oracle.com/javase/tutorial/java/IandI/super.html) must always be the first statement executed inside a subclass’ constructor. 
To see how **super()** is used, consider this improved version of the ``BoxWeight`` class:
```Java
// BoxWeight now uses super to initialize its Box attributes.
class BoxWeight extends Box {
	double weight; // weight of box
	
	BoxWeight(double w, double h, double d, double m) {
		super(w, h, d); // call superclass constructor
		weight = m;
	}
}
```

- Here ``BoxWeight()`` calls ``super()`` with the arguments **w**,**h** and **d**. This causes the ``Box`` constructor to be called, which initializes ``width`` , ``height`` and ``depth`` using these values. 
- ``BoxWeight`` no longer initializes these values itself. It only needs to initialize the value unique to it: weight. This leaves ``Box`` free to make these values private if desired.
- In the preceding example, super() was called with three arguments. Since constructors can be overloaded, super() can be called using any form defined by the superclass. 
- The constructor executed will be the one that matches the arguments. For example, here is a complete implementation of ``BoxWeight`` that provides constructors for the various ways that a box can be constructed. In each case, super() is called using the appropriate arguments.
- Notice that width, height, and depth have been made private within Box.

```Java
// BoxWeight now uses super to initialize its Box attributes.
class BoxWeight extends Box {
    double weight; // weight of box
    // initialize width, height, and depth using super()
    BoxWeight(double w, double h, double d, double m) {
        super(w, h, d); // call superclass constructor
        weight = m;
    }
}

// A complete implementation of BoxWeight.
class Box {
    private double width;
    private double height;
    private double depth;
    // construct clone of an object
    Box(Box ob) { // pass object to constructor
        width = ob.width;
        height = ob.height;
        depth = ob.depth;
    }
    // constructor used when all dimensions specified
    Box(double w, double h, double d) {
        width = w;
        height = h;
        depth = d;
    }
    // constructor used when no dimensions specified
    Box() {
        width = -1; // use -1 to indicate
        height = -1; // an uninitialized
        depth = -1; // box
    }
    // constructor used when cube is created
    Box(double len) {
        width = height = depth = len;
    }
    // compute and return volume
    double volume() {
        return width * height * depth;
    }
}

class DemoSuper {
    public static void main(String[] args) {
        BoxWeight mybox1 = new BoxWeight(10, 20, 15, 34.3);
        BoxWeight mybox2 = new BoxWeight(2, 3, 4, 0.076);
        BoxWeight mybox3 = new BoxWeight(); // default
        BoxWeight mycube = new BoxWeight(3, 2);
        BoxWeight myclone = new BoxWeight(mybox1);
        double vol;

        vol = mybox1.volume();
        System.out.println("Volume of mybox1 is " + vol);
        System.out.println("Weight of mybox1 is " + mybox1.weight);
        System.out.println();

        vol = mybox2.volume();
        System.out.println("Volume of mybox2 is " + vol);
        System.out.println("Weight of mybox2 is " + mybox2.weight);
        System.out.println();

        vol = mybox3.volume();
        System.out.println("Volume of mybox3 is " + vol);
        System.out.println("Weight of mybox3 is " + mybox3.weight);
        System.out.println();

        vol = myclone.volume();
        System.out.println("Volume of myclone is " + vol);
        System.out.println("Weight of myclone is " + myclone.weight);
        System.out.println();

        vol = mycube.volume();
        System.out.println("Volume of mycube is " + vol);
        System.out.println("Weight of mycube is " + mycube.weight);
        System.out.println();
    }
}
```

- This program outputs the following:
```
Volume of mybox1 is 3000.0
Weight of mybox1 is 34.3
Volume of mybox2 is 24.0
Weight of mybox2 is 0.076
Volume of mybox3 is -1.0
Weight of mybox3 is -1.0
Volume of myclone is 3000.0
Weight of myclone is 34.3
Volume of mycube is 27.0
Weight of mycube is 2.0
```
- Pay special attention to this constructor in ``BoxWeight``:
```Java
// construct clone of an object
BoxWeight(BoxWeight ob) { // pass object to constructor
	super(ob);
	weight = ob.weight;
}
```
- Notice that super() is passed an object of type ``BoxWeight``, not of type ``Box``. This still invokes the constructor ``Box(Box ob)``. 
- A superclass variable can be used to reference any object derived from that class. Thus, we are able to pass a ``BoxWeight`` object to the ``Box`` constructor. Of course, Box only has knowledge of its own members.

### A Second Use for Super
The second form of super acts somewhat like this, except that it always refers to the
superclass of the subclass in which it is used. This usage has the following general form:

``super.member``

Here, member can be either a method or an instance variable.
This second form of super is most applicable to situations in which member names
of a subclass hide members by the same name in the superclass. Consider this simple
class hierarchy:
```Java
// Using super to overcome name hiding.
class A {
	int i;
}
// Create a subclass by extending class A.
class B extends A {
	int i; // this i hides the i in A
	
	B(int a, int b) {
		super.i = a; // i in A
		i = b; // i in B
	}

	void show() {
		System.out.println("i in superclass: " + super.i);
		System.out.println("i in subclass: " + i);
	}
}

class UseSuper {
	public static void main(String[] args) {
		B subOb = new B(1, 2);
		subOb.show();
	}
}

```

- This program display the following:
```
i in superclass: 1
i in subclass: 2
```
- Although the instance variable i in B hides the i in A, super allows access to the i defined in the superclass. As you will see, super can also be used to call methods that are hidden by a subclass.

## Final Classes
Final classes in Java are classes that cannot be subclassed, meaning they cannot have any subclasses extending them. They serve as the endpoint of class [[Inheritance|inheritance]] and are used when you want to prevent any further extension or modification of a class. 
Sometimes you will want to prevent a class from being inherited. To do this, precede the class declaration with final. Declaring a class as final implicitly declares all of its methods as final, too.

Here are some key points about final classes:
1.  Declaration:
    -   A final class is declared using the `final` keyword before the `class` keyword.
    -   Once a class is marked as final, it cannot be subclassed.
2.  Preventing Inheritance:
    -   Final classes are used to prevent other classes from extending or inheriting from them.
    -   They provide a way to ensure that the implementation of a class remains unchanged and cannot be overridden.
3.  Advantages of Final Classes:
    -   Guarantee of immutability: Final classes cannot be modified or overridden, ensuring the stability and integrity of their implementation.
    -   Security and integrity: Final classes help protect critical functionality or sensitive data by preventing unauthorized modifications through subclassing.
    -   Performance optimizations: Final classes allow the compiler to perform certain optimizations due to the immutability and finality of the class.
4.  Final Methods and Variables:
    -   In addition to final classes, methods and variables can also be marked as final.
    -   Final methods cannot be overridden by subclasses, providing a way to enforce specific behavior in the superclass.
    -   Final variables (constants) cannot be reassigned once they are assigned a value, ensuring their immutability.
5.  Final Class Usage Considerations:
    -   Final classes should be used when you have a clear design requirement to prevent further inheritance or modification.
    -   It is important to carefully consider the implications of making a class final, as it restricts the potential for future extension or modification.
6.  Final Class Examples:
    -   Some examples of final classes in the Java Standard Library include `String`, `Integer`, and `Math`, among others.
    -   These classes are intentionally designed as final to ensure their core functionalities remain intact and consistent

Final classes provide a way to establish a clear, immutable, and unmodifiable class structure in Java. They are commonly used for utility classes, classes that provide critical services, or when there is a need to prevent any further extension or modification to a class.

### Final Class: Code Example
Here's an example of a final class in Java:
```Java
final class Circle {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

```
In this example, the `Circle` class is declared as `final`. This means that it cannot be subclassed, and no other class can extend it. The `Circle` class has a private instance variable `radius` and a public method `calculateArea()` to calculate the area of the circle.

By marking the `Circle` class as `final`, we ensure that its implementation and behavior remain unchanged and cannot be overridden. Any attempt to create a subclass of `Circle` would result in a compilation error.
```Java
// This code will result in a compilation error
class SubCircle extends Circle {
    // Compilation error: Cannot inherit from final class 'Circle'
}
```
The use of `final` here prevents any modification or extension of the `Circle` class, ensuring that its core functionality, such as calculating the area, remains intact and consistent.

## Nested Classes
Nested classes in Java are classes defined within other classes. They provide a way to logically group related classes and increase code organization and encapsulation. 

Here are some key points about nested classes:
1.  Types of Nested Classes:
    - Static Nested Classes: These are static nested classes declared as a static member of the enclosing class. They can be instantiated independently of any outer class instances.
    - Inner Classes: Also known as non-static nested classes, they are declared as a member of the enclosing class without the `static` keyword. Inner classes have access to the instance variables and methods of the outer class and require an instance of the outer class to be instantiated.
    - Local Classes: Local classes are defined within a block, such as a method or a loop, inside a method of the enclosing class. They have access to the variables of the enclosing block and can be instantiated only within that block.
    - Anonymous Classes: Anonymous classes are defined without a class name and are used for one-time implementations of interfaces or abstract classes. They are typically defined inline at the point of use.
2.  Benefits of Nested Classes:
    - Encapsulation: Nested classes can be used to encapsulate related functionality within a class, making the code more modular and maintaining a clear separation of concerns.
    - Improved Readability: By defining related classes within a single outer class, the code becomes more readable and self-contained, making it easier to understand and maintain.
    - Accessibility: Nested classes have access to private members of the enclosing class, allowing for tighter encapsulation and controlled access to members.
    - Information Hiding: Nested classes can be used to hide implementation details by limiting their visibility to the enclosing class.
3.  Scope and Accessibility:
    - Nested classes have different scope and accessibility rules based on their type.
    - Static nested classes have access to only the static members of the enclosing class.
    - Inner classes have access to both static and non-static members of the enclosing class.
    - Local classes have access to the local variables and parameters of the block they are defined in.
    - Anonymous classes have access to the final or effectively final variables of the enclosing scope.
4.  Usage Scenarios:
    - Nested classes are commonly used to implement data structures, such as linked lists or binary trees, where each node is represented as an inner class.
    - They are also useful when implementing listener interfaces or event handlers, as the nested class can directly access the enclosing class's state and methods.
    - Local classes and anonymous classes are often used to provide one-time or ad-hoc implementations of interfaces or abstract classes.

Nested classes provide a way to logically group related classes and improve code organization and encapsulation. They help in achieving better modularization and maintainability of the code. The choice of using nested classes depends on the specific design requirements and the level of encapsulation and accessibility needed for the related classes.

### Nested Class: Code Example
Here's an example that demonstrates different types of nested classes in Java:
```Java
class OuterClass {
    private int outerVariable;

    // Static nested class
    static class StaticNestedClass {
        void printMessage() {
            System.out.println("Inside StaticNestedClass");
        }
    }

    // Inner class
    class InnerClass {
        void printMessage() {
            System.out.println("Inside InnerClass");
            System.out.println("Outer variable: " + outerVariable);
        }
    }

    void outerMethod() {
        final int localVariable = 10;

        // Local class
        class LocalClass {
            void printMessage() {
                System.out.println("Inside LocalClass");
                System.out.println("Local variable: " + localVariable);
            }
        }

        // Anonymous class
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("Inside AnonymousClass");
            }
        };
        LocalClass localObj = new LocalClass();
        localObj.printMessage();
        runnable.run();
    }
}

public class NestedClassesExample {
    public static void main(String[] args) {
        OuterClass.StaticNestedClass staticNestedObj = new OuterClass.StaticNestedClass();
        staticNestedObj.printMessage();

        OuterClass outerObj = new OuterClass();
        OuterClass.InnerClass innerObj = outerObj.new InnerClass();
        innerObj.printMessage();

        outerObj.outerMethod();
    }
}
```

In this example, we have an `OuterClass` that contains different types of nested classes:
1. `StaticNestedClass`: A static nested class that can be instantiated independently of any instances of the outer class. It prints a message when its method `printMessage()` is called.
2. `InnerClass`: An inner class that requires an instance of the outer class to be instantiated. It has access to the instance variables of the outer class and can print the outer variable.
3. `LocalClass`: A local class defined within the `outerMethod()` of the `OuterClass`. It has access to the local variable `localVariable` of the method and can print its value.
4.  Anonymous class: An anonymous class implementing the `Runnable` interface. It is defined inline and can access the final or effectively final variables of the enclosing scope. It prints a message when its `run()` method is called.

In the `main` method, we create instances of each type of nested class and invoke their respective methods to demonstrate their usage.

This example showcases how nested classes provide encapsulation, access to enclosing class members, and different scoping rules depending on their type.

## Interface Classes
Interface classes in Java define a contract or a set of methods that a class can implement. They provide a way to achieve abstraction and define a common interface for multiple unrelated classes. 

Here are some key points about interface classes:
1.  Declaration:
    - An interface is declared using the `interface` keyword followed by the interface name.
    - It defines a list of abstract method signatures that must be implemented by any class that implements the interface.
    - Interfaces can also contain constant fields (implicitly `public`, `static`, and `final`) and default methods (methods with an implementation).
2.  Method Signatures:
    - Interface methods are implicitly `public` and `abstract`, meaning they have no implementation in the interface.
    - Classes that implement an interface must provide the implementation for all the methods defined in the interface.
    - The methods in an interface serve as a contract, ensuring that any class implementing the interface adheres to a specific set of behavior.
3.  Multiple Inheritance:
    - Java allows a class to implement multiple interfaces, enabling a class to inherit and provide implementations for multiple sets of behavior.
    - This feature supports the concept of multiple inheritance of type, allowing a class to exhibit behavior from multiple sources.
4.  Polymorphism and Abstraction:
    - Interfaces are used to achieve polymorphism, where objects of different classes that implement the same interface can be treated uniformly through the interface type.
    - Interfaces provide a level of abstraction, allowing programmers to work with objects at a higher level, focusing on the contract defined by the interface rather than specific implementations.
5.  Usage and Design Considerations:
    - Interfaces are used to define common behavior across unrelated classes, enabling code reuse and maintaining a consistent contract.
    - They are commonly used in callback mechanisms, event handling, and defining service contracts in applications.
    - Interfaces promote loose coupling and flexibility in code, as they allow for interchangeable implementations without modifying existing code.
6.  Examples:
    - Examples of interfaces in Java include `Runnable`, `Comparable`, and `List`, which define common behavior for different types of classes.

Here's an example illustrating an interface:
```Java
public interface Drawable {
    void draw(); // Abstract method signature

    default void info() { // Default method with an implementation
        System.out.println("Drawable interface");
    }
}
```
In the example, the `Drawable` interface defines an abstract method `draw()` and a default method `info()`. Any class that implements the `Drawable` interface must provide an implementation for the `draw()` method. The `info()` method provides a default implementation that can be overridden by implementing classes.

Interfaces are an essential part of Java's object-oriented programming paradigm, providing a way to define contracts and achieve abstraction and polymorphism. They play a vital role in designing modular and flexible systems.

## Compositions
Composition is a fundamental concept in object-oriented programming (OOP) that allows you to build complex classes by combining simpler classes or objects. It enables the creation of more flexible and modular designs by emphasizing the relationships between objects.

In composition, a class can contain other objects as member variables, creating a "has-a" relationship between them. The class that contains the objects is often referred to as the "composite" or "container" class, while the objects it holds are known as "component" objects. The composite class can delegate certain responsibilities to its component objects, thereby achieving code reuse and modular design.

Here are some key points to understand about composition:
- Relationship: Composition establishes a strong relationship between objects, where the composite class owns and controls the lifecycle of its component objects.
- [[Modularity#Code Reusability|Code Reusability]]: By utilizing composition, you can reuse existing classes or objects as components, promoting modular and reusable code. 
- Flexibility: Composition allows you to dynamically change the behavior of a class by replacing its component [[Objects and Methods|objects]] at runtime.
- [[Encapsulation]]: Composition promotes encapsulation as the component objects are encapsulated within the composite class, making it easier to manage and maintain the code.
- Composition over [[Inheritance]]: Composition is often preferred over inheritance as it provides more flexibility and avoids the limitations of single inheritance.
- Example: consider a class called "Car" that contains objects like "Engine," "Wheels," and "Chassis." The Car class can delegate tasks such as starting the engine or moving the wheels to its component objects.
To implement composition in Java, you can define member variables of the composite class as objects of other classes and instantiate them within the composite class's constructor or setter methods. The composite class can then call methods on its component objects to perform specific tasks.

Composition plays a crucial role in creating modular, maintainable, and extensible code. It enables the building of complex systems by assembling simpler objects, promoting code reuse, encapsulation, and flexibility.

## SOLID Principles
SOLID is an acronym that represents a set of principles for software design and development. These principles, when followed, help in creating maintainable, flexible, and scalable software systems. Let's go through each principle:

1. Single Responsibility Principle (SRP): This principle states that a class should have only one reason to change. It means that a class should have a single responsibility or job and should not be responsible for multiple unrelated tasks. By adhering to SRP, classes become more focused, easier to understand, and less prone to bugs. It promotes high cohesion and modular design. 
2. Open/Closed Principle (OCP): The OCP states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. It means that you should be able to add new functionality or behavior to a system without modifying its existing code. This principle promotes the use of abstractions, interfaces, and polymorphism to achieve flexibility and avoid breaking existing code when making changes.
3. Liskov Substitution Principle (LSP): LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, if a class is a subtype of another class, it should be able to be used interchangeably with its parent class without causing any issues. This principle ensures that inheritance hierarchies are well-designed, adhering to the "is-a" relationship and maintaining expected behavior.
4. Interface Segregation Principle (ISP): ISP states that clients should not be forced to depend on interfaces they do not use. It encourages the design of smaller and more focused interfaces, tailored to specific client needs. This principle avoids the problem of clients being forced to implement or depend on methods they don't need or care about.
5. Dependency Inversion Principle (DIP): DIP states that high-level modules/classes should not depend on low-level modules/classes directly. Instead, they should depend on abstractions or interfaces. This principle promotes loose coupling and the decoupling of modules, allowing for easier maintenance, testing, and flexibility. It also enables the use of dependency injection and inversion of control (IoC) containers.

By following the SOLID principles, developers can create code that is easier to understand, maintain, and extend. These principles promote modular design, separation of concerns, flexibility, and adherence to good software engineering practices. They are widely regarded as best practices in object-oriented design and development.