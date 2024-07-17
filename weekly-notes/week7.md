### Week 7 Study Notes

## Exceptions in Java

### Conceptual Difference
**What is the conceptual difference between a "checked" and "unchecked" Exception?**

- **Checked Exception:** These exceptions are checked at compile-time. The IDE will catch these and force you to handle them either using a try-catch block or by declaring them with `throws`.
- **Unchecked Exception:** These exceptions are not checked at compile-time but occur at runtime. The IDE does not enforce handling these exceptions. When they occur, the program will stop, and the problem must be fixed.

### Syntactical Difference
**What is the syntactical (syntax) difference between a "checked" and "unchecked" Exception?**

- **Checked Exceptions:**
  - Must be declared in the method signature with `throws`.
  - Must be handled (caught or declared to be thrown).

**Example:**
```java
public void readFile() throws IOException {
    // code that may throw IOException
}
```

- **Unchecked Exceptions:**
  - Do not need to be declared in the method signature.
  - Handling is optional.

**Example:**
```java
public void divide(int a, int b) {
    int result = a / b;  // May throw ArithmeticException
}
```

### Common Checked and Unchecked Exceptions
- **Checked Exceptions:** `IOException`, `SQLException`, `ClassNotFoundException`
- **Unchecked Exceptions:** `ArithmeticException`, `NullPointerException`, `ArrayIndexOutOfBoundsException`

### Why Leave RuntimeExceptions Unchecked?
**Explanation:**
RuntimeExceptions should never occur during normal program operation. When they do occur, it indicates a problem in the code that must be fixed. They represent abnormal conditions that should not happen and do not need to be explicitly handled.

## Exception Handling Best Practices

### Why Not Include Many Checked Exceptions?
Including too many checked exceptions in your code can make it harder to maintain, understand, and use. It can clutter the code and make it less readable.

### When to Catch Exceptions?
**Explanation:**
Catch exceptions at the highest level possible. Throw the exception at a lower level and catch it at a higher level to handle it appropriately.

**Example:**
```java
public void processFile(String path) {
    try {
        readFile(path);
    } catch (IOException e) {
        System.out.println("Error reading file: " + e.getMessage());
    }
}

public void readFile(String path) throws IOException {
    // code that may throw IOException
}
```

### Purpose of a "finally" Block
**Explanation:**
The code in the `finally` block will execute regardless of whether an exception is caught or not. It is typically used for cleanup activities.

**Example:**
```java
try {
    int result = 10 / 2;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("This will always execute");
}
```

## Design Patterns

### Iterator Pattern
**Problem:**
Accessing elements of a collection sequentially without exposing its internal structure.

**Implementation:**
Define an iterator interface with methods like `next()` and `hasNext()`. Implement this interface for the collection.

**Example:**
```java
public interface Iterator {
    boolean hasNext();
    Object next();
}

public class NameRepository implements Iterable {
    private String[] names = {"John", "Jane", "Jack"};

    @Override
    public Iterator iterator() {
        return new NameIterator();
    }

    private class NameIterator implements Iterator {
        int index;

        @Override
        public boolean hasNext() {
            return index < names.length;
        }

        @Override
        public Object next() {
            if (this.hasNext()) {
                return names[index++];
            }
            return null;
        }
    }
}
```

**SOLID Principles:**
- **SRP:** Separates traversal logic from collection logic.
- **OCP:** Add new iterators without modifying existing code.
- **ISP:** Iterator interface is specific and concise.

### Observer Pattern
**Problem:**
One-to-many dependency, where changes in one object (subject) are notified to all dependents (observers).

**Implementation:**
Define Subject and Observer interfaces. Implement these interfaces in concrete classes and manage the observer list in the subject.

**Example:**
```java
public interface Observer {
    void update();
}

public interface Subject {
    void registerObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}

public class WeatherStation implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private int temperature;

    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }

    @Override
    public void removeObserver(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyObservers() {
        for (Observer o : observers) {
            o.update();
        }
    }

    public void setTemperature(int temperature) {
        this.temperature = temperature;
        notifyObservers();
    }
}

public class Display implements Observer {
    @Override
    public void update() {
        // Update display based on the new state
    }
}
```

**SOLID Principles:**
- **SRP:** Separates subject and observer responsibilities.
- **OCP:** Add new observers without modifying the subject.
- **DIP:** Both subject and observers depend on abstractions.

### Strategy Pattern
**Problem:**
Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

**Implementation:**
Define a strategy interface and implement multiple concrete strategies. Use a context class to switch strategies dynamically.

**Example:**
```java
public interface Strategy {
    int doOperation(int num1, int num2);
}

public class AdditionStrategy implements Strategy {
    @Override
    public int doOperation(int num1, int num2) {
        return num1 + num2;
    }
}

public class SubtractionStrategy implements Strategy {
    @Override
    public int doOperation(int num1, int num2) {
        return num1 - num2;
    }
}

public class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public int executeStrategy(int num1, int num2) {
        return strategy.doOperation(num1, num2);
    }
}
```

**SOLID Principles:**
- **SRP:** Each strategy has a single responsibility.
- **OCP:** Add new strategies without modifying the context.
- **DIP:** Context depends on strategy abstractions, not implementations.

### Dependency Injection
**Problem:**
Decouple the creation of objects from their usage to promote loose coupling.

**Implementation:**
Use constructor, setter, or interface injection to provide dependencies.

**Example:**
```java
public interface MessageService {
    void sendMessage(String message);
}

public class EmailService implements MessageService {
    @Override
    public void sendMessage(String message) {
        System.out.println("Email message sent: " + message);
    }
}

public class UserNotification {
    private MessageService messageService;

    // Constructor injection
    public UserNotification(MessageService messageService) {
        this.messageService = messageService;
    }

    public void notifyUser(String message) {
        messageService.sendMessage(message);
    }
}
```

**SOLID Principles:**
- **SRP:** Client classes don't instantiate their dependencies.
- **OCP:** New dependencies can be added without modifying clients.
- **LSP:** Clients can use any implementation of the dependency interface.
- **DIP:** Clients depend on abstractions rather than concrete implementations.
- **ISP:** Clients depend only on the interfaces they need.