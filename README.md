import java.util.Vector;

public class VectorOperations {
    public static void main(String[] args) {
        // Create a Vector
        Vector<String> names = new Vector<>();

        // 1. Add Elements
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");
        names.add(1, "David"); // Insert at index 1

        // 2. Access Elements
        System.out.println("Element at index 0: " + names.get(0)); // Alice

        // 3. Update Element
        names.set(2, "Eve"); // Replaces Charlie with Eve

        // 4. Remove Elements
        names.remove(1);        // Removes David
        names.remove("Eve");    // Removes Eve

        // 5. Size and Capacity
        System.out.println("Current Size: " + names.size());
        System.out.println("Current Capacity: " + names.capacity());

        // 6. Check if Element Exists
        if (names.contains("Alice")) {
            System.out.println("Alice is present in the vector.");
        }

        // 7. Iterate using for-each loop
        System.out.println("All Elements:");
        for (String name : names) {
            System.out.println(name);
        }

        // 8. Clear the Vector
        names.clear();
        System.out.println("After clearing, is the vector empty? " + names.isEmpty());
    }
}
