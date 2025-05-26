@GetMapping("/employee/{name}")
public ResponseEntity<?> getEmployeeByName(@PathVariable String name) {
    return employeeRepository.findByName(name)
            .map(emp -> {
                Map<String, Object> response = new HashMap<>();
                response.put("name", emp.getName());
                response.put("age", emp.getAge());
                response.put("salary", emp.getSalary());

                Employer employer = emp.getEmployer();
                if (employer != null) {
                    response.put("employerId", employer.getEmployerId());
                    response.put("panNo", employer.getPanNo());
                }

                return ResponseEntity.ok(response);
            })
            .orElse(ResponseEntity.status(HttpStatus.NOT_FOUND)
                    .body("Employee not found"));
}
