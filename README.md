@PostMapping("/employers/{id}/detach")
public ResponseEntity<?> detachEmployer(@PathVariable Integer id) {
    Employer employer = entityManager.find(Employer.class, id);
    if (employer == null) {
        return ResponseEntity.notFound().build();
    }

    entityManager.detach(employer); // CascadeType.DETACH detaches children too

    // Store in-memory for demo purposes
    this.detachedEmployer = employer;

    return ResponseEntity.ok("Employer with ID " + id + " has been detached.");
}



ohkhhn



@PostMapping("/employers/merge")
public ResponseEntity<?> mergeEmployer() {
    if (detachedEmployer == null) {
        return ResponseEntity.badRequest().body("No detached employer found to merge.");
    }

    // Sample update (you could pass a body instead)
    detachedEmployer.setLocation("MergedCity");
    if (!detachedEmployer.getEmployees().isEmpty()) {
        detachedEmployer.getEmployees().get(0).setSalary(99999.0);
    }

    Employer merged = entityManager.merge(detachedEmployer);
    detachedEmployer = null; // Clear after merging

    return ResponseEntity.ok(merged);
}
