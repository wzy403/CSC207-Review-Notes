### Week 8 Study Notes

---

## Design Patterns

### Dependency Injection (DI)
**Problem:**
DI solves the problem of managing multiple implementations. It allows for the extension of code without modification, adhering to the Open/Closed Principle (OCP). It also helps in decoupling the creation of objects from their usage, following the Dependency Inversion Principle (DIP).

**Implementation:**
You can implement DI using constructor injection, setter injection, or interface injection. By injecting dependencies, the consumer of the dependency does not need to know the exact class being used.

**Example:**
```java
public interface Service {
    void execute();
}

public class ServiceImpl implements Service {
    @Override
    public void execute() {
        System.out.println("Service executed.");
    }
}

public class Client {
    private Service service;

    // Constructor Injection
    public Client(Service service) {
        this.service = service;
    }

    public void doWork() {
        service.execute();
    }
}

// Usage
Service service = new ServiceImpl();
Client client = new Client(service);
client.doWork();
```

**SOLID Principles:**
- **OCP:** Allows for adding new implementations without changing existing code.
- **DIP:** Clients depend on abstractions rather than concrete implementations.

### Simple Factory
**Problem:**
The Simple Factory pattern centralizes object creation logic. However, it can lead to a violation of the Open/Closed Principle (OCP) if the factory class contains multiple `if` statements to determine which object to create.

**Implementation:**
Move the creation logic to a factory class.

**Example:**
```java
public class SimpleFactory {
    public static Product createProduct(String type) {
        if (type.equals("A")) {
            return new ProductA();
        } else if (type.equals("B")) {
            return new ProductB();
        }
        return null;
    }
}

// Usage
Product product = SimpleFactory.createProduct("A");
```

**SOLID Principles:**
- **Helps with SRP** by centralizing creation logic.
- **Violates OCP** if new types need to be added.

### Facade
**Problem:**
The Facade pattern hides the complexities of a system by providing a simplified interface to the client. It helps in decoupling and makes the system easier to use.

**Implementation:**
Create a Facade class that wraps complex subsystems and provides simple methods to the client.

**Example:**
```java
public class ComplexSystem {
    public void operation1() {
        // complex operation
    }

    public void operation2() {
        // another complex operation
    }
}

public class Facade {
    private ComplexSystem complexSystem = new ComplexSystem();

    public void simpleOperation() {
        complexSystem.operation1();
        complexSystem.operation2();
    }
}

// Usage
Facade facade = new Facade();
facade.simpleOperation();
```

**SOLID Principles:**
- **SRP:** Simplifies the interface for the client.
- **OCP:** New functionalities can be added without changing the client code.

### Builder
**Problem:**
The Builder pattern helps in constructing complex objects step by step. It is useful when an object requires many attributes and avoids the need for a large constructor with many parameters.

**Implementation:**
Create a builder class that constructs the object step by step.

**Example:**
```java
public class Product {
    private String part1;
    private String part2;

    public static class Builder {
        private String part1;
        private String part2;

        public Builder setPart1(String part1) {
            this.part1 = part1;
            return this;
        }

        public Builder setPart2(String part2) {
            this.part2 = part2;
            return this;
        }

        public Product build() {
            Product product = new Product();
            product.part1 = this.part1;
            product.part2 = this.part2;
            return product;
        }
    }
}

// Usage
Product product = new Product.Builder()
                        .setPart1("Part 1")
                        .setPart2("Part 2")
                        .build();
```

**SOLID Principles:**
- **SRP:** Each builder method focuses on constructing a part of the object.
- **OCP:** New parts can be added by extending the builder.

### Adapter
**Problem:**
The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces.

**Implementation:**
Create an adapter class that implements the target interface and translates calls to the adaptee.

**Example:**
```java
public interface Target {
    void request();
}

public class Adaptee {
    public void specificRequest() {
        System.out.println("Adaptee's specific request.");
    }
}

public class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        adaptee.specificRequest();
    }
}

// Usage
Adaptee adaptee = new Adaptee();
Target target = new Adapter(adaptee);
target.request();
```

**SOLID Principles:**
- **OCP:** New adapters can be created without changing existing code.
- **SRP:** Adapter handles the translation between interfaces.

## Java Packaging

### What is a Package?
**Explanation:**
A package in Java is a namespace that organizes classes and interfaces. It helps in avoiding name conflicts and improves code modularity.

**Example:**
```java
package com.example;

public class MyClass {
    // class code
}
```

### Packaging Strategies
1. **Packaging by Component:**
   - Organize code based on components or modules.
   - **Example:** 
     ```plaintext
     com.example.app.user
     com.example.app.order
     ```

2. **Packaging by Layer:**
   - Organize code based on architectural layers.
   - **Example:**
     ```plaintext
     com.example.app.presentation
     com.example.app.service
     com.example.app.repository
     ```

3. **Packaging by Feature:**
   - Organize code based on features.
   - **Example:**
     ```plaintext
     com.example.app.usermanagement
     com.example.app.orderprocessing
     com.example.app.payment
     ```

### Benefits of Using Packages
Organizing files into different packages instead of placing them all in the `src` folder has several benefits:
- **Improves Readability:** Makes the code more organized and easier to navigate.
- **Enhances Maintainability:** Facilitates finding and modifying code related to specific functionalities.
- **Avoids Naming Conflicts:** Reduces the likelihood of class name conflicts.