In Java, the `Consumer`, `Function`, `Predicate`, and `Supplier` interfaces are functional interfaces found in the `java.util.function` package. Here's a brief explanation of each:

### 1. **`Consumer<T>`**
   - Represents an operation that accepts a single input argument and returns no result.
   - Example:
     ```java
     import java.util.function.Consumer;

     public class ConsumerExample {
         public static void main(String[] args) {
             Consumer<String> printMessage = message -> System.out.println("Message: " + message);
             printMessage.accept("Hello, World!");
         }
     }
     ```
   **Explanation**: The `Consumer` takes a `String` as input and prints it, but it does not return any value.

### 2. **`Function<T, R>`**
   - Represents a function that accepts one argument and produces a result.
   - Example:
     ```java
     import java.util.function.Function;

     public class FunctionExample {
         public static void main(String[] args) {
             Function<Integer, String> intToString = num -> "The number is " + num;
             String result = intToString.apply(5);
             System.out.println(result);
         }
     }
     ```
   **Explanation**: The `Function` takes an `Integer` as input and returns a `String`.

### 3. **`Predicate<T>`**
   - Represents a boolean-valued function of one argument (often used for filtering).
   - Example:
     ```java
     import java.util.function.Predicate;

     public class PredicateExample {
         public static void main(String[] args) {
             Predicate<Integer> isEven = num -> num % 2 == 0;
             boolean result = isEven.test(10); // true
             System.out.println("Is 10 even? " + result);
         }
     }
     ```
   **Explanation**: The `Predicate` takes an `Integer` and returns a boolean (`true` if the number is even, `false` otherwise).

### 4. **`Supplier<T>`**
   - Represents a supplier of results (it doesn't take any arguments but returns a result).
   - Example:
     ```java
     import java.util.function.Supplier;

     public class SupplierExample {
         public static void main(String[] args) {
             Supplier<String> greetingSupplier = () -> "Hello from Supplier!";
             String greeting = greetingSupplier.get();
             System.out.println(greeting);
         }
     }
     ```
   **Explanation**: The `Supplier` provides a `String` result when its `get()` method is called.

### Putting Them Together
Here's an example that uses all four functional interfaces:

```java
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class FunctionalInterfacesExample {
    public static void main(String[] args) {
        // Supplier: Provides a value without taking input
        Supplier<String> nameSupplier = () -> "John Doe";

        // Consumer: Consumes a value without returning anything
        Consumer<String> greeter = name -> System.out.println("Hello, " + name + "!");

        // Predicate: Tests a condition and returns a boolean
        Predicate<Integer> isAdult = age -> age >= 18;

        // Function: Transforms an input value into another type
        Function<String, Integer> nameLength = name -> name.length();

        // Use Supplier to get a name
        String name = nameSupplier.get();
        greeter.accept(name); // Use Consumer to greet the name

        // Check if a person is an adult using Predicate
        int age = 20;
        System.out.println("Is " + age + " an adult? " + isAdult.test(age));

        // Find the length of the name using Function
        int length = nameLength.apply(name);
        System.out.println("The length of the name is: " + length);
    }
}
```

### Explanation of the Full Example:
1. **Supplier** provides a name (`"John Doe"`).
2. **Consumer** takes the name and prints a greeting.
3. **Predicate** checks if a given age (`20`) qualifies as adult (returns `true`).
4. **Function** computes the length of the name and returns it.

This example demonstrates how these interfaces can be used together to build flexible, functional code in Java.
