
This is a short summary of Object and Methods in the context of OOP Java development.

## Objects
Objects are the fundamental building blocks of Java programs. In Java, everything is considered an object, including variables, data, and even [[classes]] themselves. An object is an instance of a class, which serves as a blueprint or template for creating objects.

When an object is created, it has its own state (data) and behavior (methods). The state of an object is represented by its instance variables, which hold the object's data. The behavior of an object is defined by its methods, which are the actions that the object can perform.


Objects in Java have several important characteristics:
- Identity: Each object has a unique identity, which distinguishes it from other objects.
- [[Encapsulation]]: Objects encapsulate data and behavior together, allowing for better organization and modularity of code.
- [[Inheritance]]: Objects can inherit characteristics and behavior from parent classes, allowing for code reuse and specialization.
- [[Polymorphism]]: Objects can take on many forms, allowing different objects to be treated interchangeably based on their shared interfaces or parent classes.

To create an object, you need to define a class that specifies its structure and behavior. A class serves as a blueprint for creating objects of that class type. It defines the instance variables to hold data and methods to perform operations on that data.

For example, consider a class called "Car." You can create multiple car objects by instantiating the Car class. Each car object will have its own state, such as the make, model, and color, represented by instance variables. The car objects can also perform actions like starting the engine or accelerating, which are defined by methods in the Car class.

Creating and interacting with objects is at the core of object-oriented programming in Java. Objects allow you to model real-world entities, represent data, and implement the desired behavior of your program. By utilizing objects effectively, you can build robust and modular applications in Java.

Example of Objects in Java:
```Java
public class Car {
    String make;
    String model;
    int year;

    public void startEngine() {
        System.out.println("Engine started for " + make + " " + model);
    }

    public void accelerate() {
        System.out.println("Car is accelerating...");
    }

    public void brake() {
        System.out.println("Car is braking...");
    }

    public static void main(String[] args) {
        // Create an instance of the Car class
        Car myCar = new Car();

        // Set the object's state
        myCar.make = "Toyota";
        myCar.model = "Camry";
        myCar.year = 2022;

        // Call the object's methods
        myCar.startEngine();
        myCar.accelerate();
        myCar.brake();
    }
}

```


## Methods
In Java, methods are blocks of code that define the behavior of objects. They encapsulate a set of instructions that can be executed when the method is called. Methods provide a way to organize and modularize code, making it easier to understand, reuse, and maintain.

Here are some key points about methods in Java:
1. Method Signature: A method is defined by its signature, which consists of the method name and the parameter list. The signature specifies the unique identifier for the method and defines the input parameters, if any, that the method expects.
2. Return Type: Methods can optionally have a return type, which indicates the type of value the method will return after executing its code. If a method doesn't return a value, its return type is specified as "void".
3. Parameters: Methods can accept input parameters, which are values passed to the method for processing. Parameters provide a way to pass data to methods and make them more flexible and reusable.
4. Method Body: The method body contains the actual code that defines the behavior of the method. It consists of statements and expressions that are executed when the method is called.
5. Method Invocation: To execute a method, you need to invoke or call it. Method invocation involves specifying the name of the method followed by parentheses, which may contain arguments if the method expects any.
6. Modularity and Code Re-usability: Methods promote modularity by allowing you to break down complex tasks into smaller, more manageable parts. By organizing code into methods, you can reuse the same code in multiple places within a program, improving code efficiency and reducing duplication.
7. Method Overloading: Java supports method overloading, which means you can define multiple methods with the same name but different parameter lists. Overloaded methods provide flexibility and convenience by allowing you to perform similar operations on different types of data.
8. Access Modifiers: Methods can have access modifiers such as "public", "private", or "protected", which control their visibility and accessibility from other parts of the program.

Methods play a crucial role in object-oriented programming by encapsulating behavior and promoting code reuse. They allow objects to perform specific actions and provide a mechanism for interaction between objects in a program.

By designing well-structured and meaningful methods, you can improve code readability, maintainability, and overall program organization. Methods are essential components in building efficient and functional Java applications.


## Method Overloading
Method overloading is a feature in Java that allows a class to have multiple methods with the same name but different parameters. Here are the key points to consider when discussing method overloading:
1. Method Signature: Method overloading is determined by the method's signature, which consists of the method name and the parameter types. The return type of the method is not considered when determining method overloading.
2. Different Parameter Types: In an overloaded method, the parameters must be different in terms of their types, order, or number. This allows you to define multiple versions of a method that perform similar operations but with different input types.
3. Return Type and Exceptions: Overloaded methods can have the same or different return types. However, the return type alone is not sufficient to differentiate between overloaded methods. Similarly, the exceptions thrown by the methods do not affect method overloading.
4. Method Invocation: During method invocation, the Java compiler matches the arguments passed to the method with the appropriate overloaded method based on the parameter types. The decision is made at compile-time, and the appropriate method is called based on the matched signature.
5. Improved Readability and Flexibility: Method overloading improves code readability by providing meaningful method names for different variations of an operation. It also enhances code flexibility by allowing developers to use the same method name for related functionality, making the code more intuitive and easier to maintain.
6. Example:
```Java
public class MathUtils {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        MathUtils math = new MathUtils();
        
        // Method invocation based on parameter types
        int sum1 = math.add(2, 3);
        double sum2 = math.add(2.5, 3.7);
        int sum3 = math.add(2, 3, 4);

        System.out.println("Sum 1: " + sum1);
        System.out.println("Sum 2: " + sum2);
        System.out.println("Sum 3: " + sum3);
    }
}
```

In this example, the `MathUtils` class demonstrates method overloading. It defines three `add()` methods that accept different parameter types: `add(int, int)`, `add(double, double)`, and `add(int, int, int)`. Each method performs addition, but they can handle different types of numeric values. During method invocation, the appropriate version of the `add()` method is chosen based on the argument types passed.

Method overloading provides flexibility and convenience in programming by allowing multiple methods with the same name to handle different variations of an operation. It enhances code readability and simplifies the naming of methods, making the code more expressive and easier to understand.


## Method Invocation
Method invocation refers to the process of calling or executing a method in Java. Here are the key points to consider when discussing method invocation:
1. Method Call: Method invocation is initiated by calling a method using its name followed by parentheses. The method call includes the method name and any required arguments enclosed within the parentheses.
2. Accessing Methods: Methods can be accessed in two ways: through an object or through a class. Instance methods are called on an object of the class, while static methods are called directly on the class itself without the need for an instance.
3. Object-Oriented Nature: Method invocation is a fundamental concept in object-oriented programming (OOP). In OOP, objects are created from classes, and methods define the behavior of those objects. By invoking methods on objects, we perform actions or operations associated with the object's behavior.
4. Method Signature: The method signature, consisting of the method name and its parameter types, is used to identify the specific method to be invoked. It ensures that the correct method is called, especially when dealing with method overloading or inheritance.
5. Method Overriding: Method invocation is closely related to method overriding, which occurs when a subclass defines a method with the same name and signature as a method in its superclass. When a method is invoked on a subclass object, the overridden method in the subclass is executed instead of the superclass method.
6. Runtime Polymorphism: Method invocation plays a crucial role in achieving runtime polymorphism in Java. Polymorphism allows different objects to respond to the same method call in different ways based on their specific implementation of the method. This enables more flexible and dynamic behavior in an object-oriented system.
7. Example:
```Java
public class Animal {
    public void makeSound() {
        System.out.println("Generic animal sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark!");
    }

    public void fetch() {
        System.out.println("Fetching the ball!");
    }
}

public class MethodInvocation {
    public static void main(String[] args) {
        Animal animal = new Animal();
        Dog dog = new Dog();

        animal.makeSound(); // Invokes makeSound() from Animal class
        dog.makeSound(); // Invokes overridden makeSound() from Dog class

        animal = dog;
        animal.makeSound();// Polymorphic invocation, still invokes Dog's makeSound()

        // dog.fetch(); // Cannot invoke fetch() as it is not present in Animal class
    }
}
```
In this example, the `Animal` class has a method called `makeSound()`, which prints a generic animal sound. The `Dog` class extends `Animal` and overrides the `makeSound()` method to print "Bark!" instead. The `MethodInvocation` class demonstrates method invocation by creating objects of `Animal` and `Dog` classes and invoking the `makeSound()` method on them. When the `makeSound()` method is invoked, the appropriate version of the method is executed based on the actual type of the object.

Method invocation is a fundamental concept in Java that enables the execution of code associated with specific methods. It allows objects to exhibit behavior defined by their class and supports important principles of OOP, such as polymorphism and method overriding.

## Constructors

1. Constructors: Constructors are special methods in Java that are used to initialize objects of a class. Here are the key points to consider when discussing constructors:    
2. Purpose: The main purpose of a constructor is to initialize the instance variables of an object when it is created. Constructors are called automatically when an object is instantiated using the `new` keyword.
3. Method Name: Constructors have the same name as the class they belong to. They do not have a return type, not even `void`. This is because the return type of a constructor is implicitly the class itself.
4. Initialization: Constructors are responsible for initializing the state of an object. They can set the initial values of instance variables, perform additional setup tasks, and ensure that the object is in a valid state before it is used.
5. Overloading: Constructors can be overloaded, which means a class can have multiple constructors with different parameter lists. This allows objects to be created with different initializations or to accommodate different ways of creating objects.
6. Default Constructor: If a class does not explicitly define any constructors, Java provides a default constructor with no parameters. This constructor initializes the instance variables to their default values (e.g., `null` for reference types, `0` for numeric types, and `false` for boolean).
7. Access Modifiers: Constructors can have access modifiers like `public`, `private`, or `protected`. These modifiers control the accessibility of the constructor from other classes.
8. Chaining Constructors: Constructors can call other constructors within the same class using the `this()` keyword. This allows constructors to reuse code and provide flexibility in initializing objects.
9. Example:
```Java
public class Car {
    private String brand;
    private String model;
    private int year;

    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Default constructor
    public Car() {
        this("Unknown", "Unknown", 0);
    }

    public String getBrand() {
        return brand;
    }

    public String getModel() {
        return model;
    }

    public int getYear() {
        return year;
    }
}

public class ConstructorsExample {
    public static void main(String[] args) {
        Car car1 = new Car("Toyota", "Camry", 2022);
        Car car2 = new Car();

        System.out.println(car1.getBrand() + " " + car1.getModel() + " " + car1.getYear());
        System.out.println(car2.getBrand() + " " + car2.getModel() + " " + car2.getYear());
    }
}
```

In this example, the `Car` class has two constructors. The parameterized constructor accepts the brand, model, and year as arguments and initializes the corresponding instance variables. The default constructor uses the `this()` constructor chaining mechanism to call the parameterized constructor with default values. The `Car` class also provides getter methods to retrieve the values of the instance variables.

In the `ConstructorsExample` class, two `Car` objects are created using different constructors. The first object is initialized with specific values, while the second object uses the default constructor, resulting in default values being assigned. The output of the program displays the brand, model, and year of each car.

Constructors play a crucial role in object initialization and provide a way to ensure that objects are properly set up before they are used. They allow classes to define how objects are created and initialized, providing flexibility and customization during object creation.

## Method Overriding
Method overriding is a feature in Java that allows a [[Classes#Subclasses|subclass]] to provide its own implementation of a method that is already defined in its [[Classes#Superclasses|superclass]]. When a method in the [[Classes#Subclasses|subclass]] has the same name, return type, and parameter list as a method in the [[Classes#Superclasses|superclass]], it is said to override the [[Classes#Superclasses|superclass]] method. Here are some key points to understand about method overriding in Java:
1.  Inheritance: Method overriding is closely related to [[inheritance]], as it allows a [[Classes#Subclasses|subclass]] to inherit methods from its superclass and modify or extend their behavior. By overriding a method, the [[Classes#Subclasses|subclass]] can provide a different implementation while maintaining the same method signature.
2.  Annotation: The `@Override` annotation is used to indicate that a method is intended to override a method from the [[Classes#Superclasses|superclass]]. It is an optional annotation but is highly recommended to use. Adding this annotation helps catch errors during compilation if the annotated method doesn't actually override a [[Classes#Superclasses|superclass]] method.
3.  Method Signature: The overriding method in the [[Classes#Subclasses|subclass]] must have the same method signature as the method in the [[Classes#Superclasses|superclass]]. The method signature includes the method name, parameter types, and the return type. The access modifier of the overriding method can be the same or more accessible than the [[Classes#Superclasses|superclass]] method.
4.  Polymorphism: Method overriding plays a crucial role in achieving [[polymorphism]] in Java. When a [[Classes#Superclasses|superclass]] reference is used to refer to a [[Classes#Subclasses|subclass]] object, and an overridden method is called on that reference, the version of the method in the subclass is executed based on the actual type of the object at runtime. This dynamic dispatch allows different objects to be treated uniformly through their common superclass.
5.  Covariant Return Types: Java 5 introduced covariant return types, which means that an overriding method in the [[Classes#Subclasses|subclass]] can have a more specific return type than the method in the [[Classes#Superclasses|superclass]]. It allows for more flexibility in the return type while ensuring compatibility with the overridden method.
6.  Exceptions: The overriding method can throw the same exceptions as the [[Classes#Superclasses|superclass]] method or its [[Classes#Subclasses|subclass]]. However, it is not allowed to throw checked exceptions that are broader or new checked exceptions that are not present in the [[Classes#Superclasses|superclass]] method's throws clause. This ensures that the overriding method does not violate the exception handling contract defined by the [[Classes#Superclasses|superclass]] method.
7.  Method Hiding: If a [[Classes#Subclasses|subclass]] defines a static method with the same name and signature as a static method in the superclass, it is not considered overriding but rather method hiding. In this case, the [[Classes#Subclasses|subclass]] method hides the [[Classes#Superclasses|superclass]] method, and the choice of which method to invoke is determined at compile-time based on the type of the reference variable.

Example of Method Overriding:
```Java
public class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

public class Square extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a square");
    }
}

public class MethodOverridingExample {
    public static void main(String[] args) {
        Shape shape1 = new Circle();
        Shape shape2 = new Square();

        shape1.draw();  // Calls overridden draw() method in Circle class
        shape2.draw();  // Calls overridden draw() method in Square class
    }
}

```
In this example, the `Shape` class has a `draw()` method that prints "Drawing a shape". The `Circle` class and the `Square` class both extend the `Shape` class and override the `draw()` method with their specific implementations. The `MethodOverridingExample` class demonstrates method overriding by creating objects of `Circle` and `Square` classes and invoking the `draw()` method using the [[Classes#Superclasses|superclass]] reference `Shape`. The actual implementation of the method is determined based on the type of the object, enabling [[Polymorphism|polymorphic]] behavior.


Method overriding is a fundamental concept in object-oriented programming that allows for the specialization and customization of behavior in [[Classes#Subclasses|subclasses]] . It enables code re-usability, flexibility, and polymorphic behavior, making Java a powerful language for building complex software systems.

## Iterable & Iterator
The `Iterable` and `Iterator` interfaces in Java are fundamental to understanding how to work with sequences of objects in a uniform way. They form the core of the Java Collections Framework, and understanding how they work can help you manipulate collections of objects more effectively.

`Iterable` is an interface that is used to represent a collection of objects which one can iterate over. A class that implements `Iterable` must override one method: `iterator()`, which returns an Iterator.

`Iterator` is an interface that provides methods to iterate over any Collection. We can get Iterator instance from any Collection using the `iterator()` method. It has three methods: `hasNext()`, `next()`, and `remove()`.

Here's a simple example:
```Java
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> list = new LinkedList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        
        // Get an iterator from the list
        Iterator<String> iterator = list.iterator();
        
        // Use the iterator to traverse the list
        while(iterator.hasNext()) {
            String fruit = iterator.next();
            System.out.println(fruit);
            
            // Remove the item from the list if it's "Banana"
            if ("Banana".equals(fruit)) {
                iterator.remove();
            }
        }
        
        System.out.println(list);  // Outputs: [Apple, Cherry]
    }
}

```
In this example, an `Iterator` is used to traverse a `LinkedList` of strings. The `Iterator`'s `hasNext()` method is used to check if there are more elements in the list, and its `next()` method is used to get each element. If the current element is "Banana", it is removed from the list using the `Iterator`'s `remove()` method. This shows how an `Iterator` can be used to safely remove elements from a collection while iterating over it.

The use of `Iterable` and `Iterator` becomes especially important when you're dealing with large data structures or data that isn't in memory. Because the data is loaded incrementally, you can start processing it immediately rather than having to wait for the entire dataset to load.

In addition, `Iterable` and `Iterator` allow you to write more generic code. For example, if you write a method that takes an `Iterable`, it can be used with any data structure that implements this interface, not just `LinkedList` or `ArrayList`. This makes your code more reusable and flexible.

## Equals method
In Java, understanding the difference between the `equals()` method and the == operator is crucial. They both can be used to compare objects, but they work in fundamentally different ways.
- The ==  operator compares the references of two objects. It checks to see if the two operands point to the exact same object in memory. This is known as reference equality or identity. When you compare two objects using == , you're asking "Do these references point to the exact same object?"
- The `equals()` method, on the other hand, is intended for comparing the state of two objects to see if they are logically "equal". This is known as state or logical equality. When you compare two objects using `equals()`, you're asking "Do these objects represent the same thing or value?"

Let's illustrate this with an example:
```Java
public class EqualsExample {
    public static void main(String[] args) {
        String str1 = new String("Hello");
        String str2 = new String("Hello");

        // Outputs: false
        System.out.println(str1 == str2);

        // Outputs: true
        System.out.println(str1.equals(str2));
    }
}
```

In this example, `str1` and `str2` are different objects (they are located at different memory locations), but they both represent the same sequence of characters "Hello". So, == returns false because `str1` and `str2` reference different objects, while `equals()` returns true because the state of `str1` and `str2` is the same.

The `equals()` method is defined in the `Object` class, which means it's available to every Java class. By default, the `equals()` method behaves the same as the == operator—it checks for reference equality. However, many classes override `equals()` to provide their own definition of state equality. For example, the `String` class overrides `equals()` to compare the contents of two strings.

If you're creating a class where logical equality could be different from reference equality, you should override the `equals()` method. For instance, if you have a `Person` class where a person is considered equal if they have the same ID, you could do something like this:
```Java
public class Person {
    private int id;
    private String name;

    // constructor, getters and setters...

    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null || getClass() != obj.getClass())
            return false;
        Person person = (Person) obj;
        return id == person.id;
    }
}
```

Here, the `equals()` method is overridden to consider two `Person` objects as equal if their `id` fields are equal, even though they might be different objects in memory.

Note: When you override `equals()`, it is generally necessary to override `hashCode()` as well in order to maintain the general contract for the `hashCode()` method, which states that equal objects must have equal hash codes.