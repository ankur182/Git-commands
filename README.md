1. GET Method in Spring
The GET method is used to retrieve data from a server without making any changes to the resource. It is commonly used to fetch data from the server.

Example of GET method in Spring:
Let's say we have a Spring Boot application where we are building an API to fetch a list of users.

Controller class:

java
Copy
Edit
package com.example.demo.controller;

import com.example.demo.model.User;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping
    public List<User> getAllUsers() {
        return List.of(
                new User(1, "John Doe", "john.doe@example.com"),
                new User(2, "Jane Smith", "jane.smith@example.com")
        );
    }
}
Model class (User.java):

java
Copy
Edit
package com.example.demo.model;

public class User {
    private int id;
    private String name;
    private String email;

    public User(int id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    // Getters and Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
In this example:

The @GetMapping annotation is used to handle HTTP GET requests.

When a GET request is made to /api/users, the getAllUsers() method is called.

It returns a list of User objects as a response.

2. POST Method in Spring
The POST method is used to submit data to be processed by the server, such as creating or updating resources.

Example of POST method in Spring:
In this example, we'll build an API that allows users to create new users using the POST method.

Controller class:

java
Copy
Edit
package com.example.demo.controller;

import com.example.demo.model.User;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public String createUser(@RequestBody User user) {
        // For demonstration, we're just returning a message instead of actually saving the user.
        return "User created: " + user.getName();
    }
}
In this example:

The @PostMapping annotation is used to handle HTTP POST requests.

The createUser() method takes a User object as input (using the @RequestBody annotation to bind the request body to the method parameter).

The User object contains the details of the new user to be created.

Sending a POST request:
To create a new user, you would send a POST request to /api/users with the user details in the body of the request.

Example Request Body (JSON):

json
Copy
Edit
{
  "id": 3,
  "name": "Alice Brown",
  "email": "alice.brown@example.com"
}
When the POST request is made with this data, the server would respond with a message like:

sql
Copy
Edit
User created: Alice Brown
