import java.util.HashSet;
import java.util.Iterator;

public class HashSetExample {
    public static void main(String[] args) {
        // 1. Create a HashSet of Strings
        HashSet<String> fruits = new HashSet<>();

        // 2. Add elements (duplicates won't be added)
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Mango");
        fruits.add("Orange");
        fruits.add("Banana"); // duplicate
        fruits.add(null);     // null allowed
        fruits.add(null);     // only one null allowed

        // 3. Print the set
        System.out.println("HashSet elements: " + fruits);

        // 4. Check if set contains an element
        System.out.println("Contains 'Apple'? " + fruits.contains("Apple"));

        // 5. Remove an element
        fruits.remove("Mango");
        System.out.println("After removing 'Mango': " + fruits);

        // 6. Size of the set
        System.out.println("Size: " + fruits.size());

        // 7. Iterate using iterator
        System.out.println("Iterating using iterator:");
        Iterator<String> it = fruits.iterator();
        while (it.hasNext()) {
            System.out.println(it.next());
        }

        // 8. Clear the set
        fruits.clear();
        System.out.println("After clearing, is empty? " + fruits.isEmpty());
    }
}
