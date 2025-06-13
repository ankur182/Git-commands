import java.util.LinkedHashSet;
import java.util.Iterator;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        // 1. Create a LinkedHashSet of Strings
        LinkedHashSet<String> cities = new LinkedHashSet<>();

        // 2. Add elements
        cities.add("Delhi");
        cities.add("Mumbai");
        cities.add("Chennai");
        cities.add("Kolkata");
        cities.add("Delhi"); // duplicate, won't be added
        cities.add(null);    // one null allowed
        cities.add(null);    // duplicate null won't be added

        // 3. Print the set
        System.out.println("LinkedHashSet elements (insertion order): " + cities);

        // 4. Check if element exists
        System.out.println("Contains 'Mumbai'? " + cities.contains("Mumbai"));

        // 5. Remove an element
        cities.remove("Chennai");
        System.out.println("After removing 'Chennai': " + cities);

        // 6. Size and isEmpty
        System.out.println("Size: " + cities.size());
        System.out.println("Is empty? " + cities.isEmpty());

        // 7. Iterate using for-each loop
        System.out.println("Iterating over elements:");
        for (String city : cities) {
            System.out.println(city);
        }

        // 8. Clear the set
        cities.clear();
        System.out.println("After clearing, is empty? " + cities.isEmpty());
    }
}


LinkedHashSet elements (insertion order): [Delhi, Mumbai, Chennai, Kolkata, null]
Contains 'Mumbai'? true
After removing 'Chennai': [Delhi, Mumbai, Kolkata, null]
Size: 4
Is empty? false
Iterating over elements:
Delhi
Mumbai
Kolkata
null
After clearing, is empty? true

