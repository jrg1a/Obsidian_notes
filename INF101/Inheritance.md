Inheritance is a process in object-oriented programming where one object acquires the properties of another object. It enables hierarchical classification and allows objects to inherit general attributes from their parent classes. Without inheritance, each object would need to define all its characteristics explicitly. Inheritance facilitates the creation of specific instances within more general cases. The hierarchical view of the world, such as animals, mammals, and dogs, reflects the natural perception of objects. [[Classes]] define attributes and behavior, and subclasses inherit attributes from their superclasses. Inheritance interacts with encapsulation, where subclasses inherit encapsulated attributes and can add their own specialization. This concept enables the linear growth of object-oriented programs, reducing unpredictable interactions with the rest of the codebase.

![[Pasted image 20230522152520.png]]
Important parts:
- Inheritance supports hierarchical classification and allows objects to acquire properties from other objects.
- It reduces the need for explicit definition of all characteristics in each object.
- Classes define attributes and behavior, while subclasses inherit attributes from superclasses.
- Inheritance interacts with encapsulation, with subclasses inheriting encapsulated attributes and adding their own specialization.
- This concept enables the linear growth of object-oriented programs and reduces unpredictable interactions with the rest of the codebase.
- Inheritance promotes code reuse: By inheriting properties and behavior from a superclass, subclasses can reuse and build upon existing code. This reduces redundancy and enhances the efficiency of development.
- [[Polymorphism]]: Inheritance is closely tied to polymorphism, another key concept in object-oriented programming. Polymorphism allows objects of different classes to be treated as objects of a common superclass, providing flexibility and extensibility in the code.
- Overriding and extending behavior: Inheritance allows subclasses to override or extend the behavior of their superclass. Subclasses can provide their own implementation of methods defined in the superclass, enabling customization and specialization.
- Inheritance hierarchies: Inheritance forms hierarchical relationships among classes, creating a structured and organized system of objects. This hierarchy allows for better organization and understanding of the relationships between classes.
- Single inheritance vs. multiple inheritance: Java supports single inheritance, meaning a class can only inherit from one superclass. This simplifies the language and avoids complications that can arise from multiple inheritance, which is supported by some other programming languages.
- Abstract classes and interfaces: In addition to concrete classes, inheritance is often used with abstract classes and interfaces. Abstract classes provide a partial implementation and can't be instantiated, while interfaces define a contract for classes to implement. Both abstract classes and interfaces play a role in defining hierarchies and facilitating inheritance relationships.
![[Pasted image 20230522152541.png]]
In summary, inheritance in object-oriented programming promotes code reuse, facilitates polymorphism, allows for behavior customization, and creates hierarchical relationships among classes. It is a powerful mechanism for structuring and organizing code and enables the creation of flexible and extensible software systems.

> Inheritance is one of the cornerstones of object-oriented programming because it allows the creation of hierarchical classifications. Using inheritance, you can create a general class that defines traits common to a set of related items. This class can then be inherited by other, more specific classes, each adding those things that are unique to it. In the terminology of Java, a class that is inherited is called a superclass. The class that does the inheriting is called a subclass. Therefore, a subclass is a specialized version of a superclass. It inherits all of the members defined by the superclass and adds its own, unique elements.

## Inheritance Basics
To inherit a class, you simply incorporate the definition of one class into another by
using the **extends** keyword.

**Example:**
The following program creates a superclass called A and a subclass called B. Notice how the keyword extends is used to create a subclass of A.

```Java
// A simple example of inheritance.
// Create a superclass.
class A {
	int i, j;
	
	void showij() {
		System.out.println("i and j: " + i + " " + j);
	}
}

// Create a subclass by extending class A.
class B extends A {
	int k;
	
	void showk() {
		System.out.println("k: " + k);
	}

	void sum() {
		System.out.println("i+j+k: " + (i+j+k));
		}
	}


class SimpleInheritance {
	public static void main(String[] args) {
		A superOb = new A();
		B subOb = new B();
		
		// The superclass may be used by itself.
		superOb.i = 10;
		superOb.j = 20;
		System.out.println("Contents of superOb: ");
		superOb.showij();
		System.out.println();
		/* The subclass has access to all public members of
		its superclass. */
		subOb.i = 7;
		subOb.j = 8;
		subOb.k = 9;
		System.out.println("Contents of subOb: ");
		subOb.showij();
		subOb.showk();
		System.out.println();
		
		System.out.println("Sum of i, j and k in subOb:");
		subOb.sum();
	}
}
```

The output of the program:

Contents of ``superOb``:
i and j: ``10 20``

Contents of ``subOb``:
i and j: ``7 8``
k: ``9``

Sum of ``i``, ``j`` and ``k`` in ``subOb``:
i+j+k: ``24``

The subclass B includes all of the members of its superclass, A. This is
why ``subOb`` can access i and j and call ``showij( )``. Also, inside ``sum( )``, i and j can be referred to directly, as if they were part of B.
Even though A is a superclass for B, it is also a completely independent, stand-alone
class. Being a superclass for a subclass does not mean that the superclass cannot be used by itself. Further, a subclass can be a superclass for another subclass.