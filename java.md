# Java Notes

### [Introduction to Java Programming [Comprehensive Version]](http://www.amazon.com/Intro-Java-Programming-Comprehensive-Version/dp/0133761312)

#### Chapter 1

* .java -> compiles to .class that's then executed by JVM
* Float 32-bit IEEE 754, double 64-bit IEEE 754
* Source file with extension .java should have same exact name as the public class name
* When executing a Java program, the JVM first loads the bytecode of the class to mem-ory using a program called the *class loader*. If your program uses other classes, the class loader dynamically loads them just before they are needed. After a class is loaded, the JVM uses a program called the *bytecode verifier* to check the validity of the bytecode and to ensure that the bytecode does not violate Java’s security restrictions
* `/**` denotes a javadoc comment

#### Chapter 2

* Naming conventions: ClassName, methodName(), variableName, CONSTANT_NAME
* Floating point literals: By default, are considered double values (e.g. 5.0). Append letter `f` of `F` to make float.
* Java expressions are evaluated in the same way as arithmetic expressions
* Avoid round off errors by using integers whenever a precise result is required
* Avoid unintended integer division by making sure one of the operands is a floating point number

### Chapter 3

* Avoid equality test of two floating point values

### Chapter 6

* The arguments are passed by value to parameters when invoking a method

### Chapter 9

* Final data members must be initialized
* All objects inherit from Object class
  * `public String toSring()`
  * `public boolean equals()`
  * `public Class<?> getClass()` - returns reference of class object
  * `public int hashcode()`
* Only one public class / file, compiles to multiple .class files
* Data field default values:
  * Reference: null (literal for reference types, related to true/false in that they are boolean literals)
  * Numeric: 0
  * boolean: false
  * char: `\u0000`
* package-private is the default visibility modifier
* Although Java passes by value, passing a reference variable actually passes a reference of the object (as that's what the variable contains, duuh)
* Immutable class contains all private data fields, and no public setters
* `this` refers to the object itself. It's often used to reference hidden data fields (e.g. `this.i = i`), and to invoke another constructor w/in the class

### Chapter 10

* BigInteger and BigDecimal classes can be used to represent integers/decimals of any size/precision
  * Both are immutable

* *interned string*: Because strings are immutable and are ubiquitous in programming, the JVM uses a unique instance for string literals with the same character sequence in order to improve efficiency and save memory

  ```java
  String s1 = "Welcome to Java";
  String s2 = new String("Welcome to Java");
  String s3 = "Welcome to Java";

  s1 == s2 is false
  s1 == s3 is true
  ```

* The StringBuilder and StringBuffer classes are similar to the String class except that the String class is immutable

### Chapter 11

* Java enforces *single inheritance*, a Java class can only inherit directly from one superclass
* Constructing an instance of a class invokes the constructors of all the superclasses along the inheritance chain
  * Subclass constructor invokes its parent class constructor before performing its own tasks, this follows up and up superclasses (Constructor Chaining)
* Use `super.methodName()` to call superclasses' methods
* Overriding: method must be defined in the subclass using the same sig- nature and the same return type as in its superclass
* Overloading: to define multiple methods with the same name but different signatures
* Every class in Java is descended from the java.lang.Object class
  * `public String toString()`: returns, by default, ClassName@memAddrInHex
  * `public boolean equals(Object o)`
    * override the default `return (this == o)` to check whether the two distinct objects have the same content
* *Polymorphism*: variable of a supertype can refer to a subtype object
* *Dynamic Binding*: A method can be implemented in several classes along the inheritance chain. The JVM decides which method is invoked at runtime
  * e.g. `Object o = new GeometricObject()`
    * declared type: Object
    * actual type: GeometricObject
  * Dynamic binding works by searching for a method p from the most specific class (actual) to the most general (Object)
* `Object o = new Student()` -> implicit casting
* `Student j = (Student) new Object` -> explicit casting
  * Good practice to use `instanceof` operator before explicit casting
* Protected member of a class can be accessed from a subclass
  * subclass can override a protected method defined in its superclass and change its visibility to public. However, a subclass cannot weaken the accessibility of a method defined in the superclass
* Neither a final class nor a final method can be extended. A final data field is a constant
* The modifiers public, protected, private, static, abstract, and final are used on classes and class members (data and methods), except that the final modifier can also be used on local variables in a method. A final local variable is a constant inside a method
* A static method cannot be overridden. If a static method defined in the superclass is redefined in a subclass, the method defined in the superclass is hidden. The hidden static methods can be invoked using the syntax SuperClassName.staticMethodName

### Chapter 12

* Best practice to make custom exceptions checked
* The order in which exceptions are specified in a catch block is important. A compile error will result if you specify an exception object of a class after an exception object of the superclass of that class
* Try-with-resources automatically closes files
  ```java
    try (declare and create resources) { Use the resource to process the file;
  }
  ```
* *token-reading* methods (e.g. nextByte(), nextInt(), etc) work by first skipping any delimiters then reads a token ending at a delimiter. The token is then converted into a value of the corresponding method call (i.e. int for nextInt())

### Chapter 13

* A superclass defines common behavior for related subclasses. An interface can be used to define common behavior for classes (including unrelated classes)

##### Abstract Classes

* An abstract class cannot be used to create objects. An abstract class can contain abstract methods, which are implemented in concrete subclasses
  * e.g. `public abstract class ClassName` and `public abstract double getArea()`
* The constructor in the abstract class is defined as protected, because it is used and invoked only by subclasses
* A class that contains abstract methods must be abstract. However, it is possible to define an abstract class that doesn’t contain any abstract methods. In this case, you cannot create instances of the class using the new operator. This class is used as a base class for defining subclasses
* A subclass can override a method from its superclass to define it as abstract
* You cannot create an instance from an abstract class using the new operator, but an abstract class can be used as a data type
  * e.g. `AbsClassName[] objects = new AbsClassName[10];`

##### Interfaces

```java
public interface Edible {
/** Describe how to eat */
public abstract String howToEat();
}
```

* Classes can implement interface with `implements` keyword
* Since all data fields are `public static final` and all methods are `public abstract` in an interface, Java allows these modifiers to be omitted
* Comparable interface

### Abstract vs. Interface

##### Abstract

* Class can only extend one abstract class
* Can have both abstract and concrete methods
* `abstract` keyword is mandatory to declare a method abstract

##### Interface

* Can extend any number of interfaces at a time
* Interface can only extend from an interface
* Can only have public abstract methods
* Can only have static final variables
* `abstract` keyword is optional to declare a method abstract


### Spring

* Spring wires the classes up with a XML file, so that all of the objects are instantiated and initialized by Spring and injected in the right places (Servlets, Web Frameworks, Business classes, DAOs, etc, etc, etc...)

* *Inversion of Control*: The application controls the framework, not vice-versa
