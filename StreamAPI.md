Here are some common **Java 8 Stream API** interview questions with code examples to help you prepare:

### 1. **What is the Stream API in Java 8?**
   - **Answer**: The Stream API in Java 8 is used to process collections of objects in a functional and declarative manner. It supports operations like filtering, mapping, reducing, and more, using lambda expressions. It can be sequential or parallel to enhance performance.

### 2. **What is the difference between `Collection` and `Stream`?**
   - **Answer**: 
     - **Collection** is a data structure that holds elements in memory. You can iterate over it multiple times.
     - **Stream** is not a data structure but a pipeline of operations on data. A stream does not store data and can only be traversed once.

### 3. **How do you create a Stream in Java 8?**
   - **Answer**: You can create streams from collections, arrays, or using static methods from the `Stream` class.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class StreamCreation {
       public static void main(String[] args) {
           // Create a stream from a list
           List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
           Stream<String> nameStream = names.stream();
           
           // Create a stream from an array
           int[] numbers = {1, 2, 3, 4, 5};
           IntStream numberStream = Arrays.stream(numbers);
           
           // Stream using Stream.of()
           Stream<String> streamOfStrings = Stream.of("Hello", "World");
       }
   }
   ```

### 4. **What are Intermediate and Terminal Operations in Stream API?**
   - **Answer**:
     - **Intermediate Operations**: These return a new stream and are lazy, meaning they don’t process the data until a terminal operation is invoked. Examples include `filter()`, `map()`, and `sorted()`.
     - **Terminal Operations**: These trigger the processing of the stream and return a result or a side-effect, such as `forEach()`, `collect()`, or `reduce()`.

### 5. **How does the `filter()` method work in Stream API?**
   - **Answer**: `filter()` is an intermediate operation that takes a `Predicate` and filters elements based on the condition provided.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class StreamFilter {
       public static void main(String[] args) {
           List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

           // Filter names starting with 'A'
           List<String> filteredNames = names.stream()
                                             .filter(name -> name.startsWith("A"))
                                             .collect(Collectors.toList());

           System.out.println(filteredNames);  // Output: [Alice]
       }
   }
   ```

### 6. **Explain the `map()` operation with an example.**
   - **Answer**: The `map()` method is used to transform the elements of a stream. It takes a `Function` and applies it to each element of the stream.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class StreamMap {
       public static void main(String[] args) {
           List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

           // Convert names to uppercase
           List<String> upperCaseNames = names.stream()
                                              .map(String::toUpperCase)
                                              .collect(Collectors.toList());

           System.out.println(upperCaseNames);  // Output: [ALICE, BOB, CHARLIE]
       }
   }
   ```

### 7. **What is the difference between `map()` and `flatMap()`?**
   - **Answer**:
     - **`map()`**: Transforms each element into one element.
     - **`flatMap()`**: Transforms each element into multiple elements (or a stream) and then flattens them into a single stream.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class FlatMapExample {
       public static void main(String[] args) {
           List<List<String>> nestedList = Arrays.asList(
                   Arrays.asList("Alice", "Bob"),
                   Arrays.asList("Charlie", "David")
           );

           // Flatten nested lists into a single list using flatMap
           List<String> flatList = nestedList.stream()
                                             .flatMap(Collection::stream)
                                             .collect(Collectors.toList());

           System.out.println(flatList);  // Output: [Alice, Bob, Charlie, David]
       }
   }
   ```

### 8. **What is the use of `reduce()` in Stream API?**
   - **Answer**: The `reduce()` method is used to perform a reduction on the elements of a stream, combining them into a single result (e.g., sum, maximum, or concatenation).

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class StreamReduce {
       public static void main(String[] args) {
           List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

           // Sum of all numbers
           int sum = numbers.stream()
                            .reduce(0, Integer::sum);

           System.out.println("Sum: " + sum);  // Output: Sum: 15
       }
   }
   ```

### 9. **How can you convert a Stream back to a Collection?**
   - **Answer**: You can use the `collect()` method to convert a stream back into a collection like a `List`, `Set`, or `Map`.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class StreamToList {
       public static void main(String[] args) {
           List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

           // Convert stream to list
           List<String> nameList = names.stream()
                                        .filter(name -> name.length() > 3)
                                        .collect(Collectors.toList());

           System.out.println(nameList);  // Output: [Alice, Charlie]
       }
   }
   ```

### 10. **What is a parallel stream, and how is it different from a regular stream?**
   - **Answer**: A parallel stream divides the stream into multiple parts and processes them concurrently using multiple threads, which can improve performance for large datasets. You can create a parallel stream by calling `parallelStream()` or using `stream().parallel()`.

   #### Code Example:
   ```java
   import java.util.*;
   import java.util.stream.*;

   public class ParallelStreamExample {
       public static void main(String[] args) {
           List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

           // Parallel stream
           int sum = numbers.parallelStream()
                            .reduce(0, Integer::sum);

           System.out.println("Sum using parallel stream: " + sum);  // Output: Sum using parallel stream: 55
       }
   }
   ```

### Key Concepts to Focus On:
- Stream creation and processing.
- Intermediate operations (filter, map, flatMap, distinct, sorted).
- Terminal operations (forEach, collect, reduce, count).
- Short-circuiting operations (findFirst, findAny, anyMatch).
- Performance implications of parallel streams.

These questions and examples should cover key areas for your interview! Let me know if you need more detailed explanations or specific questions.
