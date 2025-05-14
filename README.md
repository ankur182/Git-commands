@RestController
@RequestMapping("/api")
public class EmployerEmployeeController {

    @Autowired
    private EmployerRepository employerRepo;

    @Autowired
    private EmployeeRepository employeeRepo;

    // Add Employer
    @PostMapping("/employers")
    public Employer createEmployer(@RequestBody Employer employer) {
        return employerRepo.save(employer);
    }

    // Add Employee to Employer
    @PostMapping("/employers/{id}/employees")
    public Employee addEmployee(@PathVariable Integer id, @RequestBody Employee employee) {
        Employer employer = employerRepo.findById(id).orElse(null);
        if (employer != null) {
            employee.setEmployer(employer);
            return employeeRepo.save(employee);
        }
        return null;
    }

    // Get All Employers
    @GetMapping("/employers")
    public List<Employer> getAllEmployers() {
        return employerRepo.findAll();
    }

    // Get All Employees for a given Employer
    @GetMapping("/employers/{id}/employees")
    public List<Employee> getEmployeesByEmployer(@PathVariable Integer id) {
        return employeeRepo.findByEmployerEmployerId(id);
    }

    // Delete Employee
    @DeleteMapping("/employees/{id}")
    public void deleteEmployee(@PathVariable Integer id) {
        employeeRepo.deleteById(id);
    }
}
