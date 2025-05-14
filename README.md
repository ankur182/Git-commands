OST method too?
package com.example.demo.controller;

import com.example.demo.model.Employer;
import com.example.demo.repository.EmployerRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/employers")
public class EmployerController {

    @Autowired
    private EmployerRepository employerRepository;

    @PostMapping
    public Employer createEmployer(@RequestBody Employer employer) {
        return employerRepository.save(employer);
    }

    @GetMapping
    public List<Employer> getAllEmployers() {
        return employerRepository.findAll();
    }
}
