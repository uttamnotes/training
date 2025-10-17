Excellent choice 👍 — combining **Core Java**, **Collections Framework**, and **Exception Handling** gives students a **realistic software-like scenario**.

Here’s a **comprehensive Java demo** — not trivial, but still clear enough to teach in class.
It models a **Student Course Registration System** using `ArrayList`, `HashMap`, custom exceptions, and robust exception handling.

---

### 🧩 Concept Overview

* Use of **POJO classes** (`Student`, `Course`)
* Manage data with **Collections Framework** (`ArrayList`, `HashMap`)
* Use **custom exceptions** for validation (`CourseFullException`, `StudentNotFoundException`)
* Apply **try-catch-finally** to handle errors gracefully

---

### 💻 Full Java Code

```java
import java.util.*;

// Custom Exception: when a student is not found
class StudentNotFoundException extends Exception {
    public StudentNotFoundException(String message) {
        super(message);
    }
}

// Custom Exception: when a course has reached max capacity
class CourseFullException extends Exception {
    public CourseFullException(String message) {
        super(message);
    }
}

// POJO class for Student
class Student {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() { return id; }
    public String getName() { return name; }

    @Override
    public String toString() {
        return id + " - " + name;
    }
}

// POJO class for Course
class Course {
    private String code;
    private String title;
    private int capacity;
    private List<Student> enrolledStudents;

    public Course(String code, String title, int capacity) {
        this.code = code;
        this.title = title;
        this.capacity = capacity;
        this.enrolledStudents = new ArrayList<>();
    }

    public String getCode() { return code; }
    public String getTitle() { return title; }

    // Method to enroll a student
    public void enroll(Student student) throws CourseFullException {
        if (enrolledStudents.size() >= capacity) {
            throw new CourseFullException("Course " + title + " is full!");
        }
        enrolledStudents.add(student);
        System.out.println("✅ " + student.getName() + " enrolled in " + title);
    }

    public List<Student> getEnrolledStudents() {
        return enrolledStudents;
    }

    @Override
    public String toString() {
        return code + " - " + title + " (Capacity: " + capacity + ")";
    }
}

// Main Manager class using Collections
class RegistrationSystem {
    private Map<Integer, Student> studentMap;
    private Map<String, Course> courseMap;

    public RegistrationSystem() {
        studentMap = new HashMap<>();
        courseMap = new HashMap<>();
    }

    // Add a new student
    public void addStudent(Student s) {
        studentMap.put(s.getId(), s);
    }

    // Add a new course
    public void addCourse(Course c) {
        courseMap.put(c.getCode(), c);
    }

    // Register student to course
    public void registerStudent(int studentId, String courseCode)
            throws StudentNotFoundException, CourseFullException {

        Student student = studentMap.get(studentId);
        Course course = courseMap.get(courseCode);

        if (student == null) {
            throw new StudentNotFoundException("No student with ID " + studentId);
        }

        if (course == null) {
            System.out.println("❌ Invalid course code: " + courseCode);
            return;
        }

        course.enroll(student);
    }

    // Display all enrollments
    public void displayEnrollments() {
        System.out.println("\n=== COURSE ENROLLMENTS ===");
        for (Course course : courseMap.values()) {
            System.out.println(course.getTitle() + ":");
            for (Student s : course.getEnrolledStudents()) {
                System.out.println("  - " + s);
            }
        }
    }
}

public class CollegeApp {
    public static void main(String[] args) {

        RegistrationSystem system = new RegistrationSystem();

        // Create students
        system.addStudent(new Student(101, "Amit"));
        system.addStudent(new Student(102, "Priya"));
        system.addStudent(new Student(103, "Rahul"));

        // Create courses
        system.addCourse(new Course("CS101", "Data Structures", 2));
        system.addCourse(new Course("CS102", "Operating Systems", 2));

        try {
            // Successful registrations
            system.registerStudent(101, "CS101");
            system.registerStudent(102, "CS101");

            // This will trigger CourseFullException
            system.registerStudent(103, "CS101");

        } catch (StudentNotFoundException e) {
            System.out.println("⚠️ Student Error: " + e.getMessage());
        } catch (CourseFullException e) {
            System.out.println("⚠️ Course Error: " + e.getMessage());
        } catch (Exception e) {
            System.out.println("⚠️ Unexpected error: " + e);
        } finally {
            System.out.println("\n✅ Enrollment process complete.\n");
        }

        // Display all enrollments
        system.displayEnrollments();
    }
}
```

---

### 🧠 Key Takeaways

| Concept             | Demonstrated In                                   |
| ------------------- | ------------------------------------------------- |
| `ArrayList`         | To store enrolled students                        |
| `HashMap`           | To manage students and courses efficiently        |
| Custom Exceptions   | `CourseFullException`, `StudentNotFoundException` |
| Exception Handling  | `try-catch-finally`                               |
| OOP Concepts        | Encapsulation, Abstraction                        |
| Real-World Use Case | Course registration system                        |

---

### 🧪 Sample Output

```
✅ Amit enrolled in Data Structures
✅ Priya enrolled in Data Structures
⚠️ Course Error: Course Data Structures is full!

✅ Enrollment process complete.


=== COURSE ENROLLMENTS ===
Data Structures:
  - 101 - Amit
  - 102 - Priya
Operating Systems:
```

---

Would you like me to make this available as a **downloadable `.java` file** (ready to compile and run in Eclipse)?
