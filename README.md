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
