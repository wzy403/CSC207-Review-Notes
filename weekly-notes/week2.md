
# Week 2 Study Notes

---

## Encapsulation and Access Control

Encapsulation is a core principle in object-oriented programming that helps in data hiding and restricting unauthorized access or modifications to class variables. This is often achieved by making variables private and providing public getter and setter methods.

- **Getter Method:** A getter method allows access to private variables in a controlled manner. It helps in validation and ensures data integrity.
    ```java
    public class Example{
        private String name;

        public String getName() {
            return name;
        }
    }
    ```

- **Setter Method:** A setter method is used to modify private variables with validation to ensure that the data being assigned is correct.
    ```java
    public class Example{
        private String name;

        public void setName(String name) {
            this.name = name;
        }
    }
    ```

- **Benefits of Privacy:** Making variables and methods as private as possible prevents unauthorized access and accidental modifications, maintaining clear separation between internal representation and external interaction.
    - Example: If every developer can change a class's value, it might cause bugs during the program run.

- **Private Variables with Public Methods:** This approach provides better encapsulation as it allows controlled access and modification of variables, reducing potential bugs caused by unauthorized or incorrect modifications.

---

## Polymorphism and Inheritance

Polymorphism and inheritance are fundamental concepts that allow objects of different types to be treated as objects of a common superclass, providing flexibility and abstraction in programming.

- **Polymorphism:** is the ability of different class objects to respond uniquely to the same method call, achieved through method overriding and method overloading.
    ```java
    //Example for overriding
    public class Parent{
        public void overriding(){
            System.out.println("This is Parent");
        }
    }
    public class Child extends Parent {
        @Override
        public void overriding(){
            System.out.println("This is Child");
        }   
    }

    //Example for overloading
    public class OverloadExample{
        public void overloading(int a){
            ...
        }
        public void overloading(int a, int b){
            ...
        }
        public void overloading(String a){
            ...
        }
    }
    ```

- **Inheritance from Object Class:** Inheriting from the Object class enables polymorphism, allowing different types of objects to be treated as a common superclass.
    - Example: An array of type `Object` can hold different types of objects (e.g. Integer, String, Double).
    ```java
    public class UsageForObjectClass {
        public static void main(String[] args) {
            List<Object> test = new ArrayList<>();
            String a = "123";
            Integer b = 555;
            double c = 1145.14;
            test.add(a);
            test.add(b);
            test.add(c);

            for (Object obj : test) {
                System.out.println(obj.getClass().getName());
            }

            // Starting from Java 10, you can use the 'var' keyword
            // to automatically infer the variable's type
            for (var obj : test) {
                System.out.println(obj.getClass().getName());
            }
        }
    }
    ```

---

## Association, Aggregation, Composition

In object-oriented programming, the relationships between classes can be classified into three types: Association, Aggregation, and Composition. Each of these relationships defines a different level of dependency and lifespan between the objects.

- **Association:** a general relationship between two classes. Each class has its own lifecycle and there is no ownership, which means object can exist independently of each other.
  - This relationship can be **one-to-one**, one-to-many, many-to-one, or many-to-many.

- **Aggregation:** a specialized form of Association where all objects have their own lifecycle, but there is ownership.
  - It is a "has-a" relationship where the child can exist independently of the parent.

- **Composition:** a stronger form of Aggregation. It implies ownership and a strong lifecycle dependency between the parent and child. If the parent object is destroyed, all child objects will also be destroyed.
  - It represents a "part-of" relationship, where the child cannot exist without the parent.

---

## Abstract Classes and Interfaces

Abstract classes and interfaces define methods that must be implemented by subclasses or implementing classes, providing a way to enforce a certain structure.

- **Abstract Class:** An abstract class cannot be instantiated and may contain abstract methods without implementation.
    ```java
    public abstract class Animal {
        public abstract void makeSound();
    }
    ```

- **Interface:** A Java interface is a reference type containing abstract methods. It provides a way to enforce a contract for classes.
    ```java
    public interface Animal {
        void makeSound();
    }
    ```

- **Choosing Between Interface and Abstract Class:**
    - Use an interface for multiple inheritance, loose coupling, and flexibility in implementation.
    - Use an abstract class for providing common base functionality with default behavior or sharing code and state among related classes.

**Note:** In Java, an interface can contain not only abstract methods but also default methods, static methods, private methods, and constants. Here is an example to illustrate these features:
```java
public interface MyInterface {
    // Constant (implicitly public, static, and final)
    int MY_CONSTANT = 10;

    // Abstract method
    void absMethod();

    // Default method
    default int addNum(int a, int b) {
        return add(a, b);
    }

    // Private method (helper for default methods)
    private int add(int a, int b) {
        return a + b;
    }

    // Static method
    static String getGreeting() {
        return "Hello from MyInterface!";
    }

    // Final method (Note: In interfaces, methods cannot be explicitly declared final. 
    // Methods in interfaces are implicitly abstract unless they are default or static.)
    // Therefore, final methods cannot be defined in interfaces.
}

```

---

## Generics

Generics allow classes and methods to operate on objects of various types while providing compile-time type safety.

- **Generic Class:** Defined with type parameters, a generic class can work with any data type.
    ```java
    public class Box<T> {
        private T content;

        public void setContent(T content) {
            this.content = content;
        }

        public T getContent() {
            return content;
        }
    }
    ```

- **Bounded Type Parameters:** You can restrict the types that can be used as type parameters using `extends` and `super`.
  - **Upper Bounded** (`extends`): Restricts the type to a specific class or its subclasses.
    ```java
    public class NumberBox<T extends Number> {
        private T number;

        public T getNumber() {
            return number;
        }

        public void setNumber(T number) {
            this.number = number;
        }
    }
    ```
    *(Here we can assign `NumberBox` to `Integer`, `Double`, etc.)*

  - **Lower Bounded** (`super`): Restricts the type to a specific class or its superclasses.
    ```java
    public static void addNumbers(List<? super Integer> list) {
        for (Object obj : list) {
            System.out.println(obj);
        }
    }
    ```
    *(Here we can only input `Integer` or its superclasses, such as `Number`, to this method)*

---

## UML Diagrams and Relationships

UML diagrams visually represent relationships between elements/classes, aiding in the design and understanding of system architecture.

- **Arrows in UML:** Indicate relationships between elements/classes. Open arrowheads indicate inheritance, while solid arrowheads indicate composition. These arrows differ from memory model arrows, which represent references or pointers in memory.

---

## Software Development Concepts

Understanding user stories, use cases, and use case interactors is crucial for effective software development and requirement analysis.

- **User Story:** An informal, general explanation of a software feature from the end user's perspective. It helps define the steps or features a use case needs to include.
    - **Relation to Use Case:** A user story helps implement the steps or features a use case needs to include.
    - **Relation to Use Case Interactor:** Identifies necessary interactors for implementing the use case.
    - Example: If the user story is about checking item prices online, the use case might be "Search on Internet," and the interactor could be "PriceCheckInteractor."

---
