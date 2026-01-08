# Static Block

The`static {}`block is a fundamental, yet often underutilized, feature of the Java language. Many junior developers go years without encountering it if they don't work on framework-level code.

Let me teach you about the **static initialization block**, also known as **static block**.

***

**What is a****`static {}`****Initialization Block?**

A`static`block is a special block of code in a Java class that is used to initialize**static**variables or perform**static**setup logic.



**1. When Does It Run? (The Most Important Rule)**

A`static`block runs exactly**once**, the very first time the Java Virtual Machine (JVM) loads the class into memory.

It runs*before*any object instances of that class are created, and*before*any other static methods are called.

| Feature        | static { } block                             | Constructor (eg. ConfigReader)                             |
| -------------- | -------------------------------------------- | ---------------------------------------------------------- |
| **Runs When?** | When the class is first loaded by the JVM.   | Every time a*new object*is created (`new ConfigReader()`). |
| **How Often?** | Exactly Once per program execution.          | Many times.                                                |
| **Purpose**    | To set up shared static resources/variables. | To initialize instance variables for a specific object.    |

**2. Why Do We Use It?**

We use static blocks when complex logic is required to determine the initial value of a`static`variable.

If you had a simple static variable, you initialize it like this:

```java
public class Example {
    private static int simpleCount = 0; // Simple initialization
}
```

But what if you need to read a file, connect to a database, or run a complex algorithm just to figure out what that static variable should be*before*the rest of the application runs? That complex logic goes into the static block.

**In your****`ConfigReader`****case, you used it to load files from disk, which is complex I/O that needs to happen once at startup.**

**3. How to Declare It**

It's the simplest syntax in Java. Just the keyword`static`followed by curly braces:

```java
public class MyClass {
    // 1. Static variables declared first
    private static String configurationStatus;
    private static Properties appProperties = new Properties();

    // 2. The static initialization block
    static {
        // This runs first, when the class is loaded.
        System.out.println("LOG: Class MyClass is being loaded by the JVM.");
        
        // This is where you put your complex setup logic/I/O
        try {
           // ... load files, set 'configurationStatus' value ...
           configurationStatus = "LOADED_SUCCESSFULLY";
        } catch (Exception e) {
           configurationStatus = "FAILED";
        }
    }
    
    // 3. The constructor runs later, only when 'new MyClass()' is called
    public MyClass() {
        System.out.println("LOG: A new MyClass instance is being created.");
    }
}
```

**4. Thread Safety**

Because the static block executes during the JVM's class loading phase, the process is guaranteed to be**thread-safe**. You don't have to worry about multiple threads trying to initialize your configuration at the same time, which is why we could remove the`synchronized`keyword and the`isConfigLoaded`flag in your final version of`ConfigReader`.



**Summary for your****`ConfigReader`**

By using the`static {}`block, you ensure that your framework configures itself reliably, efficiently, and automatically as soon as the Java application needs access to any part of the`ConfigReader`class.

