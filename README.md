Got it! You want to:

Create two DTOs: EmployeeData and EmployerData

Extract data from Employee and Employer entities

Return it via your controller as a JSON response



---

Step-by-Step Setup

1. DTO Classes

EmployeeData.java

package com.example.helloworld.model;

public class EmployeeData {
    private String name;
    private int age;
    private double salary;

    public EmployeeData(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    // Getters and setters
}

EmployerData.java

package com.example.helloworld.model;

public class EmployerData {
    private Long employerId;
    private String panNo;

    public EmployerData(Long employerId, String panNo) {
        this.employerId = employerId;
        this.panNo = panNo;
    }

    // Getters and setters
}

2. Controller Method

In EmployeeController.java:

@GetMapping("/employee/{name}")
public ResponseEntity<?> getEmployeeByName(@PathVariable String name) {
    Optional<Employee> optionalEmployee = employeeRepo.findByName(name);

    if (optionalEmployee.isPresent()) {
        Employee emp = optionalEmployee.get();

        // Map to DTOs
        EmployeeData employeeData = new EmployeeData(emp.getName(), emp.getAge(), emp.getSalary());

        EmployerData employerData = null;
        if (emp.getEmployer() != null) {
            Employer employer = emp.getEmployer();
            employerData = new EmployerData(employer.getEmployerId(), employer.getPanNo());
        }

        // Final response map
        Map<String, Object> response = new HashMap<>();
        response.put("employee", employeeData);
        response.put("employer", employerData);

        return ResponseEntity.ok(response);
    } else {
        Map<String, Object> error = new HashMap<>();
        error.put("message", "Employee not found");
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
}

3. Repository Method

In EmployeeRepository.java:

@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    Optional<Employee> findByName(String name);
}


---

Output JSON

{
  "employee": {
    "name": "Ankur",
    "age": 25,
    "salary": 60000.0
  },
  "employer": {
    "employerId": 1,
    "panNo": "ABCPK1234L"
  }
}

Let me know if you'd like to merge this into a single DTO or customize the response format.

