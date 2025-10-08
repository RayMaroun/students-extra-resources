# 📋 Employee Payroll System
## A Step-by-Step Tutorial for File I/O, Exception Handling & Collections

---

## 🎯 Project Overview
We're building an Employee Payroll System that reads employee data from files, processes payroll, handles errors gracefully, and saves reports. This project teaches all Week 3 concepts: Exception Handling, File I/O (reading and writing), ArrayLists, HashMaps, and working with dates.

**What You'll Master:**
- Exception handling with try/catch
- Reading files with BufferedReader
- Writing files with FileWriter and BufferedWriter  
- Using ArrayList for dynamic lists
- Using HashMap for fast lookups
- Working with LocalDate and LocalTime
- Handling real-world data processing

---

## 📁 Project Setup

### Step 1: Create Your Project
1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `EmployeePayrollSystem`
4. Location: `~/pluralsight/workbook-3` (or `C:/pluralsight/workbook-3` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share Project to GitHub (Do This Now!)
1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `EmployeePayrollSystem`
3. Description: "Week 3 File I/O and Exception Handling practice"
4. Make sure "Private" is unchecked (unless you want it private)
5. Click **Share**
6. In the next dialog, review files and click **Add**

**Why share immediately?** This creates your remote repository right away, and you can push your commits as you work!

### Step 2: Create the Package Structure
1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight`
4. Click **OK**

---

## ⚠️ Part 1: Understanding Exception Handling

### Step 3: Learn About Exceptions First

Create a new class in the `com.pluralsight` package:
1. Right-click on `com.pluralsight`
2. Select **New → Java Class**
3. Name it: `ExceptionDemo`
4. Click **OK**

**Type this code:**
```java
package com.pluralsight;

public class ExceptionDemo {
    public static void main(String[] args) {
        // Let's see what happens when things go wrong!
        
        System.out.println("=== EXCEPTION DEMO ===\n");
        
        // Example 1: Array Index Out of Bounds
        System.out.println("Example 1: Accessing invalid array index");
        int[] numbers = {10, 20, 30};
        
        try {
            System.out.println("Trying to access index 5...");
            int value = numbers[5];  // This will cause an error!
            System.out.println("Value: " + value);
        } 
        catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("ERROR: Tried to access index that doesn't exist!");
            System.out.println("Array only has " + numbers.length + " elements");
        }
        
        System.out.println("Program continues running!\n");
        
        // Example 2: Division by Zero
        System.out.println("Example 2: Division by zero");
        try {
            int result = 10 / 0;  // This will cause an error!
            System.out.println("Result: " + result);
        }
        catch (ArithmeticException e) {
            System.out.println("ERROR: Cannot divide by zero!");
            System.out.println("Error details: " + e.getMessage());
        }
        
        System.out.println("Program still running!\n");
        
        // Example 3: Multiple catch blocks
        System.out.println("Example 3: Handling different types of errors");
        String text = null;
        
        try {
            System.out.println("Text length: " + text.length());  // NullPointerException!
        }
        catch (NullPointerException e) {
            System.out.println("ERROR: The text variable is null!");
        }
        catch (Exception e) {
            System.out.println("ERROR: Something else went wrong!");
        }
        
        System.out.println("\nProgram completed successfully!");
    }
}
```

**🔍 What's happening? Understanding Exceptions:**

**What are Exceptions?**
- Think of exceptions as "alarm bells" that Java rings when something goes wrong
- Like a smoke detector in your house - alerts you to problems
- Without handling them, your program CRASHES completely
- With try/catch, you can recover and continue

**The try/catch Structure:**
```java
try {
    // "Try" to do something risky
    // Code that might fail goes here
} 
catch (ExceptionType e) {
    // "Catch" the problem if it happens
    // Handle the error gracefully
}
```

**How it works - Step by Step:**
1. Java enters the `try` block
2. If everything works → skip the `catch` block
3. If error occurs → immediately jump to matching `catch` block
4. After handling → continue with rest of program

**Think of it like this:**
- **Without try/catch**: Like walking a tightrope with no safety net - one mistake and you fall
- **With try/catch**: Like having a safety net - if you fall, you're caught and can climb back up

**Common Exception Types:**
- `ArrayIndexOutOfBoundsException` - Accessing invalid array position
- `NullPointerException` - Using a variable that's null
- `IOException` - Problems reading/writing files
- `NumberFormatException` - Converting invalid text to number

**The Exception object `e`:**
- Contains information about what went wrong
- `.getMessage()` - Gets error description
- `.printStackTrace()` - Shows where error occurred

**Important Rule:** 
- Catch specific exceptions first, general Exception last
- Like sorting mail - specific boxes first, then "everything else" box

**▶️ Run ExceptionDemo** and see how exceptions are caught and handled!

### 📝 Commit Your Work:
1. Click the **Commit** button (✓) in the toolbar or press **Ctrl+K** (Windows) / **Cmd+K** (Mac)
2. Review your changes - you should see `ExceptionDemo.java` in blue (modified) or green (new)
3. Write commit message: `"Added exception handling demo with try-catch examples"`
4. Click **Commit and Push**
5. Confirm push in the dialog that appears

**Why commit now?** Each working feature deserves its own commit. This creates a clear history of your progress!

---

## 📖 Part 2: Reading Files with BufferedReader

### Step 4: Create Sample Employee Data File

First, let's create a data file to read from:

1. Right-click on your project name (EmployeePayrollSystem) in the project view
2. Select **New → File**
3. Name it: `employees.csv`
4. Click **OK**

**Type this data into employees.csv:**
```
id|name|hoursWorked|payRate
101|John Smith|45|25.50
102|Jane Doe|38|28.75
103|Bob Johnson|40|22.00
104|Alice Williams|42|30.25
105|Charlie Brown|35|26.50
```

### Step 5: Create Employee Class

Create a new class called `Employee`:
```java
package com.pluralsight;

public class Employee {
    private int employeeId;
    private String name;
    private double hoursWorked;
    private double payRate;
    
    // Constructor
    public Employee(int employeeId, String name, double hoursWorked, double payRate) {
        this.employeeId = employeeId;
        this.name = name;
        this.hoursWorked = hoursWorked;
        this.payRate = payRate;
    }
    
    // Calculate gross pay (regular + overtime)
    public double getGrossPay() {
        if (hoursWorked <= 40) {
            return hoursWorked * payRate;
        } else {
            double regularPay = 40 * payRate;
            double overtimeHours = hoursWorked - 40;
            double overtimePay = overtimeHours * payRate * 1.5;  // Time and a half
            return regularPay + overtimePay;
        }
    }
    
    // Getters
    public int getEmployeeId() { return employeeId; }
    public String getName() { return name; }
    public double getHoursWorked() { return hoursWorked; }
    public double getPayRate() { return payRate; }
}
```

### Step 6: Read Employee Data from File

Create a new class called `PayrollFileReader`:
```java
package com.pluralsight;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;

public class PayrollFileReader {
    public static void main(String[] args) {
        System.out.println("=== EMPLOYEE PAYROLL SYSTEM ===\n");
        
        // ArrayList to store all employees
        ArrayList<Employee> employees = new ArrayList<Employee>();
        
        // Read employees from file
        try {
            // Step 1: Create FileReader to connect to the file
            FileReader fileReader = new FileReader("employees.csv");
            
            // Step 2: Wrap in BufferedReader for efficient reading
            BufferedReader bufReader = new BufferedReader(fileReader);
            
            // Step 3: Read and skip the header line
            String line = bufReader.readLine();
            System.out.println("Skipping header: " + line);
            
            // Step 4: Read each data line
            while ((line = bufReader.readLine()) != null) {
                System.out.println("Reading: " + line);
                
                // Split the line by pipe character
                String[] parts = line.split("\\|");
                
                // Parse the data
                int id = Integer.parseInt(parts[0]);
                String name = parts[1];
                double hours = Double.parseDouble(parts[2]);
                double rate = Double.parseDouble(parts[3]);
                
                // Create employee and add to list
                Employee emp = new Employee(id, name, hours, rate);
                employees.add(emp);
            }
            
            // Step 5: Always close the reader!
            bufReader.close();
            
            System.out.println("\nSuccessfully loaded " + employees.size() + " employees");
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not read the file!");
            System.out.println("Make sure employees.csv exists in project root");
            e.printStackTrace();
        } catch (NumberFormatException e) {
            System.out.println("ERROR: Invalid number in file!");
            e.printStackTrace();
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("ERROR: File format is incorrect!");
            System.out.println("Expected format: id|name|hours|rate");
            e.printStackTrace();
        }
        
        // Display payroll report
        System.out.println("\n=== PAYROLL REPORT ===");
        double totalPayroll = 0;
        
        for (Employee emp : employees) {
            double pay = emp.getGrossPay();
            totalPayroll += pay;
            System.out.printf("%-20s: $%,.2f\n", emp.getName(), pay);
        }
        
        System.out.println("------------------------");
        System.out.printf("Total Payroll: $%,.2f\n", totalPayroll);
    }
}
```

**🔍 What's happening? File Reading Explained:**

**The File Reading Pipeline:**
```
File on Disk → FileReader → BufferedReader → Your Program
```

**FileReader - The Basic File Connection:**
```java
FileReader fileReader = new FileReader("employees.csv");
```
- Creates a connection to the file
- Like opening a book to read
- Can read character by character (slow!)
- Throws `IOException` if file doesn't exist

**BufferedReader - The Efficient Reader:**
```java
BufferedReader bufReader = new BufferedReader(fileReader);
```
- Wraps around FileReader for efficiency
- Reads chunks of data into a buffer (temporary storage)
- Like reading a page at a time instead of letter by letter
- Much faster for large files!

**Reading Lines:**
```java
while ((line = bufReader.readLine()) != null) {
    // Process each line
}
```
- `.readLine()` reads one line at a time
- Returns `null` when no more lines
- The while loop pattern: assign AND check in one step
- Like reading until you reach the end of the book

**Splitting Strings:**
```java
String[] parts = line.split("\\|");
```
- `split()` breaks a string into pieces
- `\\|` means split by pipe character (| is special, needs \\)
- Returns an array of strings
- Like cutting a sentence at each comma

**Parsing Text to Numbers:**
```java
int id = Integer.parseInt(parts[0]);
double hours = Double.parseDouble(parts[2]);
```
- Converts string "101" to number 101
- `parseInt()` for whole numbers
- `parseDouble()` for decimals
- Throws `NumberFormatException` if not a valid number

**Why Multiple Catch Blocks?**
- Different errors need different handling
- Specific exceptions first, general ones last
- Like having different emergency procedures for fire vs earthquake

**Always Close Files!**
```java
bufReader.close();
```
- Releases the file so other programs can use it
- Like closing a book when done reading
- Put in try block (after reading) or finally block

**▶️ Run PayrollFileReader** and watch it process the employee data!

### 📝 Commit Your Work:
1. Click the **Commit** button (✓) or press **Ctrl+K** / **Cmd+K**
2. You should see:
   - `employees.csv` (green - new file)
   - `Employee.java` (green - new file)
   - `PayrollFileReader.java` (green - new file)
3. Write commit message: `"Added employee data reading with BufferedReader and CSV parsing"`
4. Click **Commit and Push**

**Good practice:** Commit after each major feature works. If something breaks later, you can always go back!

---

## 📝 Part 3: Writing Files with FileWriter

### Step 7: Save Payroll Report to File

Create a new class called `PayrollFileWriter`:
```java
package com.pluralsight;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;

public class PayrollFileWriter {
    public static void main(String[] args) {
        ArrayList<Employee> employees = loadEmployees();
        
        if (employees.size() > 0) {
            generatePayrollReport(employees);
            System.out.println("\n✅ Payroll report saved to payroll-report.txt");
        }
    }
    
    // Method to load employees (reusing our reading code)
    public static ArrayList<Employee> loadEmployees() {
        ArrayList<Employee> employees = new ArrayList<Employee>();
        
        try {
            BufferedReader bufReader = new BufferedReader(
                new FileReader("employees.csv"));
            
            // Skip header
            bufReader.readLine();
            
            String line;
            while ((line = bufReader.readLine()) != null) {
                String[] parts = line.split("\\|");
                
                int id = Integer.parseInt(parts[0]);
                String name = parts[1];
                double hours = Double.parseDouble(parts[2]);
                double rate = Double.parseDouble(parts[3]);
                
                employees.add(new Employee(id, name, hours, rate));
            }
            
            bufReader.close();
            System.out.println("Loaded " + employees.size() + " employees");
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not read employees file");
            e.printStackTrace();
        }
        
        return employees;
    }
    
    // Method to generate and save payroll report
    public static void generatePayrollReport(ArrayList<Employee> employees) {
        try {
            // Create FileWriter (false = overwrite, true = append)
            FileWriter fileWriter = new FileWriter("payroll-report.txt", false);
            
            // Wrap in BufferedWriter for efficiency
            BufferedWriter bufWriter = new BufferedWriter(fileWriter);
            
            // Get current date and time
            LocalDate today = LocalDate.now();
            LocalTime now = LocalTime.now();
            DateTimeFormatter dateFormat = DateTimeFormatter.ofPattern("MMMM dd, yyyy");
            DateTimeFormatter timeFormat = DateTimeFormatter.ofPattern("hh:mm a");
            
            // Write report header
            bufWriter.write("========================================\n");
            bufWriter.write("         PAYROLL REPORT\n");
            bufWriter.write("========================================\n");
            bufWriter.write("Generated: " + today.format(dateFormat) + "\n");
            bufWriter.write("Time: " + now.format(timeFormat) + "\n");
            bufWriter.write("========================================\n\n");
            
            // Write column headers
            bufWriter.write(String.format("%-5s %-20s %10s %10s %12s\n",
                "ID", "Employee Name", "Hours", "Rate", "Gross Pay"));
            bufWriter.write("------------------------------------------------------------------\n");
            
            // Write employee data
            double totalPayroll = 0;
            int totalEmployees = 0;
            double totalHours = 0;
            
            for (Employee emp : employees) {
                double grossPay = emp.getGrossPay();
                totalPayroll += grossPay;
                totalEmployees++;
                totalHours += emp.getHoursWorked();
                
                // Format and write employee line
                String line = String.format("%-5d %-20s %10.2f $%9.2f $%,11.2f\n",
                    emp.getEmployeeId(),
                    emp.getName(),
                    emp.getHoursWorked(),
                    emp.getPayRate(),
                    grossPay);
                
                bufWriter.write(line);
                
                // Also print to console
                System.out.print(line);
            }
            
            // Write summary
            bufWriter.write("------------------------------------------------------------------\n");
            bufWriter.write(String.format("TOTALS: %d employees, %.2f hours, $%,.2f\n",
                totalEmployees, totalHours, totalPayroll));
            
            // Write average pay
            double averagePay = totalPayroll / totalEmployees;
            bufWriter.write(String.format("Average pay: $%,.2f\n", averagePay));
            
            // Find highest paid employee (bonus feature!)
            Employee highestPaid = employees.get(0);
            for (Employee emp : employees) {
                if (emp.getGrossPay() > highestPaid.getGrossPay()) {
                    highestPaid = emp;
                }
            }
            bufWriter.write("\nHighest paid: " + highestPaid.getName() + 
                          " ($" + String.format("%,.2f", highestPaid.getGrossPay()) + ")");
            
            // Close the writer - VERY IMPORTANT!
            bufWriter.close();
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not write report file!");
            e.printStackTrace();
        }
    }
}
```

**🔍 What's happening? File Writing Explained:**

**FileWriter - Creating/Opening Files:**
```java
FileWriter fileWriter = new FileWriter("payroll-report.txt", false);
```
- Creates a new file OR opens existing one
- Second parameter: `false` = overwrite, `true` = append
- Like starting a new document or adding to existing one
- Creates file in project root directory

**BufferedWriter - Efficient Writing:**
```java
BufferedWriter bufWriter = new BufferedWriter(fileWriter);
```
- Buffers (collects) data before writing to disk
- Much faster than writing character by character
- Like writing a full page before putting in folder
- Typically uses 8KB buffer

**Writing Text:**
```java
bufWriter.write("Hello\n");
bufWriter.write(someString);
```
- `.write()` adds text to the buffer
- `\n` adds a new line (like pressing Enter)
- Nothing actually saved to disk yet!

**Working with LocalDate and LocalTime:**
```java
LocalDate today = LocalDate.now();        // Gets today's date
LocalTime now = LocalTime.now();          // Gets current time
```
- Part of java.time package (modern date handling)
- No need to import Date class (old way)
- Immutable - can't be changed once created

**DateTimeFormatter - Making Dates Pretty:**
```java
DateTimeFormatter dateFormat = DateTimeFormatter.ofPattern("MMMM dd, yyyy");
String formatted = today.format(dateFormat);  // "January 15, 2024"
```
- Pattern symbols:
  - `yyyy` = 4-digit year
  - `MMMM` = Full month name
  - `MMM` = 3-letter month
  - `dd` = 2-digit day
  - `hh` = 12-hour format
  - `HH` = 24-hour format
  - `mm` = minutes
  - `a` = AM/PM

**String.format() - Creating Formatted Strings:**
```java
String.format("%-20s %10.2f", name, amount)
```
- `%-20s` = String, left-aligned, 20 characters wide
- `%10.2f` = Float, right-aligned, 10 wide, 2 decimals
- `%,11.2f` = Float with comma separators (1,234.56)
- Creates neat columns in output

**CRITICAL: Always Close Writers!**
```java
bufWriter.close();
```
- Flushes buffer to disk (actually saves the file)
- Releases file lock
- Without this, file might be empty or incomplete!
- Like clicking "Save" in Word

**▶️ Run PayrollFileWriter** and check the generated payroll-report.txt file!

### 📝 Commit Your Work:
1. Press **Ctrl+K** / **Cmd+K** for commit
2. You should see:
   - `PayrollFileWriter.java` (green - new)
   - `payroll-report.txt` might appear (you can uncheck it if you don't want to commit generated files)
3. Write commit message: `"Implemented payroll report generation with FileWriter and BufferedWriter"`
4. Click **Commit and Push**

**Pro tip:** Generally don't commit generated files (.txt reports) - commit the code that generates them!

---

## 🗂️ Part 4: Using HashMap for Employee Lookup

### Step 8: Create Employee Manager with HashMap

Create a new class called `EmployeeManager`:
```java
package com.pluralsight;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;

public class EmployeeManager {
    // Store employees in both ArrayList and HashMap
    private ArrayList<Employee> employeeList;
    private HashMap<Integer, Employee> employeeMap;
    
    // Constructor
    public EmployeeManager() {
        employeeList = new ArrayList<Employee>();
        employeeMap = new HashMap<Integer, Employee>();
        loadEmployees();
    }
    
    // Load employees from file
    private void loadEmployees() {
        try {
            BufferedReader bufReader = new BufferedReader(
                new FileReader("employees.csv"));
            
            // Skip header
            bufReader.readLine();
            
            String line;
            while ((line = bufReader.readLine()) != null) {
                String[] parts = line.split("\\|");
                
                int id = Integer.parseInt(parts[0]);
                String name = parts[1];
                double hours = Double.parseDouble(parts[2]);
                double rate = Double.parseDouble(parts[3]);
                
                Employee emp = new Employee(id, name, hours, rate);
                
                // Add to BOTH collections
                employeeList.add(emp);                // For iteration
                employeeMap.put(id, emp);            // For fast lookup
            }
            
            bufReader.close();
            System.out.println("Loaded " + employeeList.size() + " employees");
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not read file");
        } catch (Exception e) {
            System.out.println("ERROR: Problem processing file");
        }
    }
    
    // Find employee by ID using HashMap (FAST!)
    public Employee findEmployeeById(int id) {
        return employeeMap.get(id);  // Instant lookup!
    }
    
    // Find employee by name using ArrayList (SLOWER)
    public Employee findEmployeeByName(String name) {
        for (Employee emp : employeeList) {
            if (emp.getName().equalsIgnoreCase(name)) {
                return emp;
            }
        }
        return null;  // Not found
    }
    
    // Display all employees
    public void displayAllEmployees() {
        System.out.println("\n=== ALL EMPLOYEES ===");
        for (Employee emp : employeeList) {
            System.out.printf("ID: %d, Name: %-20s, Pay: $%,.2f\n",
                emp.getEmployeeId(), 
                emp.getName(), 
                emp.getGrossPay());
        }
    }
    
    // Interactive menu system
    public void runMenu() {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;
        
        while (running) {
            System.out.println("\n=== EMPLOYEE MANAGER ===");
            System.out.println("1. Find employee by ID");
            System.out.println("2. Find employee by name");
            System.out.println("3. Display all employees");
            System.out.println("4. Show HashMap vs ArrayList speed");
            System.out.println("5. Exit");
            System.out.print("Choice: ");
            
            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline
            
            switch (choice) {
                case 1:
                    System.out.print("Enter employee ID: ");
                    int id = scanner.nextInt();
                    Employee empById = findEmployeeById(id);
                    if (empById != null) {
                        System.out.println("Found: " + empById.getName());
                        System.out.println("Gross Pay: $" + 
                            String.format("%,.2f", empById.getGrossPay()));
                    } else {
                        System.out.println("Employee not found!");
                    }
                    break;
                    
                case 2:
                    System.out.print("Enter employee name: ");
                    String name = scanner.nextLine();
                    Employee empByName = findEmployeeByName(name);
                    if (empByName != null) {
                        System.out.println("Found: ID " + empByName.getEmployeeId());
                        System.out.println("Gross Pay: $" + 
                            String.format("%,.2f", empByName.getGrossPay()));
                    } else {
                        System.out.println("Employee not found!");
                    }
                    break;
                    
                case 3:
                    displayAllEmployees();
                    break;
                    
                case 4:
                    demonstrateSpeed();
                    break;
                    
                case 5:
                    running = false;
                    System.out.println("Goodbye!");
                    break;
                    
                default:
                    System.out.println("Invalid choice!");
            }
        }
        scanner.close();
    }
    
    // Demonstrate HashMap vs ArrayList speed
    public void demonstrateSpeed() {
        System.out.println("\n=== SPEED COMPARISON ===");
        
        // Test HashMap speed (finding by ID)
        long startTime = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            Employee emp = employeeMap.get(103);  // Direct lookup
        }
        long hashMapTime = System.nanoTime() - startTime;
        
        // Test ArrayList speed (searching by ID)
        startTime = System.nanoTime();
        for (int i = 0; i < 10000; i++) {
            for (Employee emp : employeeList) {
                if (emp.getEmployeeId() == 103) {
                    break;  // Found it
                }
            }
        }
        long arrayListTime = System.nanoTime() - startTime;
        
        System.out.println("HashMap lookup (10,000 times): " + 
            hashMapTime / 1000000 + " milliseconds");
        System.out.println("ArrayList search (10,000 times): " + 
            arrayListTime / 1000000 + " milliseconds");
        System.out.println("HashMap is " + (arrayListTime / hashMapTime) + 
            " times faster!");
    }
    
    // Main method
    public static void main(String[] args) {
        EmployeeManager manager = new EmployeeManager();
        manager.runMenu();
    }
}
```

**🔍 What's happening? Collections Explained:**

**ArrayList - The Flexible List:**
```java
ArrayList<Employee> employeeList = new ArrayList<Employee>();
```
- Like a stretchy array that grows/shrinks
- Maintains order of insertion
- Access by index: `list.get(0)`
- Good for: iteration, maintaining order
- Bad for: searching (must check each item)

**HashMap - The Lightning-Fast Lookup:**
```java
HashMap<Integer, Employee> employeeMap = new HashMap<Integer, Employee>();
```
- Like a dictionary or phone book
- Stores key-value pairs
- NO guaranteed order
- Access by key: `map.get(101)`
- Good for: instant lookup by unique key
- Bad for: maintaining order

**How HashMap Works - The Magic:**
1. You provide a key (employee ID)
2. HashMap uses "hashing" to calculate where to store it
3. Like having a formula that tells you exactly which filing cabinet drawer
4. Retrieval uses same formula - instant access!

**Adding to HashMap:**
```java
employeeMap.put(id, emp);
```
- `put(key, value)` stores the pair
- If key exists, REPLACES old value
- Returns previous value or null

**Getting from HashMap:**
```java
Employee emp = employeeMap.get(id);
```
- Returns the value for that key
- Returns null if key doesn't exist
- O(1) time complexity - always fast!

**ArrayList vs HashMap Search:**
- **ArrayList**: Must check every item until found
  - 1000 employees = up to 1000 checks
  - Like looking through every page of a book
  
- **HashMap**: Direct access using key
  - 1,000,000 employees = still instant!
  - Like using the index of a book

**When to Use Which:**
- **ArrayList**: 
  - Need to maintain order
  - Iterate through all items
  - Access by position
  - Allow duplicates

- **HashMap**:
  - Need fast lookup by unique identifier
  - Don't care about order
  - Frequent searching
  - Each key must be unique

**Using Both Together:**
- Store in ArrayList for ordered iteration
- Also store in HashMap for fast lookup
- Common pattern in real applications!
- Trade memory for speed

**▶️ Run EmployeeManager** and try the speed comparison!

### 📝 Commit Your Work:
1. Click **Commit** button or **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `EmployeeManager.java` (green - new class with HashMap implementation)
3. Write commit message: `"Added HashMap for fast employee lookup with performance comparison"`
4. Click **Commit and Push**

**Git tip:** Your commit messages tell a story. Someone should understand what you added just by reading them!

---

## 📅 Part 5: Working with Dates - Payroll Period

### Step 9: Create a Payroll Period Tracker

Create a new class called `PayrollPeriod`:
```java
package com.pluralsight;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Scanner;

public class PayrollPeriod {
    private LocalDate startDate;
    private LocalDate endDate;
    private LocalDate payDate;
    
    // Constructor for current pay period
    public PayrollPeriod() {
        // Assume bi-weekly pay periods
        LocalDate today = LocalDate.now();
        
        // Find the start of current pay period (assuming it starts on Sunday)
        int daysSinceSunday = today.getDayOfWeek().getValue() % 7;
        startDate = today.minusDays(daysSinceSunday);
        endDate = startDate.plusDays(13);  // Two week period
        payDate = endDate.plusDays(5);     // Pay on Friday after period ends
    }
    
    // Constructor for specific dates
    public PayrollPeriod(LocalDate startDate, LocalDate endDate) {
        this.startDate = startDate;
        this.endDate = endDate;
        this.payDate = endDate.plusDays(5);
    }
    
    // Calculate days in period
    public long getDaysInPeriod() {
        return ChronoUnit.DAYS.between(startDate, endDate) + 1;
    }
    
    // Check if a date falls within this period
    public boolean isDateInPeriod(LocalDate date) {
        return !date.isBefore(startDate) && !date.isAfter(endDate);
    }
    
    // Display period information
    public void displayPeriodInfo() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("EEEE, MMMM d, yyyy");
        
        System.out.println("\n=== PAYROLL PERIOD INFORMATION ===");
        System.out.println("Period Start: " + startDate.format(formatter));
        System.out.println("Period End: " + endDate.format(formatter));
        System.out.println("Pay Date: " + payDate.format(formatter));
        System.out.println("Days in Period: " + getDaysInPeriod());
        
        // Calculate days until payday
        LocalDate today = LocalDate.now();
        if (today.isBefore(payDate)) {
            long daysUntilPay = ChronoUnit.DAYS.between(today, payDate);
            System.out.println("Days until payday: " + daysUntilPay);
        } else if (today.equals(payDate)) {
            System.out.println("🎉 TODAY IS PAYDAY! 🎉");
        } else {
            System.out.println("Pay date has passed");
        }
    }
    
    // Generate time sheet file
    public void generateTimeSheet(ArrayList<Employee> employees) {
        String fileName = "timesheet-" + startDate + "-to-" + endDate + ".txt";
        
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(fileName));
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMM dd, yyyy");
            
            // Write header
            writer.write("====================================\n");
            writer.write("           TIME SHEET\n");
            writer.write("====================================\n");
            writer.write("Pay Period: " + startDate.format(formatter) + 
                        " to " + endDate.format(formatter) + "\n");
            writer.write("Pay Date: " + payDate.format(formatter) + "\n");
            writer.write("====================================\n\n");
            
            // Write employee hours
            for (Employee emp : employees) {
                writer.write(String.format("Employee: %s (ID: %d)\n", 
                    emp.getName(), emp.getEmployeeId()));
                writer.write(String.format("Hours Worked: %.2f\n", 
                    emp.getHoursWorked()));
                writer.write(String.format("Regular Hours: %.2f\n", 
                    Math.min(40, emp.getHoursWorked())));
                
                double overtime = Math.max(0, emp.getHoursWorked() - 40);
                if (overtime > 0) {
                    writer.write(String.format("Overtime Hours: %.2f\n", overtime));
                }
                
                writer.write("Status: [ ] Approved  [ ] Pending\n");
                writer.write("------------------------------------\n\n");
            }
            
            writer.close();
            System.out.println("✅ Time sheet saved to " + fileName);
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not create time sheet");
            e.printStackTrace();
        }
    }
    
    // Interactive date calculator
    public static void runDateCalculator() {
        Scanner scanner = new Scanner(System.in);
        DateTimeFormatter inputFormat = DateTimeFormatter.ofPattern("MM/dd/yyyy");
        
        System.out.println("\n=== PAYROLL DATE CALCULATOR ===");
        
        try {
            System.out.print("Enter start date (MM/dd/yyyy): ");
            String startStr = scanner.nextLine();
            LocalDate start = LocalDate.parse(startStr, inputFormat);
            
            System.out.print("Enter end date (MM/dd/yyyy): ");
            String endStr = scanner.nextLine();
            LocalDate end = LocalDate.parse(endStr, inputFormat);
            
            // Calculate various date differences
            long days = ChronoUnit.DAYS.between(start, end);
            long weeks = ChronoUnit.WEEKS.between(start, end);
            long months = ChronoUnit.MONTHS.between(start, end);
            
            System.out.println("\n=== CALCULATION RESULTS ===");
            System.out.println("Days between: " + days);
            System.out.println("Weeks between: " + weeks);
            System.out.println("Months between: " + months);
            
            // Business days calculation (excluding weekends)
            long businessDays = 0;
            LocalDate current = start;
            while (!current.isAfter(end)) {
                if (current.getDayOfWeek().getValue() <= 5) {  // Monday-Friday
                    businessDays++;
                }
                current = current.plusDays(1);
            }
            System.out.println("Business days: " + businessDays);
            
        } catch (Exception e) {
            System.out.println("ERROR: Invalid date format!");
            System.out.println("Please use MM/dd/yyyy format");
        }
    }
    
    // Main method to test
    public static void main(String[] args) {
        // Create current pay period
        PayrollPeriod currentPeriod = new PayrollPeriod();
        currentPeriod.displayPeriodInfo();
        
        // Load employees and generate time sheet
        ArrayList<Employee> employees = PayrollFileWriter.loadEmployees();
        if (employees.size() > 0) {
            currentPeriod.generateTimeSheet(employees);
        }
        
        // Run date calculator
        Scanner scanner = new Scanner(System.in);
        System.out.print("\nDo you want to use the date calculator? (yes/no): ");
        String answer = scanner.nextLine();
        if (answer.equalsIgnoreCase("yes")) {
            runDateCalculator();
        }
        
        scanner.close();
    }
}
```

**🔍 What's happening? Date and Time Explained:**

**LocalDate - Working with Dates:**
```java
LocalDate today = LocalDate.now();           // Current date
LocalDate specific = LocalDate.of(2024, 1, 15);  // Specific date
```
- Represents a date without time (year-month-day)
- Immutable - methods return NEW date objects
- No time zones involved (simpler!)

**Date Arithmetic - Adding/Subtracting:**
```java
LocalDate tomorrow = today.plusDays(1);
LocalDate lastWeek = today.minusWeeks(1);
LocalDate nextMonth = today.plusMonths(1);
```
- Original date unchanged (immutable)
- Chain operations: `today.plusMonths(1).minusDays(5)`
- Handles month/year boundaries automatically

**Getting Date Components:**
```java
int year = today.getYear();           // 2024
int month = today.getMonthValue();    // 1-12
int day = today.getDayOfMonth();      // 1-31
DayOfWeek dow = today.getDayOfWeek(); // MONDAY, TUESDAY, etc.
```
- `.getDayOfWeek().getValue()` returns 1=Monday, 7=Sunday
- `.getMonth()` returns Month enum (JANUARY, etc.)

**Comparing Dates:**
```java
if (date1.isBefore(date2)) { }
if (date1.isAfter(date2)) { }
if (date1.equals(date2)) { }
```
- Clear, readable comparison methods
- No need for complicated comparisons

**ChronoUnit - Calculating Time Between Dates:**
```java
long days = ChronoUnit.DAYS.between(start, end);
```
- Calculates difference between two dates
- Options: DAYS, WEEKS, MONTHS, YEARS, etc.
- Returns long value

**DateTimeFormatter Patterns:**
- `yyyy` = 4-digit year (2024)
- `yy` = 2-digit year (24)
- `MM` = 2-digit month (01, 12)
- `MMM` = 3-letter month (Jan, Dec)
- `MMMM` = Full month name (January)
- `dd` = 2-digit day (01, 31)
- `EEEE` = Full day name (Monday)
- `EEE` = 3-letter day (Mon)

**Parsing Dates from Strings:**
```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yyyy");
LocalDate date = LocalDate.parse("01/15/2024", formatter);
```
- Convert user input to LocalDate
- Must match pattern exactly
- Throws exception if invalid format

**Real-World Date Logic:**
- Pay periods often start on specific weekdays
- Business days exclude weekends
- Paydays are usually fixed days after period ends
- Date calculations crucial for payroll systems!

**▶️ Run PayrollPeriod** and explore date calculations!

### 📝 Commit Your Work:
1. **Ctrl+K** / **Cmd+K** to open commit dialog
2. Files to commit:
   - `PayrollPeriod.java` (green - new date handling class)
   - Generated timesheet files (uncheck these)
3. Write commit message: `"Added payroll period tracking with LocalDate and date calculations"`
4. Click **Commit and Push**

**Remember:** Frequent commits = easier debugging. You can always see what changed between working versions!

---

## 🎯 Part 6: Complete Payroll System

### Step 10: Bring Everything Together

Create the final class called `CompletePayrollSystem`:
```java
package com.pluralsight;

import java.io.*;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.*;

public class CompletePayrollSystem {
    private ArrayList<Employee> employees;
    private HashMap<Integer, Employee> employeeMap;
    private PayrollPeriod currentPeriod;
    private Scanner scanner;
    
    // Constructor
    public CompletePayrollSystem() {
        employees = new ArrayList<>();
        employeeMap = new HashMap<>();
        currentPeriod = new PayrollPeriod();
        scanner = new Scanner(System.in);
        
        // Load initial data
        loadEmployees();
    }
    
    // Load employees with comprehensive error handling
    private void loadEmployees() {
        String fileName = "employees.csv";
        int lineNumber = 0;
        
        try {
            File file = new File(fileName);
            if (!file.exists()) {
                System.out.println("Creating sample employees.csv file...");
                createSampleFile();
            }
            
            BufferedReader reader = new BufferedReader(new FileReader(fileName));
            
            // Skip header
            String header = reader.readLine();
            lineNumber++;
            
            String line;
            while ((line = reader.readLine()) != null) {
                lineNumber++;
                
                try {
                    String[] parts = line.split("\\|");
                    
                    if (parts.length != 4) {
                        throw new IllegalArgumentException(
                            "Expected 4 fields, found " + parts.length);
                    }
                    
                    int id = Integer.parseInt(parts[0].trim());
                    String name = parts[1].trim();
                    double hours = Double.parseDouble(parts[2].trim());
                    double rate = Double.parseDouble(parts[3].trim());
                    
                    // Validate data
                    if (hours < 0 || hours > 80) {
                        System.out.println("Warning: Unusual hours (" + hours + 
                            ") for " + name);
                    }
                    if (rate < 7.25) {  // Federal minimum wage
                        System.out.println("Warning: Pay rate below minimum wage for " + 
                            name);
                    }
                    
                    Employee emp = new Employee(id, name, hours, rate);
                    employees.add(emp);
                    employeeMap.put(id, emp);
                    
                } catch (NumberFormatException e) {
                    System.out.println("Error on line " + lineNumber + 
                        ": Invalid number format");
                    System.out.println("  Line content: " + line);
                } catch (IllegalArgumentException e) {
                    System.out.println("Error on line " + lineNumber + 
                        ": " + e.getMessage());
                    System.out.println("  Line content: " + line);
                } catch (Exception e) {
                    System.out.println("Error on line " + lineNumber + 
                        ": " + e.getMessage());
                }
            }
            
            reader.close();
            System.out.println("✅ Loaded " + employees.size() + 
                " employees successfully");
            
        } catch (FileNotFoundException e) {
            System.out.println("ERROR: File '" + fileName + "' not found!");
            System.out.println("Current directory: " + 
                System.getProperty("user.dir"));
        } catch (IOException e) {
            System.out.println("ERROR: Problem reading file!");
            e.printStackTrace();
        }
    }
    
    // Create sample file if it doesn't exist
    private void createSampleFile() {
        try {
            BufferedWriter writer = new BufferedWriter(
                new FileWriter("employees.csv"));
            
            writer.write("id|name|hoursWorked|payRate\n");
            writer.write("101|John Smith|45|25.50\n");
            writer.write("102|Jane Doe|38|28.75\n");
            writer.write("103|Bob Johnson|40|22.00\n");
            writer.write("104|Alice Williams|42|30.25\n");
            writer.write("105|Charlie Brown|35|26.50\n");
            
            writer.close();
            System.out.println("✅ Sample employees.csv created");
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not create sample file!");
        }
    }
    
    // Main menu system
    public void run() {
        boolean running = true;
        
        System.out.println("\n╔════════════════════════════════════════╗");
        System.out.println("║    COMPLETE PAYROLL MANAGEMENT SYSTEM   ║");
        System.out.println("╚════════════════════════════════════════╝");
        
        while (running) {
            displayMenu();
            
            try {
                int choice = scanner.nextInt();
                scanner.nextLine();  // Consume newline
                
                switch (choice) {
                    case 1:
                        viewAllEmployees();
                        break;
                    case 2:
                        searchEmployee();
                        break;
                    case 3:
                        generatePayrollReport();
                        break;
                    case 4:
                        viewPayPeriodInfo();
                        break;
                    case 5:
                        generateTimeSheets();
                        break;
                    case 6:
                        calculatePayrollStats();
                        break;
                    case 7:
                        exportToFile();
                        break;
                    case 8:
                        running = false;
                        System.out.println("\nThank you for using the Payroll System!");
                        System.out.println("Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice! Please try again.");
                }
                
            } catch (InputMismatchException e) {
                System.out.println("ERROR: Please enter a valid number!");
                scanner.nextLine();  // Clear invalid input
            }
            
            if (running) {
                System.out.print("\nPress Enter to continue...");
                scanner.nextLine();
            }
        }
        
        scanner.close();
    }
    
    // Display menu
    private void displayMenu() {
        System.out.println("\n=== MAIN MENU ===");
        System.out.println("1. View All Employees");
        System.out.println("2. Search Employee");
        System.out.println("3. Generate Payroll Report");
        System.out.println("4. View Pay Period Info");
        System.out.println("5. Generate Time Sheets");
        System.out.println("6. Calculate Payroll Statistics");
        System.out.println("7. Export Data to File");
        System.out.println("8. Exit");
        System.out.print("\nEnter choice: ");
    }
    
    // View all employees
    private void viewAllEmployees() {
        System.out.println("\n=== ALL EMPLOYEES ===");
        System.out.printf("%-5s %-20s %10s %10s %12s\n",
            "ID", "Name", "Hours", "Rate", "Gross Pay");
        System.out.println("---------------------------------------------------------------");
        
        for (Employee emp : employees) {
            System.out.printf("%-5d %-20s %10.2f $%9.2f $%,11.2f\n",
                emp.getEmployeeId(),
                emp.getName(),
                emp.getHoursWorked(),
                emp.getPayRate(),
                emp.getGrossPay());
        }
    }
    
    // Search for employee
    private void searchEmployee() {
        System.out.println("\n=== SEARCH EMPLOYEE ===");
        System.out.println("1. Search by ID");
        System.out.println("2. Search by Name");
        System.out.print("Choice: ");
        
        int choice = scanner.nextInt();
        scanner.nextLine();
        
        Employee found = null;
        
        if (choice == 1) {
            System.out.print("Enter employee ID: ");
            int id = scanner.nextInt();
            found = employeeMap.get(id);  // Fast HashMap lookup!
        } else if (choice == 2) {
            System.out.print("Enter employee name: ");
            String name = scanner.nextLine();
            
            // Search through ArrayList
            for (Employee emp : employees) {
                if (emp.getName().toLowerCase().contains(name.toLowerCase())) {
                    found = emp;
                    break;
                }
            }
        }
        
        if (found != null) {
            System.out.println("\n=== EMPLOYEE FOUND ===");
            System.out.println("ID: " + found.getEmployeeId());
            System.out.println("Name: " + found.getName());
            System.out.println("Hours Worked: " + found.getHoursWorked());
            System.out.println("Pay Rate: $" + found.getPayRate());
            System.out.println("Gross Pay: $" + String.format("%,.2f", found.getGrossPay()));
            
            if (found.getHoursWorked() > 40) {
                double overtime = found.getHoursWorked() - 40;
                System.out.println("Overtime Hours: " + overtime);
            }
        } else {
            System.out.println("Employee not found!");
        }
    }
    
    // Generate payroll report
    private void generatePayrollReport() {
        String fileName = "payroll-" + LocalDate.now() + ".txt";
        
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(fileName));
            
            // Write header with timestamp
            LocalDateTime now = LocalDateTime.now();
            DateTimeFormatter formatter = 
                DateTimeFormatter.ofPattern("MMMM dd, yyyy 'at' hh:mm a");
            
            writer.write("========================================\n");
            writer.write("         PAYROLL REPORT\n");
            writer.write("========================================\n");
            writer.write("Generated: " + now.format(formatter) + "\n");
            writer.write("========================================\n\n");
            
            double totalPayroll = 0;
            double totalRegularPay = 0;
            double totalOvertimePay = 0;
            
            // Process each employee
            for (Employee emp : employees) {
                double regularPay = Math.min(40, emp.getHoursWorked()) * 
                    emp.getPayRate();
                double overtimePay = 0;
                
                if (emp.getHoursWorked() > 40) {
                    double overtimeHours = emp.getHoursWorked() - 40;
                    overtimePay = overtimeHours * emp.getPayRate() * 1.5;
                }
                
                double grossPay = regularPay + overtimePay;
                totalRegularPay += regularPay;
                totalOvertimePay += overtimePay;
                totalPayroll += grossPay;
                
                writer.write(String.format("Employee: %s (ID: %d)\n", 
                    emp.getName(), emp.getEmployeeId()));
                writer.write(String.format("  Regular Pay: $%,.2f\n", regularPay));
                if (overtimePay > 0) {
                    writer.write(String.format("  Overtime Pay: $%,.2f\n", overtimePay));
                }
                writer.write(String.format("  Total Pay: $%,.2f\n\n", grossPay));
            }
            
            // Write summary
            writer.write("========================================\n");
            writer.write("SUMMARY\n");
            writer.write("========================================\n");
            writer.write(String.format("Total Employees: %d\n", employees.size()));
            writer.write(String.format("Regular Pay: $%,.2f\n", totalRegularPay));
            writer.write(String.format("Overtime Pay: $%,.2f\n", totalOvertimePay));
            writer.write(String.format("Total Payroll: $%,.2f\n", totalPayroll));
            
            writer.close();
            
            System.out.println("✅ Report saved to " + fileName);
            System.out.println("Total Payroll: $" + 
                String.format("%,.2f", totalPayroll));
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not generate report!");
            e.printStackTrace();
        }
    }
    
    // View pay period info
    private void viewPayPeriodInfo() {
        currentPeriod.displayPeriodInfo();
    }
    
    // Generate time sheets
    private void generateTimeSheets() {
        currentPeriod.generateTimeSheet(employees);
    }
    
    // Calculate statistics
    private void calculatePayrollStats() {
        System.out.println("\n=== PAYROLL STATISTICS ===");
        
        if (employees.isEmpty()) {
            System.out.println("No employees loaded!");
            return;
        }
        
        // Calculate various stats
        double totalPay = 0;
        double highestPay = 0;
        double lowestPay = Double.MAX_VALUE;
        Employee highestPaid = null;
        Employee lowestPaid = null;
        
        for (Employee emp : employees) {
            double pay = emp.getGrossPay();
            totalPay += pay;
            
            if (pay > highestPay) {
                highestPay = pay;
                highestPaid = emp;
            }
            if (pay < lowestPay) {
                lowestPay = pay;
                lowestPaid = emp;
            }
        }
        
        double averagePay = totalPay / employees.size();
        
        System.out.println("Number of Employees: " + employees.size());
        System.out.println("Total Payroll: $" + String.format("%,.2f", totalPay));
        System.out.println("Average Pay: $" + String.format("%,.2f", averagePay));
        System.out.println("Highest Paid: " + highestPaid.getName() + 
            " ($" + String.format("%,.2f", highestPay) + ")");
        System.out.println("Lowest Paid: " + lowestPaid.getName() + 
            " ($" + String.format("%,.2f", lowestPay) + ")");
    }
    
    // Export data
    private void exportToFile() {
        System.out.println("\n=== EXPORT DATA ===");
        System.out.println("1. Export as CSV");
        System.out.println("2. Export as Text Report");
        System.out.print("Choice: ");
        
        int choice = scanner.nextInt();
        scanner.nextLine();
        
        if (choice == 1) {
            exportAsCSV();
        } else if (choice == 2) {
            generatePayrollReport();
        }
    }
    
    // Export as CSV
    private void exportAsCSV() {
        String fileName = "payroll-export-" + LocalDate.now() + ".csv";
        
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(fileName));
            
            // Write header
            writer.write("ID,Name,Hours,Rate,Regular Pay,Overtime Pay,Gross Pay\n");
            
            // Write data
            for (Employee emp : employees) {
                double regularPay = Math.min(40, emp.getHoursWorked()) * 
                    emp.getPayRate();
                double overtimePay = emp.getGrossPay() - regularPay;
                
                writer.write(String.format("%d,%s,%.2f,%.2f,%.2f,%.2f,%.2f\n",
                    emp.getEmployeeId(),
                    emp.getName(),
                    emp.getHoursWorked(),
                    emp.getPayRate(),
                    regularPay,
                    overtimePay,
                    emp.getGrossPay()));
            }
            
            writer.close();
            System.out.println("✅ Data exported to " + fileName);
            
        } catch (IOException e) {
            System.out.println("ERROR: Could not export data!");
        }
    }
    
    // Main method
    public static void main(String[] args) {
        CompletePayrollSystem system = new CompletePayrollSystem();
        system.run();
    }
}
```

**🔍 What's happening? Complete System Integration:**

**Comprehensive Error Handling:**
- Multiple catch blocks for different exceptions
- Line number tracking for debugging
- Validation of data (negative hours, low wages)
- Graceful recovery from errors

**File Existence Checking:**
```java
File file = new File(fileName);
if (!file.exists()) { 
    createSampleFile();
}
```
- Check if file exists before reading
- Auto-create sample data if missing
- User-friendly experience

**Input Validation:**
```java
try {
    int choice = scanner.nextInt();
} catch (InputMismatchException e) {
    // Handle non-numeric input
}
```
- Catch bad input (letters when expecting numbers)
- Clear scanner buffer with `nextLine()`
- Prevent program crashes

**String Manipulation:**
- `.trim()` removes leading/trailing spaces
- `.toLowerCase()` for case-insensitive search
- `.contains()` for partial matching

**Multiple Export Formats:**
- Human-readable reports
- CSV for Excel import
- Different formats for different needs

**Real-World Features:**
- Overtime calculation (time and a half)
- Minimum wage validation
- Pay period tracking
- Statistical analysis

**▶️ Run CompletePayrollSystem** for the full experience!

### 📝 Final Commit:
1. Press **Ctrl+K** / **Cmd+K**
2. Review all changes:
   - `CompletePayrollSystem.java` (green - complete system integration)
   - Any modifications to existing files (blue)
3. Write commit message: `"Completed payroll system with full menu and all features integrated"`
4. Click **Commit and Push**

**Celebrate!** You've built a complete system with regular commits documenting your progress!

---

## 💾 Git Best Practices You've Learned

### Initial Project Setup (Already Done in Step 1):
When you created the project with "Create Git repository" checked, IntelliJ:
- Initialized a local Git repository
- Made an initial commit with project files

### Sharing to GitHub (First Time Only):
1. **VCS → Share Project on GitHub**
2. Repository name: `EmployeePayrollSystem`
3. Description: "Week 3 File I/O and Collections practice"
4. Click **Share**

### Your Commit History Shows Your Journey:
If you followed along, you should have these commits:
- "Initial commit" (automatic)
- "Added exception handling demo with try-catch examples"
- "Added employee data reading with BufferedReader and CSV parsing"
- "Implemented payroll report generation with FileWriter and BufferedWriter"
- "Added HashMap for fast employee lookup with performance comparison"
- "Added payroll period tracking with LocalDate and date calculations"
- "Completed payroll system with full menu and all features integrated"

**Why This Matters:**
- **Clear History**: Each commit shows one feature/concept
- **Easy Debugging**: Can identify when bugs were introduced
- **Professional Practice**: This is how developers work in companies
- **Portfolio Building**: Your GitHub shows consistent, well-documented work

### IntelliJ Git Tips:
- **Blue filenames** = Modified files
- **Green filenames** = New files
- **Git tab** (bottom) = See all changes and history
- **Annotations** = Right-click a file → Git → Annotate to see who wrote each line
- **Rollback** = Right-click a file → Git → Rollback to undo changes

---

## 🏆 Concepts You've Mastered

✅ **Exception Handling:**
- try/catch blocks
- Multiple catch blocks
- Specific vs general exceptions
- Error recovery strategies

✅ **File I/O:**
- Reading with BufferedReader
- Writing with BufferedWriter
- File existence checking
- Line-by-line processing

✅ **Collections:**
- ArrayList for dynamic lists
- HashMap for fast lookups
- When to use each type
- Combining both for efficiency

✅ **Date/Time Operations:**
- LocalDate and LocalTime
- Date arithmetic
- Formatting with DateTimeFormatter
- Calculating periods between dates

✅ **Real-World Programming:**
- Data validation
- Error messages with context
- Multiple file formats
- User-friendly interfaces

---

## 💪 Challenge Enhancements (Optional)

1. **Add employee departments**: Group employees by department
2. **Tax calculations**: Deduct federal/state taxes from gross pay
3. **Sick/vacation tracking**: Track time off balances
4. **Multiple pay rates**: Different rates for different job types
5. **Schedule management**: Track daily clock-in/out times
6. **Benefits deductions**: Health insurance, 401k, etc.
7. **Year-to-date totals**: Track cumulative earnings
8. **Email reports**: Research JavaMail API to email reports

---

## 📚 Key Takeaways

**Week 3 builds practical skills:**
- **Files** = Persistent data storage
- **Exceptions** = Graceful error handling
- **Collections** = Efficient data management
- **Dates** = Real-world time tracking

**The File I/O Pattern:**
1. Open file (FileReader/FileWriter)
2. Wrap in buffer (BufferedReader/BufferedWriter)
3. Process data (read/write)
4. ALWAYS close the file
5. ALWAYS handle exceptions

**Remember:**
- Files can fail - always use try/catch
- BufferedReader/Writer for efficiency
- HashMap for lookups, ArrayList for order
- Dates are immutable - operations return new dates

---

## 🎉 Congratulations!

You've built a complete payroll system that handles real-world data processing challenges! This project demonstrates professional Java development practices for handling files, errors, and data.

**What you've accomplished:**
- Read and write real data files
- Handle errors without crashing
- Use collections efficiently
- Process dates and times
- Build a complete, useful application

**Next steps:**
1. Type all code yourself for practice
2. Run each section separately first
3. Test with different data files
4. Try to break it (bad data) and see error handling
5. Add your own features

This is how real business applications handle data - reading from files, processing with collections, handling errors, and generating reports. You're writing professional-level code!