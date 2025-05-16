Great! Let’s now focus only on CascadeType.PERSIST to understand it thoroughly.


---

Scenario: Only CascadeType.PERSIST

@OneToMany(mappedBy = "employer", cascade = CascadeType.PERSIST)
@JsonManagedReference
private List<Employee> employees = new ArrayList<>();


---

What it does:

When you call save() on the Employer, all new (unsaved) Employee objects associated with it will also be automatically saved to the database.


---

Postman Test Case (POST Request)

Endpoint:

POST http://localhost:8080/api/employers

Request Body:

{
  "employerId": 1,
  "panNo": "ABCPK1234X",
  "estDate": "2022-01-01",
  "location": "Delhi",
  "employees": [
    {
      "empId": 101,
      "name": "Ankur",
      "age": 24,
      "salary": 50000
    }
  ]
}

Expected Result:

Employer will be inserted in the employer table.

Employee(s) will also be inserted in the employee table automatically.

You don't need to save Employee separately via employeeRepository.



---

What if CascadeType.PERSIST is NOT used?

Then you will get an error like:

javax.persistence.PersistenceException: 
org.hibernate.TransientPropertyValueException: 
object references an unsaved transient instance - save the transient instance before flushing

Reason:

JPA is trying to save the Employer.

But it sees related Employees that haven’t been saved yet.

Since there's no cascade = PERSIST, it won't automatically persist Employees.

So, it throws an error saying: "you’re referencing an unsaved object."



---

Quick Notes:

Case	Cascade.PERSIST Present	Cascade.PERSIST Absent

Employer saved with unsaved employees	Works fine – all saved	Fails – throws TransientPropertyValueException
Employer saved with already saved employees	Works	Works
Only employee saved	No effect on employer	No effect on employer



---

Conclusion:

Use cascade = CascadeType.PERSIST when you want to automatically persist the child (Employee) while saving the parent (Employer). Otherwise, you'll need to manually save all Employees before saving the Employer.


---

Let me know if you want to test this practically or move to the next cascade type like MERGE.


