### Week 5 Study Notes

## Collections Framework in Java

### Overview
**What is the Collections Framework in Java?**

A collection is an object that represents a group of objects. The Collections Framework is a unified architecture for representing and manipulating collections, enabling collections to be manipulated independently of implementation details.

**Examples:**
- `List`: An ordered collection (also known as a sequence).
- `ArrayList`: A resizable array implementation of the `List` interface.
- `LinkedList`: A doubly-linked list implementation of the `List` and `Deque` interfaces.
- `Set`: A collection that contains no duplicate elements.
- `Map`: An object that maps keys to values. A `Map` cannot contain duplicate keys.
- `HashMap`: A hash table-based implementation of the `Map` interface.

### Common Classes in Collections Framework
**List three classes in the Java Collections framework:**
- `HashMap`
- `LinkedList`
- `ArrayList`

### Expected Behaviors of Collection Types
**What behaviors do you expect to see in implementing classes of Set, Queue, and List?**

- **Set:**
  - No duplicates: Each element must be unique.
  - Unordered collection: Elements do not have a specific order.
  - Basic operations: `add()`, `remove()`, `size()`, `isEmpty()`, `contains()`

- **Queue:**
  - First In First Out (FIFO): Elements are processed in the order they were added.
  - Basic operations: `add()`, `poll()`, `peek()`, `isEmpty()`
  - Example: `LinkedList` can be used as a queue.

- **List:**
  - Ordered collection: Elements have a specific order.
  - Allows duplicates: Multiple instances of the same element can be stored.
  - Basic operations: `add()`, `size()`, `get()`, `remove()`
  - Example: `ArrayList` and `LinkedList`

### Iterating Over Collections
**What does it mean to "iterate" over a collection?**

Iterating over a collection means accessing each element in the collection one by one.

**Example:**
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

for (String element : list) {
    System.out.println(element);
}
```
In this example, the `for-each` loop iterates over each element in the `list` and prints it out.

### When to Use Different Collection Types
**What do these mean: Map, Set, Queue, List, and when would you use each one?**

- **Map:** Used when you need to associate unique keys with specific values. 
  - **Example:** `HashMap<String, Integer>` for storing a word and its frequency count.

- **Set:** Used when you need a collection of unique elements and do not care about the order.
  - **Example:** `HashSet<String>` for storing a collection of unique words from a text.

- **Queue:** Used when you need to process elements in a FIFO (First In First Out) manner.
  - **Example:** `LinkedList<String>` for a queue of tasks to be processed in order.

- **List:** Used when you need an ordered collection that allows duplicates and provides indexed access to elements.
  - **Example:** `ArrayList<String>` for a list of items that can be accessed by their position.

## SOLID Principles

### Using Interfaces
**Which SOLID principle tells us to use `List<String> x = new ArrayList<>();` instead of `ArrayList<String> x = new ArrayList<>();`?**

- **Liskov Substitution Principle (LSP):** This principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. By using the interface `List` instead of the implementation `ArrayList`, you can easily switch to a different `List` implementation (e.g., `LinkedList`) without changing the code that uses the list.

**Example:**
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
```
By declaring `list` as a `List` type, you can later change the implementation to `LinkedList` without altering the rest of the code.

### Iterator Design Pattern
**How does having an Iterator allow us to make for-each loops in Java?**

The `Iterator` interface provides a standard way to traverse elements in a collection. The `for-each` loop in Java uses the `Iterator` to iterate over elements.

**Example:**
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

for (String element : list) {
    System.out.println(element);
}
```
In the background, the `for-each` loop uses the `Iterator` provided by the `list` to access each element.

**What problem is the Iterator Design Pattern trying to solve?**

- **Encapsulation:** Keeps the internal structure of the collection hidden from the client.
- **Uniform access:** Provides a consistent way to traverse different types of collections.
- **Multiple traversals:** Allows multiple traversals of a collection without exposing its structure.
- **Simplified interface:** Provides a simple interface for iteration.

## Sequence Diagrams

### Purpose of Sequence Diagrams
**What does a sequence diagram show?**

A sequence diagram shows how objects interact with each other in a particular sequence of time. It details the interactions between different objects and the order in which these interactions occur.

### Components of Sequence Diagrams
**What do the boxes at the top of a sequence diagram represent?**

The boxes at the top of a sequence diagram represent the objects or actors involved in the interaction.

**What do the vertical lines coming out of the boxes on top of a sequence diagram denote?**

These vertical lines are called lifelines, representing the existence of an object over a period of time.

**In a sequence diagram, what are the right-facing arrows showing?**

Right-facing arrows in a sequence diagram represent messages or method calls sent from one object to another. They indicate the direction and sequence of interactions.

**In a sequence diagram, what are the left-facing arrows showing?**

Left-facing arrows typically represent return messages or responses from the receiver object back to the sender object.

**Example:**
```plaintext
+----------------+                +----------------+
|    Object A    |                |    Object B    |
+----------------+                +----------------+
        |                                |
        |-------- Message 1 ------------>|
        |                                |
        |<------- Return Message --------|
        |                                |
```