Thanks for the update. Let's solve it cleanly.


---

Based on the image and description, here's the correct version of the method:

Controller Fix:

Change your method to this:

@GetMapping("/employee/{name}")
public ResponseEntity<Map<String, Object>> getEmployeeByName(@PathVariable String name) {
    Optional<Employee> optionalEmployee = employeeRepository.findByName(name);

    if (optionalEmployee.isPresent()) {
        Employee emp = optionalEmployee.get();
        Map<String, Object> response = new HashMap<>();
        response.put("name", emp.getName());
        response.put("age", emp.getAge());
        response.put("salary", emp.getSalary());

        Employer employer = emp.getEmployer(); // make sure this is mapped in your entity
        if (employer != null) {
            response.put("employerId", employer.getEmployerId());
            response.put("panNo", employer.getPanNo());
        }

        return ResponseEntity.ok(response);
    } else {
        Map<String, Object> error = new HashMap<>();
        error.put("message", "Employee not found");
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
}


---

Required Adjustments in Entities:

Employee.java

Make sure the mapping is there:

@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "employer_id")
private Employer employer;

Employer.java

@OneToMany(mappedBy = "employer")
private List<Employee> employees;


---

Optional: Use @EntityGraph to Fetch Employer with Employee

In EmployeeRepository.java:

@EntityGraph(attributePaths = {"employer"})
Optional<Employee> findByName(String name);


---

This will:

Fix your return type issue.

Return employee details + employer ID and PAN.

Avoid lazy loading issues using @EntityGraph.


Let me know if you want a DTO-based cleaner approach too.

