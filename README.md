Great — here's an updated and complete setup so you can fetch both Employers and their Employees using Spring Boot and H2, following a proper OneToMany (Employer → Employee) structure.


---

Updated Requirements

Employer: employerId, panNo, estDate, location, and a list of employees

Employee: empId, name, job, salary, and reference to employer

You want to fetch all Employers with their Employees

Also fetch all Employees with their Employer details



---

Project Structure

src/
└── main/
    ├── java/
    │   └── com/example/demo/
    │       ├── controller/
    │       │   ├── EmployerController.java
    │       │   └── EmployeeController.java
    │       ├── entity/
    │       │   ├── Employer.java
    │       │   └── Employee.java
    │       ├── repository/
    │       │   ├── EmployerRepository.java
    │       │   └── EmployeeRepository.java
    │       └── DemoApplication.java
    └── resources/
        └── application.properties


---

1. Employer.java

package com.example.demo.entity;

import jakarta.persistence.*;
import java.util.*;

@Entity
public class Employer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int employerId;

    private String panNo;
    private Date estDate;
    private String location;

    @OneToMany(mappedBy = "employer", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Employee> employees = new ArrayList<>();

    // Getters and Setters
}


---

2. Employee.java

package com.example.demo.entity;

import jakarta.persistence.*;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int empId;

    private String name;
    private String job;
    private double salary;

    @ManyToOne
    @JoinColumn(name = "employer_id", nullable = false)
    private Employer employer;

    // Getters and Setters
}


---

3. EmployerRepository.java

package com.example.demo.repository;

import com.example.demo.entity.Employer;
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployerRepository extends JpaRepository<Employer, Integer> {
}


---

4. EmployeeRepository.java

package com.example.demo.repository;

import com.example.demo.entity.Employee;
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
}


---

5. EmployerController.java

package com.example.demo.controller;

import com.example.demo.entity.Employer;
import com.example.demo.repository.EmployerRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/employers")
public class EmployerController {

    @Autowired
    private EmployerRepository employerRepo;

    @GetMapping
    public List<Employer> getAllEmployers() {
        return employerRepo.findAll();
    }

    @GetMapping("/{id}")
    public Employer getEmployerById(@PathVariable int id) {
        return employerRepo.findById(id).orElse(null);
    }
}


---

6. EmployeeController.java

package com.example.demo.controller;

import com.example.demo.entity.Employee;
import com.example.demo.repository.EmployeeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeRepository employeeRepo;

    @GetMapping
    public List<Employee> getAllEmployees() {
        return employeeRepo.findAll();
    }

    @GetMapping("/{id}")
    public Employee getEmployeeById(@PathVariable int id) {
        return employeeRepo.findById(id).orElse(null);
    }
}


---

7. application.properties

spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update


---

8. DemoApplication.java

package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}


---

Postman Endpoints to Use

Get all Employers with Employees:
GET http://localhost:8080/employers

Get specific Employer:
GET http://localhost:8080/employers/{id}

Get all Employees with Employer details:
GET http://localhost:8080/employees

Get specific Employee:
GET http://localhost:8080/employees/{id}



---

Let me know if you'd like:

POST/PUT APIs to add data dynamically

A zip file of this entire project

DTOs to avoid recursion in JSON output


Shall I generate a .zip or POST method too?
