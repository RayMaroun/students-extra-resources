# 🗄️ Northwind Database Application

## A Step-by-Step Tutorial for JDBC, Connection Pooling & Database CRUD Operations

---

## 🎯 Project Overview

We're building a Northwind Database Application that teaches you how to connect Java applications to MySQL databases. You'll learn to perform CRUD operations (Create, Read, Update, Delete), use connection pooling for efficiency, and call stored procedures. This is how REAL enterprise applications interact with databases!

**What You'll Master:**

- Setting up JDBC (Java Database Connectivity)
- Using connection pooling with Apache DBCP2
- Writing parameterized SQL queries (preventing SQL injection)
- Performing CRUD operations on database tables
- Retrieving auto-generated keys after inserts
- Calling stored procedures from Java
- Organizing database code with proper separation of concerns
- Passing database credentials securely via command line arguments

---

## 📚 Prerequisites

Before starting this project, you should have:

1. **MySQL Server installed** on your computer
2. **The Northwind database** imported into MySQL
3. Basic understanding of SQL (SELECT, INSERT, UPDATE, DELETE)
4. Completion of previous Java bootcamp weeks (OOP fundamentals)

---

## 📁 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `NorthwindDatabaseApp`
4. Location: `~/pluralsight/workbook-jdbc` (or `C:/pluralsight/workbook-jdbc` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share Project to GitHub Immediately

1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `NorthwindDatabaseApp`
3. Description: "JDBC Database Operations with Northwind - CRUD and Stored Procedures"
4. Click **Share**
5. In the next dialog, click **Add**

**Why share now?** Professional developers version control from the start. This habit will serve you well!

---

## 🔧 Part 1: Setting Up Maven Dependencies

### Step 2: Understanding What We Need

Before we can connect to a database, we need two important libraries:

1. **MySQL Connector** - The "translator" that lets Java speak to MySQL
2. **Apache Commons DBCP2** - A connection pool manager for efficiency

**🤔 What's a Connection Pool?**

Think of database connections like phone lines to a business:
- **Without pooling:** Every customer call requires installing a new phone line, then removing it after the call. Very slow and expensive!
- **With pooling:** You have 10 phone lines ready. When a customer calls, they use an available line. When done, the line goes back to the pool for the next caller.

Connection pooling keeps database connections ready to use, making your application MUCH faster!

### Step 3: Configure the pom.xml File

1. Open the `pom.xml` file in your project root
2. Find the `<properties>` section (or add one if it doesn't exist)
3. Replace the entire contents with:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.pluralsight</groupId>
    <artifactId>NorthwindDatabaseApp</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
        </dependency>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-dbcp2</artifactId>
            <version>2.11.0</version>
        </dependency>
    </dependencies>

</project>
```

4. **Important:** Click the Maven refresh icon (🔄) in the top-right corner, or right-click on `pom.xml` → **Maven** → **Reload Project**

**🔍 What's happening?**

- **`<dependencies>`** - This section tells Maven "go download these libraries for me"
- **`mysql-connector-java`** - The JDBC driver for MySQL (the "translator")
- **`commons-dbcp2`** - Apache's Database Connection Pooling library
- **`<version>`** - Specifies exactly which version to download (for consistency)

When you reload Maven, it downloads these JAR files and adds them to your project automatically!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Check the `pom.xml` file
3. Commit message: `"Added MySQL connector and DBCP2 dependencies"`
4. Click **Commit** or **Commit and Push**

---

## 📦 Part 2: Creating the Package Structure

### Step 4: Set Up Your Packages

We'll organize our code into three packages:

1. **`com.pluralsight.models`** - Classes that represent database tables (data carriers)
2. **`com.pluralsight.db`** - Database access code (all SQL lives here)
3. **`com.pluralsight.main`** - The main application entry point

Create these packages:

1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight.models`
4. Repeat for `com.pluralsight.db`
5. Repeat for `com.pluralsight.main`

**🔍 Why separate packages?**

Think of it like organizing a restaurant:
- **models** = The menu items (what data looks like)
- **db** = The kitchen (where data is prepared/stored)
- **main** = The front counter (where customers interact)

Each area has its own responsibility!

---

## 🏗️ Part 3: Creating Model Classes

Model classes are simple Java objects that represent rows from database tables. They're like containers that hold data.

### Step 5: Create the Shipper Model

The `shippers` table in Northwind has these columns:
- `ShipperID` (int, auto-generated)
- `CompanyName` (varchar)
- `Phone` (varchar)

1. Right-click on `com.pluralsight.models`
2. Select **New → Java Class**
3. Name it: `Shipper`
4. Click **OK**

**Type this code:**

```java
package com.pluralsight.models;

public class Shipper {
    private int shipperId;
    private String companyName;
    private String phoneNumber;

    public Shipper(int shipperId, String companyName, String phoneNumber) {
        this.shipperId = shipperId;
        this.companyName = companyName;
        this.phoneNumber = phoneNumber;
    }

    public int getShipperId() {
        return shipperId;
    }

    public String getCompanyName() {
        return companyName;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }
}
```

**🔍 What's happening?**

- **Private fields** - Store the data from each column in the database table
- **Constructor** - Takes all the values needed to create a complete Shipper object
- **Getters** - Allow other classes to READ the data (but not change it)
- **No setters** - This makes the object "immutable" (unchangeable after creation), which is safer

**💡 Real-world analogy:** A Shipper object is like a shipping label. Once printed, the information doesn't change - you'd print a new label if something was wrong.

### Step 6: Create the CustomerOrderHistory Model

This model represents data returned from a stored procedure that shows what products a customer ordered.

1. Right-click on `com.pluralsight.models`
2. Select **New → Java Class**
3. Name it: `CustomerOrderHistory`
4. Click **OK**

**Type this code:**

```java
package com.pluralsight.models;

public class CustomerOrderHistory {
    private String productName;
    private int totalQuantity;

    public CustomerOrderHistory(String productName, int totalQuantity) {
        this.productName = productName;
        this.totalQuantity = totalQuantity;
    }

    public String getProductName() {
        return productName;
    }

    public int getTotalQuantity() {
        return totalQuantity;
    }
}
```

**🔍 What's happening?**

This is a simpler model because the stored procedure only returns two pieces of information:
- The product name
- The total quantity ordered across all orders

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Check both model files
3. Commit message: `"Added Shipper and CustomerOrderHistory model classes"`
4. Click **Commit** or **Commit and Push**

---

## 🗃️ Part 4: Creating the DataManager Class

This is the heart of our application - the class that handles ALL database operations!

### Step 7: Create the DataManager Class Structure

1. Right-click on `com.pluralsight.db`
2. Select **New → Java Class**
3. Name it: `DataManager`
4. Click **OK**

**Type this code:**

```java
package com.pluralsight.db;

import com.pluralsight.models.CustomerOrderHistory;
import com.pluralsight.models.Shipper;
import org.apache.commons.dbcp2.BasicDataSource;

import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.List;

public class DataManager {
    private BasicDataSource dataSource;

    public DataManager(String url, String username, String password) {
        this.dataSource = new BasicDataSource();
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
    }
}
```

**🔍 What's happening?**

Let's break down each import:

- **`BasicDataSource`** - The connection pool manager from Apache DBCP2
- **`Connection`** - Represents a connection to the database
- **`PreparedStatement`** - A pre-compiled SQL statement (safe from SQL injection!)
- **`CallableStatement`** - Used to call stored procedures
- **`ResultSet`** - Holds the results of a query (like a table of data)
- **`ArrayList` and `List`** - For storing multiple results

**The Constructor:**

```java
public DataManager(String url, String username, String password) {
    this.dataSource = new BasicDataSource();
    dataSource.setUrl(url);
    dataSource.setUsername(username);
    dataSource.setPassword(password);
}
```

- Creates a connection pool with the database location and credentials
- The pool will automatically create and manage connections as needed
- **URL format:** `jdbc:mysql://localhost:3306/northwind`
  - `jdbc:mysql://` - Protocol (like `https://` for websites)
  - `localhost:3306` - Server address and port
  - `/northwind` - Database name

---

## ➕ Part 5: CREATE Operation - Inserting a New Shipper

### Step 8: Add the Insert Method

Add this method to your `DataManager` class (inside the class, after the constructor):

```java
public void insertShipper(String companyName, String phoneNumber) {
    try (Connection connection = dataSource.getConnection();
         PreparedStatement preparedStatement = connection.prepareStatement(
                 "INSERT INTO shippers (CompanyName, Phone) VALUES (?, ?)",
                 PreparedStatement.RETURN_GENERATED_KEYS)) {

        preparedStatement.setString(1, companyName);
        preparedStatement.setString(2, phoneNumber);
        preparedStatement.executeUpdate();

        try (ResultSet generatedKeys = preparedStatement.getGeneratedKeys()) {
            if (generatedKeys.next()) {
                int shipperId = generatedKeys.getInt(1);
                System.out.println("New Shipper ID: " + shipperId);
            }
        }
    } catch (Exception ex) {
        ex.printStackTrace();
    }
}
```

**🔍 What's happening? Let's break it down line by line:**

**Try-with-resources:**
```java
try (Connection connection = dataSource.getConnection();
     PreparedStatement preparedStatement = connection.prepareStatement(...)) {
```
- Resources inside `try()` are automatically closed when done
- No need for manual `connection.close()` - Java handles it!
- Like a self-closing door - you don't need to remember to close it

**The SQL with placeholders:**
```java
"INSERT INTO shippers (CompanyName, Phone) VALUES (?, ?)"
```
- The `?` marks are **placeholders** for values
- This is called a **parameterized query**
- NEVER concatenate user input into SQL strings - that causes SQL injection vulnerabilities!

**Setting the parameters:**
```java
preparedStatement.setString(1, companyName);  // First ? gets companyName
preparedStatement.setString(2, phoneNumber);  // Second ? gets phoneNumber
```
- Parameters are numbered starting at **1** (not 0!)
- `setString()` properly escapes special characters (prevents SQL injection)

**Getting the auto-generated ID:**
```java
PreparedStatement.RETURN_GENERATED_KEYS
```
- Tells MySQL "I want to know the ID you created"
- `generatedKeys.getInt(1)` retrieves that new ID

**⚠️ Security Note:** We use `PreparedStatement` instead of `Statement` because:

```java
// ❌ DANGEROUS - SQL Injection vulnerability!
String sql = "INSERT INTO shippers VALUES ('" + companyName + "', '" + phone + "')";

// ✅ SAFE - Parameters are escaped automatically
preparedStatement.setString(1, companyName);
```

If someone entered `'; DROP TABLE shippers; --` as a company name, the dangerous version would DELETE your table!

---

## 📖 Part 6: READ Operations - Getting Shippers

### Step 9: Add Get Shipper by ID Method

Add this method to your `DataManager` class:

```java
public Shipper getShipperById(int shipperIdFromUser) {
    Shipper shipper = null;

    try (Connection connection = dataSource.getConnection();
         PreparedStatement preparedStatement = connection.prepareStatement(
                 "SELECT * FROM shippers WHERE ShipperID = ?")) {

        preparedStatement.setInt(1, shipperIdFromUser);

        try (ResultSet resultSet = preparedStatement.executeQuery()) {
            if (resultSet.next()) {
                int shipperIdFromDB = resultSet.getInt("ShipperID");
                String companyName = resultSet.getString("CompanyName");
                String phoneNumber = resultSet.getString("Phone");

                shipper = new Shipper(shipperIdFromDB, companyName, phoneNumber);
            }
        }
    } catch (Exception ex) {
        ex.printStackTrace();
    }
    return shipper;
}
```

**🔍 What's happening?**

**Initialize to null:**
```java
Shipper shipper = null;
```
- If no shipper is found, we return `null`
- The calling code should check for this!

**Execute a query (not update):**
```java
ResultSet resultSet = preparedStatement.executeQuery()
```
- `executeQuery()` - For SELECT statements (returns data)
- `executeUpdate()` - For INSERT, UPDATE, DELETE (changes data)

**Reading from ResultSet:**
```java
if (resultSet.next()) {
    int shipperIdFromDB = resultSet.getInt("ShipperID");
    String companyName = resultSet.getString("CompanyName");
```
- `resultSet.next()` moves to the next row (returns `false` if no more rows)
- `getInt("ColumnName")` reads an integer column
- `getString("ColumnName")` reads a text column

**💡 Real-world analogy:** A ResultSet is like a spreadsheet cursor. You start above the first row, and `next()` moves down one row at a time.

### Step 10: Add Get All Shippers Method

Add this method to your `DataManager` class:

```java
public List<Shipper> getAllShippers() {
    List<Shipper> shippers = new ArrayList<>();

    try (Connection connection = dataSource.getConnection();
         PreparedStatement preparedStatement = connection.prepareStatement("SELECT * FROM shippers");
         ResultSet resultSet = preparedStatement.executeQuery()) {

        while (resultSet.next()) {
            int shipperIdFromDB = resultSet.getInt("ShipperID");
            String companyName = resultSet.getString("CompanyName");
            String phoneNumber = resultSet.getString("Phone");

            Shipper shipper = new Shipper(shipperIdFromDB, companyName, phoneNumber);
            shippers.add(shipper);
        }

    } catch (Exception ex) {
        ex.printStackTrace();
    }
    return shippers;
}
```

**🔍 What's happening?**

**Return a List instead of a single object:**
```java
List<Shipper> shippers = new ArrayList<>();
```
- We expect multiple results, so we use a List
- ArrayList is a good default choice for lists

**Loop through all results:**
```java
while (resultSet.next()) {
    // ... create shipper and add to list
    shippers.add(shipper);
}
```
- `while` instead of `if` - keeps going until no more rows
- Each iteration creates a new Shipper and adds it to our list

**Notice the nested try-with-resources:**
```java
try (Connection connection = dataSource.getConnection();
     PreparedStatement preparedStatement = connection.prepareStatement("SELECT * FROM shippers");
     ResultSet resultSet = preparedStatement.executeQuery()) {
```
- All three resources are declared in the same try block
- All three are automatically closed when done!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added CREATE and READ operations for Shippers"`
3. Click **Commit** or **Commit and Push**

---

## ✏️ Part 7: UPDATE Operation - Changing a Shipper's Phone Number

### Step 11: Add the Update Method

Add this method to your `DataManager` class:

```java
public void updateShipperPhoneNumber(int shipperId, String newPhoneNumber) {
    try (Connection connection = dataSource.getConnection();
         PreparedStatement preparedStatement = connection.prepareStatement(
                 "UPDATE shippers SET Phone = ? WHERE ShipperID = ?")) {

        preparedStatement.setString(1, newPhoneNumber);
        preparedStatement.setInt(2, shipperId);
        preparedStatement.executeUpdate();
    } catch (Exception ex) {
        ex.printStackTrace();
    }
}
```

**🔍 What's happening?**

**The UPDATE SQL:**
```sql
UPDATE shippers SET Phone = ? WHERE ShipperID = ?
```
- `UPDATE tablename` - Which table to modify
- `SET column = ?` - Which column to change and the new value
- `WHERE condition` - Which row(s) to update

**⚠️ Important:** Always include a WHERE clause in UPDATE statements! Without it, you'd update EVERY row in the table!

**Parameter order matters:**
```java
preparedStatement.setString(1, newPhoneNumber);  // First ? is Phone
preparedStatement.setInt(2, shipperId);          // Second ? is ShipperID
```
- Match the order of `?` in your SQL statement
- `setString()` for text, `setInt()` for numbers

---

## 🗑️ Part 8: DELETE Operation - Removing a Shipper

### Step 12: Add the Delete Method

Add this method to your `DataManager` class:

```java
public void deleteShipper(int shipperId) {
    try (Connection connection = dataSource.getConnection();
         PreparedStatement preparedStatement = connection.prepareStatement(
                 "DELETE FROM shippers WHERE ShipperID = ?")) {
        preparedStatement.setInt(1, shipperId);
        preparedStatement.executeUpdate();
    } catch (Exception ex) {
        ex.printStackTrace();
    }
}
```

**🔍 What's happening?**

**The DELETE SQL:**
```sql
DELETE FROM shippers WHERE ShipperID = ?
```
- `DELETE FROM tablename` - Which table
- `WHERE condition` - Which row(s) to delete

**⚠️ CRITICAL:** NEVER forget the WHERE clause in a DELETE statement! Running `DELETE FROM shippers` without WHERE will delete ALL shippers!

**💡 Real-world tip:** Many production systems use "soft delete" instead - adding a column like `IsDeleted` and setting it to `true` instead of actually removing the row. This allows for data recovery!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added UPDATE and DELETE operations for Shippers"`
3. Click **Commit** or **Commit and Push**

---

## 📞 Part 9: Calling a Stored Procedure

### Step 13: Add the Stored Procedure Method

Stored procedures are pre-written SQL code stored in the database. They're like functions for databases!

Add this method to your `DataManager` class:

```java
public List<CustomerOrderHistory> searchCustomerOrderHistory(String customerId) {
    List<CustomerOrderHistory> orderHistoryList = new ArrayList<>();

    try (Connection connection = dataSource.getConnection();
         CallableStatement callableStatement = connection.prepareCall("{CALL CustOrderHist(?)}")) {
        callableStatement.setString(1, customerId);

        try (ResultSet resultSet = callableStatement.executeQuery()) {
            while (resultSet.next()) {
                String productName = resultSet.getString("ProductName");
                int totalQuantity = resultSet.getInt("Total");

                CustomerOrderHistory orderHistory = new CustomerOrderHistory(productName, totalQuantity);
                orderHistoryList.add(orderHistory);
            }
        }
    } catch (Exception ex) {
        ex.printStackTrace();
    }
    return orderHistoryList;
}
```

**🔍 What's happening?**

**CallableStatement instead of PreparedStatement:**
```java
CallableStatement callableStatement = connection.prepareCall("{CALL CustOrderHist(?)}")
```
- `CallableStatement` is specifically for stored procedures
- The syntax `{CALL ProcedureName(?)}` is JDBC's standard way to call procedures
- The curly braces `{}` are required!

**Why use stored procedures?**
1. **Performance** - Pre-compiled SQL runs faster
2. **Security** - Users can run procedures without direct table access
3. **Reusability** - Same logic available to any application
4. **Maintainability** - Change the procedure without changing application code

**The CustOrderHist procedure:**
- This is a built-in procedure in the Northwind database
- It takes a customer ID and returns their order history
- Shows product names and total quantities ordered

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added stored procedure call for customer order history"`
3. Click **Commit** or **Commit and Push**

---

## 🖥️ Part 10: Creating the Main Application

### Step 14: Create the MainApp Class

Now let's create the user interface that ties everything together!

1. Right-click on `com.pluralsight.main`
2. Select **New → Java Class**
3. Name it: `MainApp`
4. Click **OK**

**Type this code:**

```java
package com.pluralsight.main;

import com.pluralsight.db.DataManager;
import com.pluralsight.models.CustomerOrderHistory;
import com.pluralsight.models.Shipper;

import java.util.List;
import java.util.Scanner;

public class MainApp {
    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("User and Password are needed!");
            System.exit(1);
        }

        String username = args[0];
        String password = args[1];
        String url = "jdbc:mysql://localhost:3306/northwind";

        DataManager dataManager = new DataManager(url, username, password);

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Insert Shipper"); // C
            System.out.println("2. Get Shipper by ID"); // R
            System.out.println("3. Get All Shippers"); // R
            System.out.println("4. Update Shipper Phone Number"); // U
            System.out.println("5. Delete Shipper"); // D
            System.out.println("6. Search Customer Order History");
            System.out.println("7. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine();


            switch (choice) {
                case 1 -> {
                    System.out.print("Enter company name: ");
                    String companyName = scanner.nextLine();
                    System.out.print("Enter phone number: ");
                    String phoneNumber = scanner.nextLine();
                    dataManager.insertShipper(companyName, phoneNumber);
                }
                case 2 -> {
                    System.out.print("Enter Shipper ID: ");
                    int shipperId = scanner.nextInt();
                    scanner.nextLine();

                    Shipper shipper = dataManager.getShipperById(shipperId);

                    if (shipper != null) {
                        System.out.println("Shipper ID: " + shipper.getShipperId());
                        System.out.println("Company Name: " + shipper.getCompanyName());
                        System.out.println("Phone Number: " + shipper.getPhoneNumber());
                    } else {
                        System.out.println("Shipper not found!");
                    }
                }
                case 3 -> {
                    List<Shipper> shippers = dataManager.getAllShippers();
                    for (Shipper s : shippers) {
                        System.out.println("Shipper ID: " + s.getShipperId());
                        System.out.println("Company Name: " + s.getCompanyName());
                        System.out.println("Phone Number: " + s.getPhoneNumber());
                        System.out.println();
                    }
                }
                case 4 -> {
                    System.out.print("Enter shipper ID: ");
                    int updateShipperId = scanner.nextInt();
                    scanner.nextLine();
                    System.out.print("Enter new phone number: ");
                    String newPhoneNumber = scanner.nextLine();
                    dataManager.updateShipperPhoneNumber(updateShipperId, newPhoneNumber);
                }
                case 5 -> {
                    System.out.print("Enter shipper ID: ");
                    int deleteShipperId = scanner.nextInt();
                    scanner.nextLine();
                    dataManager.deleteShipper(deleteShipperId);
                }
                case 6 -> {
                    System.out.print("Enter Customer ID: ");
                    String customerId = scanner.nextLine();

                    List<CustomerOrderHistory> orderHistoryList = dataManager.searchCustomerOrderHistory(customerId);
                    for (CustomerOrderHistory orderHistory : orderHistoryList) {
                        System.out.println("Product Name: " + orderHistory.getProductName());
                        System.out.println("Total Quantity: " + orderHistory.getTotalQuantity());
                        System.out.println();
                    }
                }
                case 7 -> {
                    System.out.println("Exiting...");
                    scanner.close();
                    System.exit(0);
                }
                default -> System.out.println("Invalid choice. Please try again.");
            }

        }
    }
}
```

**🔍 What's happening? Let's break it down:**

**Command line arguments for security:**
```java
if (args.length != 2) {
    System.out.println("User and Password are needed!");
    System.exit(1);
}
String username = args[0];
String password = args[1];
```
- We NEVER hardcode database passwords in our code!
- Users provide credentials when running the program
- This keeps passwords out of version control (Git)

**The Scanner "newline trap":**
```java
int choice = scanner.nextInt();
scanner.nextLine();  // Consume the leftover newline!
```
- `nextInt()` reads the number but leaves the Enter key (newline) behind
- `nextLine()` would then read that empty newline instead of your next input
- Always add `scanner.nextLine()` after `nextInt()` to clear it!

**Enhanced switch statements:**
```java
case 1 -> {
    // code here
}
```
- This is the modern Java syntax (Java 14+)
- No `break` statements needed - no fall-through!
- Cleaner and less error-prone than traditional switch

**CRUD operations labeled:**
```java
System.out.println("1. Insert Shipper"); // C - Create
System.out.println("2. Get Shipper by ID"); // R - Read
System.out.println("4. Update Shipper Phone Number"); // U - Update
System.out.println("5. Delete Shipper"); // D - Delete
```
- These comments show the CRUD pattern in action!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added MainApp with menu-driven interface"`
3. Click **Commit** or **Commit and Push**

---

## ▶️ Part 11: Running Your Application

### Step 15: Configure Run Settings with Arguments

Since we pass username and password as arguments, we need to configure IntelliJ:

1. Click **Run → Edit Configurations...**
2. Click the **+** button → Select **Application**
3. Name: `MainApp`
4. Main class: Click the **...** button and select `com.pluralsight.main.MainApp`
5. **Program arguments:** `root yourpassword` (replace with YOUR MySQL credentials)
6. Click **Apply** then **OK**

**⚠️ Security Note:** In a real project, you'd use environment variables or a secure vault for credentials. Never commit passwords to Git!

### Step 16: Run and Test Your Application

1. Click the green **Run** button (▶️) or press **Shift+F10**
2. You should see the menu appear in the console

**Test each operation:**

**Test 1: View All Shippers (option 3)**
```
Choose an option: 3

Shipper ID: 1
Company Name: Speedy Express
Phone Number: (503) 555-9831

Shipper ID: 2
Company Name: United Package
Phone Number: (503) 555-3199
...
```

**Test 2: Insert a New Shipper (option 1)**
```
Choose an option: 1
Enter company name: Fast Delivery Inc
Enter phone number: (555) 123-4567
New Shipper ID: 4
```

**Test 3: Get Shipper by ID (option 2)**
```
Choose an option: 2
Enter Shipper ID: 4
Shipper ID: 4
Company Name: Fast Delivery Inc
Phone Number: (555) 123-4567
```

**Test 4: Update Phone Number (option 4)**
```
Choose an option: 4
Enter shipper ID: 4
Enter new phone number: (555) 999-8888
```

**Test 5: Delete Shipper (option 5)**
```
Choose an option: 5
Enter shipper ID: 4
```

**Test 6: Customer Order History (option 6)**
```
Choose an option: 6
Enter Customer ID: ALFKI

Product Name: Aniseed Syrup
Total Quantity: 6

Product Name: Chartreuse verte
Total Quantity: 21
...
```

### 🔄 Final Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Project complete - Northwind Database Application with CRUD and stored procedures"`
3. Click **Commit and Push**

---

## 📊 Complete Project Structure

Your final project should look like this:

```
NorthwindDatabaseApp/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── com/
                └── pluralsight/
                    ├── db/
                    │   └── DataManager.java
                    ├── main/
                    │   └── MainApp.java
                    └── models/
                        ├── CustomerOrderHistory.java
                        └── Shipper.java
```

---

## 🧠 Key Concepts Summary

### JDBC Basics
- **JDBC** = Java Database Connectivity - the standard API for database access
- **Connection** = A session with a database
- **PreparedStatement** = Pre-compiled SQL (safe and fast)
- **ResultSet** = Table of results from a query
- **CallableStatement** = For calling stored procedures

### Connection Pooling
- Keeps connections ready to use (no creating/destroying each time)
- **BasicDataSource** manages the pool
- Dramatically improves performance in real applications

### CRUD Operations
- **Create** = INSERT INTO
- **Read** = SELECT
- **Update** = UPDATE ... SET
- **Delete** = DELETE FROM

### Security Best Practices
1. **Always use PreparedStatement** - prevents SQL injection
2. **Never hardcode passwords** - use arguments or environment variables
3. **Always use WHERE** in UPDATE and DELETE - prevents accidental mass changes
4. **Close resources** - use try-with-resources

---

## 💪 Challenge Exercises (Optional)

1. **Add a searchShippersByName method** that finds shippers whose name contains a search term
2. **Add confirmation messages** to update and delete operations (show "Updated successfully!")
3. **Add input validation** - check that phone numbers are in the right format
4. **Count rows affected** - `executeUpdate()` returns the number of rows changed; display this to the user
5. **Add a Product model and methods** - practice CRUD on a different table

---

## 🎉 Congratulations!

You've built a complete database application! This pattern is used in:

- Web applications (Spring Boot, etc.)
- Mobile app backends
- Enterprise systems
- E-commerce platforms

**What you've mastered:**

- Connecting Java to MySQL databases
- Using connection pooling for efficiency
- Performing all CRUD operations safely
- Calling stored procedures
- Organizing database code properly
- Securing database credentials

**Next steps:**

1. Practice with other Northwind tables (Products, Customers, Orders)
2. Learn about transactions (multiple operations that succeed or fail together)
3. Explore Spring Data JPA (an easier way to do database access)
4. Add unit tests for your DataManager methods

Keep this project as a reference - you'll use these patterns in every database application you build!
