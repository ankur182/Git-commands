@GetMapping("/employee/{name}")
public ResponseEntity<?> getEmployeeByName(@PathVariable String name) {
    Employee employee = employeeRepository.findByEmpName(name);
    if (employee == null) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Employee not found");
    }

    Map<String, Object> response = new HashMap<>();
    response.put("employeeName", employee.getEmpName());
    response.put("estDate", employee.getEstDate());
    response.put("location", employee.getLocation());
    response.put("employerId", employee.getEmployer().getEmployerId());
    response.put("panNo", employee.getEmployer().getPanNo());

    return ResponseEntity.ok(response);
}
