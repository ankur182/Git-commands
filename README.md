To achieve the goal of returning both Employee and Employer data for a given employee name in a GET endpoint, you need to:

1. Have a proper mapping between Employee and Employer entities (likely many-to-one).


2. Use a DTO (Data Transfer Object) that combines the relevant fields.


3. Implement the GET endpoint in the EmployeeController.



Assuming your entity relationships are like this:

Employee.java

@Entity
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long empId;

    private String name;
    private int age;
    private double salary;

    @ManyToOne
    @JoinColumn(name = "employer_id")
    private Employer employer;

    // getters and setters
}

Employer.java

@Entity
public class Employer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long employerId;

    private String panNo;
    private Date estDate;
    private String location;

    // getters and setters
}

EmployeeData.java (DTO)

public class EmployeeData {
    private String name;
    private int age;
    private double salary;
    private EmployerData employer;

    public EmployeeData(String name, int age, double salary, EmployerData employer) {
        this.name = name;
        this.age = age;
        this.salary = salary;
        this.employer = employer;
    }

    // getters and setters
}

EmployerData.java (DTO)

public class EmployerData {
    private Long employerId;
    private String panNo;

    public EmployerData(Long employerId, String panNo) {
        this.employerId = employerId;
        this.panNo = panNo;
    }

    // getters and setters
}

EmployeeRepository.java

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    Optional<Employee> findByName(String name);
}

EmployeeController.java

@RestController
public class EmployeeController {

    @Autowired
    private EmployeeRepository employeeRepository;

    @GetMapping("/employee/{name}")
    public ResponseEntity<EmployeeData> getEmployeeByName(@PathVariable String name) {
        Optional<Employee> optionalEmployee = employeeRepository.findByName(name);
        if (optionalEmployee.isPresent()) {
            Employee emp = optionalEmployee.get();
            Employer empEmployer = emp.getEmployer();
            EmployerData employerData = new EmployerData(empEmployer.getEmployerId(), empEmployer.getPanNo());
            EmployeeData response = new EmployeeData(emp.getName(), emp.getAge(), emp.getSalary(), employerData);
            return ResponseEntity.ok(response);
        } else {
            return ResponseEntity.notFound().build();
        }
    }
}

If you want me to verify the code in the uploaded file, please let me know which file you want me to look into or share the code snippet you want help with.
