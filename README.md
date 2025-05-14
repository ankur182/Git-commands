@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeRepository employeeRepository;

    // Get all employees
    @GetMapping
    public List<Employee> getAllEmployees() {
        return employeeRepository.findAll();
    }

    // Get employee by ID
    @GetMapping("/{id}")
    public ResponseEntity<Employee> getEmployeeById(@PathVariable int id) {
        Optional<Employee> emp = employeeRepository.findById(id);
        return emp.map(ResponseEntity::ok).orElse(ResponseEntity.notFound().build());
    }

    // Get all employees by employer ID
    @GetMapping("/employer/{employerId}")
    public List<Employee> getByEmployerId(@PathVariable int employerId) {
        return employeeRepository.findByEmployerEmployerId(employerId);
    }
}
