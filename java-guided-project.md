# 📚 Student Grade Management System
## A Step-by-Step Java Tutorial Project

---

## 🎯 Project Overview
We're building a Student Grade Management System that will help you understand and practice all the Java fundamentals from weeks 1-2. You'll type each piece of code, run it, and understand what's happening at every step.

**What You'll Learn:**
- Variables and data types
- String manipulation
- Arrays
- Loops (for, while, do-while)
- Methods
- Input/Output
- Basic calculations

---

## 📁 Project Setup

### Step 1: Create Your Project
1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `StudentGradeSystem`
4. Select **Java** as language
5. Select **Maven** as build system
6. Choose **corretto-17** as JDK
7. Check ✅ **Create Git repository**
8. Click **Create**

**🔍 What's happening?** 
- **IntelliJ IDEA** is like Microsoft Word but for code - it helps you write, organize, and run Java programs
- **Maven** is like a recipe book that helps Java know what ingredients (libraries) your project needs
- **Git repository** is like a time machine for your code - it saves snapshots of your work so you can go back if something breaks
- **Corretto-17** is Amazon's version of Java 17 (like how there's Coke and Pepsi - same thing, different brand)

---

### Step 2: Create Your Main Class
1. Right-click on `src/main/java`
2. Select **New → Java Class**
3. Name it: `StudentGradeManager`
4. Click **OK**

**Type this code:**
```java
public class StudentGradeManager {
    public static void main(String[] args) {
        System.out.println("Welcome to Student Grade Management System!");
    }
}
```

**🔍 What's happening?**

Let's break this down line by line:

- **`public class StudentGradeManager`** 
  - Think of a `class` as a container or a box where we put our code
  - `public` means other parts of the program can see and use this class
  - `StudentGradeManager` is the name we gave our container (like labeling a box)
  - The class name MUST match your file name exactly!

- **`public static void main(String[] args)`**
  - This is the "start button" of your program - Java always looks for this exact line to begin
  - `public` = anyone can use it
  - `static` = you don't need to create an object to use it (we'll learn about objects later)
  - `void` = this method doesn't give back any value (like a vending machine that takes your money but doesn't return change)
  - `main` = the special name Java looks for
  - `String[] args` = a way to receive input when the program starts (we'll use this later)

- **`System.out.println("Welcome...")`**
  - `System` = Java's built-in toolbox
  - `out` = the output stream (think of it as the screen)
  - `println` = print line (write text and move to next line)
  - The text in quotes is what appears on screen
  - The semicolon `;` is like a period at the end of a sentence - it tells Java the instruction is complete

**▶️ Run it:** Click the green arrow ▶️ next to line 2 (the main method)

---

## 📊 Part 1: Working with Variables

### Step 3: Declare Student Information Variables

**Replace your main method with this code:**
```java
public static void main(String[] args) {
    // Step 3: Declaring variables for student information
    String studentName = "Alice Johnson";
    int studentId = 12345;
    int studentAge = 18;
    char gradeLevel = 'A';
    boolean isEnrolled = true;
    
    // Print the information
    System.out.println("=== STUDENT INFORMATION ===");
    System.out.println("Name: " + studentName);
    System.out.println("ID: " + studentId);
    System.out.println("Age: " + studentAge);
    System.out.println("Grade Level: " + gradeLevel);
    System.out.println("Enrolled: " + isEnrolled);
}
```

**🔍 What's happening?**

Think of variables as labeled boxes where you store information:

- **`String studentName = "Alice Johnson";`**
  - `String` = The type of box that holds text (words, sentences)
  - `studentName` = The label on the box
  - `=` = Put something in the box
  - `"Alice Johnson"` = The actual text we're storing
  - Strings ALWAYS use double quotes " "
  - A String can hold any text: names, addresses, entire paragraphs!

- **`int studentId = 12345;`**
  - `int` = Integer, a box that holds whole numbers only (no decimals)
  - Can store numbers from about -2 billion to +2 billion
  - Perfect for: counting, IDs, age, quantity

- **`char gradeLevel = 'A';`**
  - `char` = Character, stores exactly ONE letter, number, or symbol
  - Uses SINGLE quotes ' ' (not double quotes like String!)
  - Common mistake: `char grade = "A";` ❌ Wrong! Must be `'A'` ✅

- **`boolean isEnrolled = true;`**
  - `boolean` = A yes/no box (only stores `true` or `false`)
  - Like a light switch - only ON or OFF
  - Used for: flags, status checks, conditions

- **The + operator with Strings:**
  - When you use `+` with text, Java glues them together
  - `"Name: " + studentName` becomes `"Name: Alice Johnson"`
  - This is called concatenation (fancy word for joining)

**▶️ Run it** and observe the output

---

### Step 4: Working with Numbers and Calculations

**Add this code after the previous section:**
```java
// Step 4: Working with grades and calculations
double mathGrade = 85.5;
double scienceGrade = 92.0;
double englishGrade = 88.75;
double historyGrade = 91.25;

// Calculate the average
double totalGrades = mathGrade + scienceGrade + englishGrade + historyGrade;
double averageGrade = totalGrades / 4;

System.out.println("\n=== GRADE CALCULATIONS ===");
System.out.println("Math: " + mathGrade);
System.out.println("Science: " + scienceGrade);
System.out.println("English: " + englishGrade);
System.out.println("History: " + historyGrade);
System.out.println("Total: " + totalGrades);
System.out.println("Average: " + averageGrade);
```

**🔍 What's happening?**

- **`double mathGrade = 85.5;`**
  - `double` = A box that holds decimal numbers (numbers with a decimal point)
  - More precise than `int` but uses more memory
  - Perfect for: money, measurements, grades, percentages
  - Can store HUGE numbers with up to 15 digits of precision

- **Why use `double` instead of `int` for grades?**
  - `int grade = 85.5;` ❌ ERROR! int can't store decimals
  - `int grade = 85;` ✅ Works but loses the .5
  - `double grade = 85.5;` ✅ Keeps the exact value

- **Math operations:**
  - `+` adds numbers (just like a calculator)
  - `/` divides numbers
  - The computer follows math rules: multiply/divide before add/subtract
  - `totalGrades / 4` means "divide totalGrades by 4"

- **`\n` in the println:**
  - `\n` means "new line" - like pressing Enter
  - Makes output easier to read by adding blank lines
  - Try removing it to see the difference!

**Important concept:** Variables can store results of calculations!
- First, Java calculates `85.5 + 92.0 + 88.75 + 91.25 = 357.5`
- Then it stores 357.5 in the `totalGrades` box
- Later, it calculates `357.5 / 4 = 89.375` and stores it in `averageGrade`

**▶️ Run it** and verify the math is correct

---

## 📝 Part 2: String Manipulation

### Step 5: Working with Student Names

**Add this code:**
```java
// Step 5: String manipulation
System.out.println("\n=== STRING OPERATIONS ===");

// Get the length of the name
int nameLength = studentName.length();
System.out.println("Name length: " + nameLength + " characters");

// Convert to uppercase and lowercase
String upperName = studentName.toUpperCase();
String lowerName = studentName.toLowerCase();
System.out.println("Uppercase: " + upperName);
System.out.println("Lowercase: " + lowerName);

// Extract first and last name
int spaceIndex = studentName.indexOf(" ");
String firstName = studentName.substring(0, spaceIndex);
String lastName = studentName.substring(spaceIndex + 1);
System.out.println("First name: " + firstName);
System.out.println("Last name: " + lastName);

// Check if name contains certain text
boolean hasJohnson = studentName.contains("Johnson");
System.out.println("Is this a Johnson? " + hasJohnson);
```

**🔍 What's happening?**

Strings come with built-in superpowers (methods) that let us manipulate text:

- **`.length()`**
  - Counts every character including spaces
  - "Alice Johnson" has 13 characters (5 + 1 space + 7)
  - Notice the parentheses () - this tells Java to DO something
  - The result is an `int` number we can store

- **`.toUpperCase()` and `.toLowerCase()`**
  - Creates a NEW string with all capitals or all lowercase
  - The original `studentName` doesn't change!
  - "Alice Johnson" → "ALICE JOHNSON" or "alice johnson"

- **Understanding `.indexOf(" ")`**
  - Searches for a space character and tells you its position
  - Strings are like apartment buildings - each character has an address starting from 0
  - "Alice Johnson": A=0, l=1, i=2, c=3, e=4, space=5, J=6, etc.
  - So `indexOf(" ")` returns 5 (the position of the space)

- **`.substring(start, end)` - The Text Cutter**
  - Extracts a piece of text from a larger string
  - Like using scissors to cut out part of a sentence
  - `substring(0, 5)` means "give me characters from position 0 up to (but not including) position 5"
  - From "Alice Johnson": positions 0-4 give us "Alice"
  
- **`.substring(spaceIndex + 1)` - Getting the last name**
  - When you don't specify an end, it takes everything from start to the end
  - `spaceIndex + 1` means "start after the space"
  - Position 6 to end gives us "Johnson"

- **`.contains("text")`**
  - Asks a yes/no question: "Does this string contain this text?"
  - Returns `true` or `false` (boolean)
  - Case-sensitive! "Johnson" ≠ "johnson"

**Think of it like this:** If studentName is a Word document, these methods are like the Find, Replace, and Format tools!

**▶️ Run it** and watch the string transformations

---

## 🔄 Part 3: Arrays and Loops

### Step 6: Store Multiple Grades in Arrays

**Add this code:**
```java
// Step 6: Using arrays to store multiple test scores
System.out.println("\n=== WORKING WITH ARRAYS ===");

// Create an array of test scores for math class
double[] mathTestScores = {85.5, 92.0, 78.5, 95.0, 88.0};
String[] testNames = {"Test 1", "Test 2", "Test 3", "Test 4", "Test 5"};

System.out.println("Math test scores stored in array");
System.out.println("Number of tests: " + mathTestScores.length);

// Access individual elements
System.out.println("\nAccessing array elements:");
System.out.println("First test score: " + mathTestScores[0]);
System.out.println("Last test score: " + mathTestScores[mathTestScores.length - 1]);

// Modify an array element
mathTestScores[2] = 82.0;  // Change Test 3 score
System.out.println("Updated Test 3 score: " + mathTestScores[2]);
```

**🔍 What's happening?**

Arrays are like a row of lockers or a pill organizer with compartments:

- **`double[] mathTestScores`**
  - `double[]` = "I want a row of boxes that each hold a decimal number"
  - The square brackets `[]` tell Java this is an array, not a single variable
  - Think of it as 5 connected boxes labeled 0, 1, 2, 3, 4

- **`{85.5, 92.0, 78.5, 95.0, 88.0}`**
  - This creates and fills the array in one step
  - First score (85.5) goes in box 0
  - Second score (92.0) goes in box 1
  - And so on...

- **Why do arrays start at 0, not 1?**
  - Historical computing reason: 0 means "no offset from the start"
  - EVERY programming language does this
  - Common beginner mistake: trying to access mathTestScores[5] when only 0-4 exist!

- **`.length` (no parentheses!)**
  - Arrays use `.length` (property) not `.length()` (method)
  - Tells you how many compartments the array has
  - Our array has 5 elements, so length = 5

- **`mathTestScores[0]`**
  - The number in brackets is called the INDEX
  - Like saying "give me what's in locker number 0"
  - `mathTestScores[0]` = 85.5 (first element)
  - `mathTestScores[4]` = 88.0 (last element in a 5-item array)

- **`mathTestScores[mathTestScores.length - 1]`**
  - Clever trick to get the last element regardless of array size
  - If length is 5, then 5-1 = 4, which is the last valid index
  - This works for any size array!

- **Changing array values:**
  - `mathTestScores[2] = 82.0` means "put 82.0 in compartment 2"
  - This REPLACES whatever was there before (78.5)
  - Arrays are mutable (changeable)

**Visual representation:**
```
Index:    [0]    [1]    [2]    [3]    [4]
Values:  85.5   92.0   78.5   95.0   88.0
                        ↓
                      82.0 (after change)
```

**▶️ Run it** and observe how arrays store multiple values

---

### Step 7: Loop Through Arrays - Three Ways

**Add this code:**
```java
// Step 7: Different types of loops
System.out.println("\n=== LOOPS DEMONSTRATION ===");

// FOR LOOP - Traditional counting loop
System.out.println("\nUsing FOR loop:");
for (int i = 0; i < mathTestScores.length; i++) {
    System.out.println(testNames[i] + ": " + mathTestScores[i]);
}

// ENHANCED FOR LOOP (for-each) - Simpler but no index
System.out.println("\nUsing ENHANCED FOR loop:");
for (double score : mathTestScores) {
    System.out.println("Score: " + score);
}

// WHILE LOOP - Condition-based loop
System.out.println("\nUsing WHILE loop:");
int index = 0;
while (index < mathTestScores.length) {
    System.out.println("Test " + (index + 1) + ": " + mathTestScores[index]);
    index++;
}

// DO-WHILE LOOP - Executes at least once
System.out.println("\nUsing DO-WHILE loop:");
int counter = 0;
do {
    System.out.println("Processing test " + (counter + 1));
    counter++;
} while (counter < 3);  // Only process first 3
```

**🔍 What's happening?**

Loops are like instruction sets that repeat - imagine telling someone "do this 5 times" instead of repeating yourself 5 times!

**FOR LOOP - The Counter Loop:**
```java
for (int i = 0; i < mathTestScores.length; i++)
```
Let's decode this piece by piece:
1. **`int i = 0`** = Start: Create a counter called `i` starting at 0
2. **`i < mathTestScores.length`** = Condition: Keep going while i is less than array length (5)
3. **`i++`** = After each loop: Add 1 to i (i++ is shorthand for i = i + 1)

How it executes:
- Round 1: i=0, prints testNames[0] and mathTestScores[0]
- Round 2: i=1, prints testNames[1] and mathTestScores[1]
- Round 3: i=2, prints testNames[2] and mathTestScores[2]
- Round 4: i=3, prints testNames[3] and mathTestScores[3]
- Round 5: i=4, prints testNames[4] and mathTestScores[4]
- Round 6: i=5, condition (5 < 5) is false, STOP!

**ENHANCED FOR LOOP - The Simple Iterator:**
```java
for (double score : mathTestScores)
```
- Read as: "For each score in mathTestScores"
- Java automatically gets each value one by one
- `score` is a temporary variable that holds the current value
- Simpler syntax but you don't know which index you're at
- Can't use this when you need to know the position!

**WHILE LOOP - The Conditional Loop:**
```java
while (condition is true) { do something }
```
- Like saying "keep doing this as long as..."
- Checks condition FIRST, then executes
- If condition is false from start, never executes
- You must update the condition variable inside the loop or it runs forever!
- `index++` is crucial - without it, index stays 0 forever (infinite loop)!

**DO-WHILE LOOP - The Guaranteed-Once Loop:**
```java
do { something } while (condition);
```
- Executes the code block FIRST, then checks condition
- Guarantees at least one execution even if condition is false
- Useful for menus: show menu at least once, repeat if needed
- Notice the semicolon after while(condition); - easy to forget!

**When to use each loop:**
- **FOR**: When you know exactly how many times (iterating arrays, counting)
- **ENHANCED FOR**: When you just need values, not positions
- **WHILE**: When you don't know how many times (user input, searching)
- **DO-WHILE**: When you need at least one execution (menus, validation)

**▶️ Run it** and see how each loop type works differently

---

### Step 8: Find Highest and Lowest Scores

**Add this code:**
```java
// Step 8: Finding max and min values in array
System.out.println("\n=== FINDING MIN/MAX ===");

double highestScore = mathTestScores[0];  // Start with first element
double lowestScore = mathTestScores[0];   // Start with first element

for (int i = 1; i < mathTestScores.length; i++) {
    if (mathTestScores[i] > highestScore) {
        highestScore = mathTestScores[i];
    }
    if (mathTestScores[i] < lowestScore) {
        lowestScore = mathTestScores[i];
    }
}

System.out.println("Highest score: " + highestScore);
System.out.println("Lowest score: " + lowestScore);
System.out.println("Score range: " + (highestScore - lowestScore));
```

**🔍 What's happening?**

This is a classic algorithm (step-by-step solution) for finding the largest and smallest values:

**The Strategy - Like Finding the Tallest Person in a Room:**
1. Assume the first person is the tallest AND shortest (for now)
2. Compare with everyone else one by one
3. If you find someone taller, they become the new "tallest"
4. If you find someone shorter, they become the new "shortest"

**Step-by-step execution with our data [85.5, 92.0, 78.5, 95.0, 88.0]:**

- **Initial state:** highestScore = 85.5, lowestScore = 85.5
- **i = 1:** Check 92.0
  - Is 92.0 > 85.5? YES! highestScore becomes 92.0
  - Is 92.0 < 85.5? NO. lowestScore stays 85.5
- **i = 2:** Check 78.5
  - Is 78.5 > 92.0? NO. highestScore stays 92.0
  - Is 78.5 < 85.5? YES! lowestScore becomes 78.5
- **i = 3:** Check 95.0
  - Is 95.0 > 92.0? YES! highestScore becomes 95.0
  - Is 95.0 < 78.5? NO. lowestScore stays 78.5
- **i = 4:** Check 88.0
  - Is 88.0 > 95.0? NO. highestScore stays 95.0
  - Is 88.0 < 78.5? NO. lowestScore stays 78.5
- **Final result:** Highest = 95.0, Lowest = 78.5

**Why start the loop at i = 1?**
- We already used element 0 as our initial values
- No point comparing it with itself
- Saves one unnecessary comparison

**The IF statement:**
```java
if (condition) {
    // do this only if condition is true
}
```
- The code inside {} only runs if the condition is true
- No `else` needed here - we just skip if condition is false

**▶️ Run it** and verify it finds the correct min/max values

---

## ⚙️ Part 4: Methods (Functions)

### Step 9: Create Reusable Methods

**Add these methods OUTSIDE the main method but INSIDE the class:**
```java
// Step 9: Creating methods for reusable code
// Method to calculate average of an array
public static double calculateAverage(double[] scores) {
    double sum = 0;
    for (double score : scores) {
        sum += score;  // Same as: sum = sum + score
    }
    return sum / scores.length;
}

// Method to determine letter grade
public static char getLetterGrade(double score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

// Method to print a formatted report
public static void printReport(String name, double[] scores) {
    System.out.println("\n=== STUDENT REPORT FOR " + name.toUpperCase() + " ===");
    double average = calculateAverage(scores);
    char letterGrade = getLetterGrade(average);
    
    System.out.println("Test Scores: ");
    for (int i = 0; i < scores.length; i++) {
        System.out.println("  Test " + (i + 1) + ": " + scores[i]);
    }
    System.out.println("Average: " + average);
    System.out.println("Letter Grade: " + letterGrade);
}
```

**Now add this to your main method:**
```java
// Step 9: Using our custom methods
System.out.println("\n=== USING METHODS ===");

double mathAverage = calculateAverage(mathTestScores);
System.out.println("Math average (using method): " + mathAverage);

char mathLetterGrade = getLetterGrade(mathAverage);
System.out.println("Math letter grade: " + mathLetterGrade);

// Print full report
printReport(studentName, mathTestScores);
```

**🔍 What's happening?**

Methods are like recipes or mini-programs that do specific tasks. Instead of writing the same code over and over, we write it once and reuse it!

**Understanding Method Structure:**
```java
public static returnType methodName(parameters) {
    // method body
    return value;
}
```

**Let's decode `calculateAverage` method:**
- **`public`** = Other parts of the program can use this method
- **`static`** = Can be called without creating an object (advanced topic)
- **`double`** = This method gives back a decimal number
- **`calculateAverage`** = The name we chose (describes what it does)
- **`double[] scores`** = Input it needs (an array of decimals)
- **`return sum / scores.length`** = The answer it sends back

**Think of it like a vending machine:**
- Input: You put in money and press a button (parameters)
- Process: Machine does its work (method body)
- Output: You get a snack (return value)

**The `calculateAverage` method:**
1. Creates a sum variable starting at 0
2. Loops through each score in the array
3. Adds each score to the sum (sum += score means sum = sum + score)
4. Divides total by number of scores
5. Returns (gives back) the result

**The `getLetterGrade` method - The Decision Tree:**
- Uses if-else chain to make decisions
- `else if` only checks if previous conditions were false
- Once a condition is true, it returns immediately (method stops)
- The final `else` catches everything below 60

**How the grading logic flows:**
- Score 95: Is 95 >= 90? YES → Return 'A' (stop here)
- Score 85: Is 85 >= 90? NO → Is 85 >= 80? YES → Return 'B'
- Score 75: Is 75 >= 90? NO → Is 75 >= 80? NO → Is 75 >= 70? YES → Return 'C'
- And so on...

**The `printReport` method - void returns nothing:**
- **`void`** means "this method doesn't give back a value"
- It just does something (prints to screen) but doesn't return data
- Like a printer - you send it a document, it prints, but doesn't give you anything back

**Calling methods:**
- `calculateAverage(mathTestScores)` = "Run the calculateAverage recipe using mathTestScores"
- The result can be stored: `double avg = calculateAverage(mathTestScores)`
- Or used directly: `System.out.println(calculateAverage(mathTestScores))`

**Why use methods?**
1. **DRY Principle**: Don't Repeat Yourself
2. **Easier to test**: Test one method instead of multiple copies
3. **Easier to fix**: Fix bugs in one place
4. **Readable code**: `calculateAverage(scores)` is self-explanatory

**▶️ Run it** and see how methods make code reusable

---

## 📥 Part 5: User Input

### Step 10: Get Input from User

**Add this import at the very top of your file (before the class):**
```java
import java.util.Scanner;
```

**Add this code to your main method:**
```java
// Step 10: Getting user input
System.out.println("\n=== USER INPUT ===");
Scanner scanner = new Scanner(System.in);

System.out.print("Enter student name: ");
String inputName = scanner.nextLine();

System.out.print("How many test scores to enter? ");
int numberOfTests = scanner.nextInt();

double[] userScores = new double[numberOfTests];
for (int i = 0; i < numberOfTests; i++) {
    System.out.print("Enter score for Test " + (i + 1) + ": ");
    userScores[i] = scanner.nextDouble();
}

// Use our methods with user input
printReport(inputName, userScores);

scanner.close();
```

**🔍 What's happening?**

The Scanner is like a cashier at a store - it takes input from the customer (user) and processes it:

**`import java.util.Scanner;`**
- Java has thousands of pre-built tools in its library
- `import` means "I want to use this specific tool"
- Must be at the very top of your file, before the class
- Like getting a tool from the garage before starting work

**`Scanner scanner = new Scanner(System.in);`**
- Creates a new Scanner object (think of it as hiring a cashier)
- `System.in` means "read from the keyboard"
- `scanner` is the name we gave our Scanner (like naming a variable)
- The `new` keyword creates a fresh Scanner ready to work

**Different Scanner methods for different types:**
- **`.nextLine()`** = Reads entire line of text (until Enter key)
  - Good for: names, sentences, addresses
  - Reads everything including spaces
  
- **`.nextInt()`** = Reads a whole number
  - Good for: age, count, ID numbers
  - Will crash if user types letters or decimals!
  
- **`.nextDouble()`** = Reads a decimal number
  - Good for: prices, grades, measurements
  - Can accept whole numbers too (treats 85 as 85.0)

**`System.out.print()` vs `System.out.println()`**
- `print()` stays on the same line (cursor waits there)
- `println()` moves to next line after printing
- Using `print()` for prompts makes input appear on same line

**Dynamic array creation:**
```java
double[] userScores = new double[numberOfTests];
```
- We don't know the size until the user tells us
- `new double[numberOfTests]` creates an array of that exact size
- If user says 3, we get an array with 3 slots
- All slots start with 0.0 (default for double)

**The input loop:**
- Asks for each test score one by one
- `(i + 1)` for display because humans count from 1, not 0
- Stores each score in the correct array position

**`scanner.close()`**
- Tells Java "I'm done with the Scanner"
- Like hanging up the phone when done talking
- Good practice but not always necessary for simple programs

**Common Scanner gotchas:**
1. Mixing nextLine() with nextInt() can cause issues (leaves Enter key in buffer)
2. User typing wrong type causes crash (typing "abc" when expecting number)
3. Forgetting to import Scanner gives error

**▶️ Run it** and try entering your own data!

---

## 🎯 Part 6: Putting It All Together

### Step 11: Complete Student Management System

**Create a new method for the complete system:**
```java
public static void runCompleteSystem() {
    Scanner scanner = new Scanner(System.in);
    System.out.println("\n╔════════════════════════════════════════╗");
    System.out.println("║   STUDENT GRADE MANAGEMENT SYSTEM      ║");
    System.out.println("╚════════════════════════════════════════╝");
    
    // Get student information
    System.out.print("\nEnter student name: ");
    String name = scanner.nextLine();
    
    System.out.print("Enter student ID: ");
    int id = scanner.nextInt();
    
    // Get grades for multiple subjects
    String[] subjects = {"Math", "Science", "English", "History"};
    double[] subjectAverages = new double[subjects.length];
    
    for (int i = 0; i < subjects.length; i++) {
        System.out.println("\n--- " + subjects[i] + " Grades ---");
        System.out.print("How many " + subjects[i] + " tests? ");
        int testCount = scanner.nextInt();
        
        double[] testScores = new double[testCount];
        for (int j = 0; j < testCount; j++) {
            System.out.print("Enter " + subjects[i] + " Test " + (j + 1) + " score: ");
            testScores[j] = scanner.nextDouble();
        }
        
        subjectAverages[i] = calculateAverage(testScores);
    }
    
    // Generate final report
    System.out.println("\n╔════════════════════════════════════════╗");
    System.out.println("║           FINAL REPORT                 ║");
    System.out.println("╚════════════════════════════════════════╝");
    System.out.println("Student: " + name);
    System.out.println("ID: " + id);
    System.out.println("\nSubject Averages:");
    
    double overallTotal = 0;
    for (int i = 0; i < subjects.length; i++) {
        char grade = getLetterGrade(subjectAverages[i]);
        System.out.printf("  %-10s: %.2f (%c)\n", subjects[i], subjectAverages[i], grade);
        overallTotal += subjectAverages[i];
    }
    
    double overallAverage = overallTotal / subjects.length;
    char overallGrade = getLetterGrade(overallAverage);
    
    System.out.println("\nOverall Average: " + String.format("%.2f", overallAverage));
    System.out.println("Overall Grade: " + overallGrade);
    
    // Determine pass/fail
    if (overallAverage >= 60) {
        System.out.println("Status: ✅ PASSING");
    } else {
        System.out.println("Status: ❌ NEEDS IMPROVEMENT");
    }
    
    scanner.close();
}
```

**Call this method from main:**
```java
// Step 11: Run the complete system
runCompleteSystem();
```

**🔍 What's happening?**

This is where everything comes together - like assembling a puzzle where each piece is a concept we learned:

**The fancy borders:**
```java
System.out.println("╔════════════╗");
```
- These are Unicode characters that create nice boxes
- Makes output look professional
- You can copy-paste these or use simple dashes ---

**Parallel arrays - subjects and subjectAverages:**
- `subjects[0]` = "Math" corresponds to `subjectAverages[0]` = Math average
- Like having two filing cabinets where drawer 1 in each contains related items
- This keeps subject names and their averages synchronized

**Nested loops - A loop inside another loop:**
```java
for (int i = 0; i < subjects.length; i++) {      // Outer loop
    for (int j = 0; j < testCount; j++) {        // Inner loop
```
- Outer loop: Goes through each subject (Math, Science, etc.)
- Inner loop: For EACH subject, gets multiple test scores
- If we have 4 subjects and 3 tests each, inner loop runs 12 times total!

**Why use different variable names (i and j)?**
- Each loop needs its own counter
- Using `i` for both would cause conflicts
- Convention: i for outer, j for inner, k for third level

**The printf magic - Formatted output:**
```java
System.out.printf("  %-10s: %.2f (%c)\n", subjects[i], subjectAverages[i], grade);
```
- `printf` = Print with formatting (like a template)
- `%-10s` = String, left-aligned, 10 characters wide
- `%.2f` = Float/double with 2 decimal places
- `%c` = Character
- Values after the template fill in the blanks in order

**Example output:**
```
Math      : 87.50 (B)
Science   : 92.33 (A)
```

**String.format() - Another way to format:**
```java
String.format("%.2f", overallAverage)
```
- Formats a number to 2 decimal places
- 89.33333 becomes "89.33"
- Returns a String you can print or store

**The decision logic:**
```java
if (overallAverage >= 60) {
    System.out.println("Status: ✅ PASSING");
} else {
    System.out.println("Status: ❌ NEEDS IMPROVEMENT");
}
```
- Simple if-else: one thing OR the other
- The emojis (✅ ❌) make output more visual
- 60 is the threshold - change this to adjust pass/fail criteria

**How the complete flow works:**
1. Get student info (name, ID)
2. For each subject:
   - Ask how many tests
   - Get each test score
   - Calculate and store the average
3. Calculate overall average from subject averages
4. Display formatted report
5. Determine pass/fail status

**▶️ Run it** and test the complete system! Try different numbers of tests per subject.

---

## 💾 Part 7: Version Control with IntelliJ

### Step 12: Share Your Project to GitHub

**Initial Setup - Share Project to GitHub:**

1. **In IntelliJ**, go to **VCS → Share Project on GitHub**
   - If VCS menu isn't visible, look for **Git → GitHub → Share Project on GitHub**

2. **In the dialog that appears:**
   - Repository name: `StudentGradeSystem` (or keep the suggested name)
   - Description: "Java fundamentals practice project"
   - Private repository: Your choice (unchecked = public)
   - Click **Share**

3. **In the next dialog (Add Files to Git):**
   - Make sure all files are checked ✅
   - Add commit message: "Initial project setup"
   - Click **Add**

4. IntelliJ will create the repository and push your code. You'll see a notification with a link to your GitHub repository!

**Making Changes and Saving to Git:**

After making changes to your code:

1. **Check what changed:**
   - Look at the **Git** tab at the bottom of IntelliJ
   - Changed files appear in different colors:
     - Blue = Modified files
     - Green = New files
     - Red = Deleted files

2. **Commit your changes:**
   - Click the **Commit** button (checkmark icon) in the toolbar, OR
   - Press **Ctrl+K** (Windows) or **Cmd+K** (Mac)
   
3. **In the Commit dialog:**
   - Review the files being committed
   - Write a meaningful commit message like:
     - "Added user input functionality"
     - "Implemented grade calculation methods"
     - "Fixed average calculation bug"
   - Click **Commit** or **Commit and Push**

4. **Push to GitHub:**
   - If you chose just "Commit", push separately:
   - Click the **Push** button (green arrow) in the toolbar, OR
   - Press **Ctrl+Shift+K** (Windows) or **Cmd+Shift+K** (Mac)
   - Click **Push** in the dialog

**🔍 What's happening with Git?**

Think of Git like a save system in a video game:

- **Commit** = Creating a save point in your game
  - Records the current state of your code
  - You can return to any commit if something breaks
  - Each commit has a message describing what changed

- **Push** = Uploading your save to the cloud
  - Sends your commits to GitHub
  - Others can see your code (if public)
  - Backup in case your computer crashes

- **Repository** = The container for your entire project
  - Includes all files and entire history
  - Like a folder with superpowers - it remembers everything!

**IntelliJ Git Visual Indicators:**
- **Green filename** = New file not yet in Git
- **Blue filename** = Modified file
- **White/normal filename** = No changes since last commit
- **Green line on the left of code** = New lines added
- **Blue line on the left** = Lines modified

**Best Practices:**
- Commit often (every time something works)
- Write clear commit messages
- Push at the end of each coding session
- Never commit broken code if you can help it

---

## 🏆 Concepts You've Practiced

✅ **Variables & Data Types**: String, int, double, char, boolean  
✅ **Arrays**: Declaration, initialization, accessing elements  
✅ **Loops**: for, enhanced for, while, do-while  
✅ **String Methods**: length(), toUpperCase(), substring(), indexOf()  
✅ **Conditionals**: if, else if, else  
✅ **Methods**: Parameters, return values, void methods  
✅ **User Input**: Scanner class  
✅ **Calculations**: Average, sum, min/max  
✅ **Git with IntelliJ**: Repository creation, commits, pushing  

---

## 💪 Challenge Modifications (Optional)

Once you understand the code, try these modifications:

1. **Add attendance tracking**: Create a boolean array for attendance (present/absent for each class)
2. **Add more subjects**: Expand the subjects array to include Art, PE, Music
3. **Grade validation**: Check that entered grades are between 0-100
4. **Add date/time**: Include when the report was generated using `LocalDateTime.now()`
5. **Grade curving**: Add 5 bonus points to all scores below 70
6. **Find top subject**: Identify which subject has the highest average

---

## 📚 Key Takeaways

1. **Variables** are like labeled boxes that store data
2. **Arrays** are like rows of lockers holding multiple values
3. **Loops** are like "repeat" instructions to avoid writing the same code multiple times
4. **Methods** are like recipes you can reuse whenever needed
5. **Scanner** is your way to talk with the user
6. **Git** is your safety net and collaboration tool

---

## 🎉 Congratulations!

You've built a complete Java application using all the fundamentals from weeks 1-2! 

**What to do next:**
1. Type all the code yourself (don't copy-paste) - muscle memory is important!
2. Run after each step to see the progression
3. When you get an error, read it carefully - Java tells you exactly what's wrong and which line
4. Change values and see what happens
5. Try to explain each line to a classmate or rubber duck
6. Keep this project as a reference - you'll use these patterns again and again!

Remember: Programming is like learning to ride a bike - you might wobble at first, but with practice, it becomes second nature. Every error is a learning opportunity, and every working program is an achievement!

**The most important thing:** If something doesn't make sense, that's normal! Re-read the explanation, run the code again, change something and see what happens. Understanding comes from doing, breaking, and fixing!