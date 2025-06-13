import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        // 1. Create a LinkedHashMap
        LinkedHashMap<Integer, String> students = new LinkedHashMap<>();

        // 2. Add key-value pairs
        students.put(101, "Alice");
        students.put(102, "Bob");
        students.put(103, "Charlie");
        students.put(null, "NullKey");
        students.put(104, null); // null value

        // 3. Access values
        System.out.println("Student with ID 102: " + students.get(102));
        System.out.println("Value of null key: " + students.get(null));

        // 4. Check presence
        System.out.println("Contains key 103? " + students.containsKey(103));
        System.out.println("Contains value 'Bob'? " + students.containsValue("Bob"));

        // 5. Iterate using entrySet
        System.out.println("\nAll entries in insertion order:");
        for (Map.Entry<Integer, String> entry : students.entrySet()) {
            System.out.println("ID: " + entry.getKey() + ", Name: " + entry.getValue());
        }

        // 6. Size and clear
        System.out.println("\nSize before clear: " + students.size());
        students.clear();
        System.out.println("Is map empty? " + students.isEmpty());
    }
}
