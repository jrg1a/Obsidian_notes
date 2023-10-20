Design patterns are proven solutions to recurring design problems in software development. They serve as best practices and guidelines that help in creating flexible, reusable, and maintainable code. Design patterns provide a common language and vocabulary for developers to communicate and share solutions to common design challenges.

## What are Design Patterns?
Design patterns are reusable solutions to common software design problems. They provide guidelines and best practices for structuring and organizing code to achieve flexibility, maintainability, and reusability. Design patterns are not specific implementations but rather high-level concepts and templates that can be applied to various situations.

## Categories of Design Patterns
- ***Creational Patterns:*** Creational patterns focus on object creation mechanisms. Examples of creational patterns include:
	- Singleton: Ensures that only one instance of a class is created and provides a global point of access to it.
	- Factory Method: Defines an [[Classes#Interface Classes|interface]] for creating objects, but allows subclasses to decide which class to instantiate.
	- [[Abstraction|Abstract]] Factory: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

- ***Structural Patterns***: Structural patterns deal with the composition of classes and objects. Examples of structural patterns include:
	- Adapter: Converts the interface of one class into another interface that clients expect, allowing classes to work together that couldn't otherwise.
	- Decorator: Adds additional behavior or responsibilities to an object dynamically without modifying its structure.
	- Composite: Composes [[Objects and Methods#Objects|objects]] into tree structures to represent part-whole hierarchies, treating individual objects and compositions uniformly.

- ***Behavioral Patterns***: Behavioral patterns focus on the interaction between objects. Examples of behavioral patterns include:
	- Observer: Defines a one-to-many dependency between objects, so that when one object changes state, its dependents are automatically notified and updated.
	- Strategy: Defines a family of interchangeable algorithms and encapsulates each one, allowing them to be used interchangeably.
	- Template Method: Defines the skeleton of an algorithm in a base class but lets subclasses override specific steps of the algorithm without changing its structure.

## Benefits of Design Patterns
- [[Modularity#Code Reusability|Reusability]]: Design patterns promote code reuse by providing proven solutions to common problems, reducing the need for reinventing the wheel.
- Maintainability: Patterns improve code maintainability by separating concerns, making code more modular and easier to understand and modify.
- [[Modularity#Modular Deployment and Scalability|Scalability]]: Design patterns allow systems to evolve and scale as requirements change, enabling flexible and adaptable software architectures.
- Communication: Using design patterns facilitates communication among developers as patterns provide a common language and shared understanding of software design concepts.

## When to Use Design Patterns
- Solving common problems: Design patterns are most useful when facing recurring design challenges or known issues with well-documented solutions.
- Balancing flexibility and complexity: Patterns help strike a balance between making code flexible enough to accommodate future changes without adding unnecessary complexity.
- Collaborative development: Design patterns promote collaboration among team members by providing a shared vocabulary and established design principles.

## Implementation Considerations
Design patterns should be used judiciously, considering factors such as project requirements, team expertise, and potential trade-offs. Overusing patterns can lead to unnecessarily complex code, while ignoring patterns altogether may result in missed opportunities for code improvement and maintainability.

## Code Examples
Here are code examples illustrating the usage of some design patterns:
- Singleton
```Java
  public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor to prevent instantiation
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
- Adapter
```Java
public interface MediaPlayer {
    void play(String filename);
}

public interface AdvancedMediaPlayer {
    void playMp4(String filename);
}

public class Mp4Player implements AdvancedMediaPlayer {
    @Override
    public void playMp4(String filename) {
        System.out.println("Playing mp4 file: " + filename);
    }
}

public class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer = new Mp4Player();
        }
    }

    @Override
    public void play(String filename) {
        advancedMediaPlayer.playMp4(filename);
    }
}

public class AudioPlayer implements MediaPlayer {
    private MediaAdapter mediaAdapter;

    @Override
    public void play(String filename) {
        if (filename.endsWith(".mp3")) {
            System.out.println("Playing mp3 file: " + filename);
        } else if (filename.endsWith(".mp4")) {
            mediaAdapter = new MediaAdapter("mp4");
            mediaAdapter.play(filename);
        } else {
            System.out.println("Invalid media format: " + filename);
        }
    }
}
```
- Observer
```Java
public interface Observer {
    void update();
}

public interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

public class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();

    @Override
    public void attach(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }
}

public class ConcreteObserver implements Observer {
    @Override
    public void update() {
        System.out.println("Observer has been notified of a change.");
    }
}
```

These examples showcase the implementation of the Singleton, Adapter, and Observer design patterns in Java.
Design patterns are a powerful tool for software development, helping developers create well-structured, maintainable, and reusable code. By understanding and applying design patterns effectively, you can enhance the quality and efficiency of your software projects.