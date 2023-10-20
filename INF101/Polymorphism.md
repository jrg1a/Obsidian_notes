Polymorphism is a feature in object-oriented programming that allows one interface to be used for multiple related actions. It enables the design of generic interfaces that can handle different types of data or situations. In non-object-oriented languages, separate sets of routines would be required for each type of data. However, in Java, polymorphism allows the specification of a general set of routines with the same names, reducing complexity. The specific action or method is determined by the compiler based on the situation, relieving the programmer from making manual selections. Polymorphism can be compared to a dog's sense of smell, which reacts differently to different scents but utilizes the same underlying mechanism.

Important parts:
- Polymorphism allows one interface to be used for multiple related actions.
- It reduces complexity by enabling the use of a generic interface for a class of actions.
- In Java, polymorphism eliminates the need for separate routines by specifying a general set of routines with the same names.
- The compiler selects the specific action or method based on the situation.
- Polymorphism can be compared to a dog's sense of smell, where different scents evoke different reactions but utilize the same underlying mechanism.
- Polymorphism applies to methods within a Java program, allowing for flexibility and code re-usability.

[[Polymorphism]], [[encapsulation]], and[[ inheritance]] are essential components of object-oriented programming that work together to create robust and scalable programs. A well-designed hierarchy of classes enables code reuse, while encapsulation allows for the migration of implementations without breaking dependent code. Polymorphism contributes to creating clean, readable, and resilient code. The example of automobiles illustrates the power of object-oriented design, as drivers rely on inheritance to operate different types of vehicles while interacting with encapsulated features like pedals. Car manufacturers offer various options while maintaining a consistent interface for control. Similarly, in computer programs, the application of object-oriented principles brings together different parts to form a cohesive and maintainable whole. Although some example programs may not exhibit all features, encapsulation, inheritance, and polymorphism are present in Java programs and extensively utilized in its built-in class libraries.

Important parts:
- Polymorphism, encapsulation, and inheritance work together to support the development of robust and scalable programs.
- A well-designed hierarchy of classes enables code reuse and investment in development and testing.
- [[Encapsulation]] allows for the migration of implementations without breaking dependent code.
- Polymorphism contributes to creating clean, readable, and resilient code.
- The automobile example illustrates the application of [[inheritance]] and [[encapsulation]], with drivers operating different vehicles while interacting with common [[Classes#Interface Classes|interfaces]] like pedals.
- Car manufacturers offer various options while maintaining a consistent interface for control.
- Object-oriented principles bring together different parts of a complex program to create a cohesive and maintainable whole.
- Java programs involve [[encapsulation]], [[inheritance]], and [[polymorphism]], which are extensively used in its built-in class libraries.

## Polymorphism: Code
In this example, we have a base class called `Shape` with a method `draw()`. This class is inherited by two subclasses, `Circle` and `Rectangle`. Each subclass overrides the `draw()` method with its specific implementation.

In the `main()` method, we create objects of the `Circle` and `Rectangle` classes and assign them to variables of type `Shape`. This demonstrates polymorphism, as we are treating objects of different subclasses as objects of the superclass.

When we invoke the `draw()` method on `shape1` and `shape2`, the appropriate implementation is called based on the actual type of the object. Even though the variables are of type `Shape`, the overridden methods in the respective subclasses (`Circle` and `Rectangle`) are executed. This dynamic method dispatch based on the object's actual type is an example of polymorphism.

```Java
class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Shape shape1 = new Circle();
        Shape shape2 = new Rectangle();

        shape1.draw(); // Output: Drawing a circle
        shape2.draw(); // Output: Drawing a rectangle
    }
}

```