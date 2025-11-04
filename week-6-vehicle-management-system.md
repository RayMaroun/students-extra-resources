# 🚗 Vehicle Management System

## A Step-by-Step Tutorial for Java Inheritance

---

## 🎯 Project Overview

We're building a Vehicle Management System that teaches Java inheritance and abstract class concepts from Workbook 5a. You'll understand how parent and child classes work together, share code through inheritance, create abstract classes with abstract methods, and build realistic object hierarchies. This project demonstrates why inheritance and abstraction are fundamental pillars of Object-Oriented Programming!

**What You'll Master:**

- Understanding inheritance and IS-A relationships
- Creating parent (super) and child (sub) classes
- Using the `extends` keyword
- Understanding `protected` access modifier
- Method overriding
- Constructor chaining with `super()`
- Polymorphism basics
- Abstract classes and abstract methods
- When to use abstract vs concrete classes
- Template method pattern
- Real-world class hierarchies

---

## 📝 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `VehicleManagementSystem`
4. Location: `~/pluralsight/workbook-5` (or `C:/pluralsight/workbook-5` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share Project to GitHub Immediately

1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `VehicleManagementSystem`
3. Description: "Week 5a Java Inheritance practice with vehicle hierarchy"
4. Click **Share**
5. In the next dialog, click **Add**

**Why share now?** Start with version control from the beginning - it's a professional habit!

### Step 2: Create Package Structure

1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight.vehicles`
4. Click **OK**

---

## 🤔 Part 1: Understanding Inheritance - The Family Tree of Code

### Step 3: Understanding the Problem Without Inheritance

Create a new class called `NoInheritanceExample`:

```java
package com.pluralsight.vehicles;

public class NoInheritanceExample {
    public static void main(String[] args) {
        System.out.println("=== WITHOUT INHERITANCE - THE PROBLEM ===\n");

        // Imagine we need to create different vehicle types
        // Without inheritance, we'd repeat A LOT of code:

        /*
         * Class Car would have:
         * - String color
         * - int numberOfPassengers
         * - int cargoCapacity
         * - int fuelCapacity
         * - String vin
         * - methods: start(), stop(), accelerate(), brake()
         *
         * Class Motorcycle would have:
         * - String color (DUPLICATE!)
         * - int numberOfPassengers (DUPLICATE!)
         * - int cargoCapacity (DUPLICATE!)
         * - int fuelCapacity (DUPLICATE!)
         * - String vin (DUPLICATE!)
         * - methods: start(), stop(), accelerate(), brake() (ALL DUPLICATES!)
         *
         * Class Truck would have:
         * - String color (DUPLICATE AGAIN!)
         * - int numberOfPassengers (DUPLICATE AGAIN!)
         * - ...and so on
         */

        System.out.println("Problem 1: We repeat the same fields in every class");
        System.out.println("Problem 2: If we need to change something, we update EVERY class");
        System.out.println("Problem 3: No clear relationship between similar things");
        System.out.println("\nSolution? INHERITANCE! Let's learn how...");
    }
}
```

**🔍 What's happening?**

Think about inheritance like a family tree:

- **Grandparents** pass traits to parents
- **Parents** pass traits to children
- **Children** inherit traits but can also have their own unique features

In programming:

- We write common features ONCE in a parent class
- Child classes automatically get these features
- Children can add their own special features
- This follows the DRY principle: Don't Repeat Yourself!

**▶️ Run it** to understand the problem inheritance solves

### Step 4: Commit Your Initial Setup

1. Click the **Commit** button (checkmark icon) in the toolbar
2. Write commit message: "Initial project setup - understanding inheritance problem"
3. Click **Commit and Push**
4. Click **Push** in the dialog

---

## 🏗️ Part 2: Creating the Parent Class

### Step 5: Create the Vehicle Parent Class

Create a new class called `Vehicle`:

```java
package com.pluralsight.vehicles;

public class Vehicle {
    // These are PROTECTED - child classes can access them directly
    protected String color;
    protected int numberOfPassengers;
    protected int cargoCapacity;
    protected int fuelCapacity;
    protected String vin;  // Vehicle Identification Number

    // Private field - only THIS class can access directly
    private boolean isRunning;

    // Constructor - called when creating ANY vehicle
    public Vehicle() {
        System.out.println("Vehicle constructor called");
        this.isRunning = false;
    }

    // Methods that ALL vehicles share
    public void start() {
        if (isRunning) {
            System.out.println("Vehicle is already running!");
        } else {
            isRunning = true;
            System.out.println("Starting the vehicle... Vroooom!");
        }
    }

    public void stop() {
        if (!isRunning) {
            System.out.println("Vehicle is already stopped!");
        } else {
            isRunning = false;
            System.out.println("Stopping the vehicle...");
        }
    }

    public void accelerate() {
        if (isRunning) {
            System.out.println("Vehicle is accelerating... Speed increasing!");
        } else {
            System.out.println("Start the vehicle first!");
        }
    }

    public void brake() {
        System.out.println("Applying brakes... Slowing down!");
    }

    // Getters and Setters
    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getNumberOfPassengers() {
        return numberOfPassengers;
    }

    public void setNumberOfPassengers(int numberOfPassengers) {
        this.numberOfPassengers = numberOfPassengers;
    }

    public int getCargoCapacity() {
        return cargoCapacity;
    }

    public void setCargoCapacity(int cargoCapacity) {
        this.cargoCapacity = cargoCapacity;
    }

    public int getFuelCapacity() {
        return fuelCapacity;
    }

    public void setFuelCapacity(int fuelCapacity) {
        this.fuelCapacity = fuelCapacity;
    }

    public String getVin() {
        return vin;
    }

    public void setVin(String vin) {
        this.vin = vin;
    }

    public boolean isRunning() {
        return isRunning;
    }

    // Method to display vehicle info
    public void displayInfo() {
        System.out.println("=== Vehicle Information ===");
        System.out.println("VIN: " + vin);
        System.out.println("Color: " + color);
        System.out.println("Passengers: " + numberOfPassengers);
        System.out.println("Cargo Capacity: " + cargoCapacity + " lbs");
        System.out.println("Fuel Capacity: " + fuelCapacity + " gallons");
        System.out.println("Running: " + (isRunning ? "Yes" : "No"));
    }
}
```

**🔍 What's happening?**

**Access Modifiers Explained:**

- **`private`**: Only THIS class can see/use it (like a diary - only you can read)
- **`protected`**: This class AND child classes can use it (like family recipes)
- **`public`**: Everyone can use it (like a public library)

**Why use `protected`?**

- Child classes can directly access these fields
- But outside classes cannot
- It's a middle ground between private and public
- Perfect for inheritance scenarios

**The parent class contains:**

- Common attributes ALL vehicles have
- Common methods ALL vehicles need
- This becomes our template or blueprint

**Real-world analogy:**
Think of Vehicle like "Animal" class:

- All animals eat, sleep, move
- But HOW they do it differs
- Dogs bark, cats meow, birds chirp
- Same concept applies to vehicles!

---

## 👶 Part 3: Creating Child Classes

### Step 6: Create the Car Class (Child of Vehicle)

Create a new class called `Car`:

```java
package com.pluralsight.vehicles;

public class Car extends Vehicle {
    // Car-specific fields
    private int numberOfDoors;
    private boolean hasSunroof;

    // Constructor
    public Car() {
        super();  // Calls Vehicle constructor first!
        System.out.println("Car constructor called");
        // Set default values for a car
        this.numberOfPassengers = 5;  // Can access protected field!
        this.cargoCapacity = 500;
        this.fuelCapacity = 15;
    }

    // Car-specific constructor with parameters
    public Car(String color, String vin, int numberOfDoors, boolean hasSunroof) {
        super();  // Always call parent constructor
        this.color = color;  // Can access protected field directly!
        this.vin = vin;
        this.numberOfDoors = numberOfDoors;
        this.hasSunroof = hasSunroof;
        this.numberOfPassengers = 5;
        this.cargoCapacity = 500;
        this.fuelCapacity = 15;
    }

    // Car-specific methods
    public void openTrunk() {
        System.out.println("Opening the car trunk...");
    }

    public void honkHorn() {
        System.out.println("BEEP BEEP! 🚗");
    }

    // Override parent method - Car has its own way of starting
    @Override
    public void start() {
        System.out.println("Inserting key... Turning ignition...");
        super.start();  // Call parent's start method
        System.out.println("Car dashboard lights up!");
    }

    // Override displayInfo to include car-specific info
    @Override
    public void displayInfo() {
        System.out.println("=== Car Information ===");
        super.displayInfo();  // First show vehicle info
        System.out.println("Number of Doors: " + numberOfDoors);
        System.out.println("Has Sunroof: " + (hasSunroof ? "Yes" : "No"));
    }

    // Getters and Setters for car-specific fields
    public int getNumberOfDoors() {
        return numberOfDoors;
    }

    public void setNumberOfDoors(int numberOfDoors) {
        this.numberOfDoors = numberOfDoors;
    }

    public boolean hasSunroof() {
        return hasSunroof;
    }

    public void setHasSunroof(boolean hasSunroof) {
        this.hasSunroof = hasSunroof;
    }
}
```

**🔍 What's happening?**

**The magic word `extends`:**

- `Car extends Vehicle` means "Car IS-A Vehicle"
- Car gets ALL public and protected members from Vehicle
- Car doesn't need to redefine color, vin, start(), stop(), etc.
- It's like Car says "I'll take everything Vehicle has, plus add my own stuff"

**The `super()` keyword:**

- Calls the parent's constructor
- Must be the FIRST line in child constructor
- Like calling your parents before making your own decisions!

**Method Overriding with `@Override`:**

- Child can change how a parent's method works
- `@Override` tells Java "I'm intentionally replacing parent's version"
- Can still call parent's version with `super.methodName()`

**IS-A Relationship Test:**

- A Car IS-A Vehicle ✅ (makes sense!)
- A Vehicle IS-A Car ❌ (not all vehicles are cars)
- If it passes this test, inheritance is appropriate!

### Step 7: Create the Motorcycle Class

Create a new class called `Motorcycle`:

```java
package com.pluralsight.vehicles;

public class Motorcycle extends Vehicle {
    // Motorcycle-specific fields
    private boolean hasSidecar;
    private String handlebarType;  // "standard", "cruiser", "sport"

    // Constructor
    public Motorcycle() {
        super();
        System.out.println("Motorcycle constructor called");
        // Set motorcycle defaults
        this.numberOfPassengers = 2;
        this.cargoCapacity = 50;
        this.fuelCapacity = 5;
        this.handlebarType = "standard";
    }

    // Parameterized constructor
    public Motorcycle(String color, String vin, boolean hasSidecar) {
        super();
        this.color = color;
        this.vin = vin;
        this.hasSidecar = hasSidecar;
        this.numberOfPassengers = hasSidecar ? 3 : 2;  // Sidecar adds a passenger
        this.cargoCapacity = hasSidecar ? 100 : 50;
        this.fuelCapacity = 5;
        this.handlebarType = "standard";
    }

    // Motorcycle-specific methods
    public void doWheelie() {
        if (isRunning()) {
            System.out.println("Pulling a wheelie! 🏍️ Front wheel up!");
        } else {
            System.out.println("Start the motorcycle first!");
        }
    }

    public void leanIntoTurn() {
        System.out.println("Leaning into the turn... Expert riding!");
    }

    // Override start method
    @Override
    public void start() {
        System.out.println("Kick-starting the motorcycle...");
        super.start();
        System.out.println("Engine rumbling... Ready to ride!");
    }

    // Override accelerate for motorcycle-specific behavior
    @Override
    public void accelerate() {
        if (isRunning()) {
            System.out.println("Twisting throttle... VROOOM VROOOM!");
            System.out.println("Wind rushing past... Freedom!");
        } else {
            System.out.println("Kick-start the motorcycle first!");
        }
    }

    @Override
    public void displayInfo() {
        System.out.println("=== Motorcycle Information ===");
        super.displayInfo();
        System.out.println("Has Sidecar: " + (hasSidecar ? "Yes" : "No"));
        System.out.println("Handlebar Type: " + handlebarType);
    }

    // Getters and Setters
    public boolean hasSidecar() {
        return hasSidecar;
    }

    public void setHasSidecar(boolean hasSidecar) {
        this.hasSidecar = hasSidecar;
        // Adjust passenger capacity based on sidecar
        this.numberOfPassengers = hasSidecar ? 3 : 2;
    }

    public String getHandlebarType() {
        return handlebarType;
    }

    public void setHandlebarType(String handlebarType) {
        this.handlebarType = handlebarType;
    }
}
```

### Step 8: Create the Truck Class

Create a new class called `Truck`:

```java
package com.pluralsight.vehicles;

public class Truck extends Vehicle {
    // Truck-specific fields
    private int numberOfAxles;
    private boolean hasTrailer;
    private double towingCapacity;  // in pounds

    // Constructor
    public Truck() {
        super();
        System.out.println("Truck constructor called");
        // Set truck defaults
        this.numberOfPassengers = 3;
        this.cargoCapacity = 5000;
        this.fuelCapacity = 30;
        this.numberOfAxles = 2;
        this.towingCapacity = 10000;
    }

    // Parameterized constructor
    public Truck(String color, String vin, int numberOfAxles, double towingCapacity) {
        super();
        this.color = color;
        this.vin = vin;
        this.numberOfAxles = numberOfAxles;
        this.towingCapacity = towingCapacity;
        // Bigger trucks have more capacity
        this.numberOfPassengers = 3;
        this.cargoCapacity = numberOfAxles * 2500;  // More axles = more cargo
        this.fuelCapacity = numberOfAxles * 15;      // More axles = more fuel
    }

    // Truck-specific methods
    public void attachTrailer() {
        if (hasTrailer) {
            System.out.println("Trailer already attached!");
        } else {
            hasTrailer = true;
            System.out.println("Attaching trailer... Secured and ready!");
            cargoCapacity += 8000;  // Trailer adds cargo space
        }
    }

    public void detachTrailer() {
        if (!hasTrailer) {
            System.out.println("No trailer to detach!");
        } else {
            hasTrailer = false;
            System.out.println("Detaching trailer... Trailer removed!");
            cargoCapacity -= 8000;  // Remove trailer cargo space
        }
    }

    public void engageFourWheelDrive() {
        System.out.println("Engaging 4WD... Ready for rough terrain! 🚚");
    }

    // Override start method for truck
    @Override
    public void start() {
        System.out.println("Turning truck key... Diesel engine starting...");
        super.start();
        System.out.println("Engine rumbling deeply... Power ready!");
        if (hasTrailer) {
            System.out.println("Checking trailer connection... All secure!");
        }
    }

    // Override brake for truck (needs more braking power)
    @Override
    public void brake() {
        System.out.println("Engaging air brakes... PSSSHHHHH!");
        super.brake();
        if (hasTrailer) {
            System.out.println("Trailer brakes engaged too!");
        }
    }

    @Override
    public void displayInfo() {
        System.out.println("=== Truck Information ===");
        super.displayInfo();
        System.out.println("Number of Axles: " + numberOfAxles);
        System.out.println("Towing Capacity: " + towingCapacity + " lbs");
        System.out.println("Has Trailer: " + (hasTrailer ? "Yes" : "No"));
    }

    // Getters and Setters
    public int getNumberOfAxles() {
        return numberOfAxles;
    }

    public void setNumberOfAxles(int numberOfAxles) {
        this.numberOfAxles = numberOfAxles;
        // Adjust capacities based on axles
        this.cargoCapacity = numberOfAxles * 2500;
        this.fuelCapacity = numberOfAxles * 15;
    }

    public boolean hasTrailer() {
        return hasTrailer;
    }

    public double getTowingCapacity() {
        return towingCapacity;
    }

    public void setTowingCapacity(double towingCapacity) {
        this.towingCapacity = towingCapacity;
    }
}
```

### Step 9: Commit Your Vehicle Classes

1. Click the **Commit** button in the toolbar
2. Write commit message: "Add Vehicle parent class and Car, Motorcycle, Truck child classes"
3. Click **Commit and Push**

---

## 🎮 Part 4: Testing Our Inheritance Hierarchy

### Step 10: Create a Test Class to See Inheritance in Action

Create a new class called `VehicleTest`:

```java
package com.pluralsight.vehicles;

public class VehicleTest {
    public static void main(String[] args) {
        System.out.println("=== VEHICLE INHERITANCE DEMONSTRATION ===\n");

        // Test 1: Creating different vehicles
        System.out.println("--- Creating Vehicles ---");

        Car myCar = new Car("Red", "1HGCM82633A123456", 4, true);
        System.out.println("\n");

        Motorcycle myBike = new Motorcycle("Black", "JH2RC5004LM200291", false);
        System.out.println("\n");

        Truck myTruck = new Truck("Blue", "1FTFW1ET5DFC10312", 3, 15000);
        System.out.println("\n");

        // Test 2: Using inherited methods
        System.out.println("--- Testing Inherited Methods ---");

        System.out.println("Starting all vehicles:");
        myCar.start();
        myBike.start();
        myTruck.start();

        System.out.println("\nAccelerating all vehicles:");
        myCar.accelerate();
        myBike.accelerate();
        myTruck.accelerate();

        // Test 3: Using specific methods
        System.out.println("\n--- Testing Specific Methods ---");

        myCar.honkHorn();
        myCar.openTrunk();

        myBike.doWheelie();
        myBike.leanIntoTurn();

        myTruck.attachTrailer();
        myTruck.engageFourWheelDrive();

        // Test 4: Display information
        System.out.println("\n--- Vehicle Information ---");
        myCar.displayInfo();
        System.out.println();
        myBike.displayInfo();
        System.out.println();
        myTruck.displayInfo();

        // Test 5: Stopping vehicles
        System.out.println("\n--- Stopping All Vehicles ---");
        myCar.brake();
        myCar.stop();

        myBike.brake();
        myBike.stop();

        myTruck.brake();
        myTruck.stop();
    }
}
```

**▶️ Run it** and observe how inheritance works!

---

## 🔄 Part 5: Understanding Polymorphism

### Step 11: Create a Class Demonstrating Polymorphism

Create a new class called `PolymorphismDemo`:

```java
package com.pluralsight.vehicles;

import java.util.ArrayList;

public class PolymorphismDemo {
    public static void main(String[] args) {
        System.out.println("=== POLYMORPHISM WITH VEHICLES ===\n");

        // Polymorphism: A Vehicle reference can hold any vehicle type!
        Vehicle vehicle1 = new Car("Silver", "CAR123", 4, false);
        Vehicle vehicle2 = new Motorcycle("Green", "BIKE456", true);
        Vehicle vehicle3 = new Truck("Yellow", "TRUCK789", 4, 20000);

        // All are treated as Vehicle type, but each acts according to its actual type
        System.out.println("--- Starting all vehicles through Vehicle reference ---");
        vehicle1.start();  // Calls Car's start method
        vehicle2.start();  // Calls Motorcycle's start method
        vehicle3.start();  // Calls Truck's start method

        // Store different vehicle types in same collection!
        System.out.println("\n--- Vehicle Fleet Management ---");
        ArrayList<Vehicle> fleet = new ArrayList<>();

        // Add different types to same list
        fleet.add(new Car("White", "CAR001", 2, true));
        fleet.add(new Motorcycle("Red", "BIKE001", false));
        fleet.add(new Truck("Black", "TRUCK001", 2, 12000));
        fleet.add(new Car("Blue", "CAR002", 4, false));
        fleet.add(new Truck("Gray", "TRUCK002", 3, 18000));

        // Process all vehicles the same way
        System.out.println("\nStarting entire fleet:");
        for (Vehicle v : fleet) {
            v.start();  // Each vehicle starts its own way!
        }

        System.out.println("\nFleet inventory:");
        System.out.println("Total vehicles: " + fleet.size());

        // Count vehicle types
        int cars = 0, motorcycles = 0, trucks = 0;
        for (Vehicle v : fleet) {
            if (v instanceof Car) {
                cars++;
            } else if (v instanceof Motorcycle) {
                motorcycles++;
            } else if (v instanceof Truck) {
                trucks++;
            }
        }

        System.out.println("Cars: " + cars);
        System.out.println("Motorcycles: " + motorcycles);
        System.out.println("Trucks: " + trucks);

        // Calculate total capacity
        int totalPassengers = 0;
        int totalCargo = 0;

        for (Vehicle v : fleet) {
            totalPassengers += v.getNumberOfPassengers();
            totalCargo += v.getCargoCapacity();
        }

        System.out.println("\nFleet Capacity:");
        System.out.println("Total passenger capacity: " + totalPassengers);
        System.out.println("Total cargo capacity: " + totalCargo + " lbs");
    }
}
```

**🔍 What's happening?**

**Polymorphism - "Many Forms":**

- A Vehicle reference can hold ANY type of vehicle
- Like saying "Animal" can mean dog, cat, or bird
- The actual type determines the behavior

**The `instanceof` operator:**

- Checks if an object is a certain type
- `vehicle instanceof Car` returns true if it's a Car
- Useful for type-specific operations

**Why is this powerful?**

- Can process different types uniformly
- Add new vehicle types without changing existing code
- Foundation of flexible, extensible programs

---

## 🏗️ Part 6: Advanced Inheritance Features

### Step 12: Create an Advanced Example with Method Chaining

Create a new class called `LuxuryCar` that extends `Car`:

```java
package com.pluralsight.vehicles;

public class LuxuryCar extends Car {
    // LuxuryCar-specific fields
    private boolean hasMassageSeats;
    private boolean hasAutoPilot;
    private String interiorMaterial;  // "leather", "alcantara", "carbon fiber"
    private int soundSystemSpeakers;

    // Constructor
    public LuxuryCar() {
        super();  // Calls Car constructor
        System.out.println("LuxuryCar constructor called");
        this.interiorMaterial = "leather";
        this.soundSystemSpeakers = 12;
    }

    // Full constructor
    public LuxuryCar(String color, String vin, int doors, boolean sunroof,
                      boolean massageSeats, boolean autoPilot) {
        super(color, vin, doors, sunroof);  // Call Car's constructor
        this.hasMassageSeats = massageSeats;
        this.hasAutoPilot = autoPilot;
        this.interiorMaterial = "leather";
        this.soundSystemSpeakers = 16;
        // Luxury cars have premium capacity
        this.fuelCapacity = 20;  // Bigger tank
    }

    // Luxury-specific methods
    public void activateMassageSeats() {
        if (hasMassageSeats) {
            System.out.println("Massage seats activated... Ahhh, relaxing! 💆");
        } else {
            System.out.println("This model doesn't have massage seats.");
        }
    }

    public void engageAutoPilot() {
        if (hasAutoPilot) {
            if (isRunning()) {
                System.out.println("Auto-pilot engaged! Hands-free driving activated. 🤖");
            } else {
                System.out.println("Start the car before engaging auto-pilot!");
            }
        } else {
            System.out.println("This model doesn't have auto-pilot.");
        }
    }

    public void playPremiumSound() {
        System.out.println("Playing music on " + soundSystemSpeakers +
                          "-speaker premium system... 🎵 Crystal clear sound!");
    }

    // Override start with luxury features
    @Override
    public void start() {
        System.out.println("Welcome! Adjusting seat to saved position...");
        System.out.println("Climate control set to preferred temperature...");
        super.start();  // Call Car's start (which calls Vehicle's start)
        System.out.println("Premium sound system ready.");
        if (hasAutoPilot) {
            System.out.println("Auto-pilot system checked and ready.");
        }
    }

    @Override
    public void displayInfo() {
        System.out.println("=== Luxury Car Information ===");
        super.displayInfo();  // Call Car's displayInfo (which calls Vehicle's)
        System.out.println("--- Luxury Features ---");
        System.out.println("Massage Seats: " + (hasMassageSeats ? "Yes" : "No"));
        System.out.println("Auto-Pilot: " + (hasAutoPilot ? "Yes" : "No"));
        System.out.println("Interior: " + interiorMaterial);
        System.out.println("Sound System: " + soundSystemSpeakers + " speakers");
    }

    // Getters and Setters
    public boolean hasMassageSeats() {
        return hasMassageSeats;
    }

    public void setMassageSeats(boolean hasMassageSeats) {
        this.hasMassageSeats = hasMassageSeats;
    }

    public boolean hasAutoPilot() {
        return hasAutoPilot;
    }

    public void setAutoPilot(boolean hasAutoPilot) {
        this.hasAutoPilot = hasAutoPilot;
    }

    public String getInteriorMaterial() {
        return interiorMaterial;
    }

    public void setInteriorMaterial(String interiorMaterial) {
        this.interiorMaterial = interiorMaterial;
    }

    public int getSoundSystemSpeakers() {
        return soundSystemSpeakers;
    }

    public void setSoundSystemSpeakers(int soundSystemSpeakers) {
        this.soundSystemSpeakers = soundSystemSpeakers;
    }
}
```

**🔍 What's happening?**

**Multi-level Inheritance:**

- LuxuryCar → Car → Vehicle
- Like grandchild → parent → grandparent
- LuxuryCar has features from BOTH Car and Vehicle

**Constructor Chaining:**

- LuxuryCar constructor calls Car constructor
- Car constructor calls Vehicle constructor
- Each level adds its own initialization

**This demonstrates:**

- You can have multiple levels of inheritance
- Each level adds more specialization
- Real-world hierarchies can be complex

---

## 🎯 Part 7: Practical Fleet Management System

### Step 13: Create a Complete Fleet Management Application

Create a new class called `FleetManagementSystem`:

```java
package com.pluralsight.vehicles;

import java.util.ArrayList;
import java.util.Scanner;

public class FleetManagementSystem {
    private static ArrayList<Vehicle> fleet = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        System.out.println("╔════════════════════════════════════════╗");
        System.out.println("║    VEHICLE FLEET MANAGEMENT SYSTEM    ║");
        System.out.println("╚════════════════════════════════════════╝\n");

        // Pre-populate with some vehicles
        initializeFleet();

        boolean running = true;
        while (running) {
            displayMenu();
            int choice = scanner.nextInt();
            scanner.nextLine(); // Clear buffer

            switch (choice) {
                case 1 -> addVehicle();
                case 2 -> displayAllVehicles();
                case 3 -> startAllVehicles();
                case 4 -> stopAllVehicles();
                case 5 -> displayFleetStatistics();
                case 6 -> testVehicle();
                case 7 -> {
                    System.out.println("Thank you for using Fleet Management System!");
                    running = false;
                }
                default -> System.out.println("Invalid option! Please try again.");
            }
        }

        scanner.close();
    }

    private static void initializeFleet() {
        // Add some default vehicles
        fleet.add(new Car("Red", "CAR001", 4, true));
        fleet.add(new Motorcycle("Black", "BIKE001", false));
        fleet.add(new Truck("Blue", "TRUCK001", 3, 15000));
        fleet.add(new LuxuryCar("Silver", "LUX001", 4, true, true, true));
        System.out.println("Fleet initialized with 4 vehicles.\n");
    }

    private static void displayMenu() {
        System.out.println("\n=== MAIN MENU ===");
        System.out.println("1. Add New Vehicle");
        System.out.println("2. Display All Vehicles");
        System.out.println("3. Start All Vehicles");
        System.out.println("4. Stop All Vehicles");
        System.out.println("5. Display Fleet Statistics");
        System.out.println("6. Test Drive a Vehicle");
        System.out.println("7. Exit");
        System.out.print("Enter your choice: ");
    }

    private static void addVehicle() {
        System.out.println("\n--- Add New Vehicle ---");
        System.out.println("1. Car");
        System.out.println("2. Motorcycle");
        System.out.println("3. Truck");
        System.out.println("4. Luxury Car");
        System.out.print("Select vehicle type: ");

        int type = scanner.nextInt();
        scanner.nextLine(); // Clear buffer

        System.out.print("Enter color: ");
        String color = scanner.nextLine();

        System.out.print("Enter VIN: ");
        String vin = scanner.nextLine();

        Vehicle newVehicle = null;

        switch (type) {
            case 1 -> {
                System.out.print("Number of doors: ");
                int doors = scanner.nextInt();
                System.out.print("Has sunroof? (true/false): ");
                boolean sunroof = scanner.nextBoolean();
                newVehicle = new Car(color, vin, doors, sunroof);
            }
            case 2 -> {
                System.out.print("Has sidecar? (true/false): ");
                boolean sidecar = scanner.nextBoolean();
                newVehicle = new Motorcycle(color, vin, sidecar);
            }
            case 3 -> {
                System.out.print("Number of axles: ");
                int axles = scanner.nextInt();
                System.out.print("Towing capacity (lbs): ");
                double towing = scanner.nextDouble();
                newVehicle = new Truck(color, vin, axles, towing);
            }
            case 4 -> {
                System.out.print("Number of doors: ");
                int doors = scanner.nextInt();
                System.out.print("Has sunroof? (true/false): ");
                boolean sunroof = scanner.nextBoolean();
                System.out.print("Has massage seats? (true/false): ");
                boolean massage = scanner.nextBoolean();
                System.out.print("Has autopilot? (true/false): ");
                boolean autopilot = scanner.nextBoolean();
                newVehicle = new LuxuryCar(color, vin, doors, sunroof, massage, autopilot);
            }
        }

        if (newVehicle != null) {
            fleet.add(newVehicle);
            System.out.println("✅ Vehicle added successfully!");
        }
    }

    private static void displayAllVehicles() {
        System.out.println("\n--- Fleet Inventory ---");
        if (fleet.isEmpty()) {
            System.out.println("No vehicles in fleet.");
            return;
        }

        for (int i = 0; i < fleet.size(); i++) {
            System.out.println("\nVehicle #" + (i + 1) + ":");
            fleet.get(i).displayInfo();
        }
    }

    private static void startAllVehicles() {
        System.out.println("\n--- Starting All Vehicles ---");
        for (Vehicle v : fleet) {
            v.start();
        }
        System.out.println("✅ All vehicles started!");
    }

    private static void stopAllVehicles() {
        System.out.println("\n--- Stopping All Vehicles ---");
        for (Vehicle v : fleet) {
            v.stop();
        }
        System.out.println("✅ All vehicles stopped!");
    }

    private static void displayFleetStatistics() {
        System.out.println("\n╔════════════════════════════════╗");
        System.out.println("║     FLEET STATISTICS          ║");
        System.out.println("╚════════════════════════════════╝");

        int cars = 0, motorcycles = 0, trucks = 0, luxuryCars = 0;
        int totalPassengers = 0, totalCargo = 0, totalFuel = 0;

        for (Vehicle v : fleet) {
            if (v instanceof LuxuryCar) {
                luxuryCars++;
            } else if (v instanceof Car) {
                cars++;
            } else if (v instanceof Motorcycle) {
                motorcycles++;
            } else if (v instanceof Truck) {
                trucks++;
            }

            totalPassengers += v.getNumberOfPassengers();
            totalCargo += v.getCargoCapacity();
            totalFuel += v.getFuelCapacity();
        }

        System.out.println("Total Vehicles: " + fleet.size());
        System.out.println("├── Cars: " + cars);
        System.out.println("├── Luxury Cars: " + luxuryCars);
        System.out.println("├── Motorcycles: " + motorcycles);
        System.out.println("└── Trucks: " + trucks);
        System.out.println("\nCapacity Totals:");
        System.out.println("├── Passengers: " + totalPassengers);
        System.out.println("├── Cargo: " + totalCargo + " lbs");
        System.out.println("└── Fuel: " + totalFuel + " gallons");

        if (!fleet.isEmpty()) {
            System.out.println("\nAverages per Vehicle:");
            System.out.println("├── Avg Passengers: " + (totalPassengers / fleet.size()));
            System.out.println("├── Avg Cargo: " + (totalCargo / fleet.size()) + " lbs");
            System.out.println("└── Avg Fuel: " + (totalFuel / fleet.size()) + " gallons");
        }
    }

    private static void testVehicle() {
        System.out.println("\n--- Test Drive ---");
        displayAllVehicles();

        System.out.print("\nEnter vehicle number to test (1-" + fleet.size() + "): ");
        int index = scanner.nextInt() - 1;

        if (index < 0 || index >= fleet.size()) {
            System.out.println("Invalid vehicle number!");
            return;
        }

        Vehicle vehicle = fleet.get(index);
        System.out.println("\nTest driving vehicle #" + (index + 1));

        vehicle.start();
        vehicle.accelerate();

        // Type-specific actions
        if (vehicle instanceof LuxuryCar) {
            LuxuryCar lux = (LuxuryCar) vehicle;  // Cast to access specific methods
            lux.activateMassageSeats();
            lux.playPremiumSound();
            lux.engageAutoPilot();
        } else if (vehicle instanceof Car) {
            Car car = (Car) vehicle;
            car.honkHorn();
            car.openTrunk();
        } else if (vehicle instanceof Motorcycle) {
            Motorcycle bike = (Motorcycle) vehicle;
            bike.doWheelie();
            bike.leanIntoTurn();
        } else if (vehicle instanceof Truck) {
            Truck truck = (Truck) vehicle;
            truck.attachTrailer();
            truck.engageFourWheelDrive();
        }

        vehicle.brake();
        vehicle.stop();

        System.out.println("\n✅ Test drive completed!");
    }
}
```

**🔍 What's happening?**

**Complete System Features:**

- Menu-driven interface for user interaction
- Dynamic vehicle addition
- Fleet-wide operations (start all, stop all)
- Statistics calculation using polymorphism
- Type checking with `instanceof`
- Casting to access specific features

**Key Inheritance Concepts Applied:**

1. **Polymorphism**: Storing different types in Vehicle list
2. **Dynamic Binding**: Correct methods called at runtime
3. **Type Checking**: Using instanceof to identify types
4. **Casting**: Converting to specific type when needed
5. **Code Reuse**: All vehicles share common behavior

**▶️ Run it** and explore the complete system!

### Step 14: Final Commit and Push

1. Click the **Commit** button
2. Write commit message: "Complete Vehicle Management System with inheritance hierarchy"
3. Click **Commit and Push**

---

## 🎨 Part 8: Understanding Abstract Classes

### Step 15: Understanding the Need for Abstract Classes

Create a new class called `AbstractionIntro`:

```java
package com.pluralsight.vehicles;

public class AbstractionIntro {
    public static void main(String[] args) {
        System.out.println("=== WHY WE NEED ABSTRACT CLASSES ===\n");

        /*
         * Sometimes we want to:
         * 1. Define a base class that should never be instantiated
         * 2. Force child classes to implement certain methods
         * 3. Provide some common implementation while leaving some details to children
         *
         * Example: Vehicle
         * - Every vehicle must accelerate, but HOW is different
         * - Every vehicle has a color, but the TYPE varies
         * - We never want just a "Vehicle" - it's always a specific type
         *
         * Abstract classes solve this!
         */

        System.out.println("Abstract Class Benefits:");
        System.out.println("1. Cannot create instances of incomplete concepts");
        System.out.println("2. Forces children to implement critical methods");
        System.out.println("3. Shares common code while enforcing contracts");
        System.out.println("4. Creates a clear template for subclasses");
    }
}
```

### Step 16: Create an Abstract Vehicle Class

Create a new abstract class called `AbstractVehicle`:

```java
package com.pluralsight.vehicles;

// Abstract class - cannot be instantiated directly
public abstract class AbstractVehicle {
    // Protected fields accessible by subclasses
    protected String color;
    protected int numberOfPassengers;
    protected int cargoCapacity;
    protected int fuelCapacity;
    protected String vin;
    protected boolean isRunning;

    // Constructor - called by child classes
    public AbstractVehicle() {
        System.out.println("AbstractVehicle constructor called");
        this.isRunning = false;
    }

    // Concrete methods - all vehicles share this implementation
    public void start() {
        if (isRunning) {
            System.out.println("Vehicle is already running!");
        } else {
            isRunning = true;
            performStartupChecks();  // Call abstract method
            System.out.println("Vehicle started successfully!");
        }
    }

    public void stop() {
        if (!isRunning) {
            System.out.println("Vehicle is already stopped!");
        } else {
            isRunning = false;
            System.out.println("Vehicle stopped.");
        }
    }

    // Abstract methods - MUST be implemented by child classes
    public abstract void performStartupChecks();
    public abstract void accelerate();
    public abstract double calculateFuelEfficiency();
    public abstract String getVehicleType();

    // Regular getters and setters
    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getNumberOfPassengers() {
        return numberOfPassengers;
    }

    public void setNumberOfPassengers(int numberOfPassengers) {
        this.numberOfPassengers = numberOfPassengers;
    }

    public boolean isRunning() {
        return isRunning;
    }

    // Template method pattern - defines algorithm structure
    public final void performMaintenance() {
        System.out.println("=== Starting Maintenance for " + getVehicleType() + " ===");
        checkFluids();          // Abstract method
        inspectTires();         // Abstract method
        runDiagnostics();       // Concrete method
        System.out.println("=== Maintenance Complete ===\n");
    }

    // More abstract methods for maintenance
    protected abstract void checkFluids();
    protected abstract void inspectTires();

    // Concrete method used in template
    private void runDiagnostics() {
        System.out.println("Running computer diagnostics...");
        System.out.println("All systems checked!");
    }
}
```

**🔍 What's happening?**

**Abstract Classes Explained:**

- **Cannot be instantiated**: You can't do `new AbstractVehicle()`
- **Can have both abstract and concrete methods**
- **Abstract methods have no body** - just method signature with semicolon
- **Child classes MUST implement ALL abstract methods**
- **Can have constructors** (called by children with super())
- **Can have instance variables** (fields with any access modifier)

**Think of it like:**

- A blueprint with some rooms finished and some just outlined
- Children must complete the unfinished rooms
- Like saying "All vehicles start somehow, but each accelerates differently"

**Real-world analogy:**

- Think of a cooking recipe template
- Some steps are the same for everyone (preheat oven to 350°)
- Some steps vary (season to taste - each chef decides how)

### Step 17: Create Concrete Implementations

Create a new `ModernCar` class that extends `AbstractVehicle`:

```java
package com.pluralsight.vehicles;

public class ModernCar extends AbstractVehicle {
    private int numberOfDoors;
    private boolean hasBackupCamera;

    public ModernCar(String color, String vin, int doors) {
        super();  // Call abstract class constructor
        this.color = color;
        this.vin = vin;
        this.numberOfDoors = doors;
        this.hasBackupCamera = true;
        this.numberOfPassengers = 5;
        this.cargoCapacity = 500;
        this.fuelCapacity = 15;
    }

    // MUST implement all abstract methods
    @Override
    public void performStartupChecks() {
        System.out.println("Car: Checking seatbelts...");
        System.out.println("Car: Adjusting mirrors...");
        System.out.println("Car: Dashboard lights check...");
    }

    @Override
    public void accelerate() {
        if (isRunning) {
            System.out.println("Car: Pressing gas pedal... Speed increasing!");
        } else {
            System.out.println("Car: Start the engine first!");
        }
    }

    @Override
    public double calculateFuelEfficiency() {
        // Miles per gallon calculation
        return 25.5;  // Example MPG
    }

    @Override
    public String getVehicleType() {
        return "Modern Car";
    }

    @Override
    protected void checkFluids() {
        System.out.println("Checking oil level...");
        System.out.println("Checking coolant...");
        System.out.println("Checking windshield washer fluid...");
    }

    @Override
    protected void inspectTires() {
        System.out.println("Checking tire pressure...");
        System.out.println("Inspecting tire tread depth...");
    }

    // Car-specific methods
    public void honkHorn() {
        System.out.println("BEEP BEEP! 🚗");
    }

    public int getNumberOfDoors() {
        return numberOfDoors;
    }
}
```

Create a `SportsBike` class:

```java
package com.pluralsight.vehicles;

public class SportsBike extends AbstractVehicle {
    private boolean hasQuickShifter;
    private int topSpeed;

    public SportsBike(String color, String vin, int topSpeed) {
        super();
        this.color = color;
        this.vin = vin;
        this.topSpeed = topSpeed;
        this.hasQuickShifter = true;
        this.numberOfPassengers = 2;
        this.cargoCapacity = 20;
        this.fuelCapacity = 4;
    }

    @Override
    public void performStartupChecks() {
        System.out.println("SportsBike: Checking chain tension...");
        System.out.println("SportsBike: Testing brakes...");
        System.out.println("SportsBike: Checking tire pressure...");
    }

    @Override
    public void accelerate() {
        if (isRunning) {
            System.out.println("SportsBike: Twisting throttle... 0-60 in 3 seconds!");
            System.out.println("SportsBike: Engine screaming at " + topSpeed + " mph capability!");
        } else {
            System.out.println("SportsBike: Hit the ignition first!");
        }
    }

    @Override
    public double calculateFuelEfficiency() {
        return 45.0;  // MPG - bikes are efficient!
    }

    @Override
    public String getVehicleType() {
        return "Sports Bike";
    }

    @Override
    protected void checkFluids() {
        System.out.println("Checking brake fluid...");
        System.out.println("Checking engine oil...");
        System.out.println("Checking coolant level...");
    }

    @Override
    protected void inspectTires() {
        System.out.println("Inspecting front tire wear pattern...");
        System.out.println("Inspecting rear tire wear pattern...");
        System.out.println("Checking for proper tire temperature...");
    }

    // Bike-specific method
    public void doWheelie() {
        if (isRunning) {
            System.out.println("Pulling a wheelie! Front wheel up! 🏍️");
        } else {
            System.out.println("Start the bike first!");
        }
    }
}
```

### Step 18: Demonstrate Abstract Classes in Action

Create a demonstration class:

```java
package com.pluralsight.vehicles;

import java.util.ArrayList;

public class AbstractClassDemo {
    public static void main(String[] args) {
        System.out.println("=== ABSTRACT CLASS DEMONSTRATION ===\n");

        // This would cause an error - cannot instantiate abstract class!
        // AbstractVehicle vehicle = new AbstractVehicle();  // COMPILATION ERROR!

        // But we CAN use abstract class as a reference type
        System.out.println("--- Creating Concrete Vehicles ---");
        AbstractVehicle car = new ModernCar("Blue", "CAR123", 4);
        AbstractVehicle bike = new SportsBike("Red", "BIKE456", 180);

        // Test the template method pattern
        System.out.println("\n--- Template Method Pattern ---");
        car.performMaintenance();  // Uses combination of abstract and concrete methods
        bike.performMaintenance();  // Same structure, different implementation

        // Test polymorphism with abstract classes
        System.out.println("--- Polymorphism with Abstract Classes ---");
        ArrayList<AbstractVehicle> fleet = new ArrayList<>();
        fleet.add(new ModernCar("White", "CAR001", 2));
        fleet.add(new SportsBike("Black", "BIKE001", 200));
        fleet.add(new ModernCar("Silver", "CAR002", 4));

        System.out.println("\nStarting all vehicles:");
        for (AbstractVehicle v : fleet) {
            v.start();  // Each performs their own startup checks
            v.accelerate();  // Each accelerates their own way
            System.out.println("Fuel Efficiency: " + v.calculateFuelEfficiency() + " MPG\n");
        }

        // Demonstrate type checking and casting
        System.out.println("--- Type-Specific Operations ---");
        for (AbstractVehicle v : fleet) {
            System.out.println("Vehicle Type: " + v.getVehicleType());

            if (v instanceof ModernCar) {
                ModernCar car2 = (ModernCar) v;
                car2.honkHorn();
            } else if (v instanceof SportsBike) {
                SportsBike bike2 = (SportsBike) v;
                bike2.doWheelie();
            }
            System.out.println();
        }

        // Stop all vehicles
        System.out.println("--- Stopping All Vehicles ---");
        for (AbstractVehicle v : fleet) {
            v.stop();
        }
    }
}
```

### Step 19: Create the Animal Example from Workbook

To match the workbook's example, let's create the Animal hierarchy using abstract classes:

```java
package com.pluralsight.vehicles;

// Abstract Animal class - matching workbook example
public abstract class Animal {
    protected String name;
    protected int age;
    protected double weight;

    // Constructor
    public Animal(String name, int age, double weight) {
        this.name = name;
        this.age = age;
        this.weight = weight;
    }

    // Concrete methods - shared by all animals
    public void eat() {
        System.out.println(name + " is eating.");
    }

    public void sleep() {
        System.out.println(name + " is sleeping.");
    }

    // Abstract methods - each animal implements differently
    public abstract void makeSound();
    public abstract void move();
    public abstract String getSpecies();

    // Template method pattern - defines daily routine
    public final void performDailyRoutine() {
        System.out.println("\n=== " + name + "'s Daily Routine ===");
        wakeUp();
        makeSound();
        eat();
        move();
        play();  // Abstract method
        sleep();
    }

    // Protected abstract method - must be implemented by subclasses
    protected abstract void play();

    // Private concrete method
    private void wakeUp() {
        System.out.println(name + " is waking up.");
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public double getWeight() {
        return weight;
    }
}
```

Create concrete animal classes:

```java
package com.pluralsight.vehicles;

// Concrete Dog class
public class Dog extends Animal {
    private String breed;

    public Dog(String name, int age, double weight, String breed) {
        super(name, age, weight);
        this.breed = breed;
    }

    @Override
    public void makeSound() {
        System.out.println(name + " barks: Woof! Woof!");
    }

    @Override
    public void move() {
        System.out.println(name + " runs on four legs.");
    }

    @Override
    public String getSpecies() {
        return "Canine";
    }

    @Override
    protected void play() {
        System.out.println(name + " plays fetch with a ball.");
    }

    // Dog-specific method
    public void wagTail() {
        System.out.println(name + " is wagging its tail happily!");
    }

    public String getBreed() {
        return breed;
    }
}

// Concrete Cat class
class Cat extends Animal {
    private boolean isIndoor;

    public Cat(String name, int age, double weight, boolean isIndoor) {
        super(name, age, weight);
        this.isIndoor = isIndoor;
    }

    @Override
    public void makeSound() {
        System.out.println(name + " meows: Meow! Meow!");
    }

    @Override
    public void move() {
        System.out.println(name + " walks gracefully on four legs.");
    }

    @Override
    public String getSpecies() {
        return "Feline";
    }

    @Override
    protected void play() {
        System.out.println(name + " plays with a toy mouse.");
    }

    // Cat-specific method
    public void purr() {
        System.out.println(name + " is purring contentedly.");
    }

    public boolean isIndoor() {
        return isIndoor;
    }
}

// Concrete Bird class
class Bird extends Animal {
    private double wingspan;

    public Bird(String name, int age, double weight, double wingspan) {
        super(name, age, weight);
        this.wingspan = wingspan;
    }

    @Override
    public void makeSound() {
        System.out.println(name + " chirps: Tweet! Tweet!");
    }

    @Override
    public void move() {
        System.out.println(name + " flies through the air with " + wingspan + " inch wingspan.");
    }

    @Override
    public String getSpecies() {
        return "Avian";
    }

    @Override
    protected void play() {
        System.out.println(name + " plays on a swing.");
    }

    // Bird-specific method
    public void buildNest() {
        System.out.println(name + " is building a nest with twigs.");
    }

    public double getWingspan() {
        return wingspan;
    }
}
```

### Step 20: Test the Animal Hierarchy

Create a test class for the animals:

```java
package com.pluralsight.vehicles;

public class AnimalDemo {
    public static void main(String[] args) {
        System.out.println("=== ANIMAL ABSTRACTION EXAMPLE ===\n");

        // Cannot instantiate abstract class
        // Animal genericAnimal = new Animal("Generic", 5, 10.0);  // ERROR!

        // Create concrete animals
        Dog dog = new Dog("Max", 3, 25.5, "Golden Retriever");
        Cat cat = new Cat("Whiskers", 2, 8.3, true);
        Bird bird = new Bird("Tweety", 1, 0.5, 6.5);

        // Test individual behaviors
        System.out.println("--- Individual Animal Behaviors ---");
        dog.makeSound();
        dog.move();
        dog.wagTail();

        System.out.println();
        cat.makeSound();
        cat.move();
        cat.purr();

        System.out.println();
        bird.makeSound();
        bird.move();
        bird.buildNest();

        // Demonstrate polymorphism with abstract class
        System.out.println("\n--- Polymorphic Behavior ---");
        Animal[] shelter = {
            new Dog("Buddy", 5, 30.0, "Labrador"),
            new Cat("Luna", 4, 9.0, false),
            new Bird("Chirpy", 2, 0.3, 5.0),
            new Dog("Rex", 7, 40.0, "German Shepherd")
        };

        System.out.println("All animals in the shelter:");
        for (Animal animal : shelter) {
            System.out.println("\n" + animal.getName() + " (" + animal.getSpecies() + "):");
            animal.makeSound();
            animal.move();
            animal.eat();
        }

        // Demonstrate template method pattern
        System.out.println("\n--- Template Method Pattern ---");
        dog.performDailyRoutine();
        cat.performDailyRoutine();

        // Type checking and downcasting
        System.out.println("\n--- Special Abilities ---");
        for (Animal animal : shelter) {
            System.out.print(animal.getName() + ": ");

            if (animal instanceof Dog) {
                Dog d = (Dog) animal;
                d.wagTail();
            } else if (animal instanceof Cat) {
                Cat c = (Cat) animal;
                c.purr();
            } else if (animal instanceof Bird) {
                Bird b = (Bird) animal;
                System.out.println("Wingspan: " + b.getWingspan() + " inches");
            }
        }
    }
}
```

### Step 21: Key Concepts Summary

Create a summary class:

```java
package com.pluralsight.vehicles;

public class AbstractClassSummary {
    public static void main(String[] args) {
        System.out.println("=== ABSTRACT CLASS KEY CONCEPTS ===\n");

        System.out.println("1. DEFINITION:");
        System.out.println("   • A class declared with 'abstract' keyword");
        System.out.println("   • Cannot be instantiated (no new AbstractClass())");
        System.out.println("   • Can contain both abstract and concrete methods");
        System.out.println("   • Can have constructors, fields, and regular methods");

        System.out.println("\n2. ABSTRACT METHODS:");
        System.out.println("   • Declared without implementation (no body)");
        System.out.println("   • End with semicolon instead of curly braces");
        System.out.println("   • MUST be implemented by concrete subclasses");
        System.out.println("   • Forces a contract on child classes");

        System.out.println("\n3. WHEN TO USE:");
        System.out.println("   • When you have related classes with common behavior");
        System.out.println("   • When some methods have default implementation");
        System.out.println("   • When you want to force certain methods to be implemented");
        System.out.println("   • When you need to share code among several classes");

        System.out.println("\n4. BENEFITS:");
        System.out.println("   • Code reusability - share common implementation");
        System.out.println("   • Enforces structure - child classes must implement abstracts");
        System.out.println("   • Prevents instantiation of incomplete concepts");
        System.out.println("   • Template Method Pattern - define algorithm structure");

        System.out.println("\n5. REAL-WORLD EXAMPLES:");
        System.out.println("   • Shape (abstract) → Circle, Rectangle, Triangle");
        System.out.println("   • Employee (abstract) → Manager, Developer, Designer");
        System.out.println("   • Game Character (abstract) → Player, Enemy, NPC");
        System.out.println("   • Document (abstract) → PDFDocument, WordDocument");

        System.out.println("\n6. ABSTRACT vs CONCRETE:");
        System.out.println("   • Abstract Class: Incomplete, template, cannot instantiate");
        System.out.println("   • Concrete Class: Complete, can instantiate, all methods implemented");

        System.out.println("\n7. REMEMBER:");
        System.out.println("   • A class with even ONE abstract method MUST be abstract");
        System.out.println("   • Abstract classes can have zero abstract methods");
        System.out.println("   • Child must implement ALL abstract methods or be abstract itself");
        System.out.println("   • Use 'extends' keyword just like regular inheritance");
    }
}
```

### Step 22: Commit Your Abstract Class Code

1. Click the **Commit** button
2. Write commit message: "Add abstract class concepts with Vehicle and Animal examples"
3. Click **Commit and Push**

---

## 🎯 Challenge Exercises

Try these enhancements to deepen your understanding:

1. **Add a Boat class**: Extends Vehicle, has propellerType, maxSpeed
2. **Create abstract Shape hierarchy**: Abstract Shape with abstract calculateArea(), calculatePerimeter()
3. **Implement concrete shapes**: Circle, Rectangle, Triangle extending Shape
4. **Add abstract Employee class**: With abstract calculateSalary(), concrete clockIn/clockOut
5. **Create SemiTruck**: Extends Truck with additional trailer management
6. **Abstract Game Character**: Create abstract GameCharacter with Player, Enemy, NPC subclasses
7. **Add Moped class**: As mentioned in workbook, extends Vehicle
8. **Create Hovercraft**: As mentioned in workbook, unique vehicle type
9. **Abstract Document class**: With PDFDocument, WordDocument, TextDocument subclasses
10. **Add abstract Appliance**: With Refrigerator, Washer, Microwave implementations
11. **Create racing system**: Abstract RaceVehicle with different speed calculations
12. **Abstract BankAccount**: With Checking, Savings, CD implementations
13. **Add maintenance scheduling**: Abstract method for service intervals
14. **Create abstract Instrument**: Musical instruments with play() abstract method
15. **Abstract MenuItem**: For restaurant system with Appetizer, Entree, Dessert

---

## 📚 Key Takeaways

### Inheritance Concepts Mastered:

1. **IS-A Relationship**: Child IS-A type of Parent

   - Car IS-A Vehicle ✅
   - Test this relationship before using inheritance

2. **Code Reusability**: Write once in parent, use in all children

   - No code duplication
   - Changes in parent affect all children

3. **Protected Access**: Perfect for inheritance

   - Children can access directly
   - Outside classes cannot

4. **Method Overriding**: Children customize parent behavior

   - Use @Override annotation
   - Can call super.method() for parent version

5. **Constructor Chaining**: Constructors call parent constructors

   - super() must be first line
   - Ensures proper initialization

6. **Polymorphism**: One reference type, many actual types

   - Vehicle ref can hold Car, Truck, etc.
   - Enables flexible, extensible code

7. **Multi-level Inheritance**: Chains of inheritance
   - LuxuryCar → Car → Vehicle
   - Each level adds specialization

### Abstract Class Concepts Mastered:

8. **Abstract Classes**: Partial implementation templates

   - Cannot be instantiated directly
   - Can have both abstract and concrete methods
   - Can have instance variables and constructors
   - Single inheritance only (extends one abstract class)

9. **Abstract Methods**: Method signature without implementation

   - No method body, just signature with semicolon
   - Child classes MUST implement all abstract methods
   - Enforces contract for subclasses

10. **Template Method Pattern**: Algorithm structure

    - Abstract class defines overall process
    - Subclasses implement specific steps
    - Ensures consistent process across implementations

11. **When to Use Abstract Classes**:
    - Related classes with shared behavior
    - Some methods have default implementation
    - Need to force certain methods to be overridden
    - Want to prevent instantiation of incomplete concept

### When to Use Each:

#### Use Regular (Concrete) Classes When:

✅ All methods have meaningful implementation  
✅ The class represents a complete, usable concept  
✅ You want to create instances of the class  
✅ No need to force method overriding

#### Use Abstract Classes When:

✅ Classes share common implementation  
✅ Some methods are common, others vary by subclass  
✅ Want to prevent instantiation of the base class  
✅ Need to enforce that subclasses implement certain methods  
✅ Creating a template for a family of related classes

### Real-World Applications:

**Abstract Classes in Java:**

- **Collections**: AbstractList, AbstractSet, AbstractMap
- **GUI Components**: AbstractButton → JButton, JCheckBox
- **I/O Streams**: InputStream (abstract) → FileInputStream, ByteArrayInputStream
- **Game Development**: AbstractCharacter → Player, Enemy, NPC

**Common Abstract Class Patterns:**

- **Shape** (abstract) → Circle, Rectangle, Triangle
  - Abstract: calculateArea(), calculatePerimeter()
  - Concrete: draw(), setColor()
- **Animal** (abstract) → Dog, Cat, Bird
  - Abstract: makeSound(), move()
  - Concrete: eat(), sleep()
- **Employee** (abstract) → Manager, Developer, Designer
  - Abstract: calculateSalary(), getPerformanceReview()
  - Concrete: clockIn(), clockOut()

---

## 🎉 Congratulations!

You've mastered Java inheritance and abstract classes! You've learned:

✅ How to create parent and child classes  
✅ Using extends keyword for inheritance  
✅ Protected access modifier usage  
✅ Method overriding with @Override  
✅ Constructor chaining with super()  
✅ Polymorphism and dynamic binding  
✅ Multi-level inheritance hierarchies  
✅ Abstract classes and abstract methods  
✅ When to use abstract vs concrete classes  
✅ Template method pattern  
✅ Preventing instantiation of incomplete concepts  
✅ Forcing implementation contracts on subclasses  
✅ Real-world application of inheritance and abstraction

**What you built:**

- A complete vehicle hierarchy system
- Abstract vehicle implementations with forced contracts
- Demonstrated inheritance with abstract classes
- Created a practical fleet management application
- Implemented the Animal hierarchy from the workbook
- Showed real-world use cases for abstract classes

**Next Steps:**

1. Try the challenge exercises
2. Add more vehicle types with different abstract implementations
3. Create more abstract hierarchies (shapes, employees, etc.)
4. Experiment with deeper inheritance chains
5. Practice identifying when to make a class abstract
6. Learn about interfaces in the next workbook

Remember: Inheritance is about relationships and code reuse, while abstract classes are about defining partial implementations and forcing certain behaviors. Abstract classes let you say "all subclasses MUST have this behavior, but each implements it differently." This creates powerful, flexible designs!

**The journey continues:** You've now mastered two of the four pillars of OOP (Inheritance and Abstraction through abstract classes). Next up: Interfaces, and then deep dives into Encapsulation and Polymorphism!

Keep coding, keep learning, and keep building! 🚀
