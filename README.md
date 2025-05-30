import org.springframework.transaction.annotation.Transactional;

@DeleteMapping("/employers/remove")
@Transactional
public ResponseEntity<?> removeDetachedEmployer() {
    if (detachedEmployer != null) {
        // First merge to attach it to persistence context
        Employer managed = entityManager.merge(detachedEmployer);
        // Now remove the managed entity
        entityManager.remove(managed);
        detachedEmployer = null; // Clear the reference
        return ResponseEntity.ok("Detached Employer has been successfully removed");
    } else {
        return ResponseEntity.badRequest().body("No detached employer available to remove");
    }
}
