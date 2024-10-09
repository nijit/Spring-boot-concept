In Spring Data JPA, **Query by Example (QBE)** is a powerful feature that allows you to construct queries based on the properties of an instance of a class. It is useful when you need dynamic query generation based on user input without writing explicit queries.

Spring Data JPA provides the `QueryByExampleExecutor` interface, which offers methods like `findAll()`, `findOne()`, `count()`, and `exists()`, allowing you to query based on an example instance.

### Steps to use Query by Example:
1. **Define an entity.**
2. **Create a repository that extends `JpaRepository` and `QueryByExampleExecutor`.**
3. **Use the example instance to execute dynamic queries.**

### Example:

Let's create a sample `Employee` entity and repository to demonstrate `QueryByExampleExecutor`.

#### 1. **Entity Class:**

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Employee {

    @Id
    private Long id;
    private String firstName;
    private String lastName;
    private String department;

    // Getters and Setters

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }
}
```

#### 2. **Repository Interface:**
Extend both `JpaRepository` and `QueryByExampleExecutor`.

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.repository.query.QueryByExampleExecutor;

public interface EmployeeRepository extends JpaRepository<Employee, Long>, QueryByExampleExecutor<Employee> {
}
```

#### 3. **Service Layer:**
Use `Query by Example` to search for employees by example.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.Example;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    public List<Employee> searchEmployees(String firstName, String lastName, String department) {
        // Create an example employee with the search criteria
        Employee exampleEmployee = new Employee();
        exampleEmployee.setFirstName(firstName);
        exampleEmployee.setLastName(lastName);
        exampleEmployee.setDepartment(department);

        // Create the Example object, ignoring null fields (to allow partial matching)
        Example<Employee> example = Example.of(exampleEmployee);

        // Perform the query
        return employeeRepository.findAll(example);
    }
}
```

#### 4. **Controller Layer:**
You can create a controller to expose this search functionality through an API.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @GetMapping("/search")
    public List<Employee> searchEmployees(
            @RequestParam(required = false) String firstName,
            @RequestParam(required = false) String lastName,
            @RequestParam(required = false) String department) {

        return employeeService.searchEmployees(firstName, lastName, department);
    }
}
```

### Explanation:

1. **Entity**: `Employee` class represents the entity with properties like `firstName`, `lastName`, and `department`.
   
2. **Repository**: `EmployeeRepository` extends both `JpaRepository` and `QueryByExampleExecutor`, allowing the repository to use example-based queries.
   
3. **Example Object**: In the `EmployeeService`, we create an instance of `Employee` based on the input and pass it to the `Example.of()` method to construct the query dynamically. Fields that are `null` are ignored, allowing for partial matches.

4. **Controller**: The `/search` endpoint allows the user to pass optional parameters (`firstName`, `lastName`, `department`). The `searchEmployees()` method returns a list of employees matching the provided fields.

#### Example Query:
- If you hit `/search?firstName=John`, it will return all employees with the first name "John."
- If you hit `/search?department=IT`, it will return all employees in the "IT" department.

### Notes:
- You can also customize the matching strategy by using `ExampleMatcher` to specify whether matches should be case-insensitive, match only the start of a string, etc.

#### ExampleMatcher:

```java
import org.springframework.data.domain.ExampleMatcher;

ExampleMatcher matcher = ExampleMatcher.matching()
    .withIgnoreCase("firstName")
    .withStringMatcher(ExampleMatcher.StringMatcher.STARTING);  // First name starts with

Example<Employee> example = Example.of(exampleEmployee, matcher);
```

This allows you to control how each field is matched.
