Swing is a framework that provides more powerful and flexible GUI components than does the ``AWT``. As a result, it is the GUI that has been widely used by Java programmers for more than two decades.

# Introducing Swing

We will look at swing in three different segments, first we will look at an introduction of Swing, and describing Swings core concepts.

## The Origin of Swing
Swing was developed as a response to the limitations of Java's original GUI subsystem, the Abstract Window Toolkit (AWT). Here are some key points to understand about Swing and its role in Java's graphical user interface development:

1. Background: Swing was introduced in 1997 as part of the Java Foundation Classes (JFC). It was created to overcome the deficiencies of the AWT and provide a more powerful and flexible GUI framework for Java applications.
2. AWT Limitations: The AWT offered a basic set of controls and components, but its main limitation was its reliance on platform-specific peers to render the GUI components. This led to inconsistent behavior and appearance across different operating systems, which was not in line with Java's "write once, run anywhere" principle.
3. Lightweight Components: Unlike the heavyweight components of AWT, Swing introduced lightweight components. These components are rendered entirely in Java and do not rely on platform-specific peers. This allowed for greater consistency and control over the look and feel of the GUI components.
4. Pluggable Look and Feel: Swing introduced the concept of pluggable look and feel, which means that the visual appearance of Swing components can be customized independently of the underlying platform. Swing provides several look and feel options, including the cross-platform "Metal" look and feel.
5. Rich Component Set: Swing expanded the range of GUI components available in Java, providing developers with a broader set of controls, windows, and dialog boxes. It included components such as buttons, text fields, tables, menus, and more, allowing for the creation of more sophisticated and feature-rich user interfaces.
6. Customizability: Swing components offer extensive customization options, allowing developers to tailor the appearance and behavior of components to suit their application's requirements. This can be achieved through properties, styles, event handling, and layout managers.
7. Integration with Java: Starting from Java 1.2, Swing became an integral part of the Java platform. It was fully integrated into the Java API, making it readily available for developers without the need for additional libraries or dependencies.

Swing revolutionized Java's GUI development by providing a more flexible, consistent, and feature-rich framework compared to the AWT. It enabled developers to create visually appealing and interactive user interfaces that could run on different platforms without sacrificing the cross-platform compatibility that Java is known for.

## Swing is Built on the AWT
Before moving on, it is necessary to make one important point: although Swing eliminates a number of the limitations inherent in the AWT, Swing does not replace it. Instead, Swing is built on the foundation of the AWT. This is why the AWT is still a crucial part of Java. Swing also uses the same event handling mechanism as the AWT. Therefore, a basic understanding of the AWT and of event handling is required to use Swing.

## Two Key Swing Features
Swing was created to address the limitations present in the AWT. It does this through two key features: lightweight components and a pluggable look and feel. Together they provide an elegant, yet easy-to-use solution to the problems of the AWT. More than anything else, it is these two features that define the essence of Swing. Each is examined here.

### Swing Components Are Lightweight
Swing components are lightweight (with a few exceptions). By this we means that they are written entirely in Java, and do not map directly to platform-specific peers. Thus,
lightweight components are more efficient and more flexible Furthermore, because
lightweight components do not translate into native peers, the look and feel of each
component is determined by Swing, not by the underlying operating system. As a result, each component will work in a consistent manner across all platforms.

### Swing Supports a Pluggable Look and Feel
Swing supports a pluggable look and feel (PLAF). Because each Swing component is rendered by Java code rather than by native peers, the look and feel of a component is under the control of Swing. This fact means that it is possible to separate the look and feel of a component from the logic of the component, and this is what Swing does. Separating out the look and feel provides a significant advantage: it becomes possible to change the way that a component is rendered without affecting any of its other aspects. In other words, it is possible to “plug in” a new look and feel for any given component without creating any side effects in the code that uses that component. Moreover, it becomes possible to define entire sets of look-and-feels that represent different GUI styles. To use a specific style, its look and feel is simply “plugged in.” Once this is done, all components are automatically rendered using that style.

Pluggable look-and-feels offer several important advantages. It is possible to define a look
and feel that is consistent across all platforms. Conversely, it is possible to create a look and
feel that acts like a specific platform. It is also possible to design a custom look and feel.
Finally, the look and feel can be changed dynamically at run time.
Java provides look-and-feels, such as metal and Nimbus, that are available to all Swing
users. The metal look and feel is also called the Java look and feel. It is platform-independent
and available in all Java execution environments. It is also the default look and feel. This book
uses the default Java look and feel (metal) because it is platform independent.

## The MVC Connection
In general, a visual component is a composite of three distinct aspects:
- The way that the component looks when rendered on the screen
- The way that the component reacts to the user
- The state information associated with the component
No matter what architecture is used to implement a component, it must implicitly contain
these three parts. Over the years, one component architecture has proven itself to be exceptionally effective: Model-View-Controller, or MVC for short.

The MVC architecture is successful because each piece of the design corresponds to an aspect of a component. In MVC terminology, the model corresponds to the state information associated with the component.
- For example, in the case of a check box, the model contains a field that indicates if the box is checked or unchecked.
- The view determines how the component is displayed on the screen, including any aspects of the view that are affected by the current state of the model.
- The controller determines how the component reacts to the user. For example, when the user clicks a check box, the controller reacts by changing the model to reflect the user’s choice (checked or unchecked).
- This then results in the view being updated. By separating a component into a model, a view, and a controller, the specific implementation of each can be changed without affecting the other two.
- For instance, different view implementations can render the same component in different ways without affecting the model or the controller.

Although the MVC architecture and the principles behind it are conceptually sound, the
high level of separation between the view and the controller is not beneficial for Swing
components. Instead, Swing uses a modified version of MVC that combines the view and the controller into a single logical entity called the UI delegate. For this reason, Swing’s approach
is called either the Model-Delegate architecture or the Separable Model architecture.
Therefore, although Swing’s component architecture is based on MVC, it does not use a
classical implementation of it.

Swing’s pluggable look and feel is made possible by its Model-Delegate architecture.
Because the view (look) and controller (feel) are separate from the model, the look and feel
can be changed without affecting how the component is used within a program. Conversely,
it is possible to customize the model without affecting the way that the component appears
on the screen or responds to user input.

To support the Model-Delegate architecture, most Swing components contain two
objects. The first represents the model. The second represents the UI delegate. Models are
defined by interfaces. For example, the model for a button is defined by the ``ButtonModel``
interface. UI delegates are classes that inherit ``ComponentUI``. For example, the UI delegate
for a button is ``ButtonUI``. Normally, your programs will not interact directly with the UI
delegate.

## Components and Containers
A Swing GUI consists of two key items:
- Components
- Containers
- This distinction is mostly conceptual because all containers are also components.
- The difference between the two is found in their intended purpose:
	- As the term is commonly used, a component is an independent visual control, such as a push button or slider
	- A container holds a group of components. Thus, a container is a special type of component that is designed to hold other components. Furthermore, in order for a component to be displayed, it must be held within a container
- Thus, all Swing GUIs will have at least one container. Because containers are components, a container can also hold other containers.
	- This enables Swing to define what is called a containment hierarchy, at the top of which must be a top-level container.

### Components
In general, Swing components are derived from the ``JComponent`` class.
- The only exceptions to this are the four top-level containers
``JComponent`` provides the functionality that is common to all components. 
For example, ``JComponent`` supports the pluggable look and feel. ``JComponent`` inherits the AWT classes ``Container`` and ``Component``. Thus, a Swing component is built on and compatible with an AWT component.

All of Swing’s components are represented by classes defined within the package ``javax.swing``.

Overview of the class names for Swing Components:
![[Pasted image 20230522215149.png]]
![[Pasted image 20230522215202.png]]
- Notice: all the component classes begin with the letter ``J`` . 

### Containers
Swing defines two types of containers, the first are top-level containers:
- ``JFrame``, ``JApplet``, ``JWindow`` and ``JDialog``. 
- These containers do not [[Inheritance|inherit]] ``JComponents``. 
	- They do inherit the ``AWT`` classes ``Component`` and ``Container``. 
- Unlike Swing’s other components, which are lightweight, the top-level containers are heavyweight. This makes the top-level containers a special case in the Swing component library.
As the name implies, a top-level container must be at the top of a containment hierarchy.
A top-level container is not contained within any other container. Furthermore, every
containment hierarchy must begin with a top-level container. The one most commonly used
for applications is ``JFrame``. 
- In the past, the one used for applets was ``JApplets``. 
- beginning with JDK 9 applets have been deprecated, and are now deprecated for removal. As a result, ``JApplet`` is also deprecated for removal
- Furthermore, beginning with JDK 11, applet support has been removed.

The second type of containers supported by Swing are lightweight containers. Lightweight
containers do [[Inheritance|inherit]]  ``JComponent``.
Lightweight containers are often used to organize and manage groups of related components because a lightweight container can be contained within another container.
- you can use lightweight containers such as ``JPanel`` to create subgroups of related controls that are contained within an outer container.

### The Top-Level Container Panes
Each top-level container defines a set of panes. At the top of the hierarchy is an instance
of ``JRootPane``
- ``JRootPane`` is a lightweight container whose purpose is to manage the other panes. It also helps manage the optional menu bar.
- The panes that comprise the root pane are called the *glass pane*, the *content pane*, and the *layered pane*.
The glass pane is the top-level pane. It sits above and completely covers all other panes.
By default, it is a transparent instance of ``JPanel``
- The glass pane enables you to manage mouse events that affect the entire container (rather than an individual control) or to paint over any other component, for example.
- In most cases, you won’t need to use the glass pane directly, but it is there if you need it.

The layered pane is an instance of ``JLayeredPane``.
- The layered pane allows components to be given a depth value. 
- This value determines which component overlays another.
	- Thus, the layered pane lets you specify a Z-order for a component, although this is not something that you will usually need to do.
- The layered pane holds the content pane and the (optional) menu bar.

Although the glass pane and the layered panes are integral to the operation of a top-level
container and serve important purposes, much of what they provide occurs behind the scene.
The pane with which your application will interact the most is the content pane, because this
is the pane to which you will add visual components.
- In other words, when you add a component, such as a button, to a top-level container, you will add it to the content pane.
- By default, the content pane is an opaque instance of [``JPanel``](https://docs.oracle.com/javase/8/docs/api/javax/swing/JPanel.html)


## The Swing Packages 
Swing is a very large subsystem and makes use of many packages. At the time of this writing,
these are the packages defined by Swing
![[Pasted image 20230522221006.png]]
Beginning the JDK 9, the Swing packages are part of the java.desktop module.
The main package is javax.swing. This package must be imported into any program that
uses Swing. It contains the classes that implement the basic Swing components, such as push
buttons, labels, and check boxes.

## A Simple Swing Application
Swing programs differ from both the console-based programs and the AWT-based programs.  They use a different set of components and a different container hierarchy than does the AWT. Swing programs also have special requirements that relate to threading.The best way to understand the structure of a Swing program is to work through an code example.
- it is necessary to point out that in the past there were two types of Java programs in which Swing was typically used:
	- The first is a desktop application. This type of Swing application is widely used, and is the type of Swing program described here
	- The second is the applet. Because applets are now deprecated and not suitable for use in new code, they are not discussed in this section. 
The following program shows one way to write a Swing application.
In the process, it demonstrates several key features of Swing. It uses two Swing components:
[``JFrame``](https://docs.oracle.com/javase/8/docs/api/javax/swing/JFrame.html) and [``JLabel``](https://docs.oracle.com/javase/8/docs/api/javax/swing/JLabel.html). [``JFrame``](<[``JFrame``](https://docs.oracle.com/javase/8/docs/api/javax/swing/JFrame.html)>) is the top-level container that is commonly used for Swing applications. 
``JLabel`` is the Swing component that creates a label, which is a component that displays information. The label is Swing’s simplest component because it is passive.
- That is, a label does not respond to user input. It just displays output.
The program uses a ``JFrame`` container to hold an instance of a ``JLabel``. The label displays a short text message. 

Example:
```Java
// A simple Swing application.
import javax.swing.*;

class SwingDemo {
	SwingDemo() {
		// Create a new JFrame container.
		JFrame jfrm = new JFrame("A Simple Swing Application");
		// Give the frame an initial size.
		jfrm.setSize(275, 100);
		// Terminate the program when the user closes the application.
		jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		// Create a text-based label.
		JLabel jlab = new JLabel(" Swing means powerful GUIs.");
		// Add the label to the content pane.
		jfrm.add(jlab);
		// Display the frame.
		jfrm.setVisible(true);
	}
	
	public static void main(String[] args) {
		// Create the frame on the event dispatching thread.
		SwingUtilities.invokeLater(new Runnable() {
			public void run() {
				new SwingDemo();
			}
		});
	}
}
```

Swing programs are compiled and run in the same way as other Java applications. Thus,
to compile this program, you can use this command line:
```
javac SwingDemo.java
```
To run the program, use this command line:
```
java SwingDemo
```
When the program is run, it will produce a window popping up with the text "Swing means powerful GUIs.". The ``SwingDemo`` program illustrates several core Swing concepts. Lets take a look at each line of the program:
1. The program begins by importing ``javax.swing``. This package contains the components and models defined by Swing. 
2. Next, the program declares the ``SwingDemo`` class and a constructor for that class. The constructor is where most of the action of the program occurs. It begins by creating a ``JFrame``, using this line of code:
	- ``JFrame jfrm = new JFrame("A Simple Swing Application");``
	- This creates a container called ``jfrm`` that defines a rectangular window complete with a title bar; close, minimize, maximize, and restore buttons; and a system menu.
	- Thus, it creates a standard, top-level window. The title of the window is passed to the constructor
3.  Next, the window is sized using this statement:
	- ``jfrm.setSize(275, 100);``
	- The ``setSize()`` method (which is inherited by ``JFrame`` from the AWT class ``Component``) sets the dimensions of the window, which are specified in pixels.
	- Its general form is shown here:
		-  ``void setSize(int width, int height)``
	- By default, when a top-level window is closed (such as when the user clicks the close box), the window is removed from the screen, but the application is not terminated.
		- While this default behavior is useful in some situations, it is not what is needed for most applications.
		- Instead, you will usually want the entire application to terminate when its top-level window is closed. There are a couple of ways to achieve this. The easiest way is to call ``setDefaultCloseOperation()``
		- ``jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);``
4. After the ``jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);`` call executes, closing the window causes the entire app to terminate. 
	- The general form of ``setDefaultCloseOperation()`` is shown here:
		- ``void setDefaultCloseOperation(int what)``
		- The value passed in what determines what happens when the window is closed.
	- There are several other options in addition to ``JFrame.EXIT_ON_CLOSE``.
		- ``DISPOSE_ON_CLOSE``
		- ``HIDE_ON_CLOSE``
		- ``DO_NOTHING_ON_CLOSE``
5. The next line of code creates a Swing ``JLabel`` component:
	- ``JLabel jlab = new JLabel(" Swing means powerful GUIs.");``
	- ``JLabel`` is the simplest and easiest-to-use component because it does not accept user input.
	- It simply displays information, which can consist of text, an icon, or a combination of the two.
	- The label created by the program contains only text, which is passed to its constructor
6. The next line of code adds the label to the content pane of the frame:
	- ``jfrm.add(jlab);``
	- all top-level containers have a content pane in which components are stored. Thus, to add a component to a frame, you must add it to the frame’s content pane.
	- This is accomplished by calling ``add()`` on the ``JFrame`` reference (``jfrm`` in this case).
	- The general form of ``add()`` is shown here:
		- ``Component add(Component comp)``
		- The ``add()`` method is inherited by ``JFrame`` from the AWT class ``Container``.
		- By default, the content pane associated with a ``JFrame`` uses border layout. The version of ``add()`` just shown adds the label to the center location. Other versions of ``add()`` enable you to specify one of the border regions.
		- When a component is added to the center, its size is adjusted automatically to fit the size of the center.
7. The last statement in the ``SwingDemo`` constructor causes the window to become visible:
	- ``jfrm.setVisible(true);``
	- The ``setVisible()`` method is inherited from the AWT ``Component`` class.
	- If its argument is true, the window will be displayed. Otherwise, it will be hidden. By default, a ``JFrame`` is invisible, so ``setVisible(true)`` must be called to show it.
8. Inside ``main()``, a ``SwingDemo`` object is created, which causes the window and the label to be displayed. Notice that the ``SwingDemo`` constructor is invoked using these lines of code:
```Java
SwingUtilities.invokeLater(new Runnable() {
	public void run() {
		new SwingDemo();
	}
});
```
- This sequence causes a ``SwingDemo`` object to be created on the event dispatching thread
rather than on the main thread of the application.
- Why:
	- In general, Swing programs are event-driven.
	- An event is passed to the application by calling an event handler defined by the application.
	- However, the handler is executed on the event dispatching thread provided by Swing and not on the main thread of the application. Thus, although event handlers are defined by your program, they are called on a thread that was not created by your program.
	- To avoid problems (including the potential for [[deadlock]]), all Swing GUI components must be created and updated from the event dispatching thread, not the main thread of the application.
	- However, ``main()`` is executed on the main thread. Thus, ``main()`` cannot directly instantiate a ``SwingDemo`` object. Instead, it must create a ``Runnable`` object that executes on the event dispatching thread and have this object create the GUI.
	- To enable the GUI code to be created on the event dispatching thread, you must use one of two methods that are defined by the ``SwingUtilities`` class. These methods are:
		- ``invokeLater()`` -- ``static void invokeLater(Runnable obj)``
		- ``invokeAndWait()`` -- ``static void invokeAndWait(Runnable obj) throws InterruptedException, InvocationTargetException``
	- ``obj`` is a ``Runnable`` object that will have its ``run()`` method called by the event dispatching thread.
	- The difference between the two methods is that ``invokeLater()`` returns immediately, but ``invokeAndWait()`` waits until ``obj.run()`` returns.

## Event Handling
So far we have looked at examples that shows the basic form of a Swing program, but we have not yet touched on the topic of event handling. Since the example's above use ``JPanel`` which does not take input from users, it does not generate events, so event handling was not needed.
If we were to use any of the other Swing components that responds to user input and the events generated by those interactions, we need to handle them.
- Event can be generated in ways that is not directly related to user input. Such as a timer going off and starting an event etc.
Event handing is a large part of any Swing-based application, and the mechanism for handling those events in Swing, are the same used in AWT. This approach is called *delegation event model*.

In many cases, Swing uses the same events as does the AWT, and these events are packaged
in ``java.awt.event``. Events specific to Swing are stored in ``javax.swing.event``.
The following program handles the event generated by a Swing push button:
```Java
// Handle an event in a Swing program.
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class EventDemo {
	JLabel jlab;
	EventDemo() {
		// Create a new JFrame container.
		JFrame jfrm = new JFrame("An Event Example");
		// Specify FlowLayout for the layout manager.
		jfrm.setLayout(new FlowLayout());
		// Give the frame an initial size.
		jfrm.setSize(220, 90);
		// Terminate the program when the user closes the application.
		jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
		// Make two buttons.
		JButton jbtnAlpha = new JButton("Alpha");
		JButton jbtnBeta = new JButton("Beta");
		
		// Add action listener for Alpha.
		jbtnAlpha.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent ae) {
				jlab.setText("Alpha was pressed.");
			}
		});
		
		// Add action listener for Beta.
		jbtnBeta.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent ae) {
				jlab.setText("Beta was pressed.");
			}
		});
		
		// Add the buttons to the content pane.
		jfrm.add(jbtnAlpha);
		jfrm.add(jbtnBeta);
		
		// Create a text-based label.
		jlab = new JLabel("Press a button.");
		
		// Add the label to the content pane.
		jfrm.add(jlab);
		// Display the frame.
		jfrm.setVisible(true);
	}
	
	public static void main(String[] args) {
		// Create the frame on the event dispatching thread.
		SwingUtilities.invokeLater(new Runnable() {
			public void run() {
				new EventDemo();
			}
		});
	}
}
```
- notice that the program now imports both the ``java.awt`` and ``java.awt.event`` packages.

## Painting in Swing






