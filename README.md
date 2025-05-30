@PostMapping("/employers/{id}/detach")
public ResponseEntity<?> detachEmployer(@PathVariable Integer id) {
    Employer employer = entityManager.find(Employer.class, id);
    if (employer == null) {
        return ResponseEntity.notFound().build();
    }

    entityManager.detach(employer);

    boolean isDetached = !entityManager.contains(employer);
    this.detachedEmployer = employer;

    String message = isDetached
            ? "✅ Employer with ID " + id + " has been successfully detached."
            : "❌ Detach failed for Employer with ID " + id;

    return ResponseEntity.ok(message);
}
_-----++++++++--6-666667--+++---+-


@PostMapping("/employers/merge")
public ResponseEntity<?> mergeEmployer() {
    if (detachedEmployer == null) {
        return ResponseEntity.badRequest().body("❌ No detached employer found. Please call /detach first.");
    }

    // Example: Simulate an update before merge (you can skip this or accept updates via @RequestBody)
    detachedEmployer.setLocation("UpdatedCity");
    if (!detachedEmployer.getEmployees().isEmpty()) {
        detachedEmployer.getEmployees().get(0).setSalary(75000.0); // Demo update
    }

    Employer merged = entityManager.merge(detachedEmployer);

    // Optionally flush to force update now
    entityManager.flush();

    // Clear reference after merge
    detachedEmployer = null;

    return ResponseEntity.ok("✅ Detached Employer has been successfully merged and updated.");
}
