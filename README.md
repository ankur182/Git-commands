Thanks for the image and clarification. Here's how you can implement the task in Java.


---

✅ Problem Summary

Create a Map of Ride objects.

Key = hashCode() of each Ride object.

Value = the Ride object itself.

Then, count how many rides are booked from a particular source (e.g., "Malad").



---

✅ Step-by-Step Java Code

import java.util.*;

class Ride {
    String source;
    String destination;
    double fare;

    // Constructor
    public Ride(String source, String destination, double fare) {
        this.source = source;
        this.destination = destination;
        this.fare = fare;
    }

    // Override hashCode (optional but good practice)
    @Override
    public int hashCode() {
        return Objects.hash(source, destination, fare);
    }

    // Optional: to print Ride object
    @Override
    public String toString() {
        return "Ride{" + "source='" + source + "', destination='" + destination + "', fare=" + fare + '}';
    }
}

public class RideMapExample {

    public static void main(String[] args) {
        // Create list of rides
        List<Ride> rideList = Arrays.asList(
            new Ride("Malad", "Thane", 200),
            new Ride("Andheri", "Borivali", 150),
            new Ride("Malad", "Kandivali", 120),
            new Ride("Malad", "Andheri", 180),
            new Ride("Thane", "Malad", 220)
        );

        // Create map with hashCode as key and Ride object as value
        Map<Integer, Ride> rideMap = new HashMap<>();
        for (Ride ride : rideList) {
            rideMap.put(ride.hashCode(), ride);
        }

        // Function to count rides from a specific source
        String searchSource = "Malad";
        int count = 0;
        for (Ride ride : rideMap.values()) {
            if (ride.source.equalsIgnoreCase(searchSource)) {
                count++;
            }
        }

        System.out.println("Number of rides booked from source '" + searchSource + "': " + count);
    }
}


---

✅ Output (for above data):

Number of rides booked from source 'Malad': 3


---

🔎 Key Concepts Used:

HashMap<Integer, Ride> to store hashcode → object

hashCode() ensures unique keys

Counting rides from a given source using ride.source.equalsIgnoreCase(searchSource)


Let me know if you want to add sorting, filtering by fare, or convert this to a Spring Boot or web app.
