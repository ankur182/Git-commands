Great! Let's dive deeper into Functional Interfaces in Java, specifically their types, usage, and examples using built-in interfaces from the java.util.function package.


---

✅ What is a Functional Interface?

A Functional Interface has exactly one abstract method. It can have multiple default or static methods but only one method to implement, making it perfect for lambda expressions.


---

✅ Types of Functional Interfaces (Built-in in Java)

Java 8 introduced many predefined functional interfaces in the java.util.function package. Let’s break them down by functionality:


---

🔹 1. Function<T, R>

Takes an input of type T and returns a result of type R.


Function<Integer, String> converter = (i) -> "Number: " + i;
System.out.println(converter.apply(5)); // Output: Number: 5


---

🔹 2. Consumer<T>

Takes an input T and returns nothing (void). Used for performing operations like printing, logging, etc.


Consumer<String> printer = (msg) -> System.out.println(msg);
printer.accept("Hello, world!"); // Output: Hello, world!


---

🔹 3. Supplier<T>

Takes no input but returns a value of type T.


Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get()); // Output: Random number


---

🔹 4. Predicate<T>

Takes an input T and returns a boolean value. Often used for filtering.


Predicate<Integer> isEven = (num) -> num % 2 == 0;
System.out.println(isEven.test(4)); // Output: true


---

🔹 5. BiFunction<T, U, R>

Takes two inputs (T, U) and returns one output (R).


BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
System.out.println(add.apply(2, 3)); // Output: 5


---

🔹 6. BiPredicate<T, U>

Takes two inputs and returns a boolean.


BiPredicate<String, Integer> isLonger = (str, len) -> str.length() > len;
System.out.println(isLonger.test("Hello", 3)); // Output: true


---

🔹 7. UnaryOperator<T>

A Function where input and output are of the same type.


UnaryOperator<Integer> square = x -> x * x;
System.out.println(square.apply(5)); // Output: 25


---

🔹 8. BinaryOperator<T>

A BiFunction with same input and output types.


BinaryOperator<Integer> multiply = (a, b) -> a * b;
System.out.println(multiply.apply(2, 3)); // Output: 6


---

✅ Summary Table:

Interface	Input	Output	Use Case

Function<T, R>	1	1	Convert T to R
Consumer<T>	1	void	Do something with T
Supplier<T>	None	1	Generate a value
Predicate<T>	1	boolean	Test a condition
BiFunction<T, U, R>	2	1	Combine two inputs
UnaryOperator<T>	1 (T)	1 (T)	Modify and return same type
BinaryOperator<T>	2 (T, T)	1 (T)	Combine two of same type



---

Would you like a short quiz or practical problem using these to test your understanding?
