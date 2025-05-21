To run your Hibernate + Spring Boot program and check how EntityGraph works with Employer and Employee, follow these steps:


---

1. Ensure Your Entities Are Set Correctly

Employer.java

@Entity
public class Employer {

    @Id
    private int employerId;

    private String panNo;
    private LocalDate estDate;
    private String location;

    @OneToMany(mappedBy = "employer", fetch = FetchType.LAZY)
    private List<Employee> employees;

    // Getters & Setters
}

Employee.java

@Entity
public class Employee {

    @Id
    private int empId;
    private String name;
    private int age;
    private double salary;

    @ManyToOne
    @JoinColumn(name = "employer_id")
    private Employer employer;

    // Getters & Setters
}


---

2. Add EntityGraph in EmployerRepository

public interface EmployerRepository extends JpaRepository<Employer, Integer> {

    // This EntityGraph fetches employees along with employers to avoid N+1 problem
    @EntityGraph(attributePaths = "employees")
    @Query("SELECT e FROM Employer e WHERE e.employerId = :id")
    Optional<Employer> findWithEmployeesById(@Param("id") Integer id);
}


---

3. Create a REST Controller to Test It

EmployerController.java

@RestController
@RequestMapping("/employers")
public class EmployerController {

    @Autowired
    private EmployerRepository employerRepository;

    @GetMapping("/{id}")
    public ResponseEntity<Employer> getEmployerWithEmployees(@PathVariable int id) {
        Optional<Employer> employer = employerRepository.findWithEmployeesById(id);
        return employer.map(ResponseEntity::ok)
                       .orElse(ResponseEntity.notFound().build());
    }
}


---

4. Run the Program

Use the HelloWorldSpringApplication.java with SpringApplication.run(...).

Make sure your Liquibase has run and tables + data are created (check DB logs).

Run the Spring Boot app from your IDE or using mvn spring-boot:run.



---

5. Test the Endpoint

Open browser or Postman and go to:

http://localhost:8080/employers/1

You should get an output like:

{
  "employerId": 1,
  "panNo": "ABC023",
  "estDate": "2020-01-01",
  "location": "Delhi",
  "employees": [
    { "empId": 1, "name": "Ankur", ... },
    { "empId": 2, "name": "Anjali", ... },
    ...
  ]
}

This confirms the EntityGraph is working and fetching employees eagerly.


---

Let me know if you want a version that avoids circular references (like using DTOs or @JsonIgnore).
