[[[010 CS1331 MOC]]

The final is **cumulative**. Along with the recitation notes provided here, you are expected to know everything from the following documents:
- [[CS1331 Exam 1 Recitation Notes]]
- [[CS1331 Exam 2 Recitation Notes]]
- [[CS1331 Exam 3 Recitation Notes]]

*IMPORTANT* You are EXPECTED to know how to compile with modules.

*IMPORTANT* You **WILL** need to know the difference between radio buttons and check boxes

# Recitation 12 - JavaFX
> [!note] Exam preparation
> Although I am not entirely sure what will be tested for the final regarding JavaFX, I do know (from a comment Landry made) that being able to correctly include modules in your `javac` and `java` commands will be required knowledge.

## JavaFX Installation
For installing, follow the tutorial on Canvas:
- Canvas -> Modules -> JavaFX Tutorials and Links -> JavaFX_Guide.pdf

Follow along with the JavaFX installation Guide
1. Download JavaFX SDK your operating system
2. Download HelloWorldJavaFx.java
3. Make sure it compiles and runs


#### IMPORTANT: Commands
**REMEMBER**: After compiling, you STILL have to use the modules when running `java`!!

```sh
javac --module-path path_to_lib_folder --add-modules javafx.controls FileName.java
java --module-path path_to_lib_folder --add-modules javafx.controls FileName.java
```

## JavaFX Basics
JavaFX main classes extend **Application** (abstract class)

- You **MUST** override the `start(Stage primaryStage)` method
	- Setups up objects in GUI
	- Takes in stage object (already made for you)

- `public static void main(String[] args)` - calls `launch(args)` to launch the JavaFX GUI
	- Optional, as the abstract method already internally does this

Javafx Package:
- `import javafx.application.Application;`

#### Note on JavaFX and Javadocs
The library is *HUGE*, and you need to reference the [JavaFX documentation](https://openjfx.io/javadoc/11/)to learn about the various methods and classes it provides.
 
> [!caution] Compilation
> The command for compiling a java file **WILL** be on the final.

Basic Class:
```java
import javafx.application.Application;
import javafx.stage.Stage;

public class FXDemo extends Application {
	public void start(Stage primaryStage) {
		primaryStage.show();
	}

	public static void main(String[] args) {
		launch(args);
	}
}
```

#### Stages and Scenes
**Stage** - window holding all other components
- Primary stage is provided in the `start` method

**Scene** - contains objects for the GUI in a scene graph (tree)
- Placed in stage
- Contains a root `Node`

**Pane** - area within scene to put GUI objects in

**Node** - ALL visual components, e.g. shape, ImageView, UI controls, etc
- Each has its own properties (e.g. style, rotate, fill, etc.)

#### Color
Self-explanatory. Multiple ways of declaring:

> [!caution] Be careful about the range of the two colors!
> Although it won't throw an exception, the Color constructor takes in values in the range of `[0, 1]`, while `Color.rgb` takes in values in the range `[0, 255]`

Constructors:
`Color(double red, double green, double blue, double opacity)`
- values in range `[0, 1]`

Static methods:
`Color.rgb(int red, int green, int blue, double opacity)`
- int values in range `[0, 255]`, but opacity in range `[0, 1]`

Enum presets:
e.g. `Color.BLUE`, `Color.GREEN`, `Color.DEEPSKYBLUE`

#### Class Hierarchy
I have no idea whether you're supposed to memorize this or not, but most of it is fairly logical to think about. Everything either explicitly or implicitly extends `Node`, and it makes sense for things like a `TextField` to be part of a `TextInputControl`.
![[Pasted image 20231201220608.png]]
#### Image
**Image** - abstract representation of an image from a path or URL
- **MUST** be put into an `ImageView`

```java
Image image = new Image("images/cs1331logo.png");
ImageView imageView = new ImageView(image);
```

#### Label/Button
**Label** - non-editable text label with font, alignment, text

**Button** - labeled button, has some sort of action when clicked (see [[EventHandler]])

#### Shape
**Shape** - abstract subclass of node, and base class for all `Shape` objects
- has fill (background color), stroke (border), strokewidth

Examples: `Circle`, `Rectangle`, `Line`, `Arc`

```java
Rectangle rect = new Rectangle(400, 300, 20, 30);
rect.setFill(Color.GREEN);
```

## Topic Trivia
![[Pasted image 20231201220617.png]]
## JavaFX Layouts
**Layout** - "GUI Manager" allowing you to control where components go
![[Pasted image 20231201220626.png]]
Different Layout types:
![[Pasted image 20231201220637.png]]

> [!info] Difference between TilePane and GridPane
> A `TilePane` will **always** have children nodes of *uniform (equal) size*, whereas a `GridPane` is only aligned to a Grid (e.g. you can still have a rectangle and square in one Grid).
> 
> Look at the diagram above to see the difference!

`

# Recitation 13 - JavaFX Events
## Event-Driven Programming
We represent events through the **Event** object.

Events are *fired (outputted)* from some sort of **source object** (e.g. a button)
- holds data about what (e.g. if you clicked on a button, was it while holding shift?)

Events are *handled* through an **EventHandler** -> "what do I do when this happens"
- MUST be instance of `EventHandler<T extends Event>`
- Typically registered through `source.setOnAction(EventHandler)`

Example:
```java
Button b = new Button("Enter");

// Handler class implementing EventHandler<ActionEvent>
BtnHandlerClass handler = new BtnHandlerClass();

// When an action (Event) occurs, button will call the handler we assign
b.setOnAction(handler);
```

![[Pasted image 20231201220705.png]]

## (Nested) Inner Classes
**[[Nested class]]** - class inside of a class, belonging to *enclosing* (we use enclosing to not confuse it with extend/implement by saying parent) class
- *has access* to enclosing fields and methods
- acts like a normal class
- typically made *private*

Example:
```java

class SomeClass {
	Button button; // Imagine this was instantiated somewhere
	
	class CircleButtonHandler implements EventHandler<ActionEvent> {
		// ActionEvent REQUIRES handle to be implemented, so we override it here:
		public void handle(ActionEvent actionEvent) {
			circle.setRadius(circle.getRadius() * 2);
		}
	}

	// Start method for JavaFX
	public void start(Stage primaryStage) {
		// Assign action of button to our handler inner class
		button.setOnAction(new CircleButtonHandler());
	}
}

```

## Anonymous Inner Classes
Very similar to a **Nested class**, but *without* a class name. 
- All methods it must override are written when you instantiate it (rather than in a class)

Same example as the **Nested class**, but *no class name*.
- Can look verbose and hinder readability--used for one-time event handles

Example (Same as inner class example):
```java
public void start(Stage primaryStage) {
	// Because we are making an anonymous inner class of ActionEvent,
	// we must ALSO write what the handle method will do (exact same as if it was a standalone class)
	button.setOnAction(new EventHandler<ActionEvent>() {
		@Override
		public void handle(ActionEvent actionEvent) {
			circle.setRadius(circle.getRadius() * 2);
		}
	})
}
```

#### Why use anonymous inner classes?
For one-off events, there's no point in creating a giant class for each.

Imagine you had 1000 buttons each with a different function--would you really want to create 1000 classes? No! And as you'll see in [[Lambda Expressions]], they can be simplified even more if they're [[Functional Interface]]s.

## Lambda Expressions
**[[Lambda Expressions]]** = A less verbose way of doing [[Anonymous Inner Class]]es

> [!info] USE CASE
> You can **only** use lambda expressions for a [[Functional Interface]]!!!

3 Components:
- Argument list
- Arrow token
- Body

![[Pasted image 20231201220721.png]]
Example with the button handler:
```java
@Override
public void start(Stage primaryStage) {
	btnNew.setOnAction((ActionEvent e) -> {
		circle.setRadius(circle.getRadius() * 2);
	}
}
```

If it's one line, it can be reduced even further:
```java
@Override
public void start(Stage primaryStage) {
	// (ActionEvent e) could be changed to just e, as there is only one parameter
	// The {} brackets could be removed as the body only has one line
	btnNew.setOnAction(e -> circle.setRadius(circle.getRadius) * 2);
}
```

#### Assigning to variables
```java
EventHandler<ActionEvent> someEventHandler = e -> circle.setRadius(circle.getRadius) * 2;

button.setAction(someEventHandler);
```


## Topic Trivia
![[Pasted image 20231201220732.png]]

## Event Example: JavaFX MouseEvents
- `MouseEvent` fired when a mouse button is pressed, released, clicked, moved, or dragged

There are several different handlers for a `Node`, including ones for mouse events:
```java
button.setOnMouseReleased(...);
```

![[Pasted image 20231126170712.png]]

## Event Example: JavaFX KeyEvent
- `KeyEvent` fired when a keystroke action occurs inside of a component

![[Pasted image 20231126170749.png]]

# Recitation 14 
- Extremely short recitation period
## GUI Controls
**label** - non-editgable text control, CAN contain an image
**button** - actionable element, potentially containing text and graphics
- uses `setOnAction(EventHandler<ActionEvent> handler`

**textfield** - text input components allowing **one** line of text (this does **NOT** go multiline)

**checkbox** - toggleable selection control; fires **ActionEvent** when toggled
- can be checked with `isSelected()`

**RadioButton** - selection item where only one item can be selected from a serie sof items
- you have to create a **ToggleGroup** in order to manage several RadioButtons together, where you then use `bt.setToggleGroup(group)` to set the toggle group accordingly
- Pressing and releasing a `RadioButton` will also fire an `ActionEvent`

**ComboBox** - think of multiselect dropdown box; if the number exceeds a certain limit or height it will be automatically converted into a scrollable dropdown list. 

When instantiating a ComboBox:
```java
ComboBox<String> combo = new ComboBox<>();
```

to add multiple elements at the same time to the combo box:
```java
combo.getItems().addAll("1331", )
```](<The final is **cumulative**. Along with the recitation notes provided here, you are expected to know everything from the following documents:
- [[CS1331 Exam 1 Recitation Notes]]
- [[CS1331 Exam 2 Recitation Notes]]
- [[CS1331 Exam 3 Recitation Notes]]

*IMPORTANT* You are EXPECTED to know how to compile with modules.

*IMPORTANT* You **WILL** need to know the difference between radio buttons and check boxes

# Recitation 12 - JavaFX
%3E [!note] Exam preparation
> Although I am not entirely sure what will be tested for the final regarding JavaFX, I do know (from a comment Landry made) that being able to correctly include modules in your `javac` and `java` commands will be required knowledge.

## JavaFX Installation
For installing, follow the tutorial on Canvas:
- Canvas -> Modules -> JavaFX Tutorials and Links -> JavaFX_Guide.pdf

Follow along with the JavaFX installation Guide
1. Download JavaFX SDK your operating system
2. Download HelloWorldJavaFx.java
3. Make sure it compiles and runs


#### IMPORTANT: Commands
**REMEMBER**: After compiling, you STILL have to use the modules when running `java`!!

```sh
javac --module-path path_to_lib_folder --add-modules javafx.controls FileName.java
java --module-path path_to_lib_folder --add-modules javafx.controls FileName.java
```

## JavaFX Basics
JavaFX main classes extend **Application** (abstract class)

- You **MUST** override the `start(Stage primaryStage)` method
	- Setups up objects in GUI
	- Takes in stage object (already made for you)

- `public static void main(String[] args)` - calls `launch(args)` to launch the JavaFX GUI
	- Optional, as the abstract method already internally does this

Javafx Package:
- `import javafx.application.Application;`

#### Note on JavaFX and Javadocs
The library is *HUGE*, and you need to reference the [JavaFX documentation](https://openjfx.io/javadoc/11/)to learn about the various methods and classes it provides.
 
> [!caution] Compilation
> The command for compiling a java file **WILL** be on the final.

Basic Class:
```java
import javafx.application.Application;
import javafx.stage.Stage;

public class FXDemo extends Application {
	public void start(Stage primaryStage) {
		primaryStage.show();
	}

	public static void main(String[] args) {
		launch(args);
	}
}
```

#### Stages and Scenes
**Stage** - window holding all other components
- Primary stage is provided in the `start` method

**Scene** - contains objects for the GUI in a scene graph (tree)
- Placed in stage
- Contains a root `Node`

**Pane** - area within scene to put GUI objects in

**Node** - ALL visual components, e.g. shape, ImageView, UI controls, etc
- Each has its own properties (e.g. style, rotate, fill, etc.)

#### Color
Self-explanatory. Multiple ways of declaring:

> [!caution] Be careful about the range of the two colors!
> Although it won't throw an exception, the Color constructor takes in values in the range of `[0, 1]`, while `Color.rgb` takes in values in the range `[0, 255]`

Constructors:
`Color(double red, double green, double blue, double opacity)`
- values in range `[0, 1]`

Static methods:
`Color.rgb(int red, int green, int blue, double opacity)`
- int values in range `[0, 255]`, but opacity in range `[0, 1]`

Enum presets:
e.g. `Color.BLUE`, `Color.GREEN`, `Color.DEEPSKYBLUE`

#### Class Hierarchy
I have no idea whether you're supposed to memorize this or not, but most of it is fairly logical to think about. Everything either explicitly or implicitly extends `Node`, and it makes sense for things like a `TextField` to be part of a `TextInputControl`.
![[Pasted image 20231126172202.png]]

#### Image
**Image** - abstract representation of an image from a path or URL
- **MUST** be put into an `ImageView`

```java
Image image = new Image("images/cs1331logo.png");
ImageView imageView = new ImageView(image);
```

#### Label/Button
**Label** - non-editable text label with font, alignment, text

**Button** - labeled button, has some sort of action when clicked (see [[EventHandler]])

#### Shape
**Shape** - abstract subclass of node, and base class for all `Shape` objects
- has fill (background color), stroke (border), strokewidth

Examples: `Circle`, `Rectangle`, `Line`, `Arc`

```java
Rectangle rect = new Rectangle(400, 300, 20, 30);
rect.setFill(Color.GREEN);
```

## Topic Trivia
![[Pasted image 20231126172611.png]]

## JavaFX Layouts
**Layout** - "GUI Manager" allowing you to control where components go
![[Pasted image 20231126172655.png]]

Different Layout types:
![[Pasted image 20231126172707.png]]

> [!info] Difference between TilePane and GridPane
> A `TilePane` will **always** have children nodes of *uniform (equal) size*, whereas a `GridPane` is only aligned to a Grid (e.g. you can still have a rectangle and square in one Grid).
> 
> Look at the diagram above to see the difference!

`

# Recitation 13 - JavaFX Events
## Event-Driven Programming
We represent events through the **Event** object.

Events are *fired (outputted)* from some sort of **source object** (e.g. a button)
- holds data about what (e.g. if you clicked on a button, was it while holding shift?)

Events are *handled* through an **EventHandler** -> "what do I do when this happens"
- MUST be instance of `EventHandler%3CT extends Event>`
- Typically registered through `source.setOnAction(EventHandler)`

Example:
```java
Button b = new Button("Enter");

// Handler class implementing EventHandler<ActionEvent>
BtnHandlerClass handler = new BtnHandlerClass();

// When an action (Event) occurs, button will call the handler we assign
b.setOnAction(handler);
```

![[Pasted image 20231126164431.png]]

## (Nested) Inner Classes
**[[Nested class]]** - class inside of a class, belonging to *enclosing* (we use enclosing to not confuse it with extend/implement by saying parent) class
- *has access* to enclosing fields and methods
- acts like a normal class
- typically made *private*

Example:
```java

class SomeClass {
	Button button; // Imagine this was instantiated somewhere
	
	class CircleButtonHandler implements EventHandler<ActionEvent> {
		// ActionEvent REQUIRES handle to be implemented, so we override it here:
		public void handle(ActionEvent actionEvent) {
			circle.setRadius(circle.getRadius() * 2);
		}
	}

	// Start method for JavaFX
	public void start(Stage primaryStage) {
		// Assign action of button to our handler inner class
		button.setOnAction(new CircleButtonHandler());
	}
}

```

## Anonymous Inner Classes
Very similar to a **Nested class**, but *without* a class name. 
- All methods it must override are written when you instantiate it (rather than in a class)

Same example as the **Nested class**, but *no class name*.
- Can look verbose and hinder readability--used for one-time event handles

Example (Same as inner class example):
```java
public void start(Stage primaryStage) {
	// Because we are making an anonymous inner class of ActionEvent,
	// we must ALSO write what the handle method will do (exact same as if it was a standalone class)
	button.setOnAction(new EventHandler<ActionEvent>() {
		@Override
		public void handle(ActionEvent actionEvent) {
			circle.setRadius(circle.getRadius() * 2);
		}
	})
}
```

#### Why use anonymous inner classes?
For one-off events, there's no point in creating a giant class for each.

Imagine you had 1000 buttons each with a different function--would you really want to create 1000 classes? No! And as you'll see in [[Lambda Expressions]], they can be simplified even more if they're [[Functional Interface]]s.

## Lambda Expressions
**[[Lambda Expressions]]** = A less verbose way of doing [[Anonymous Inner Class]]es

> [!info] USE CASE
> You can **only** use lambda expressions for a [[Functional Interface]]!!!

3 Components:
- Argument list
- Arrow token
- Body

![[Pasted image 20231126170134.png]]

Example with the button handler:
```java
@Override
public void start(Stage primaryStage) {
	btnNew.setOnAction((ActionEvent e) -> {
		circle.setRadius(circle.getRadius() * 2);
	}
}
```

If it's one line, it can be reduced even further:
```java
@Override
public void start(Stage primaryStage) {
	// (ActionEvent e) could be changed to just e, as there is only one parameter
	// The {} brackets could be removed as the body only has one line
	btnNew.setOnAction(e -> circle.setRadius(circle.getRadius) * 2);
}
```

#### Assigning to variables
```java
EventHandler<ActionEvent> someEventHandler = e -> circle.setRadius(circle.getRadius) * 2;

button.setAction(someEventHandler);
```


## Topic Trivia
![[Pasted image 20231126170536.png]]


## Event Example: JavaFX MouseEvents
- `MouseEvent` fired when a mouse button is pressed, released, clicked, moved, or dragged

There are several different handlers for a `Node`, including ones for mouse events:
```java
button.setOnMouseReleased(...);
```

![[Pasted image 20231126170712.png]]

## Event Example: JavaFX KeyEvent
- `KeyEvent` fired when a keystroke action occurs inside of a component

![[Pasted image 20231126170749.png]]

# Recitation 14 
- Extremely short recitation period
## GUI Controls
**label** - non-editgable text control, CAN contain an image
**button** - actionable element, potentially containing text and graphics
- uses `setOnAction(EventHandler<ActionEvent> handler`

**textfield** - text input components allowing **one** line of text (this does **NOT** go multiline)

**checkbox** - toggleable selection control; fires **ActionEvent** when toggled
- can be checked with `isSelected()`

**RadioButton** - selection item where only one item can be selected from a serie sof items
- you have to create a **ToggleGroup** in order to manage several RadioButtons together, where you then use `bt.setToggleGroup(group)` to set the toggle group accordingly
- Pressing and releasing a `RadioButton` will also fire an `ActionEvent`

**ComboBox** - think of multiselect dropdown box; if the number exceeds a certain limit or height it will be automatically converted into a scrollable dropdown list. 

When instantiating a ComboBox:
```java
ComboBox<String> combo = new ComboBox<>();
```

to add multiple elements at the same time to the combo box:
```java
combo.getItems().addAll("1331", )
```>)