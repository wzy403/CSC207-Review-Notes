### Week 6 Study Notes

## Types of Testing

### Unit Test
**Explanation:** 
Unit testing tests the smallest unit of cohesive code, often a method. It focuses on individual functions or methods to ensure they work correctly in isolation.

**Example:**
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

public class CalculatorTest {
    @Test
    public void testAdd() {
        Calculator calc = new Calculator();
        assertEquals(5, calc.add(2, 3));
    }
}
```

### Integration Test
**Explanation:** 
Integration testing tests how two components interact with each other. It ensures that different parts of the system work together as expected.

**Example:**
```java
public class UserService {
    private UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }

    public User getUser(String id) {
        return userDao.findById(id);
    }
}

public class UserServiceIntegrationTest {
    private UserDao userDao = new InMemoryUserDao();
    private UserService userService = new UserService(userDao);

    @Test
    public void testGetUser() {
        User user = new User("1", "John");
        userDao.save(user);
        assertEquals(user, userService.getUser("1"));
    }
}
```

### End-To-End Test
**Explanation:** 
End-to-end testing is a type of system testing that tests an entire path through the code from input to output. This can start and end with the view layer, ensuring the complete system works as intended.

**Example:**
```java
// Pseudo-code for an end-to-end test
@Test
public void testUserRegistration() {
    // Simulate user input on the UI
    simulateUserInput("username", "password");

    // Submit the form
    submitForm();

    // Check if the user is successfully registered and redirected to the homepage
    assertTrue(isRedirectedToHomepage());
    assertTrue(isUserLoggedIn("username"));
}
```

## Choosing Test Cases

### Criteria for Choosing Test Cases
- **Test for high-risk areas:** Focus on parts of the code that are most likely to fail or cause issues.
- **Equivalence Partitioning and Boundary Value Analysis:** Use techniques to test a range of inputs, including edge cases.
- **User-Focused Scenarios:** Create tests based on how users will interact with the system.
- **Edge Cases:** Test unusual or extreme cases to ensure the system can handle them.
- **New or Modified Code:** Prioritize testing for recently changed or added code.
- **Frequently Used Functions:** Ensure the most commonly used parts of the system are thoroughly tested.

## Setup and Teardown in Testing

### Setup and Teardown
**Explanation:**
- **Setup:** Before running a test, setup involves initializing the required state or conditions needed for the test. This ensures the test environment is consistent and isolated.

**Example:**
```java
@BeforeEach
public void setUp() {
    // Initialize objects needed for the test
    userDao = new InMemoryUserDao();
    userService = new UserService(userDao);
}
```

- **Teardown:** After running a test, teardown involves cleaning up any state or conditions that were modified during the test. This ensures no side effects impact subsequent tests.

**Example:**
```java
@AfterEach
public void tearDown() {
    // Clean up resources
    userDao.clear();
}
```

### Annotations
**@BeforeEach and @AfterEach:**
- `@BeforeEach`: Runs the annotated method before each test. Equivalent to `@Before`.
- `@AfterEach`: Runs the annotated method after each test. Equivalent to `@After`.

**Example:**
```java
@BeforeEach
public void init() {
    // Code to set up test environment
}

@AfterEach
public void cleanUp() {
    // Code to clean up after test
}
```

## Test Driven Development (TDD)

### Explanation:
Test Driven Development (TDD) is a software development approach that emphasizes writing tests before writing the actual code. With TDD, tests are based on requirements rather than existing code, guiding the development process.

**Example Workflow:**
1. **Write a test:** Create a test for a new feature based on requirements.
2. **Run the test:** The test should fail initially, indicating that the feature is not yet implemented.
3. **Write the code:** Implement the feature to pass the test.
4. **Run the test again:** Ensure the test passes after the implementation.
5. **Refactor the code:** Improve the code while ensuring the test still passes.

**Example:**
```java
// Step 1: Write a test
@Test
public void testAdd() {
    Calculator calc = new Calculator();
    assertEquals(5, calc.add(2, 3));
}

// Step 2: Run the test (it will fail)

// Step 3: Write the code
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

// Step 4: Run the test (it should pass)

// Step 5: Refactor if needed
```

## Exception Handling in Java

### What is an Exception?
**Explanation:**
Exceptions report exceptional conditions, such as unusual, strange, or unexpected events that disrupt normal program flow.

**Example:**
```java
try {
    int result = 10 / 0;  // This will cause an ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
}
```

### Purpose of a "finally" Block
**Explanation:**
A `finally` block is part of the `try-catch` structure. The code inside the `finally` block will run regardless of whether an exception occurs or not. It is typically used for cleanup activities.

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