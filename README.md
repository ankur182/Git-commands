@Override
public Category updateCategory(Category category, Long categoryId) {
    Optional<Category> optionalCategory = categories.stream()
        .filter(c -> c.getCategoryId().equals(categoryId))
        .findFirst();

    if (optionalCategory.isPresent()) {
        Category existingCategory = optionalCategory.get();
        existingCategory.setCategoryName(category.getCategoryName());
        return existingCategory;
    } else {
        throw new ResponseStatusException(HttpStatus.NOT_FOUND, "Category not found");
    }
}
