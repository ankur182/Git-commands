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
