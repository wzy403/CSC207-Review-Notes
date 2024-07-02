### Week 4 Study Notes 

## Roles and Responsibilities in Software Design

### Entity
Responsible for the basic business rules.

**Example:**
```java
public class User {
    private String username;
    private String password;

    // Business rule: password must be at least 8 characters
    public void setPassword(String password) {
        if (password.length() >= 8) {
            this.password = password;
        } else {
            throw new IllegalArgumentException("Password must be at least 8 characters");
        }
    }
}
```

### Data Access Object (DAO)
Responsible for accessing the database and sending data back to where the use cases are needed.

**Example:**
```java
public interface UserDao {
    void save(User user);
    User findByUsername(String username);
}

public class UserDaoImpl implements UserDao {
    private Map<String, User> database = new HashMap<>();

    @Override
    public void save(User user) {
        database.put(user.getUsername(), user);
    }

    @Override
    public User findByUsername(String username) {
        return database.get(username);
    }
}
```

### Controller
Responsible for getting user input and sending it to the use case.

**Example:**
```java
public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    public void handleUserSignup(String username, String password) {
        userService.signup(username, password);
    }
}
```

### Presenter
Responsible for presenting the data to the user.

**Example:**
```java
public class UserPresenter {
    public void displayUserDetails(User user) {
        System.out.println("Username: " + user.getUsername());
    }
}
```

### View
Responsible for the User Interface (UI).

**Example:**
```java
public class UserView {
    public void show() {
        System.out.println("User Interface Displayed");
    }
}
```

### View Model
Responsible for the template of the data for the UI.

**Example:**
```java
public class UserViewModel {
    private String username;
    private String displayMessage;

    // Getters and setters for the ViewModel
}
```

### Use Case Interactor
Responsible for applying the business rules.

**Example:**
```java
public class UserSignupInteractor {
    private UserDao userDao;
    private UserPresenter userPresenter;

    public UserSignupInteractor(UserDao userDao, UserPresenter userPresenter) {
        this.userDao = userDao;
        this.userPresenter = userPresenter;
    }

    public void signup(String username, String password) {
        User user = new User();
        user.setUsername(username);
        user.setPassword(password);
        userDao.save(user);
        userPresenter.displayUserDetails(user);
    }
}
```

---

## Business Rules

### Enterprise Business Rules
Provide a broad framework for organizational operations and compliance, affecting multiple applications and processes across the company.

**Example:**
Enterprise rules might include security policies, data integrity checks, or transaction management that apply across all applications within an organization.

### Application Business Rules
Detailed guidelines that govern the behavior and functionality of specific software applications, ensuring they meet user requirements and perform as intended.

**Example:**
Application rules might include specific validation for a user registration form, such as ensuring the password meets certain complexity requirements.

---

## Clean Architecture Dependency Rules
High-level layers and low-level layers all depend on abstraction.

**Example:**
In Clean Architecture, the business logic should not depend on UI or database layers. Instead, they should all depend on abstractions (interfaces).

```java
public interface UserRepository {
    void save(User user);
    User findById(String userId);
}

public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Business logic methods
}
```

---

## Implementing Interfaces and Their Importance

### Classes Implementing Interfaces
In Clean Architecture, the classes implementing interfaces are typically found in the Interface Adapters and Frameworks & Drivers layers.

**Example:**
```java
public interface UserRepository {
    void save(User user);
    User findById(String userId);
}

public class InMemoryUserRepository implements UserRepository {
    private Map<String, User> users = new HashMap<>();

    @Override
    public void save(User user) {
        users.put(user.getId(), user);
    }

    @Override
    public User findById(String userId) {
        return users.get(userId);
    }
}
```

### Example Classes for Each Role
**Entity:**
- [CommonUser.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/CommonUser.java)
- [CommonUserFactory.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/CommonUserFactory.java)
- [PasswordValidator.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/PasswordValidator.java)
- [PasswordValidatorService.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/PasswordValidatorService.java)
- [User.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/User.java)
- [UserFactory.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/entity/UserFactory.java)

**Data Access Object:**
- [FileUserDataAccessObject.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/data_access/FileUserDataAccessObject.java)
- [InMemoryUserDataAccessObject.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/data_access/InMemoryUserDataAccessObject.java)
- [UserSignupDataAccessInterface.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/data_access/UserSignupDataAccessInterface.java)

**Controller & Presenter:**
- [LoginState.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/interface_adapter/LoginState.java)
- [LoginViewModel.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/interface_adapter/LoginViewModel.java)
- [SignupController.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/interface_adapter/SignupController.java)
- [SignupPresenter.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/interface_adapter/SignupPresenter.java)

**View & View Model:**
- [LabelTextPanel.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/view/LabelTextPanel.java)
- [LoginView.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/view/LoginView.java)
- [SignupView.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/view/SignupView.java)
- [ViewManager.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/view/ViewManager.java)

**Use Case Interactor:**
- [SignupInputBoundary.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/use_case/SignupInputBoundary.java)
- [SignupInputData.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/use_case/SignupInputData.java)
- [SignupInteractor.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/use_case/SignupInteractor.java)
- [SignupOutputBoundary.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/use_case/SignupOutputBoundary.java)
- [SignupOutputData.java](https://github.com/paulgries/LoginCleanArchitecture/blob/main/src/use_case/SignupOutputData.java)

---

## SOLID Principles

### Single Responsibility Principle (SRP)
Each class/interface should focus on one responsibility. For example, a data access object should only have methods that deal with user input.

**Example:**
```java
public class User {
    private String username;
    private String password;

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        if (password.length() >= 8) {
            this.password = password;
        } else {
            throw new IllegalArgumentException("Password must be at least 8 characters");
        }
    }
}
```

### Open/Closed Principle (OCP)
Classes should be open for extension but closed for modification. For example, if each time you add a new feature for a subclass, you need to change other implementations, it means you are not following OCP and should change your code.

**Example:**
```java
public abstract class Shape {
    public abstract double area();
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

public class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}
```

### Liskov Substitution Principle (LSP)
A derived class should be able to substitute its base class without causing errors. It should be removable for the extension.

**Example:**
```java
public class Bird {
    public void fly() {
        System.out.println("Bird is flying");
    }
}

public class Sparrow extends Bird

 {
    // Inherits fly method without changes
}

public class Ostrich extends Bird {
    // Ostrich cannot fly, violating LSP if fly method is used
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostrich cannot fly");
    }
}
```

### Interface Segregation Principle (ISP)
One interface can be broken down into multiple interfaces for implementation.

**Example:**
```java
public interface Printer {
    void print(Document doc);
}

public interface Scanner {
    void scan(Document doc);
}

public class MultiFunctionPrinter implements Printer, Scanner {
    @Override
    public void print(Document doc) {
        // printing logic
    }

    @Override
    public void scan(Document doc) {
        // scanning logic
    }
}
```

### Dependency Inversion Principle (DIP)
It is the principle of dependency injection.

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

    // Dependency is injected via constructor
    public UserNotification(MessageService messageService) {
        this.messageService = messageService;
    }

    public void notifyUser(String message) {
        messageService.sendMessage(message);
    }
}
```

**How SOLID principles are followed by Clean Architecture:**
Clean Architecture adheres to all SOLID principles, as these principles form the rules for Clean Architecture.