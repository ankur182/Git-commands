Thanks! Based on the SQL schema in your image, here’s how to implement the One-to-Many mapping in Spring Boot using H2 Database, with tables:

employer: employer_id (PK), pan_no, est_date, location

employee: emp_id (PK), name, age, salary, employer_id (FK)



---

1. Employer.java

@Entity
public class Employer {
    @Id
    private Integer employerId;

    private String panNo;
    private LocalDate estDate;
    private String location;

    @OneToMany(mappedBy = "employer", cascade = CascadeType.ALL)
    private List<Employee> employees;

    // Getters and Setters
}


---

2. Employee.java

@Entity
public class Employee {
    @Id
    private Integer empId;

    private String name;
    private int age;
    private int salary;

    @ManyToOne
    @JoinColumn(name = "employer_id")
    private Employer employer;

    // Getters and Setters
}


---

3. Repositories

public interface EmployerRepository extends JpaRepository<Employer, Integer> {}
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {}


---

4. Controller for CRUD

@RestController
@RequestMapping("/api")
public class EmployerEmployeeController {

    @Autowired
    private EmployerRepository employerRepo;

    @Autowired
    private EmployeeRepository employeeRepo;

    // Create Employer
    @PostMapping("/employers")
    public Employer addEmployer(@RequestBody Employer employer) {
        return employerRepo.save(employer);
    }

    // Add Employee under Employer
    @PostMapping("/employers/{id}/employees")
    public Employee addEmployee(@PathVariable Integer id, @RequestBody Employee employee) {
        Employer employer = employerRepo.findById(id).orElseThrow();
        employee.setEmployer(employer);
        return employeeRepo.save(employee);
    }

    // Get all Employers
    @GetMapping("/employers")
    public List<Employer> getEmployers() {
        return employerRepo.findAll();
    }

    // Get Employees of one Employer
    @GetMapping("/employers/{id}/employees")
    public List<Employee> getEmployees(@PathVariable Integer id) {
        return employeeRepo.findAll().stream()
                .filter(e -> e.getEmployer().getEmployerId().equals(id))
                .toList();
    }

    // Delete an Employee
    @DeleteMapping("/employees/{id}")
    public void deleteEmployee(@PathVariable Integer id) {
        employeeRepo.deleteById(id);
    }
}


---

5. application.properties

spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=true


---

Do you want a full ZIP file of this project to download and run directly?
