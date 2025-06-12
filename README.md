import java.util.Stack;

public class StackOperations {
    public static void main(String[] args) {
        // Create a Stack of Strings
        Stack<String> books = new Stack<>();

        // 1. Push elements onto the stack
        books.push("Java");
        books.push("Python");
        books.push("C++");
        books.push("JavaScript");

        // 2. Peek at the top element
        System.out.println("Top element (peek): " + books.peek()); // JavaScript

        // 3. Pop element from the stack
        String removed = books.pop();
        System.out.println("Removed element (pop): " + removed);   // JavaScript

        // 4. Check if stack is empty
        System.out.println("Is the stack empty? " + books.isEmpty());

        // 5. Size of the stack
        System.out.println("Size of stack: " + books.size());

        // 6. Search for an element (1-based index from top)
        int position = books.search("Python");
        if (position != -1) {
            System.out.println("Found 'Python' at position (from top): " + position);
        } else {
            System.out.println("'Python' not found.");
        }

        // 7. Iterate through the stack (from bottom to top)
        System.out.println("Current Stack elements:");
        for (String book : books) {
            System.out.println(book);
        }

        // 8. Clear the stack
        books.clear();
        System.out.println("After clearing, is the stack empty? " + books.isEmpty());
    }
}


output
Top element (peek): JavaScript
Removed element (pop): JavaScript
Is the stack empty? false
Size of stack: 3
Found 'Python' at position (from top): 2
Current Stack elements:
Java
Python
C++
After clearing, is the stack empty? true
