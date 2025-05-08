package com.example.helloworld.service;

import com.example.helloworld.model.Employee;
import com.example.helloworld.repository.EmployeeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class EmployeeService {

    @Autowired
    private EmployeeRepository repository;

    public Employee save(Employee employee) {
        return repository.save(employee);
    }

    public List<Employee> getAll() {
        return repository.findAll();
    }

    public Optional<Employee> getById(Long id) {
        return repository.findById(id);
    }

    public Employee update(Long id, Employee updated) {
        Employee emp = repository.findById(id).orElseThrow();
        emp.setName(updated.getName());
        emp.setDepartment(updated.getDepartment());
        emp.setSalary(updated.getSalary());
        return repository.save(emp);
    }

    public void delete(Long id) {
        repository.deleteById(id);
    }
}


Based on your current Spring Boot project structure (as seen in the image), here's how to structure your project to add the Employee CRUD functionality with H2 database:


---

Updated Project Structure

src/
 └── main/
     └── java/
         └── com.example.helloworld/
             ├── controller/
             │   └── EmployeeController.java
             ├── model/
             │   └── Employee.java
             ├── repository/
             │   └── EmployeeRepository.java
             ├── HelloWorldSpringApplication.java
     └── resources/
         ├── application.properties
         └── static/


---

1. Employee Entity (model/Employee.java)

package com.example.helloworld.model;

import jakarta.persistence.*;

@Entity
public class Employee {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String department;
    private double salary;

    public Employee() {}

    public Employee(String name, String department, double salary) {
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    // Getters and setters
    // ...
}


---

2. Employee Repository (repository/EmployeeRepository.java)

package com.example.helloworld.repository;

import com.example.helloworld.model.Employee;
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}


---

3. Employee Controller (controller/EmployeeController.java)

package com.example.helloworld.controller;

import com.example.helloworld.model.Employee;
import com.example.helloworld.repository.EmployeeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeRepository employeeRepository;

    @GetMapping
    public List<Employee> getAllEmployees() {
        return employeeRepository.findAll();
    }

    @PostMapping
    public Employee createEmployee(@RequestBody Employee employee) {
        return employeeRepository.save(employee);
    }

    @GetMapping("/{id}")
    public Employee getEmployeeById(@PathVariable Long id) {
        return employeeRepository.findById(id).orElse(null);
    }

    @PutMapping("/{id}")
    public Employee updateEmployee(@PathVariable Long id, @RequestBody Employee newEmp) {
        return employeeRepository.findById(id).map(emp -> {
            emp.setName(newEmp.getName());
            emp.setDepartment(newEmp.getDepartment());
            emp.setSalary(newEmp.getSalary());
            return employeeRepository.save(emp);
        }).orElse(null);
    }

    @DeleteMapping("/{id}")
    public String deleteEmployee(@PathVariable Long id) {
        employeeRepository.deleteById(id);
        return "Employee deleted with id: " + id;
    }
}


---

4. application.properties

spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.h2.console.enabled=true


---

Once this is ready, let me know and I’ll guide you through Postman API testing step-by-step. Do you want me to write the JSON payloads next?

