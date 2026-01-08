# New Things That I have learnt about coding

### 1. Try block inside another try block

**The Common****`catch`****for Nested****`try`****Blocks**

The pattern of having nested`try`blocks (specifically`try-with-resources`inside a single outer`try`) is an elegant way to manage resource closing automatically without cluttering your code with redundant`catch`blocks for every single I/O operation.

It enforces a**single point of failure handling**, which is cleaner to manage and debug.

### **2. Multi-Catch Syntax (****`catch (ExceptionA | ExceptionB e)`****)**

one common catch block catch(IOException|IllegalStateException e) { } which will handle all catch blocks alone. so you don't need to use multiple catch blocks.

The syntax`catch (IOException | IllegalStateException e)`is a feature introduced in**Java 7**known as the**multi-catch block**.

Its purpose is to reduce code duplication when several different exception types are handled in the exact same way. Instead of writing:

```java
try {
    // ...
} catch (IOException e) {
    // handle error
} catch (IllegalStateException e) {
    // handle error exactly the same way
}
```

You can combine them with a vertical bar (`|`) into a single, more concise line:

```java
try {
    // ...
} catch (IOException | IllegalStateException e) {
    // handle error for both types identically
}
```

### 3. Static Block [Static Block](file:///workspace/27e9a829-499a-48db-a4f5-e6ec25e9ae1c/RIUec9-rg-s5hndqrO6Cm)
