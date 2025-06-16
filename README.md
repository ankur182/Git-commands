✅ What is a Lambda Expression in Java?

A Lambda expression in Java is a short block of code that takes in parameters and returns a value. Lambda expressions are used primarily to define inline implementations of functional interfaces.

Introduced in Java 8, it allows us to treat function as method argument or treat code as data.


---

📌 Syntax of Lambda Expression

(parameters) -> { body }

If there is only one statement, you can skip the curly braces {} and the return keyword.


---

✅ Example 1: Basic Lambda Expression (No Return)

@FunctionalInterface
interface Greeting {
    void sayHello();
}

public class LambdaExample {
    public static void main(String[] args) {
        Greeting greet = () -> System.out.println("Hello from Lambda!");
        greet.sayHello();
    }
}


---

✅ Example 2: Lambda with Parameters and Return

@FunctionalInterface
interface Add {
    int sum(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        Add addition = (a, b) -> a + b;
        System.out.println("Sum: " + addition.sum(5, 3));  // Output: 8
    }
}


---

✅ Example 3: Lambda with Collection (Using forEach)

import java.util.*;

public class LambdaListExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("Apple", "Banana", "Mango");

        list.forEach(item -> System.out.println("Fruit: " + item));
    }
}


---

✅ Key Points

Lambda expressions can only be used with functional interfaces (interface with only one abstract method).

Makes code concise and readable.

Often used with streams, collections, and functional programming.



---

Would you like examples with threads, sorting with lambda, or streams too?

