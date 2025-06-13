✅ HashMap in Java – Complete Guide with Example

A HashMap is a part of the Java Collections Framework used to store key-value pairs. It is:

Not thread-safe

Allows one null key and multiple null values

Does not maintain order (unlike LinkedHashMap or TreeMap)



---

🔑 Key Methods of HashMap

put(K key, V value)

get(Object key)

containsKey(Object key)

containsValue(Object value)

remove(Object key)

keySet(), values(), entrySet()

size(), isEmpty(), clear()



---

✅ Complete Example: All Basic Operations in One File

import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        // 1. Create a HashMap
        HashMap<Integer, String> map = new HashMap<>();

        // 2. Add entries (put)
        map.put(101, "Alice");
        map.put(102, "Bob");
        map.put(103, "Charlie");
        map.put(104, "David");
        map.put(null, "NullKeyExample");
        map.put(105, null);  // null value
        map.put(106, null);  // multiple null values

        // 3. Access elements
        System.out.println("Value for key 102: " + map.get(102));
        System.out.println("Value for null key: " + map.get(null));

        // 4. Check key or value
        System.out.println("Contains key 103? " + map.containsKey(103));
        System.out.println("Contains value 'Bob'? " + map.containsValue("Bob"));

        // 5. Remove element
        map.remove(104);

        // 6. Iterate using entrySet
        System.out.println("\nAll key-value pairs:");
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }

        // 7. Get all keys and values separately
        System.out.println("\nAll keys: " + map.keySet());
        System.out.println("All values: " + map.values());

        // 8. Size and empty check
        System.out.println("Size of map: " + map.size());
        System.out.println("Is map empty? " + map.isEmpty());

        // 9. Clear the map
        map.clear();
        System.out.println("After clear, size: " + map.size());
    }
}


---

🖥️ Sample Output

Value for key 102: Bob
Value for null key: NullKeyExample
Contains key 103? true
Contains value 'Bob'? true

All key-value pairs:
Key: null, Value: NullKeyExample
Key: 101, Value: Alice
Key: 102, Value: Bob
Key: 103, Value: Charlie
Key: 105, Value: null
Key: 106, Value: null

All keys: [null, 101, 102, 103, 105, 106]
All values: [NullKeyExample, Alice, Bob, Charlie, null, null]
Size of map: 6
Is map empty? false
After clear, size: 0


---

⚠️ Thread Safety in HashMap

HashMap is not thread-safe.

Use Collections.synchronizedMap(map) or ConcurrentHashMap in multi-threaded programs.



---

✅ Bonus: ConcurrentHashMap Example for Thread-Safe Map?

Would you like that too?
