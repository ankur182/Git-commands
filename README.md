import java.util.TreeSet;
import java.util.Iterator;

public class TreeSetExample {
    public static void main(String[] args) {
        // 1. Create a TreeSet of Strings
        TreeSet<String> names = new TreeSet<>();

        // 2. Add elements (automatically sorted)
        names.add("Zara");
        names.add("Ankit");
        names.add("Mohan");
        names.add("Ritika");
        names.add("Ankit"); // Duplicate (ignored)

        // names.add(null); // Uncommenting this throws NullPointerException

        // 3. Print TreeSet (sorted)
        System.out.println("Sorted names in TreeSet: " + names);

        // 4. First and Last Elements
        System.out.println("First: " + names.first());
        System.out.println("Last: " + names.last());

        // 5. Check if contains
        System.out.println("Contains 'Mohan'? " + names.contains("Mohan"));

        // 6. Remove an element
        names.remove("Ritika");
        System.out.println("After removing Ritika: " + names);

        // 7. Iterate
        System.out.println("Iterating over TreeSet:");
        for (String name : names) {
            System.out.println(name);
        }

        // 8. Clear
        names.clear();
        System.out.println("Is TreeSet empty after clearing? " + names.isEmpty());
    }
}





Sorted names in TreeSet: [Ankit, Mohan, Ritika, Zara]
First: Ankit
Last: Zara
Contains 'Mohan'? true
After removing Ritika: [Ankit, Mohan, Zara]
Iterating over TreeSet:
Ankit
Mohan
Zara
Is TreeSet empty after clearing? true
