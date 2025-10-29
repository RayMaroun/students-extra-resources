# 🏨 Hotel Reservation System

## A Step-by-Step Tutorial for Object-Oriented Programming, Unit Testing & Class Interactions

---

## 🎯 Project Overview

We're building a Hotel Reservation System that teaches all Week 5 concepts: Object-Oriented Programming principles, creating proper classes with encapsulation, writing unit tests with JUnit, using static methods/variables, and making classes interact. This project shows how real-world systems are designed using OOP!

**What You'll Master:**

- Thinking in objects and responsibilities
- Creating classes with proper encapsulation
- Writing constructors, getters, and setters
- Method overloading
- Unit testing with JUnit 5
- Static methods and variables
- Class relationships (Has-A)
- Making objects work together

---

## 📁 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `HotelReservationSystem`
4. Location: `~/pluralsight/workbook-4` (or `C:/pluralsight/workbook-4` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share Project to GitHub Immediately

1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `HotelReservationSystem`
3. Description: "Week 5 OOP, Unit Testing, and Class Interactions practice"
4. Click **Share**
5. In the next dialog, click **Add**

**Why share now?** Start with good habits - version control from the beginning!

### Step 2: Create Package Structure

1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight.hotel`
4. Click **OK**

---

## 🤔 Part 1: Thinking in Objects - Understanding Responsibilities

### Step 3: Planning Our System (The OOP Way)

Before writing any code, let's think about our hotel system like a real hotel:

Create a new class called `HotelSystemPlanning`:

```java
package com.pluralsight.hotel;

public class HotelSystemPlanning {
    public static void main(String[] args) {
        /*
         * THINKING IN OBJECTS - HOTEL SYSTEM
         *
         * What OBJECTS do we need? (Nouns)
         * - Room (the physical hotel room)
         * - Guest (the person staying)
         * - Reservation (the booking)
         * - Hotel (the building with rooms)
         * - Employee (workers at the hotel)
         *
         * What are their RESPONSIBILITIES?
         *
         * Room - KNOWS:
         *   - Room number
         *   - Room type (single, double, suite)
         *   - Price per night
         *   - Is it clean?
         *   - Is it occupied?
         * Room - DOES:
         *   - Can be checked into
         *   - Can be checked out of
         *   - Can be cleaned
         *
         * Guest - KNOWS:
         *   - Name
         *   - Email
         *   - Phone number
         * Guest - DOES:
         *   - Makes reservations
         *   - Checks in/out
         *
         * Reservation - KNOWS:
         *   - Which guest
         *   - Which room
         *   - Check-in date
         *   - Check-out date
         *   - Total cost
         * Reservation - DOES:
         *   - Calculates total cost
         *   - Confirms booking
         *   - Cancels booking
         *
         * This is ENCAPSULATION - each object has its own data and methods!
         */

        System.out.println("=== HOTEL SYSTEM PLANNING ===");
        System.out.println("Objects identified: Room, Guest, Reservation, Hotel");
        System.out.println("Each object has specific responsibilities");
        System.out.println("This is Object-Oriented thinking!");
    }
}
```

**🔍 What's happening? Understanding OOP Thinking:**

**Objects vs Procedural Programming:**

- **Procedural**: One big file with all functions and variables mixed together
- **OOP**: Separate "things" (objects) each responsible for their own data and actions
- Like a real hotel - the front desk doesn't clean rooms, housekeeping doesn't make reservations

**The Two Types of Responsibilities:**

1. **KNOWS** (Data/Attributes) - Information the object stores
   - Room knows its number, type, price
   - Like a filing cabinet with labeled folders
2. **DOES** (Methods/Behaviors) - Actions the object can perform
   - Room can be cleaned, checked into
   - Like buttons on a machine

**Encapsulation - The Core Principle:**

- Each object is a "black box" - hides HOW it works
- Other objects only see WHAT it can do
- Like a TV - you use the remote, not the internal circuits
- Protects data from being changed incorrectly

**Specialization:**

- Each object is an expert at ONE thing
- Room doesn't know about payments
- Reservation doesn't clean rooms
- Like real jobs - chef cooks, waiter serves, cashier handles money

**▶️ Run HotelSystemPlanning** to see the planning output!

### 📝 Commit Your Work:

1. Click **Commit** button (✓) or press **Ctrl+K** / **Cmd+K**
2. Review changes - `HotelSystemPlanning.java` should be green (new file)
3. Commit message: `"Added OOP planning and object identification for hotel system"`
4. Click **Commit and Push**

---

## 🏗️ Part 2: Creating Classes with Proper Encapsulation

### Step 4: Create the Room Class

Create a new class called `Room`:

```java
package com.pluralsight.hotel;

public class Room {
    // PRIVATE instance variables - hidden from outside world
    private int roomNumber;
    private String roomType;  // "SINGLE", "DOUBLE", "SUITE"
    private double pricePerNight;
    private boolean isOccupied;
    private boolean isClean;

    // CONSTRUCTOR - The "birth certificate" of Room objects
    public Room(int roomNumber, String roomType, double pricePerNight) {
        this.roomNumber = roomNumber;
        this.roomType = roomType;
        this.pricePerNight = pricePerNight;
        this.isOccupied = false;  // New rooms start unoccupied
        this.isClean = true;       // New rooms start clean
    }

    // GETTERS - "Windows" to look at private data
    public int getRoomNumber() {
        return roomNumber;
    }

    public String getRoomType() {
        return roomType;
    }

    public double getPricePerNight() {
        return pricePerNight;
    }

    public boolean isOccupied() {
        return isOccupied;
    }

    public boolean isClean() {
        return isClean;
    }

    // DERIVED GETTER - Calculates based on other data
    public boolean isAvailable() {
        // A room is only available if it's clean AND not occupied
        return isClean && !isOccupied;
    }

    // SETTER - Only for price (things that should change)
    public void setPricePerNight(double pricePerNight) {
        // Validation - price can't be negative!
        if (pricePerNight > 0) {
            this.pricePerNight = pricePerNight;
        } else {
            System.out.println("ERROR: Price must be positive!");
        }
    }

    // METHODS - Actions the room can perform
    public void checkIn() {
        if (isAvailable()) {
            isOccupied = true;
            isClean = false;  // Room gets dirty when used
            System.out.println("Room " + roomNumber + " checked in successfully");
        } else {
            System.out.println("Room " + roomNumber + " is not available!");
        }
    }

    public void checkOut() {
        if (isOccupied) {
            isOccupied = false;
            System.out.println("Room " + roomNumber + " checked out");
        } else {
            System.out.println("Room " + roomNumber + " is not occupied!");
        }
    }

    public void cleanRoom() {
        if (!isOccupied) {
            isClean = true;
            System.out.println("Room " + roomNumber + " has been cleaned");
        } else {
            System.out.println("Cannot clean occupied room " + roomNumber);
        }
    }

    // toString method - for easy printing
    @Override
    public String toString() {
        return String.format("Room %d (%s): $%.2f/night - %s",
            roomNumber, roomType, pricePerNight,
            isAvailable() ? "Available" : "Not Available");
    }
}
```

**🔍 What's happening? Deep Dive into Class Structure:**

**Access Modifiers - The Security System:**

- **`private`** = Only this class can see/touch
  - Like a locked diary - only you have the key
  - Protects data from being messed up by other classes
- **`public`** = Everyone can use
  - Like a public phone - anyone can use it
  - Methods are usually public (the interface to the world)

**Instance Variables - The Object's Memory:**

```java
private int roomNumber;
```

- Each Room object gets its OWN copy
- Room 101's `roomNumber` is separate from Room 102's
- Like each person having their own wallet

**Constructor - The Object Factory:**

```java
public Room(int roomNumber, String roomType, double pricePerNight)
```

- Special method that runs ONCE when object is created
- Name MUST match class name exactly
- NO return type (not even void)
- Sets initial values - like filling out a form

**The `this` Keyword - "My Own":**

```java
this.roomNumber = roomNumber;
```

- `this.roomNumber` = "MY roomNumber variable"
- `roomNumber` = "the parameter passed in"
- Solves naming conflict
- Like saying "MY car" vs "THE car you're talking about"

**Getters - Read-Only Access:**

- Allow reading private data
- Can't accidentally change values
- Standard naming: `get` + VariableName
- Boolean getters use `is` instead: `isOccupied()`

**Setters - Controlled Modification:**

- Allow changing private data WITH RULES
- Can validate before changing
- We only made setter for price (not room number - that shouldn't change!)
- Can reject invalid values

**Derived Getters - Calculated Properties:**

```java
public boolean isAvailable() {
    return isClean && !isOccupied;
}
```

- No backing variable - calculates on the fly
- Based on other variables
- Avoids redundant storage

**Business Logic Methods:**

- `checkIn()`, `checkOut()`, `cleanRoom()`
- Contain the "rules" of the business
- Change object state in controlled ways
- Enforce real-world constraints

### Step 5: Test the Room Class

Create `TestRoom` class:

```java
package com.pluralsight.hotel;

public class TestRoom {
    public static void main(String[] args) {
        System.out.println("=== TESTING ROOM CLASS ===\n");

        // Create a room object
        Room room101 = new Room(101, "DOUBLE", 150.00);

        // Test getters
        System.out.println("Room Number: " + room101.getRoomNumber());
        System.out.println("Room Type: " + room101.getRoomType());
        System.out.println("Price: $" + room101.getPricePerNight());
        System.out.println("Is Available? " + room101.isAvailable());
        System.out.println();

        // Test checking in
        System.out.println("Guest checking in...");
        room101.checkIn();
        System.out.println("Is Available now? " + room101.isAvailable());
        System.out.println("Is Occupied? " + room101.isOccupied());
        System.out.println("Is Clean? " + room101.isClean());
        System.out.println();

        // Try to clean occupied room (should fail)
        System.out.println("Trying to clean occupied room...");
        room101.cleanRoom();
        System.out.println();

        // Check out
        System.out.println("Guest checking out...");
        room101.checkOut();
        System.out.println("Is Occupied? " + room101.isOccupied());
        System.out.println();

        // Clean the room
        System.out.println("Housekeeping cleaning room...");
        room101.cleanRoom();
        System.out.println("Is Available now? " + room101.isAvailable());
        System.out.println();

        // Test price setter with validation
        System.out.println("Testing price validation...");
        room101.setPricePerNight(-50);  // Should fail
        room101.setPricePerNight(175.00);  // Should work
        System.out.println("New price: $" + room101.getPricePerNight());

        // Test toString
        System.out.println("\n" + room101);
    }
}
```

**▶️ Run TestRoom** and watch how encapsulation protects the data!

### 📝 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `Room.java` (green - new class)
   - `TestRoom.java` (green - test class)
3. Commit message: `"Added Room class with proper encapsulation and business logic"`
4. Click **Commit and Push**

---

## 🧪 Part 3: Unit Testing with JUnit

### Step 6: Create Your First Unit Test

The easiest way to create a test class:

1. Open `Room.java`
2. Right-click on the class name `Room` (or press **Alt+Enter** on Windows / **Option+Enter** on Mac)
3. Select **Generate** → **Test** (or just **Create Test** from Alt+Enter menu)
4. In the dialog:
   - Testing library: **JUnit5**
   - If you see "JUnit5 library not found in the module":
     - Click the **Fix** button
     - This automatically adds JUnit to your project!
   - Select methods you want to test (or leave unchecked to start empty)
   - Click **OK**

This creates an empty test class in `src/test/java/com/pluralsight/hotel/`

### Step 7: Write Unit Tests with Proper Structure

```java
package com.pluralsight.hotel;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class RoomTest {

    @Test
    public void isAvailable_NewRoom_ReturnsTrue() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);

        // Act
        boolean isAvailable = testRoom.isAvailable();

        // Assert
        assertTrue(isAvailable, "New room should be available");
    }

    @Test
    public void isOccupied_NewRoom_ReturnsFalse() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);

        // Act
        boolean isOccupied = testRoom.isOccupied();

        // Assert
        assertFalse(isOccupied, "New room should not be occupied");
    }

    @Test
    public void isClean_NewRoom_ReturnsTrue() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);

        // Act
        boolean isClean = testRoom.isClean();

        // Assert
        assertTrue(isClean, "New room should be clean");
    }

    @Test
    public void checkIn_AvailableRoom_MakesRoomOccupiedAndDirty() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);

        // Act
        testRoom.checkIn();

        // Assert
        assertTrue(testRoom.isOccupied(), "Room should be occupied after check-in");
        assertFalse(testRoom.isClean(), "Room should be dirty after check-in");
        assertFalse(testRoom.isAvailable(), "Room should not be available after check-in");
    }

    @Test
    public void checkIn_UnavailableRoom_DoesNotChangeStatus() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        testRoom.checkIn();  // First guest checks in
        testRoom.checkOut(); // Guest checks out - room is now dirty

        // Act
        testRoom.checkIn();  // Try to check into dirty room

        // Assert
        assertFalse(testRoom.isOccupied(), "Dirty room should not allow check-in");
        assertFalse(testRoom.isAvailable(), "Dirty room should remain unavailable");
    }

    @Test
    public void checkOut_OccupiedRoom_MakesRoomUnoccupied() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        testRoom.checkIn();  // Guest checks in first

        // Act
        testRoom.checkOut();

        // Assert
        assertFalse(testRoom.isOccupied(), "Room should not be occupied after checkout");
        assertFalse(testRoom.isClean(), "Room should still be dirty after checkout");
    }

    @Test
    public void cleanRoom_UnoccupiedRoom_MakesRoomClean() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        testRoom.checkIn();   // Guest checks in
        testRoom.checkOut();  // Guest checks out - room is dirty

        // Act
        testRoom.cleanRoom();

        // Assert
        assertTrue(testRoom.isClean(), "Room should be clean after cleaning");
        assertTrue(testRoom.isAvailable(), "Clean, unoccupied room should be available");
    }

    @Test
    public void cleanRoom_OccupiedRoom_DoesNotClean() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        testRoom.checkIn();  // Room is occupied

        // Act
        testRoom.cleanRoom();  // Try to clean occupied room

        // Assert
        assertFalse(testRoom.isClean(), "Occupied room should not be cleaned");
    }

    @Test
    public void setPricePerNight_NegativePrice_DoesNotChangePrice() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        double originalPrice = testRoom.getPricePerNight();

        // Act
        testRoom.setPricePerNight(-50);

        // Assert
        assertEquals(originalPrice, testRoom.getPricePerNight(),
            "Negative price should not be accepted");
    }

    @Test
    public void setPricePerNight_ValidPrice_UpdatesPrice() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        double newPrice = 200.00;

        // Act
        testRoom.setPricePerNight(newPrice);

        // Assert
        assertEquals(newPrice, testRoom.getPricePerNight(),
            "Valid price should be accepted");
    }

    @Test
    public void isAvailable_CleanAndNotOccupied_ReturnsTrue() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        // Room starts clean and not occupied

        // Act
        boolean available = testRoom.isAvailable();

        // Assert
        assertTrue(available, "Clean and unoccupied room should be available");
    }

    @Test
    public void isAvailable_DirtyRoom_ReturnsFalse() {
        // Arrange
        Room testRoom = new Room(101, "DOUBLE", 150.00);
        testRoom.checkIn();   // Make room occupied and dirty
        testRoom.checkOut();  // Now unoccupied but still dirty

        // Act
        boolean available = testRoom.isAvailable();

        // Assert
        assertFalse(available, "Dirty room should not be available");
    }
}
```

**🔍 What's happening? Understanding Unit Testing:**

**What is Unit Testing?**

- Testing individual "units" (methods) of code
- Automated - runs with one click
- Repeatable - same test, same result
- Fast - milliseconds to run
- Like quality control in a factory

**Test Naming Convention:**

```java
methodName_StateUnderTest_ExpectedBehavior()
```

- **methodName**: The method you're testing
- **StateUnderTest**: What situation/condition
- **ExpectedBehavior**: What should happen

Examples:

- `checkIn_AvailableRoom_MakesRoomOccupied`
- `setPricePerNight_NegativePrice_DoesNotChangePrice`
- `isAvailable_DirtyRoom_ReturnsFalse`

This naming makes it IMMEDIATELY clear:

1. What method is being tested
2. Under what conditions
3. What the expected result is

**Test Structure - The AAA Pattern:**
Every test MUST have these three sections clearly marked:

1. **ARRANGE** - Set up test data

   ```java
   // Arrange
   Room testRoom = new Room(101, "DOUBLE", 150.00);
   ```

   - Create objects needed
   - Set initial state
   - Prepare all data for the test

2. **ACT** - Execute the method being tested

   ```java
   // Act
   testRoom.checkIn();
   ```

   - Usually just one or two lines
   - This is THE thing you're testing
   - Keep it focused

3. **ASSERT** - Verify the result
   ```java
   // Assert
   assertTrue(testRoom.isOccupied(), "Room should be occupied");
   ```
   - Check if result matches expectation
   - Can have multiple assertions
   - Include meaningful message for failures

**The @Test Annotation:**

- Marks a method as a test
- JUnit runner finds and executes these
- That's all you need to know for now!

**Assertion Methods You'll Use:**

```java
assertTrue(condition, message)    // Passes if condition is true
assertFalse(condition, message)   // Passes if condition is false
assertEquals(expected, actual, message)  // Passes if values are equal
assertNotEquals(expected, actual, message) // Passes if values are not equal
assertNull(object, message)       // Passes if object is null
assertNotNull(object, message)    // Passes if object is not null
```

**Why Write Tests?**

- Catch bugs early
- Document how code should work
- Confidence when changing code
- Proof that code works correctly
- Professional practice in the industry

**Running Your Tests:**

- Click green arrow next to class name to run ALL tests
- Click green arrow next to specific test method to run ONE test
- Green checkmark ✅ = Test passed
- Red X ❌ = Test failed

**Important Testing Principles:**

1. **Test Behavior, Not Implementation** - Test WHAT it does, not HOW
2. **Each Test is Independent** - One test shouldn't depend on another
3. **Test Edge Cases** - Empty values, negative numbers, null values
4. **Keep Tests Simple** - If a test is complex, the code might be too complex

**▶️ Run the tests:**

- Click green arrow next to class name to run all tests
- Click green arrow next to method to run one test
- Look for green checkmarks!

### 📝 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `pom.xml` (blue - modified with JUnit)
   - `RoomTest.java` (green - new test class)
3. Commit message: `"Added comprehensive JUnit tests for Room class"`
4. Click **Commit and Push**

---

## 🔧 Part 4: Static Methods and Variables

### Step 8: Create a Hotel Class with Static Members

Create `Hotel` class:

```java
package com.pluralsight.hotel;

import java.util.ArrayList;

public class Hotel {
    // INSTANCE variables - each Hotel has its own
    private String hotelName;
    private ArrayList<Room> rooms;

    // STATIC variables - shared by ALL hotels
    private static int totalHotelsCreated = 0;
    private static double totalRevenueAllHotels = 0;

    // STATIC FINAL - constants that never change
    public static final double TAX_RATE = 0.08;  // 8% tax
    public static final int MAX_ROOMS_PER_HOTEL = 100;

    // Constructor
    public Hotel(String hotelName) {
        this.hotelName = hotelName;
        this.rooms = new ArrayList<>();
        totalHotelsCreated++;  // Increment static counter
    }

    // INSTANCE method - works with THIS hotel's data
    public void addRoom(Room room) {
        if (rooms.size() < MAX_ROOMS_PER_HOTEL) {
            rooms.add(room);
            System.out.println("Added room " + room.getRoomNumber() +
                             " to " + hotelName);
        } else {
            System.out.println("Hotel is at maximum capacity!");
        }
    }

    // INSTANCE method - counts THIS hotel's available rooms
    public int getAvailableRoomCount() {
        int count = 0;
        for (Room room : rooms) {
            if (room.isAvailable()) {
                count++;
            }
        }
        return count;
    }

    // STATIC method - doesn't need a hotel object
    public static double calculateTotalWithTax(double amount) {
        return amount + (amount * TAX_RATE);
    }

    // STATIC method - works with static data
    public static int getTotalHotelsCreated() {
        return totalHotelsCreated;
    }

    // STATIC method - adds to global revenue
    public static void recordRevenue(double amount) {
        totalRevenueAllHotels += amount;
    }

    // STATIC method - gets global revenue
    public static double getTotalRevenueAllHotels() {
        return totalRevenueAllHotels;
    }

    // Instance getter
    public String getHotelName() {
        return hotelName;
    }

    // Instance method that uses static method
    public double calculateRoomTotalWithTax(Room room, int nights) {
        double subtotal = room.getPricePerNight() * nights;
        return calculateTotalWithTax(subtotal);  // Using static method
    }
}
```

### Step 9: Create a Utility Class (All Static)

Create `HotelManagementUtils`:

```java
package com.pluralsight.hotel;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;

public class HotelManagementUtils {

    // Private constructor - prevents instantiation
    private HotelManagementUtils() {
        // This class should never be instantiated
        // It's just a collection of static utility methods
    }

    // Static method - formats currency
    public static String formatCurrency(double amount) {
        return String.format("$%,.2f", amount);
    }

    // Static method - calculates nights between dates
    public static long calculateNights(LocalDate checkIn, LocalDate checkOut) {
        return ChronoUnit.DAYS.between(checkIn, checkOut);
    }

    // Static method - validates email format
    public static boolean isValidEmail(String email) {
        return email != null &&
               email.contains("@") &&
               email.contains(".") &&
               email.indexOf("@") < email.lastIndexOf(".");
    }

    // Static method - generates confirmation code
    public static String generateConfirmationCode(String guestName, int roomNumber) {
        // Simple confirmation code: first 3 letters + room number + random
        String prefix = guestName.length() >= 3 ?
            guestName.substring(0, 3).toUpperCase() :
            guestName.toUpperCase();
        int random = (int)(Math.random() * 1000);
        return prefix + "-" + roomNumber + "-" + random;
    }

    // Static method - formats date for display
    public static String formatDate(LocalDate date) {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMM dd, yyyy");
        return date.format(formatter);
    }

    // Static method - calculates season multiplier
    public static double getSeasonMultiplier(LocalDate date) {
        int month = date.getMonthValue();

        // Summer months (June-August) - peak season
        if (month >= 6 && month <= 8) {
            return 1.25;  // 25% increase
        }
        // Winter months (December-February) - off season
        else if (month == 12 || month <= 2) {
            return 0.85;  // 15% discount
        }
        // Spring/Fall - regular season
        else {
            return 1.0;  // No change
        }
    }
}
```

### Step 10: Test Static vs Instance

Create `TestStaticVsInstance`:

```java
package com.pluralsight.hotel;

import java.time.LocalDate;

public class TestStaticVsInstance {
    public static void main(String[] args) {
        System.out.println("=== STATIC VS INSTANCE DEMONSTRATION ===\n");

        // Using STATIC methods without creating objects
        System.out.println("--- Using Static Methods (No Object Needed) ---");
        double price = 150.00;
        double withTax = Hotel.calculateTotalWithTax(price);
        System.out.println("Price: " + HotelManagementUtils.formatCurrency(price));
        System.out.println("With Tax: " + HotelManagementUtils.formatCurrency(withTax));
        System.out.println("Tax Rate: " + (Hotel.TAX_RATE * 100) + "%");

        // Date calculations using static utility
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(3);
        long nights = HotelManagementUtils.calculateNights(checkIn, checkOut);
        System.out.println("\nStay Duration: " + nights + " nights");
        System.out.println("Check-in: " + HotelManagementUtils.formatDate(checkIn));
        System.out.println("Check-out: " + HotelManagementUtils.formatDate(checkOut));

        // Season pricing
        double seasonMultiplier = HotelManagementUtils.getSeasonMultiplier(checkIn);
        System.out.println("Season Multiplier: " + seasonMultiplier);

        System.out.println("\n--- Using Instance Methods (Need Objects) ---");

        // Create hotel instances
        Hotel downtownHotel = new Hotel("Downtown Grand");
        Hotel airportHotel = new Hotel("Airport Express");

        // Each hotel has its OWN rooms (instance data)
        downtownHotel.addRoom(new Room(101, "SUITE", 250.00));
        downtownHotel.addRoom(new Room(102, "DOUBLE", 150.00));

        airportHotel.addRoom(new Room(201, "SINGLE", 99.00));
        airportHotel.addRoom(new Room(202, "DOUBLE", 125.00));

        // Instance method - each hotel counts its OWN rooms
        System.out.println("\n" + downtownHotel.getHotelName() +
            " has " + downtownHotel.getAvailableRoomCount() + " available rooms");
        System.out.println(airportHotel.getHotelName() +
            " has " + airportHotel.getAvailableRoomCount() + " available rooms");

        // Static variable - shared by ALL hotels
        System.out.println("\nTotal Hotels Created: " + Hotel.getTotalHotelsCreated());

        // Recording revenue (static - affects all hotels)
        System.out.println("\n--- Revenue Tracking (Static) ---");
        Hotel.recordRevenue(500.00);  // Downtown hotel revenue
        Hotel.recordRevenue(300.00);  // Airport hotel revenue
        System.out.println("Total Revenue All Hotels: " +
            HotelManagementUtils.formatCurrency(Hotel.getTotalRevenueAllHotels()));

        // Confirmation codes
        System.out.println("\n--- Generating Confirmation Codes ---");
        String code1 = HotelManagementUtils.generateConfirmationCode("John Smith", 101);
        String code2 = HotelManagementUtils.generateConfirmationCode("Jane Doe", 202);
        System.out.println("Confirmation 1: " + code1);
        System.out.println("Confirmation 2: " + code2);

        // Email validation
        System.out.println("\n--- Email Validation ---");
        System.out.println("john@email.com valid? " +
            HotelManagementUtils.isValidEmail("john@email.com"));
        System.out.println("invalid.email valid? " +
            HotelManagementUtils.isValidEmail("invalid.email"));
    }
}
```

**🔍 What's happening? Static vs Instance Explained:**

**Instance Members - Belong to Objects:**

```java
private String hotelName;  // Each hotel has its OWN name
```

- Created when you use `new`
- Each object gets its own copy
- Like each person having their own phone

**Static Members - Belong to the Class:**

```java
private static int totalHotelsCreated;  // Shared by ALL hotels
```

- Created once when program starts
- All objects share the same copy
- Like a public bulletin board everyone reads

**When to Use Static:**

1. **Utility Methods** - Don't need object data

   - Math calculations
   - Formatting functions
   - Validation methods

2. **Shared Data** - Same for all instances

   - Configuration values
   - Counters across all objects
   - Constants (with `final`)

3. **Factory Methods** - Create objects
   - Alternative to constructors
   - Can return null or existing objects

**When NOT to Use Static:**

- Object-specific data (name, ID, etc.)
- Methods that work with instance data
- Anything that should be different per object

**Memory Implications:**

- **Instance**: New copy for each object
- **Static**: Only one copy in memory
- Static uses less memory for shared data
- But can't be garbage collected

**The Math Class Pattern:**

```java
private HotelManagementUtils() { }  // Private constructor
```

- Prevents creating instances
- Class is just a container for static methods
- Like Java's Math class

**Static Final - Constants:**

```java
public static final double TAX_RATE = 0.08;
```

- `static` = Shared by all
- `final` = Can't change (constant)
- `public` = Everyone can read
- NAMING_CONVENTION = ALL_CAPS_WITH_UNDERSCORES

**▶️ Run TestStaticVsInstance** to see the difference!

### 📝 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `Hotel.java` (green)
   - `HotelManagementUtils.java` (green)
   - `TestStaticVsInstance.java` (green)
3. Commit message: `"Added static methods and variables demonstration with Hotel and Utils classes"`
4. Click **Commit and Push**

---

## 🔗 Part 5: Class Interactions - Building Relationships

### Step 11: Create the Guest Class

Create `Guest`:

```java
package com.pluralsight.hotel;

import java.time.LocalDate;

public class Guest {
    private String guestId;
    private String firstName;
    private String lastName;
    private String email;
    private String phoneNumber;
    private LocalDate dateJoined;

    public Guest(String firstName, String lastName, String email, String phoneNumber) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.phoneNumber = phoneNumber;
        this.dateJoined = LocalDate.now();
        // Generate simple ID
        this.guestId = "G" + System.currentTimeMillis() % 10000;
    }

    // Getters
    public String getGuestId() { return guestId; }
    public String getFirstName() { return firstName; }
    public String getLastName() { return lastName; }
    public String getFullName() { return firstName + " " + lastName; }
    public String getEmail() { return email; }
    public String getPhoneNumber() { return phoneNumber; }
    public LocalDate getDateJoined() { return dateJoined; }

    @Override
    public String toString() {
        return String.format("Guest: %s (%s)", getFullName(), email);
    }
}
```

### Step 12: Create the Reservation Class (Has-A Relationships)

Create `Reservation`:

```java
package com.pluralsight.hotel;

import java.time.LocalDate;

public class Reservation {
    // HAS-A relationships - Reservation HAS A Guest and HAS A Room
    private String confirmationCode;
    private Guest guest;              // Composition - needs a guest
    private Room room;                // Composition - needs a room
    private LocalDate checkInDate;
    private LocalDate checkOutDate;
    private double totalCost;
    private String status;  // "CONFIRMED", "CHECKED_IN", "COMPLETED", "CANCELLED"

    // Constructor - requires both guest and room
    public Reservation(Guest guest, Room room, LocalDate checkInDate, LocalDate checkOutDate) {
        this.guest = guest;
        this.room = room;
        this.checkInDate = checkInDate;
        this.checkOutDate = checkOutDate;
        this.status = "CONFIRMED";

        // Generate confirmation code using static utility
        this.confirmationCode = HotelManagementUtils.generateConfirmationCode(
            guest.getLastName(), room.getRoomNumber());

        // Calculate total cost
        calculateTotalCost();
    }

    // Private method to calculate cost
    private void calculateTotalCost() {
        long nights = HotelManagementUtils.calculateNights(checkInDate, checkOutDate);
        double basePrice = room.getPricePerNight() * nights;

        // Apply seasonal pricing
        double seasonMultiplier = HotelManagementUtils.getSeasonMultiplier(checkInDate);
        double adjustedPrice = basePrice * seasonMultiplier;

        // Add tax
        this.totalCost = Hotel.calculateTotalWithTax(adjustedPrice);
    }

    // Method to check in (changes both reservation and room status)
    public boolean performCheckIn(LocalDate actualDate) {
        if (status.equals("CONFIRMED") && actualDate.equals(checkInDate)) {
            room.checkIn();  // Room's status changes
            status = "CHECKED_IN";
            System.out.println("Check-in successful for " + guest.getFullName());
            return true;
        } else {
            System.out.println("Cannot check in: Wrong date or status");
            return false;
        }
    }

    // Method to check out
    public boolean performCheckOut(LocalDate actualDate) {
        if (status.equals("CHECKED_IN")) {
            room.checkOut();  // Room's status changes
            status = "COMPLETED";
            Hotel.recordRevenue(totalCost);  // Record revenue (static)
            System.out.println("Check-out successful for " + guest.getFullName());
            return true;
        } else {
            System.out.println("Cannot check out: Not checked in");
            return false;
        }
    }

    // Method to cancel reservation
    public boolean cancel() {
        if (status.equals("CONFIRMED")) {
            status = "CANCELLED";
            System.out.println("Reservation cancelled for " + guest.getFullName());
            return true;
        } else {
            System.out.println("Cannot cancel: Reservation already started");
            return false;
        }
    }

    // Display reservation details
    public void displayReservation() {
        System.out.println("\n=== RESERVATION DETAILS ===");
        System.out.println("Confirmation Code: " + confirmationCode);
        System.out.println("Guest: " + guest.getFullName());
        System.out.println("Email: " + guest.getEmail());
        System.out.println("Room: " + room.getRoomNumber() + " (" + room.getRoomType() + ")");
        System.out.println("Check-in: " + HotelManagementUtils.formatDate(checkInDate));
        System.out.println("Check-out: " + HotelManagementUtils.formatDate(checkOutDate));
        long nights = HotelManagementUtils.calculateNights(checkInDate, checkOutDate);
        System.out.println("Nights: " + nights);
        System.out.println("Total Cost: " + HotelManagementUtils.formatCurrency(totalCost));
        System.out.println("Status: " + status);
    }

    // Getters
    public String getConfirmationCode() { return confirmationCode; }
    public Guest getGuest() { return guest; }
    public Room getRoom() { return room; }
    public LocalDate getCheckInDate() { return checkInDate; }
    public LocalDate getCheckOutDate() { return checkOutDate; }
    public double getTotalCost() { return totalCost; }
    public String getStatus() { return status; }
}
```

### Step 13: Method Overloading - Multiple Ways to Create

Update `Room` class with overloaded constructors:

```java
// Add these constructors to the Room class

// Original constructor
public Room(int roomNumber, String roomType, double pricePerNight) {
    this.roomNumber = roomNumber;
    this.roomType = roomType;
    this.pricePerNight = pricePerNight;
    this.isOccupied = false;
    this.isClean = true;
}

// Overloaded constructor - default price based on type
public Room(int roomNumber, String roomType) {
    this.roomNumber = roomNumber;
    this.roomType = roomType;
    // Set default price based on room type
    switch (roomType.toUpperCase()) {
        case "SINGLE":
            this.pricePerNight = 99.00;
            break;
        case "DOUBLE":
            this.pricePerNight = 149.00;
            break;
        case "SUITE":
            this.pricePerNight = 299.00;
            break;
        default:
            this.pricePerNight = 100.00;
    }
    this.isOccupied = false;
    this.isClean = true;
}

// Overloaded constructor - specify initial state
public Room(int roomNumber, String roomType, double pricePerNight,
           boolean isOccupied, boolean isClean) {
    this.roomNumber = roomNumber;
    this.roomType = roomType;
    this.pricePerNight = pricePerNight;
    this.isOccupied = isOccupied;
    this.isClean = isClean;
}
```

### Step 14: Test Class Interactions

Create `TestHotelSystem`:

```java
package com.pluralsight.hotel;

import java.time.LocalDate;

public class TestHotelSystem {
    public static void main(String[] args) {
        System.out.println("=== COMPLETE HOTEL SYSTEM TEST ===\n");

        // Create a hotel
        Hotel grandHotel = new Hotel("Grand Plaza Hotel");

        // Create rooms using different constructors (overloading)
        Room room101 = new Room(101, "SUITE", 350.00);  // Full constructor
        Room room102 = new Room(102, "DOUBLE");         // Default price
        Room room103 = new Room(103, "SINGLE", 95.00, false, true); // With state

        // Add rooms to hotel
        grandHotel.addRoom(room101);
        grandHotel.addRoom(room102);
        grandHotel.addRoom(room103);

        System.out.println("\nAvailable rooms: " + grandHotel.getAvailableRoomCount());

        // Create guests
        Guest guest1 = new Guest("John", "Smith", "john@email.com", "555-1234");
        Guest guest2 = new Guest("Jane", "Doe", "jane@email.com", "555-5678");

        System.out.println("\n--- Creating Reservations ---");

        // Create reservations (showing HAS-A relationships)
        LocalDate today = LocalDate.now();
        LocalDate tomorrow = today.plusDays(1);
        LocalDate in3Days = today.plusDays(3);

        // Reservation HAS-A Guest and HAS-A Room
        Reservation res1 = new Reservation(guest1, room101, today, in3Days);
        res1.displayReservation();

        Reservation res2 = new Reservation(guest2, room102, tomorrow, tomorrow.plusDays(2));
        res2.displayReservation();

        System.out.println("\n--- Testing Check-in Process ---");

        // John checks in today
        System.out.println("\nJohn attempting to check in...");
        res1.performCheckIn(today);
        System.out.println("Room 101 available? " + room101.isAvailable());

        // Jane tries to check in early (should fail)
        System.out.println("\nJane attempting to check in early...");
        res2.performCheckIn(today);  // Wrong date!

        System.out.println("\n--- Testing Check-out Process ---");

        // John checks out
        System.out.println("\nJohn checking out...");
        res1.performCheckOut(today.plusDays(3));
        System.out.println("Room 101 occupied? " + room101.isOccupied());
        System.out.println("Room 101 clean? " + room101.isClean());

        // Clean the room
        room101.cleanRoom();
        System.out.println("Room 101 available after cleaning? " + room101.isAvailable());

        System.out.println("\n--- Testing Cancellation ---");

        // Create new reservation and cancel it
        Reservation res3 = new Reservation(
            new Guest("Bob", "Wilson", "bob@email.com", "555-9999"),
            room103,
            tomorrow,
            tomorrow.plusDays(1)
        );
        System.out.println("\nBob's reservation created");
        res3.cancel();

        System.out.println("\n--- Final Statistics ---");
        System.out.println("Total Hotels Created: " + Hotel.getTotalHotelsCreated());
        System.out.println("Total Revenue: " +
            HotelManagementUtils.formatCurrency(Hotel.getTotalRevenueAllHotels()));
        System.out.println("Available Rooms: " + grandHotel.getAvailableRoomCount());

        // Demonstrating object relationships
        System.out.println("\n--- Object Relationships ---");
        System.out.println("Reservation " + res1.getConfirmationCode() + " belongs to:");
        System.out.println("  Guest: " + res1.getGuest().getFullName());
        System.out.println("  Room: " + res1.getRoom().getRoomNumber());
        System.out.println("These objects work together to manage the reservation!");
    }
}
```

**🔍 What's happening? Understanding Class Relationships:**

**HAS-A Relationship (Composition/Aggregation):**

```java
private Guest guest;  // Reservation HAS-A Guest
private Room room;    // Reservation HAS-A Room
```

- One class contains another class
- Like a car HAS-A engine
- Reservation can't exist without Guest and Room
- Creates dependencies between classes

**Object Communication:**

- Reservation tells Room to check in: `room.checkIn()`
- Reservation asks Guest for name: `guest.getFullName()`
- Objects send messages (method calls) to each other
- Like people working together in a company

**Method Overloading - Multiple Constructors:**

```java
Room(int roomNumber, String roomType, double price)
Room(int roomNumber, String roomType)  // Different parameters
```

- Same method name, different parameters
- Java knows which to use by what you pass
- Provides flexibility in object creation
- Like having multiple ways to order coffee

**Encapsulation in Action:**

- Reservation doesn't directly change Room's variables
- It calls Room's methods (`checkIn()`, `checkOut()`)
- Room controls HOW it changes state
- Maintains data integrity

**Static vs Instance in Practice:**

- `HotelManagementUtils.formatDate()` - Static utility
- `room.checkIn()` - Instance method
- `Hotel.recordRevenue()` - Static tracking
- Mix both as needed

**Object Lifecycle:**

1. Guest created
2. Room created
3. Reservation created (needs both)
4. Reservation manages check-in/out
5. Room state changes
6. Revenue recorded (static)

**Why This Design?**

- **Separation of Concerns** - Each class has one job
- **Reusability** - Guest can have multiple reservations
- **Flexibility** - Easy to add features
- **Maintainability** - Changes isolated to relevant class

**▶️ Run TestHotelSystem** to see all the pieces working together!

### 📝 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `Guest.java` (green)
   - `Reservation.java` (green)
   - `Room.java` (blue - modified with overloading)
   - `TestHotelSystem.java` (green)
3. Commit message: `"Added Guest and Reservation classes demonstrating HAS-A relationships and method overloading"`
4. Click **Commit and Push**

---

## 🧪 Part 6: More Unit Testing

### Step 15: Test the Complete System

Create `ReservationTest`:

```java
package com.pluralsight.hotel;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.time.LocalDate;

public class ReservationTest {

    @Test
    public void getStatus_NewReservation_ReturnsConfirmed() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);

        // Act
        String status = testReservation.getStatus();

        // Assert
        assertEquals("CONFIRMED", status, "New reservation should have CONFIRMED status");
    }

    @Test
    public void getConfirmationCode_NewReservation_ReturnsNotNull() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);

        // Act
        String confirmationCode = testReservation.getConfirmationCode();

        // Assert
        assertNotNull(confirmationCode, "Confirmation code should not be null");
    }

    @Test
    public void performCheckIn_CorrectDate_ReturnsTrue() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);

        // Act
        boolean success = testReservation.performCheckIn(checkIn);

        // Assert
        assertTrue(success, "Check-in on correct date should succeed");
        assertEquals("CHECKED_IN", testReservation.getStatus(),
            "Status should be CHECKED_IN after successful check-in");
        assertTrue(testRoom.isOccupied(), "Room should be occupied after check-in");
    }

    @Test
    public void performCheckIn_WrongDate_ReturnsFalse() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);
        LocalDate wrongDate = checkIn.plusDays(1);

        // Act
        boolean success = testReservation.performCheckIn(wrongDate);

        // Assert
        assertFalse(success, "Check-in on wrong date should fail");
        assertEquals("CONFIRMED", testReservation.getStatus(),
            "Status should remain CONFIRMED after failed check-in");
        assertFalse(testRoom.isOccupied(), "Room should not be occupied after failed check-in");
    }

    @Test
    public void performCheckOut_AfterCheckIn_ReturnsTrue() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);
        testReservation.performCheckIn(checkIn);  // Check in first

        // Act
        boolean success = testReservation.performCheckOut(checkOut);

        // Assert
        assertTrue(success, "Check-out after check-in should succeed");
        assertEquals("COMPLETED", testReservation.getStatus(),
            "Status should be COMPLETED after check-out");
        assertFalse(testRoom.isOccupied(), "Room should not be occupied after check-out");
    }

    @Test
    public void cancel_ConfirmedReservation_ReturnsTrue() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);

        // Act
        boolean success = testReservation.cancel();

        // Assert
        assertTrue(success, "Cancelling confirmed reservation should succeed");
        assertEquals("CANCELLED", testReservation.getStatus(),
            "Status should be CANCELLED after cancellation");
    }

    @Test
    public void getTotalCost_TwoNightStay_CalculatesCorrectly() {
        // Arrange
        Guest testGuest = new Guest("Test", "User", "test@email.com", "555-0000");
        Room testRoom = new Room(999, "DOUBLE", 150.00);
        LocalDate checkIn = LocalDate.now();
        LocalDate checkOut = checkIn.plusDays(2);
        Reservation testReservation = new Reservation(testGuest, testRoom, checkIn, checkOut);

        // Act
        double totalCost = testReservation.getTotalCost();

        // Assert
        // Base cost: 2 nights * $150 = $300
        // With tax and possible seasonal adjustments
        assertTrue(totalCost > 0, "Total cost should be greater than zero");
        // Check it's at least base cost with tax (8%)
        assertTrue(totalCost >= 300 * 1.08 * 0.85,
            "Total cost should include base price with tax (accounting for possible discount)");
    }
}
```

Create `HotelManagementUtilsTest`:

```java
package com.pluralsight.hotel;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.time.LocalDate;

public class HotelManagementUtilsTest {

    @Test
    public void isValidEmail_ValidEmail_ReturnsTrue() {
        // Arrange
        String validEmail = "test@email.com";

        // Act
        boolean isValid = HotelManagementUtils.isValidEmail(validEmail);

        // Assert
        assertTrue(isValid, "Valid email should return true");
    }

    @Test
    public void isValidEmail_EmailWithoutAtSign_ReturnsFalse() {
        // Arrange
        String invalidEmail = "testemail.com";

        // Act
        boolean isValid = HotelManagementUtils.isValidEmail(invalidEmail);

        // Assert
        assertFalse(isValid, "Email without @ should return false");
    }

    @Test
    public void isValidEmail_EmailWithoutDot_ReturnsFalse() {
        // Arrange
        String invalidEmail = "test@email";

        // Act
        boolean isValid = HotelManagementUtils.isValidEmail(invalidEmail);

        // Assert
        assertFalse(isValid, "Email without dot should return false");
    }

    @Test
    public void isValidEmail_NullEmail_ReturnsFalse() {
        // Arrange
        String nullEmail = null;

        // Act
        boolean isValid = HotelManagementUtils.isValidEmail(nullEmail);

        // Assert
        assertFalse(isValid, "Null email should return false");
    }

    @Test
    public void formatCurrency_PositiveAmount_ReturnsFormattedString() {
        // Arrange
        double amount = 1234.56;

        // Act
        String formatted = HotelManagementUtils.formatCurrency(amount);

        // Assert
        assertEquals("$1,234.56", formatted, "Should format with dollar sign and comma");
    }

    @Test
    public void formatCurrency_ZeroAmount_ReturnsZeroDollars() {
        // Arrange
        double amount = 0;

        // Act
        String formatted = HotelManagementUtils.formatCurrency(amount);

        // Assert
        assertEquals("$0.00", formatted, "Zero should format as $0.00");
    }

    @Test
    public void calculateNights_FourNightStay_ReturnsFour() {
        // Arrange
        LocalDate checkIn = LocalDate.of(2024, 1, 1);
        LocalDate checkOut = LocalDate.of(2024, 1, 5);

        // Act
        long nights = HotelManagementUtils.calculateNights(checkIn, checkOut);

        // Assert
        assertEquals(4, nights, "Jan 1 to Jan 5 should be 4 nights");
    }

    @Test
    public void getSeasonMultiplier_SummerMonth_ReturnsPeakRate() {
        // Arrange
        LocalDate summerDate = LocalDate.of(2024, 7, 15);  // July

        // Act
        double multiplier = HotelManagementUtils.getSeasonMultiplier(summerDate);

        // Assert
        assertEquals(1.25, multiplier, "Summer months should return 1.25 multiplier");
    }

    @Test
    public void getSeasonMultiplier_WinterMonth_ReturnsOffSeasonRate() {
        // Arrange
        LocalDate winterDate = LocalDate.of(2024, 1, 15);  // January

        // Act
        double multiplier = HotelManagementUtils.getSeasonMultiplier(winterDate);

        // Assert
        assertEquals(0.85, multiplier, "Winter months should return 0.85 multiplier");
    }

    @Test
    public void getSeasonMultiplier_SpringMonth_ReturnsRegularRate() {
        // Arrange
        LocalDate springDate = LocalDate.of(2024, 4, 15);  // April

        // Act
        double multiplier = HotelManagementUtils.getSeasonMultiplier(springDate);

        // Assert
        assertEquals(1.0, multiplier, "Spring months should return 1.0 multiplier");
    }

    @Test
    public void generateConfirmationCode_ValidInputs_ContainsNameAndRoom() {
        // Arrange
        String guestName = "Smith";
        int roomNumber = 101;

        // Act
        String code = HotelManagementUtils.generateConfirmationCode(guestName, roomNumber);

        // Assert
        assertNotNull(code, "Confirmation code should not be null");
        assertTrue(code.contains("SMI"), "Code should contain first 3 letters of name");
        assertTrue(code.contains("101"), "Code should contain room number");
    }
}
```

**▶️ Run all tests** by right-clicking on the test folder and selecting "Run All Tests"

### 📝 Final Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Review changes:
   - `ReservationTest.java` (green)
   - `HotelManagementUtilsTest.java` (green)
3. Commit message: `"Added comprehensive unit tests for Reservation and Utility classes"`
4. Click **Commit and Push**

---

## 🎉 Congratulations!

You've built a complete Hotel Reservation System demonstrating ALL Week 5 concepts!

## 🏆 What You've Mastered

✅ **Object-Oriented Thinking:**

- Identifying objects and responsibilities
- Understanding encapsulation
- Separating concerns

✅ **Class Design:**

- Private variables, public methods
- Constructors
- Getters, setters, derived getters
- Business logic methods
- Method overloading

✅ **Unit Testing with JUnit:**

- Test structure (AAA pattern)
- Test naming convention
- @Test annotation
- Assertions
- Testing behavior, not just getters/setters

✅ **Static vs Instance:**

- When to use static
- Utility classes
- Shared data vs object data
- Memory implications

✅ **Class Relationships:**

- HAS-A relationships
- Object communication
- Composition
- Making objects work together

## 📊 Your Git History Should Show:

1. Initial project setup
2. OOP planning and object identification
3. Room class with encapsulation
4. JUnit tests for Room
5. Static methods and utilities
6. Guest and Reservation with relationships
7. Complete system tests

## 💪 Challenge Yourself (Optional)

1. **Add a RoomService class** - Orders that can be charged to rooms
2. **Create different room categories** - With different amenities
3. **Add a loyalty program** - Points for frequent guests
4. **Implement discounts** - For long stays or groups
5. **Add a waiting list** - When hotel is full
6. **Create reports** - Occupancy rate, revenue by room type
7. **Add payment processing** - Different payment methods

## 📚 Key Takeaways

**The OOP Mindset:**

- Think in terms of objects and their responsibilities
- Each class should do ONE thing well
- Hide implementation details (encapsulation)
- Objects collaborate through method calls

**Professional Practices:**

- Write tests for your code
- Commit frequently with clear messages
- Use static appropriately
- Design classes that work together

**Remember:** This is how real software is built - multiple classes working together, each handling its own responsibilities, with tests ensuring everything works correctly. You're now thinking and coding like a professional Java developer!

**Next Steps:**

1. Review each class and understand its role
2. Trace through the flow of a reservation
3. Add your own features
4. Write tests for any new features
5. Keep this as a reference for future projects

The transition from procedural to object-oriented programming is complete - you're now building real systems with multiple cooperating objects!
