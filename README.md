@DeleteMapping("/employers/{id}/remove")
@Transactional
public ResponseEntity<Void> removeEmployer(@PathVariable Integer id) {
    Employer employer = entityManager.find(Employer.class, id);
    if (employer != null) {
        entityManager.remove(employer);  // Will also remove employees if cascade is configured
        return ResponseEntity.ok().build();
    } else {
        return ResponseEntity.notFound().build();
    }
}
