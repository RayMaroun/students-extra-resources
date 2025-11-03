# 📦 Java Package Organization System

## A Step-by-Step Tutorial for Package Structure, Naming Conventions & Best Practices

---

## 🎯 Project Overview

We're building a School Management System that teaches proper Java package organization. You'll learn how professional Java developers structure their code, use packages to organize related classes, and follow industry naming conventions. This is how REAL Java applications are organized!

**What You'll Master:**

- Package declaration and structure
- Naming conventions (reverse domain notation)
- Import statements and visibility
- Package-private vs public access
- Organizing related classes
- Best practices for package structure
- Multi-package project organization

---

## 📚 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `SchoolManagementSystem`
4. Location: `~/pluralsight/workbook-4` (or `C:/pluralsight/workbook-4` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share Project to GitHub Immediately

1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `SchoolManagementSystem`
3. Description: "Learning Java packages, organization, and naming conventions"
4. Click **Share**
5. In the next dialog, click **Add**

**Why share now?** Good habits start from day one - version control everything!

---

## 🤔 Part 1: Understanding Packages - Why We Need Them

### Step 2: The Problem Without Packages

First, let's see what happens WITHOUT proper package organization.

Create a class directly in `src/main/java` (no package):

```java
public class Teacher {
    private String name;

    public Teacher(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

Create another class in the same location:

```java
public class Student {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

Now create a Main class:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("=== WITHOUT PACKAGES ===");
        System.out.println("All classes are in the same folder - messy!");
        System.out.println("Imagine having 100 classes all mixed together!");

        Teacher teacher = new Teacher("Ms. Johnson");
        Student student = new Student("Alice");

        System.out.println("Teacher: " + teacher.getName());
        System.out.println("Student: " + student.getName());
    }
}
```

**🔍 What's happening? The Problem:**

Without packages, it's like having all your clothes thrown in one giant pile instead of organized in drawers and closets:

- **No Organization** - Everything is in one place
- **Name Conflicts** - Can't have two classes with same name
- **No Access Control** - Everything sees everything
- **Hard to Find Things** - Imagine 500 classes in one folder!
- **No Logical Grouping** - Teachers mixed with Students mixed with Courses

**Think of it like this:**

- Without packages = All papers thrown on your desk
- With packages = Papers organized in labeled folders in filing cabinets

**▶️ Run Main** to see it works, but it's not organized!

### 🔄 Commit Your Work:

1. Click **Commit** button (✓) or press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Initial setup - demonstrating the problem without packages"`
3. Click **Commit and Push**

---

## 📂 Part 2: Creating Your First Package Structure

### Step 3: Delete the Unorganized Classes

Delete the three classes we just created (Teacher, Student, Main) - we're going to reorganize properly!

### Step 4: Create a Professional Package Structure

Let's create a proper package structure. In IntelliJ:

1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight.school`
4. Click **OK**

**🔍 What's happening? Package Naming Convention:**

`com.pluralsight.school` follows the **Reverse Domain Name Convention**:

- **`com`** = Commercial organization (could be org, edu, gov, etc.)
- **`pluralsight`** = Company/organization name
- **`school`** = Project/application name

**Why reverse domain?**

- Domain names are globally unique (only one pluralsight.com exists)
- Reversing prevents conflicts (com.google vs com.microsoft)
- Industry standard that every Java developer follows
- Like a unique address for your code

**Other examples:**

- Google: `com.google.maps`
- Apache: `org.apache.commons`
- University: `edu.harvard.cs50`

### Step 5: Create Sub-packages for Organization

Create these sub-packages under `com.pluralsight.school`:

1. **Models package** (for data classes):

   - Right-click on `com.pluralsight.school`
   - New → Package
   - Name: `models` (so full path is `com.pluralsight.school.models`)

2. **Services package** (for business logic):

   - Right-click on `com.pluralsight.school`
   - New → Package
   - Name: `services`

3. **Utils package** (for utility/helper classes):

   - Right-click on `com.pluralsight.school`
   - New → Package
   - Name: `utils`

4. **Main package** (for application entry point):
   - Right-click on `com.pluralsight.school`
   - New → Package
   - Name: `main`

Your structure should look like:

```
src/main/java/
└── com/
    └── pluralsight/
        └── school/
            ├── main/
            ├── models/
            ├── services/
            └── utils/
```

**🔍 What's happening? Package Organization:**

Think of packages like departments in a company:

- **models/** = Data Department (stores information)
  - Like filing cabinets with forms and records
  - Classes that represent "things" (Student, Teacher, Course)
- **services/** = Operations Department (does the work)
  - Like workers who process the forms
  - Classes that perform actions (EnrollmentService, GradeService)
- **utils/** = Support Department (helps everyone)
  - Like office supplies everyone uses
  - Helper classes (DateUtils, ValidationUtils)
- **main/** = Reception/Entry Point
  - Where everything starts
  - Contains the main class

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Created proper package structure with sub-packages"`
3. Click **Commit and Push**

---

## 🏗️ Part 3: Creating Classes in Packages

### Step 6: Create Model Classes

In the `models` package, create `Student.java`:

```java
package com.pluralsight.school.models;

public class Student {
    private int studentId;
    private String firstName;
    private String lastName;
    private int gradeLevel;
    private String email;

    // Constructor
    public Student(int studentId, String firstName, String lastName, int gradeLevel) {
        this.studentId = studentId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.gradeLevel = gradeLevel;
        this.email = generateEmail();
    }

    // Private helper method - only visible in this class
    private String generateEmail() {
        return firstName.toLowerCase() + "." + lastName.toLowerCase() + "@school.edu";
    }

    // Public getters - visible everywhere
    public int getStudentId() {
        return studentId;
    }

    public String getFullName() {
        return firstName + " " + lastName;
    }

    public int getGradeLevel() {
        return gradeLevel;
    }

    public String getEmail() {
        return email;
    }

    @Override
    public String toString() {
        return String.format("Student #%d: %s (Grade %d)",
            studentId, getFullName(), gradeLevel);
    }
}
```

In the same `models` package, create `Teacher.java`:

```java
package com.pluralsight.school.models;

import java.util.ArrayList;
import java.util.List;

public class Teacher {
    private int teacherId;
    private String firstName;
    private String lastName;
    private String subject;
    private List<String> certifications;

    public Teacher(int teacherId, String firstName, String lastName, String subject) {
        this.teacherId = teacherId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.subject = subject;
        this.certifications = new ArrayList<>();
    }

    public void addCertification(String certification) {
        certifications.add(certification);
    }

    public int getTeacherId() {
        return teacherId;
    }

    public String getFullName() {
        return "Mr./Ms. " + lastName;
    }

    public String getSubject() {
        return subject;
    }

    public List<String> getCertifications() {
        return new ArrayList<>(certifications); // Return a copy for safety
    }

    @Override
    public String toString() {
        return String.format("Teacher #%d: %s - %s",
            teacherId, getFullName(), subject);
    }
}
```

Create `Course.java` in `models`:

```java
package com.pluralsight.school.models;

public class Course {
    private String courseCode;
    private String courseName;
    private int credits;
    private Teacher instructor;
    private int maxStudents;
    private int currentEnrollment;

    public Course(String courseCode, String courseName, int credits, int maxStudents) {
        this.courseCode = courseCode;
        this.courseName = courseName;
        this.credits = credits;
        this.maxStudents = maxStudents;
        this.currentEnrollment = 0;
    }

    public void assignInstructor(Teacher instructor) {
        this.instructor = instructor;
    }

    public boolean hasSpace() {
        return currentEnrollment < maxStudents;
    }

    public boolean enrollStudent() {
        if (hasSpace()) {
            currentEnrollment++;
            return true;
        }
        return false;
    }

    // Getters
    public String getCourseCode() {
        return courseCode;
    }

    public String getCourseName() {
        return courseName;
    }

    public Teacher getInstructor() {
        return instructor;
    }

    public int getAvailableSeats() {
        return maxStudents - currentEnrollment;
    }

    @Override
    public String toString() {
        return String.format("%s: %s (%d credits) - %d/%d students",
            courseCode, courseName, credits, currentEnrollment, maxStudents);
    }
}
```

**🔍 What's happening? Package Declaration:**

```java
package com.pluralsight.school.models;
```

- **MUST be the first line** (except for comments)
- Tells Java "this class belongs to this package"
- Like putting a return address on an envelope
- Package name matches the folder structure exactly

**Import Statements:**

```java
import java.util.ArrayList;
import java.util.List;
```

- Goes AFTER package declaration
- Tells Java "I need to use classes from other packages"
- Like ordering supplies from another department
- Without import, you'd have to write the full name: `java.util.ArrayList`

**Access Between Classes in Same Package:**

- Classes in the same package can see each other
- No import needed for classes in same package
- Like coworkers in the same department

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added model classes with proper package declarations"`
3. Click **Commit and Push**

---

## 🔧 Part 4: Creating Service Classes

### Step 7: Create Service Layer

In the `services` package, create `EnrollmentService.java`:

```java
package com.pluralsight.school.services;

import com.pluralsight.school.models.Course;
import com.pluralsight.school.models.Student;
import com.pluralsight.school.models.Teacher;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class EnrollmentService {
    private Map<Integer, List<Course>> studentEnrollments;
    private Map<String, List<Student>> courseRosters;

    public EnrollmentService() {
        this.studentEnrollments = new HashMap<>();
        this.courseRosters = new HashMap<>();
    }

    public boolean enrollStudentInCourse(Student student, Course course) {
        // Check if course has space
        if (!course.hasSpace()) {
            System.out.println("Course " + course.getCourseCode() + " is full!");
            return false;
        }

        // Enroll the student
        if (course.enrollStudent()) {
            // Track student's courses
            studentEnrollments.computeIfAbsent(student.getStudentId(),
                k -> new ArrayList<>()).add(course);

            // Track course's students
            courseRosters.computeIfAbsent(course.getCourseCode(),
                k -> new ArrayList<>()).add(student);

            System.out.println("Successfully enrolled " + student.getFullName() +
                             " in " + course.getCourseName());
            return true;
        }

        return false;
    }

    public List<Course> getStudentCourses(Student student) {
        return studentEnrollments.getOrDefault(student.getStudentId(),
            new ArrayList<>());
    }

    public List<Student> getCourseRoster(Course course) {
        return courseRosters.getOrDefault(course.getCourseCode(),
            new ArrayList<>());
    }

    public void printStudentSchedule(Student student) {
        System.out.println("\n=== Schedule for " + student.getFullName() + " ===");
        List<Course> courses = getStudentCourses(student);

        if (courses.isEmpty()) {
            System.out.println("No courses enrolled");
        } else {
            for (Course course : courses) {
                System.out.println("- " + course);
            }
        }
    }
}
```

In `services`, create `GradeService.java`:

```java
package com.pluralsight.school.services;

import com.pluralsight.school.models.Course;
import com.pluralsight.school.models.Student;
import com.pluralsight.school.utils.GradeCalculator;

import java.util.HashMap;
import java.util.Map;

public class GradeService {
    // Store grades: StudentId -> CourseCode -> Grade
    private Map<Integer, Map<String, Double>> gradeBook;

    public GradeService() {
        this.gradeBook = new HashMap<>();
    }

    public void assignGrade(Student student, Course course, double grade) {
        // Validate grade using utility class (we'll create this)
        if (!GradeCalculator.isValidGrade(grade)) {
            System.out.println("Invalid grade: " + grade);
            return;
        }

        // Store the grade
        gradeBook.computeIfAbsent(student.getStudentId(), k -> new HashMap<>())
                .put(course.getCourseCode(), grade);

        char letterGrade = GradeCalculator.getLetterGrade(grade);
        System.out.printf("Assigned grade %.1f (%c) to %s for %s%n",
            grade, letterGrade, student.getFullName(), course.getCourseCode());
    }

    public Double getGrade(Student student, Course course) {
        Map<String, Double> studentGrades = gradeBook.get(student.getStudentId());
        if (studentGrades != null) {
            return studentGrades.get(course.getCourseCode());
        }
        return null;
    }

    public double calculateGPA(Student student) {
        Map<String, Double> studentGrades = gradeBook.get(student.getStudentId());
        if (studentGrades == null || studentGrades.isEmpty()) {
            return 0.0;
        }

        double total = 0;
        for (double grade : studentGrades.values()) {
            total += GradeCalculator.gradeToGPA(grade);
        }

        return total / studentGrades.size();
    }
}
```

**🔍 What's happening? Import Statements Explained:**

```java
import com.pluralsight.school.models.Course;
import com.pluralsight.school.models.Student;
```

**Types of imports:**

1. **Specific imports** (recommended):

   ```java
   import com.pluralsight.school.models.Student;
   ```

   - Imports one specific class
   - Clear what you're using
   - Best practice!

2. **Wildcard imports** (use sparingly):
   ```java
   import com.pluralsight.school.models.*;
   ```
   - Imports ALL classes from package
   - Can cause naming conflicts
   - Makes code less clear

**Why imports are needed:**

- Classes in different packages can't see each other automatically
- Import creates a "bridge" between packages
- Like getting a visitor pass to another department

**Package visibility:**

- `services` package can't directly see `models` package
- Must import to use Student, Teacher, Course
- Enforces organization and dependencies

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added service layer with enrollment and grade management"`
3. Click **Commit and Push**

---

## 🛠️ Part 5: Creating Utility Classes

### Step 8: Create Utility/Helper Classes

In the `utils` package, create `GradeCalculator.java`:

```java
package com.pluralsight.school.utils;

public class GradeCalculator {

    // Private constructor - this class should never be instantiated
    private GradeCalculator() {
        throw new IllegalStateException("Utility class - do not instantiate");
    }

    // All methods are public static - accessible from anywhere
    public static boolean isValidGrade(double grade) {
        return grade >= 0 && grade <= 100;
    }

    public static char getLetterGrade(double grade) {
        if (grade >= 90) return 'A';
        if (grade >= 80) return 'B';
        if (grade >= 70) return 'C';
        if (grade >= 60) return 'D';
        return 'F';
    }

    public static double gradeToGPA(double grade) {
        if (grade >= 90) return 4.0;
        if (grade >= 80) return 3.0;
        if (grade >= 70) return 2.0;
        if (grade >= 60) return 1.0;
        return 0.0;
    }

    public static String getGradeDescription(char letterGrade) {
        switch (letterGrade) {
            case 'A': return "Excellent";
            case 'B': return "Good";
            case 'C': return "Satisfactory";
            case 'D': return "Needs Improvement";
            case 'F': return "Failing";
            default: return "Invalid Grade";
        }
    }
}
```

In `utils`, create `IDGenerator.java`:

```java
package com.pluralsight.school.utils;

public class IDGenerator {
    // Static variables - shared across all uses
    private static int nextStudentId = 1000;
    private static int nextTeacherId = 100;
    private static int nextCourseNumber = 1;

    private IDGenerator() {
        // Prevent instantiation
    }

    public static synchronized int generateStudentId() {
        return nextStudentId++;
    }

    public static synchronized int generateTeacherId() {
        return nextTeacherId++;
    }

    public static synchronized String generateCourseCode(String subject) {
        String prefix = subject.substring(0, Math.min(3, subject.length())).toUpperCase();
        String code = prefix + String.format("%03d", nextCourseNumber++);
        return code;
    }

    // Reset methods for testing
    static void resetCounters() {
        nextStudentId = 1000;
        nextTeacherId = 100;
        nextCourseNumber = 1;
    }
}
```

**🔍 What's happening? Utility Classes Best Practices:**

**Why private constructor?**

```java
private GradeCalculator() {
    throw new IllegalStateException("Utility class");
}
```

- Prevents creating objects of this class
- Utility classes are just containers for static methods
- Like a toolbox - you don't "create" a toolbox, you just use the tools

**Static methods in utilities:**

- All methods are `public static`
- Can be called from anywhere without creating objects
- `GradeCalculator.getLetterGrade(85)` - direct use

**Package-private access:**

```java
static void resetCounters() {  // No 'public'
```

- No access modifier = package-private
- Only classes in same package can see it
- Good for testing methods you don't want public

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added utility classes for grade calculation and ID generation"`
3. Click **Commit and Push**

---

## 🎯 Part 6: Main Application - Bringing It Together

### Step 9: Create the Main Application

In the `main` package, create `SchoolApp.java`:

```java
package com.pluralsight.school.main;

// Import from models package
import com.pluralsight.school.models.Course;
import com.pluralsight.school.models.Student;
import com.pluralsight.school.models.Teacher;

// Import from services package
import com.pluralsight.school.services.EnrollmentService;
import com.pluralsight.school.services.GradeService;

// Import from utils package
import com.pluralsight.school.utils.GradeCalculator;
import com.pluralsight.school.utils.IDGenerator;

// Import from Java standard library
import java.util.Scanner;

public class SchoolApp {
    private static EnrollmentService enrollmentService = new EnrollmentService();
    private static GradeService gradeService = new GradeService();

    public static void main(String[] args) {
        System.out.println("╔════════════════════════════════════════╗");
        System.out.println("║     SCHOOL MANAGEMENT SYSTEM           ║");
        System.out.println("║     Package Organization Demo          ║");
        System.out.println("╚════════════════════════════════════════╝\n");

        // Demonstrate package organization
        demonstratePackageStructure();

        // Create sample data
        System.out.println("\n=== CREATING SCHOOL DATA ===");

        // Create teachers (using models package)
        Teacher mathTeacher = new Teacher(
            IDGenerator.generateTeacherId(),
            "John", "Smith", "Mathematics"
        );
        mathTeacher.addCertification("Advanced Calculus");
        mathTeacher.addCertification("Statistics");

        Teacher scienceTeacher = new Teacher(
            IDGenerator.generateTeacherId(),
            "Mary", "Johnson", "Science"
        );
        scienceTeacher.addCertification("Physics");
        scienceTeacher.addCertification("Chemistry");

        System.out.println("Created: " + mathTeacher);
        System.out.println("Created: " + scienceTeacher);

        // Create courses (using models and utils packages)
        Course algebra = new Course(
            IDGenerator.generateCourseCode("MATH"),
            "Algebra II", 3, 25
        );
        algebra.assignInstructor(mathTeacher);

        Course physics = new Course(
            IDGenerator.generateCourseCode("SCI"),
            "Physics 101", 4, 20
        );
        physics.assignInstructor(scienceTeacher);

        System.out.println("Created: " + algebra);
        System.out.println("Created: " + physics);

        // Create students (using models and utils packages)
        Student alice = new Student(
            IDGenerator.generateStudentId(),
            "Alice", "Anderson", 10
        );

        Student bob = new Student(
            IDGenerator.generateStudentId(),
            "Bob", "Brown", 11
        );

        Student charlie = new Student(
            IDGenerator.generateStudentId(),
            "Charlie", "Chen", 10
        );

        System.out.println("Created: " + alice);
        System.out.println("Created: " + bob);
        System.out.println("Created: " + charlie);

        // Demonstrate enrollment (using services package)
        System.out.println("\n=== ENROLLMENT PROCESS ===");
        enrollmentService.enrollStudentInCourse(alice, algebra);
        enrollmentService.enrollStudentInCourse(alice, physics);
        enrollmentService.enrollStudentInCourse(bob, algebra);
        enrollmentService.enrollStudentInCourse(charlie, physics);

        // Display schedules
        enrollmentService.printStudentSchedule(alice);
        enrollmentService.printStudentSchedule(bob);
        enrollmentService.printStudentSchedule(charlie);

        // Assign grades (using services and utils packages)
        System.out.println("\n=== ASSIGNING GRADES ===");
        gradeService.assignGrade(alice, algebra, 92.5);
        gradeService.assignGrade(alice, physics, 88.0);
        gradeService.assignGrade(bob, algebra, 85.5);
        gradeService.assignGrade(charlie, physics, 91.0);

        // Calculate GPAs
        System.out.println("\n=== GPA CALCULATIONS ===");
        System.out.printf("%s GPA: %.2f%n",
            alice.getFullName(), gradeService.calculateGPA(alice));
        System.out.printf("%s GPA: %.2f%n",
            bob.getFullName(), gradeService.calculateGPA(bob));
        System.out.printf("%s GPA: %.2f%n",
            charlie.getFullName(), gradeService.calculateGPA(charlie));

        // Interactive menu
        runInteractiveMenu();
    }

    private static void demonstratePackageStructure() {
        System.out.println("=== PACKAGE STRUCTURE DEMONSTRATION ===");
        System.out.println("This application uses proper package organization:");
        System.out.println();
        System.out.println("com.pluralsight.school/");
        System.out.println("  ├── main/        (Application entry point)");
        System.out.println("  │   └── SchoolApp.java");
        System.out.println("  ├── models/      (Data classes)");
        System.out.println("  │   ├── Student.java");
        System.out.println("  │   ├── Teacher.java");
        System.out.println("  │   └── Course.java");
        System.out.println("  ├── services/    (Business logic)");
        System.out.println("  │   ├── EnrollmentService.java");
        System.out.println("  │   └── GradeService.java");
        System.out.println("  └── utils/       (Helper utilities)");
        System.out.println("      ├── GradeCalculator.java");
        System.out.println("      └── IDGenerator.java");
        System.out.println();
        System.out.println("Benefits:");
        System.out.println("✓ Organized code structure");
        System.out.println("✓ Clear separation of concerns");
        System.out.println("✓ Easy to navigate and maintain");
        System.out.println("✓ Follows Java best practices");
    }

    private static void runInteractiveMenu() {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        System.out.println("\n=== INTERACTIVE DEMONSTRATION ===");

        while (running) {
            System.out.println("\n--- Menu ---");
            System.out.println("1. Show package information");
            System.out.println("2. Test grade calculator");
            System.out.println("3. Generate new IDs");
            System.out.println("4. Exit");
            System.out.print("Choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    showPackageInfo();
                    break;
                case 2:
                    testGradeCalculator(scanner);
                    break;
                case 3:
                    generateNewIds();
                    break;
                case 4:
                    running = false;
                    System.out.println("Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice!");
            }
        }

        scanner.close();
    }

    private static void showPackageInfo() {
        System.out.println("\n=== PACKAGE INFORMATION ===");
        System.out.println("Package naming convention: com.pluralsight.school");
        System.out.println("  com         - Commercial organization");
        System.out.println("  pluralsight - Company/organization");
        System.out.println("  school      - Project name");
        System.out.println("\nEach package groups related functionality:");
        System.out.println("  models   - What we work with (nouns)");
        System.out.println("  services - What we do (verbs)");
        System.out.println("  utils    - How we help (tools)");
        System.out.println("  main     - Where we start (entry)");
    }

    private static void testGradeCalculator(Scanner scanner) {
        System.out.print("Enter a numeric grade (0-100): ");
        double grade = scanner.nextDouble();
        scanner.nextLine();

        if (GradeCalculator.isValidGrade(grade)) {
            char letter = GradeCalculator.getLetterGrade(grade);
            double gpa = GradeCalculator.gradeToGPA(grade);
            String description = GradeCalculator.getGradeDescription(letter);

            System.out.printf("Grade: %.1f%n", grade);
            System.out.printf("Letter: %c%n", letter);
            System.out.printf("GPA Points: %.1f%n", gpa);
            System.out.printf("Description: %s%n", description);
        } else {
            System.out.println("Invalid grade!");
        }
    }

    private static void generateNewIds() {
        System.out.println("\n=== GENERATING NEW IDS ===");
        System.out.println("New Student ID: " + IDGenerator.generateStudentId());
        System.out.println("New Teacher ID: " + IDGenerator.generateTeacherId());
        System.out.println("New Math Course: " + IDGenerator.generateCourseCode("MATH"));
        System.out.println("New Science Course: " + IDGenerator.generateCourseCode("SCI"));
    }
}
```

**🔍 What's happening? Main Class Organization:**

**Import organization (top to bottom):**

1. Your own packages first (com.pluralsight...)
2. Third-party libraries (if any)
3. Java standard library (java.util...)

**Why this main package?**

- Separates application logic from business logic
- Entry point is clearly identified
- Can have multiple main classes for different purposes

**Cross-package communication:**

- Main uses classes from ALL other packages
- Shows how packages work together
- Like a conductor orchestrating different sections

**▶️ Run SchoolApp** to see the complete system working!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added main application demonstrating package interactions"`
3. Click **Commit and Push**

---

## 📋 Part 7: Package Best Practices

### Step 10: Create a Package Info File

In the `com.pluralsight.school` package, create `package-info.java`:

```java
/**
 * School Management System - Root Package
 *
 * This package contains all classes for managing a school system.
 *
 * Package Structure:
 * - models: Data representations (Student, Teacher, Course)
 * - services: Business logic (Enrollment, Grading)
 * - utils: Helper utilities (Calculators, Generators)
 * - main: Application entry points
 *
 * @author Your Name
 * @version 1.0
 * @since 2024
 */
package com.pluralsight.school;
```

### Step 11: Create a Test to Show Package Access

Create a new package `com.pluralsight.school.tests` and add `PackageAccessDemo.java`:

```java
package com.pluralsight.school.tests;

import com.pluralsight.school.models.Student;
import com.pluralsight.school.utils.GradeCalculator;
// import com.pluralsight.school.utils.IDGenerator;
// Won't work for package-private methods!

public class PackageAccessDemo {
    public static void main(String[] args) {
        System.out.println("=== PACKAGE ACCESS DEMONSTRATION ===\n");

        // Can use public classes from other packages
        Student student = new Student(1001, "Test", "Student", 10);
        System.out.println("Created: " + student);

        // Can use public static methods from utils
        double grade = 85.5;
        char letter = GradeCalculator.getLetterGrade(grade);
        System.out.println("Grade " + grade + " = " + letter);

        // CANNOT access package-private methods from utils
        // IDGenerator.resetCounters(); // This would cause error!
        // Only classes in same package can access package-private

        System.out.println("\n=== ACCESS MODIFIERS SUMMARY ===");
        System.out.println("public    - Accessible from any package");
        System.out.println("protected - Accessible from same package + subclasses");
        System.out.println("(default) - Accessible only from same package");
        System.out.println("private   - Accessible only within same class");
    }
}
```

**🔍 What's happening? Package Access Rules:**

**Access Levels (most to least restrictive):**

1. **private** - Only same class
2. **package-private** (no modifier) - Only same package
3. **protected** - Same package + subclasses
4. **public** - Everyone

**Why package-private is useful:**

- Internal helper methods
- Testing utilities
- Implementation details you don't want public

### 🔄 Final Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added package documentation and access demonstration"`
3. Click **Commit and Push**

---

## 🏆 Package Organization Best Practices Summary

### ✅ **DO's:**

1. **Use reverse domain notation**

   - `com.company.project`
   - Ensures global uniqueness

2. **Keep packages focused**

   - One package = one purpose
   - Like departments in a company

3. **Use clear, descriptive names**

   - `models`, `services`, `utils`, `controllers`
   - Lowercase only, no underscores

4. **Organize by functionality**

   ```
   com.company.app/
   ├── models/      (data)
   ├── services/    (logic)
   ├── utils/       (helpers)
   └── ui/          (interface)
   ```

5. **Import specifically**
   ```java
   import com.example.models.Student;  // Good
   import com.example.models.*;        // Avoid
   ```

### ❌ **DON'Ts:**

1. **Don't use default package**

   - Always declare package
   - Default package = no organization

2. **Don't create too many levels**

   - `com.company.app.models` ✅
   - `com.company.app.models.students.undergraduate.freshman` ❌

3. **Don't mix unrelated classes**

   - Keep packages cohesive
   - Student and Car shouldn't be in same package

4. **Don't use uppercase in package names**
   - `com.company.Models` ❌
   - `com.company.models` ✅

---

## 💡 Common Package Structures in Real Projects

### Small Project:

```
com.company.project/
├── models/
├── services/
└── Main.java
```

### Medium Project:

```
com.company.project/
├── models/
├── services/
├── controllers/
├── utils/
├── exceptions/
└── main/
```

### Large Project:

```
com.company.project/
├── core/
│   ├── models/
│   └── services/
├── api/
│   ├── controllers/
│   └── dto/
├── data/
│   ├── repositories/
│   └── entities/
├── utils/
├── config/
└── main/
```

---

## 🎯 Key Takeaways

1. **Packages are folders for organization** - Like filing cabinets for your code
2. **Reverse domain prevents conflicts** - Your unique namespace
3. **Import connects packages** - Building bridges between departments
4. **Access modifiers control visibility** - Security levels for your code
5. **Good organization scales** - Start organized, stay organized

---

## 💪 Challenge Exercises (Optional)

1. **Add a `database` package** with classes for data storage
2. **Create an `exceptions` package** with custom exception classes
3. **Add a `reports` package** for generating student reports
4. **Implement a `security` package** with login functionality
5. **Create sub-packages** like `models.academic` and `models.administrative`

---

## 🎉 Congratulations!

You've learned how professional Java developers organize code! This package structure is used in:

- Spring Boot applications
- Android apps
- Enterprise systems
- Open-source projects

**What you've mastered:**

- Package declaration and structure
- Naming conventions
- Import statements
- Access control between packages
- Industry best practices

**Next steps:**

1. Look at open-source Java projects on GitHub - notice their package structure
2. Apply this organization to your previous projects
3. Start every new project with proper package structure
4. Remember: Good organization is a habit, not a one-time thing!

Keep this project as a reference - you'll use these patterns in every Java project you create!
