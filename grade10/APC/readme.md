# UNIT 1

In **AP Computer Science A**, **Unit 1: Primitive Types** covers how Java prints output, stores basic data in memory, evaluates arithmetic expressions, and converts between data types. Every topic below is strictly within the official AP-CSA Java Subset.

---

### Key Takeaways for AP-CSA Unit 1

* **Only three primitive types are tested on the AP-CSA exam: `int` (whole numbers), `double` (decimal numbers), and `boolean` (`true` or `false`).**
* **Integer division (`int / int`) always truncates (cuts off) the decimal portion without rounding—for example, `9 / 4` evaluates to `2`.**
* **The modulus operator (`%`) returns the remainder of division—for example, `9 % 4` evaluates to `1`.**
* **Explicit casting (`(int)` or `(double)`) has higher precedence than `*`, `/`, and `%`, meaning `(double) 5 / 2` casts `5` to `5.0` *before* dividing.**
* **Integer overflow occurs when an `int` exceeds `Integer.MAX_VALUE` (`2147483647`) or drops below `Integer.MIN_VALUE` (`-2147483648`), wrapping around silently to the opposite extreme.**

---

### 1. Output & String Literals (`System.out`)

Java displays console output using `System.out.print()` and `System.out.println()`.

* **`System.out.print(item)`:** Outputs `item` and keeps the cursor on the **same line**.
* **`System.out.println(item)`:** Outputs `item` and moves the cursor to the **next line**. Calling `System.out.println()` with no arguments prints a blank line.
* **Escape Sequences:** Special two-character codes inside double quotes `"..."`:
* `\"` prints a literal double quote (`"`)
* `\\` prints a literal backslash (`\`)
* `\n` inserts a newline



#### String Concatenation Order of Operations

When `+` joins a `String` with numbers, Java evaluates **left-to-right**. Once a `String` appears, every `+` after it performs text concatenation rather than math:

```text
Expression: 2 + 3 + "Result: " + 2 + 3
            \___/
              5   + "Result: "
              \______________/
                "5Result: "    + 2
                \________________/
                  "5Result: 2"   + 3  ---> "5Result: 23"

```

---

### 2. Variables & Primitive Data Types

#### Analogy: Kitchen Storage Containers

* **`int` (Egg Carton):** Holds whole items only (`-2,147,483,648` to `2,147,483,647`). You cannot put half an egg in a slot.
* **`double` (Liquid Measuring Cup):** Holds decimal numbers with floating-point precision (e.g., `3.14`, `-0.5`, `4.0`). Because computers store decimals in binary, `double` values can have tiny rounding inaccuracies (e.g., `0.1 + 0.2` might store as `0.30000000000000004`).
* **`boolean` (Light Switch):** Holds only one of two states: `true` or `false`. In Java, `boolean` cannot be converted to `0` or `1`.

#### Declaring, Initializing & Constants (`final`)

* **Declaration:** Reserving memory with a type and name (`int score;`).
* **Initialization:** Assigning the first value (`score = 100;`).
* **Naming Convention:** Variables use `camelCase` (`highScore`). Constants declared with `final` use `UPPER_SNAKE_CASE` (`final int MAX_LIVES = 3;`) and cannot be reassigned once set.

---

### 3. Arithmetic & Compound Assignment Operators

#### Precedence Hierarchy (Highest to Lowest)

1. **Parentheses:** `()`
2. **Casting & Unary Operators:** `(int)`, `(double)`, unary `-`
3. **Multiplicative (Left-to-Right):** `*`, `/`, `%`
4. **Additive (Left-to-Right):** `+`, `-`
5. **Assignment (Right-to-Left):** `=`, `+=`, `-=`, `*=`, `/=`, `%=`

#### Compound Assignment & Increment Shortcuts

| Shortcut | Equivalent Expression | Example (`x` starts at `10`) | New Value of `x` |
| --- | --- | --- | --- |
| `x += 4;` | `x = x + 4;` | `10 + 4` | `14` |
| `x -= 3;` | `x = x - 3;` | `10 - 3` | `7` |
| `x *= 2;` | `x = x * 2;` | `10 * 2` | `20` |
| `x /= 4;` | `x = x / 4;` | `10 / 4` (int division) | `2` |
| `x %= 3;` | `x = x % 3;` | `10 % 3` (remainder) | `1` |
| `x++;` | `x = x + 1;` | `10 + 1` | `11` |
| `x--;` | `x = x - 1;` | `10 - 1` | `9` |

*(Note: Prefix operators like `++x` are not tested on the AP-CSA exam—only postfix `x++` and `x--`.)*

---

### 4. Casting, Rounding & Overflow

#### Widening vs. Narrowing Conversion Flow

```text
WIDENING (Automatic - Safe, no data lost)
  int (5)  ------------------------------>  double (5.0)
  double d = 5;  // Legal! Java automatically converts 5 to 5.0

NARROWING (Manual Cast Required - Truncates decimal)
  double (5.9)  ---[ (int) 5.9 ]--------->  int (5)
  int n = 5.9;        // COMPILE ERROR! Possible lossy conversion
  int n = (int) 5.9;  // Legal! Truncates .9 and stores 5

```

#### AP-CSA Casting Traps

* **Trap 1 — Casting Too Late:**
* `(double) (7 / 2)` evaluates `7 / 2` first (`3`), then casts `3` to `3.0`.
* `(double) 7 / 2` casts `7` to `7.0` first, then evaluates `7.0 / 2` to `3.5`.


* **Trap 2 — Rounding Formula (High-Frequency MCQ Topic):**
Because `(int)` always chops toward zero, add `0.5` before casting positive numbers, or subtract `0.5` before casting negative numbers:
* **Positive `double x`:** `int rounded = (int) (x + 0.5);`
* **Negative `double x`:** `int rounded = (int) (x - 0.5);`


* **Trap 3 — Integer Overflow:**
`Integer.MAX_VALUE` is `2147483647` and `Integer.MIN_VALUE` is `-2147483648`. Adding `1` to `Integer.MAX_VALUE` wraps around to `-2147483648` without throwing an error.

---

### Practice Programs to Solidify Unit 1

#### Program 1: Cash Register Change Breakdown (`/` and `%`)

Uses integer division and modulus chaining to break a cent amount into the fewest coins.

```java
public class CoinChanger {
    public static void main(String[] args) {
        int totalCents = 187;

        int quarters = totalCents / 25;         // 187 / 25 = 7 quarters
        int remainder = totalCents % 25;        // 187 % 25 = 12 cents left

        int dimes = remainder / 10;             // 12 / 10 = 1 dime
        remainder = remainder % 10;             // 12 % 10 = 2 cents left

        int nickels = remainder / 5;            // 2 / 5 = 0 nickels
        int pennies = remainder % 5;            // 2 % 5 = 2 pennies

        System.out.println("Total Cents: " + totalCents);
        System.out.println("Quarters: " + quarters);
        System.out.println("Dimes: " + dimes);
        System.out.println("Nickels: " + nickels);
        System.out.println("Pennies: " + pennies);
    }
}

```

#### Program 2: Casting, Rounding & Precedence Lab

Demonstrates the exact difference between casting before vs. after division and how to round both positive and negative numbers.

```java
public class CastingAndRounding {
    public static void main(String[] args) {
        int pointsEarned = 43;
        int totalPoints = 50;

        // 1. Integer division bug vs. proper casting
        double wrongPercent = (pointsEarned / totalPoints) * 100;         // 0 * 100 = 0.0
        double exactPercent = ((double) pointsEarned / totalPoints) * 100; // 0.86 * 100 = 86.0

        // 2. Rounding positive and negative doubles
        double posTemp = 72.6;
        double negTemp = -4.6;

        int roundedPos = (int) (posTemp + 0.5); // (int)(73.1) = 73
        int roundedNeg = (int) (negTemp - 0.5); // (int)(-5.1) = -5

        System.out.println("Wrong Percent: " + wrongPercent + "%");
        System.out.println("Exact Percent: " + exactPercent + "%");
        System.out.println("Rounded Positive: " + roundedPos);
        System.out.println("Rounded Negative: " + roundedNeg);
    }
}

```

#### Program 3: Integer Overflow & String Concatenation Tracer

Demonstrates `Integer.MAX_VALUE` wraparound and left-to-right concatenation rules commonly tested on AP Multiple Choice Questions.

```java
public class OverflowAndOutput {
    public static void main(String[] args) {
        int max = Integer.MAX_VALUE;
        int overflowed = max + 1;

        System.out.println("Max int: " + max);               // 2147483647
        System.out.println("Max + 1: " + overflowed);        // -2147483648

        // Left-to-right evaluation trace
        System.out.println(4 + 5 + " is the sum");           // "9 is the sum"
        System.out.println("The sum is " + 4 + 5);           // "The sum is 45"
        System.out.println("The sum is " + (4 + 5));         // "The sum is 9"
    }
}

```



# Unit 2

In **AP Computer Science A**, **Unit 2: Using Objects** shifts from raw numbers to working with pre-built objects, calling methods, manipulating `String` objects, converting between primitives and wrapper classes (`Integer`, `Double`), and calling static methods in the `Math` class. Every concept below is strictly within the AP-CSA Java Subset.

---

### Key Takeaways for AP-CSA Unit 2

* **Objects are instances of classes created with the `new` keyword and a constructor (`ClassName obj = new ClassName(args);`), while reference variables store the memory address pointing to the object.**
* **`String` objects are immutable—methods like `substring()` and `toUpperCase()` never change the original `String`; they return a brand-new `String` object.**
* **`String` indices are zero-based (`0` to `length() - 1`), and `substring(from, to)` includes `from` but excludes `to` (returning `to - from` characters).**
* **Wrapper classes (`Integer` and `Double`) wrap primitive values inside objects so they can be used with object-only structures, using autoboxing and unboxing automatically.**
* **`Math.random()` returns a `double` in `[0.0, 1.0)` (including `0.0`, never reaching `1.0`); use `(int) (Math.random() * range) + min` to generate random integers.**

---

### 1. Objects, References & Method Calls

#### Analogy: The TV and the Remote Control

* **The Object (The TV):** Lives in Heap memory and contains the actual data and built-in capabilities.
* **The Reference Variable (The Remote Control):** Lives in Stack memory and holds the connection (memory address) to that specific TV.
* **`null` Reference:** A remote control that has not been paired with any TV yet. Pressing a button on an unpaired remote (`obj.doSomething()`) causes a **`NullPointerException`** at runtime.

#### Void vs. Non-Void Methods

* **`void` Methods:** Perform an action (like printing or modifying state) and return nothing. Called as a standalone statement: `turtle.moveForward();`.
* **Non-Void Methods:** Compute and return a value. Must be stored in a variable, printed, or used inside an expression: `int len = word.length();`.

---

### 2. The `String` Class (AP-CSA Subset Methods)

`String` objects are **immutable** (cannot be modified in place). You can create them using a String literal (`String s = "Java";`) or `new` (`String s = new String("Java");`).

#### Zero-Based Indexing & `substring` Visual Flow

```text
String str = "COMPUTER";
Index:        0   1   2   3   4   5   6   7     (str.length() == 8)
Characters: [ C | O | M | P | U | T | E | R ]

1. str.substring(3, 6)  --> Starts at index 3 ('P'), stops BEFORE index 6 ('E')
                        --> Length = 6 - 3 = 3 characters ---> "PUT"

2. str.substring(5)     --> Starts at index 5 ('T'), goes all the way to the end
                        --> Returns ---> "TER"

3. str.substring(8)     --> Valid! Returns empty String "" (no error)
4. str.substring(9)     --> Runtime Error: StringIndexOutOfBoundsException

```

#### Official AP-CSA `String` Methods Table

| Method Signature | Return Type | Behavior & AP-CSA Exam Rules | Example (`s = "APCSA"`) |
| --- | --- | --- | --- |
| `int length()` | `int` | Returns total number of characters (last valid index is `length() - 1`). | `s.length()` $\rightarrow$ `5` |
| `String substring(int from, int to)` | `String` | Returns substring from index `from` up to `to - 1`. | `s.substring(1, 4)` $\rightarrow$ `"PCS"` |
| `String substring(int from)` | `String` | Returns substring from index `from` through the end of the String. | `s.substring(2)` $\rightarrow$ `"CSA"` |
| `int indexOf(String str)` | `int` | Returns index of **first** occurrence of `str`, or **`-1`** if not found. | `s.indexOf("CS")` $\rightarrow$ `2`<br>

<br>`s.indexOf("Z")` $\rightarrow$ `-1` |
| `boolean equals(String other)` | `boolean` | Returns `true` if both Strings have identical characters (case-sensitive). | `s.equals("APCSA")` $\rightarrow$ `true` |
| `int compareTo(String other)` | `int` | Alphabetical/lexicographical comparison: returns `< 0` if `s` comes before `other`, `0` if equal, `> 0` if `s` comes after `other`. | `"Apple".compareTo("Banana")` $\rightarrow$ `< 0` |

*(Note: Methods like `charAt()`, `replace()`, `toLowerCase()`, and `trim()` are NOT on the AP-CSA Java Subset—always use `substring(i, i + 1)` to extract a single character!)*

---

### 3. Wrapper Classes: `Integer` and `Double`

Wrapper classes convert primitive `int` and `double` values into objects (required later in Unit 7 for `ArrayList`).

#### Autoboxing vs. Unboxing Flow

```text
AUTOBOXING (Primitive ---> Wrapper Object automatically)
  int num = 42;
  Integer obj = num;          // Java automatically wraps 42 into an Integer object

UNBOXING (Wrapper Object ---> Primitive automatically)
  Integer obj = new Integer(42);
  int val = obj + 8;          // Java automatically unwraps obj to 42, then adds 8

```

#### AP-CSA Wrapper Constants & Methods

* `Integer.MIN_VALUE` (`-2147483648`) and `Integer.MAX_VALUE` (`2147483647`)
* `int intValue()` — returns the `int` inside an `Integer` object
* `double doubleValue()` — returns the `double` inside a `Double` object

---

### 4. The `Math` Class (Static Methods)

All `Math` methods are **`static`**, meaning you call them using the class name `Math.` without creating an object.

| Method Signature | Return Type | Behavior | Example |
| --- | --- | --- | --- |
| `Math.abs(int x)` | `int` | Absolute value of an `int`. | `Math.abs(-7)` $\rightarrow$ `7` |
| `Math.abs(double x)` | `double` | Absolute value of a `double`. | `Math.abs(-4.5)` $\rightarrow$ `4.5` |
| `Math.pow(double base, double exp)` | `double` | Returns `base` raised to `exp` power. | `Math.pow(2, 3)` $\rightarrow$ `8.0` |
| `Math.sqrt(double x)` | `double` | Returns positive square root of `x` (`NaN` if `x < 0`). | `Math.sqrt(16)` $\rightarrow$ `4.0` |
| `Math.random()` | `double` | Returns a random `double` in `[0.0, 1.0)`. | `0.0 <= Math.random() < 1.0` |

#### `Math.random()` Scaling Formula (High-Frequency Exam Topic)

To generate a random integer between `min` and `max` (**inclusive**):

$$\text{int rand} = (\text{int})(\text{Math.random()} \times (\text{max} - \text{min} + 1)) + \text{min};$$

```text
Example: Random integer from 5 to 12 (inclusive)
  1. Number of possible outcomes (range) = 12 - 5 + 1 = 8
  2. Math.random() * 8                   --> [0.0, 8.0)
  3. (int) (Math.random() * 8)           --> 0, 1, 2, 3, 4, 5, 6, or 7
  4. + 5 (shift by min)                  --> 5, 6, 7, 8, 9, 10, 11, or 12

```

---

### Practice Programs to Solidify Unit 2

#### Program 1: `String` Slicer & Word Swapper

Demonstrates `indexOf()`, `substring(from, to)`, `substring(from)`, and `length()` without using out-of-scope methods.

```java
public class StringSlicer {
    public static void main(String[] args) {
        String fullName = "Grace Hopper";

        // 1. Find the location of the space separating first and last name
        int spaceIndex = fullName.indexOf(" "); // 5

        // 2. Extract first and last names using substring
        String firstName = fullName.substring(0, spaceIndex);   // "Grace"
        String lastName = fullName.substring(spaceIndex + 1);   // "Hopper"

        // 3. Extract initials using substring(i, i + 1) (AP-CSA way instead of charAt)
        String initials = firstName.substring(0, 1) + "." + lastName.substring(0, 1) + ".";

        // 4. Remove the first occurrence of "p" from lastName
        int pIndex = lastName.indexOf("p"); // 2
        String withoutFirstP = lastName.substring(0, pIndex) + lastName.substring(pIndex + 1);

        System.out.println("Formatted: " + lastName + ", " + firstName); // Hopper, Grace
        System.out.println("Initials: " + initials);                     // G.H.
        System.out.println("Without first 'p': " + withoutFirstP);       // Hoper
    }
}

```

#### Program 2: Random Dice & Range Simulator (`Math.random()`)

Demonstrates generating random integers within specific ranges and calculating Euclidean distance with `Math.pow()` and `Math.sqrt()`.

```java
public class MathSimulator {
    public static void main(String[] args) {
        // 1. Roll a standard 6-sided die (1 to 6 inclusive)
        // range = 6 - 1 + 1 = 6; min = 1
        int die1 = (int) (Math.random() * 6) + 1;
        int die2 = (int) (Math.random() * 6) + 1;

        // 2. Generate a random temperature between -10 and 35 (inclusive)
        // range = 35 - (-10) + 1 = 46; min = -10
        int randomTemp = (int) (Math.random() * 46) - 10;

        // 3. Calculate distance between two points (x1, y1) and (x2, y2)
        int x1 = 2, y1 = 3;
        int x2 = 5, y2 = 7;
        double distance = Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));

        System.out.println("Dice Roll: " + die1 + " and " + die2 + " (Total: " + (die1 + die2) + ")");
        System.out.println("Random Temp (-10 to 35): " + randomTemp);
        System.out.println("Distance between points: " + distance); // 5.0
    }
}

```

#### Program 3: String Immutability & Wrapper Class Lab

Demonstrates why calling a `String` method without reassigning leaves the original `String` unchanged, and how `Integer`/`Double` autoboxing works.

```java
public class ImmutabilityAndWrappers {
    public static void main(String[] args) {
        // 1. String Immutability Trap
        String word = "Computer";
        word.substring(0, 4); // Return value "Comp" is discarded! 'word' is unchanged.
        System.out.println("After ignored substring: " + word); // Still "Computer"

        word = word.substring(0, 4); // Reassigning updates the reference
        System.out.println("After reassigned substring: " + word); // "Comp"

        // 2. Wrapper Classes & Autoboxing/Unboxing
        Integer boxedScore = 95;                // Autoboxing int -> Integer
        Double boxedBonus = new Double(4.5);    // Explicit Double object creation

        // Automatic unboxing during arithmetic
        double finalGrade = boxedScore + boxedBonus; // 99.5

        System.out.println("Final Grade: " + finalGrade);
        System.out.println("compareTo test: " + "Cat".compareTo("Dog")); // Negative (< 0)
    }
}

```
# Unit 3
In **AP Computer Science A**, **Unit 3: Boolean Expressions and `if` Statements** introduces decision-making in Java. It covers how programs compare values, combine boolean conditions, trace multi-branch selection statements, apply De Morgan's Laws, and compare object references versus object contents. Every concept below is strictly within the official AP-CSA Java Subset.

---

### Key Takeaways for AP-CSA Unit 3

* **Relational operators (`==`, `!=`, `<`, `<=`, `>`, `>=`) compare primitive values and always evaluate to a `boolean` (`true` or `false`).**
* **Logical operators follow strict precedence: `!` (NOT) runs first, `&&` (AND) runs second, and `||` (OR) runs third.**
* **Short-circuit evaluation stops evaluating `&&` as soon as the left side is `false`, and stops evaluating `||` as soon as the left side is `true`.**
* **De Morgan's Laws distribute `!` across parentheses by flipping `&&` to `||` (and vice versa) and negating every relational operator.**
* **Never use `==` to compare `String` or object content—`==` checks if two references point to the exact same memory address (aliasing), whereas `.equals()` checks if their actual contents match.**

---

### 1. Relational & Logical Operators

#### Relational Operators (For Primitives)

* `==` (equal to — **do not confuse with `=` assignment**)
* `!=` (not equal to)
* `<` (less than), `<=` (less than or equal to)
* `>` (greater than), `>=` (greater than or equal to)

#### Logical Operators & Precedence

1. **`!` (Logical NOT):** Flips `true` to `false` and `false` to `true`.
2. **`&&` (Logical AND):** Evaluates to `true` **only if BOTH** sides are `true`.
3. **`||` (Logical OR):** Evaluates to `true` if **AT LEAST ONE** side is `true`.

#### Analogy: Airport Security Checkpoints

* **`&&` (AND):** Getting onto an international flight requires **both** a valid boarding pass **and** a valid passport. If your boarding pass fails at the first scanner, the agent stops immediately without checking your passport (**short-circuiting**).
* **`||` (OR):** Entering an airport lounge requires **either** a first-class ticket **or** an annual lounge membership. If your first-class ticket scans valid, the attendant waves you right in without asking to see a membership card (**short-circuiting**).

---

### 2. Selection Statements (`if`, `if-else`, `if-else if-else`)

#### Execution Flow: Multi-Branch `if-else if-else` vs. Sequential `if` Statements

```text
MULTI-BRANCH (Mutually Exclusive - At most ONE block runs)
  if (score >= 90)      ---> True ---> [ Print "A" ] ---+
       | False                                          |
  else if (score >= 80) ---> True ---> [ Print "B" ] ---+---> [ Exit Chain ]
       | False                                          |
  else                  -------------> [ Print "C" ] ---+

SEQUENTIAL 'if's (Independent - MULTIPLE blocks can run)
  if (score >= 90)      ---> True ---> [ Print "A" ] ---+
       |                                                |
       v                                                |
  if (score >= 80)      ---> True ---> [ Print "B" ] <--+ (Runs BOTH "A" and "B" if score is 95!)

```

#### Dangling `else` Rule (AP-CSA MCQ Trap)

In Java, indentation is ignored by the compiler. An `else` clause **always pairs with the nearest unmatched `if**` above it unless curly braces `{}` specify otherwise:

```java
// Indentation is misleading here!
if (x > 0)
    if (y > 0)
        System.out.println("Both positive");
else
    System.out.println("Which 'if' does this belong to?"); // Pairs with (y > 0), NOT (x > 0)!

```

---

### 3. De Morgan's Laws & Equivalent Boolean Expressions

De Morgan's Laws are heavily tested on AP-CSA Multiple Choice Questions to simplify or rewrite negated boolean expressions.

#### Transformation Rules

| Original Negated Expression | Equivalent Expanded Expression |
| --- | --- |
| `!(A && B)` | `!A || !B` |
| `!(A || B)` | `!A && !B` |
| `!(x < 5)` | `x >= 5` *(notice `<` flips to `>=`, not `>`)* |
| `!(x >= 10)` | `x < 10` *(notice `>=` flips to `<`, not `<=`)* |
| `!(x == 0 || y != 3)` | `x != 0 && y == 3` |

---

### 4. Comparing Objects: `==` vs. `.equals()` & Aliasing

#### Memory Reference Diagram (Aliasing vs. Separate Objects)

```text
Stack Memory                      Heap Memory
+------------------+              +-----------------------+
| s1: [0x100A] ----+------------->| String: "Java"        | (Address 0x100A)
| s2: [0x100A] ----+------^       +-----------------------+
|                  |              +-----------------------+
| s3: [0x200B] ----+------------->| String: "Java"        | (Address 0x200B)
+------------------+              +-----------------------+

1. s1 == s2       --> TRUE  (Aliases: both point to 0x100A)
2. s1 == s3       --> FALSE (Different memory addresses: 0x100A vs 0x200B)
3. s1.equals(s3)  --> TRUE  (Identical text content: "Java")

```

* **Aliasing:** When two reference variables store the exact same memory address (`String s2 = s1;`), they are **aliases** for the same object.
* **`null` Guard Pattern:** Always check `str != null` on the left side of `&&` before calling `str.equals(...)` so short-circuiting prevents a `NullPointerException`.

---

### Practice Programs to Solidify Unit 3

#### Program 1: Leap Year & Valid Date Checker (Compound Boolean Logic)

Demonstrates nested conditions, precedence between `&&` and `||`, and clean boolean returns.

```java
public class LeapYearChecker {
    public static void main(String[] args) {
        int year = 2024;

        // A year is a leap year if:
        // (divisible by 4 AND not divisible by 100) OR (divisible by 400)
        boolean isLeapYear = (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);

        if (isLeapYear) {
            System.out.println(year + " is a leap year (366 days).");
        } else {
            System.out.println(year + " is a common year (365 days).");
        }
    }
}

```

#### Program 2: Short-Circuit Guard & Safe String Comparison

Demonstrates preventing runtime crashes (`ArithmeticException` and `NullPointerException`) using short-circuit evaluation and `.equals()`.

```java
public class SafeComparisons {
    public static void main(String[] args) {
        // 1. Short-circuit division guard
        int totalPoints = 450;
        int gamesPlayed = 0;

        if (gamesPlayed > 0 && (double) totalPoints / gamesPlayed >= 50.0) {
            System.out.println("High scoring average!");
        } else {
            // Safely reaches here without dividing by zero because (gamesPlayed > 0) is false
            System.out.println("Not enough games played to qualify.");
        }

        // 2. Object reference (==) vs. content (.equals) and null guard
        String targetCode = "APCSA2026";
        String userCode = new String("APCSA2026");
        String emptyInput = null;

        System.out.println("Using == : " + (targetCode == userCode));         // false
        System.out.println("Using .equals() : " + targetCode.equals(userCode)); // true

        // Safe null check using short-circuit &&
        if (emptyInput != null && emptyInput.equals(targetCode)) {
            System.out.println("Access Granted");
        } else {
            System.out.println("Invalid or null input.");
        }
    }
}

```

#### Program 3: Shipping Cost & Discount Tier Calculator (`if-else if-else` & De Morgan's)

Demonstrates mutually exclusive selection chains and applying De Morgan's Law for eligibility validation.

```java
public class ShippingCalculator {
    public static void main(String[] args) {
        double orderTotal = 65.00;
        boolean isMember = false;
        boolean isRestrictedItem = false;

        // De Morgan's Law in action:
        // Eligible for express shipping if NOT (order under $25 AND not a member) AND NOT restricted
        // Equivalent to: (orderTotal >= 25.0 || isMember) && !isRestrictedItem
        if (!(orderTotal < 25.0 && !isMember) && !isRestrictedItem) {
            double shippingFee;

            if (isMember || orderTotal >= 100.0) {
                shippingFee = 0.0;
            } else if (orderTotal >= 50.0) {
                shippingFee = 4.99;
            } else {
                shippingFee = 8.99;
            }

            System.out.println("Express Shipping Fee: $" + shippingFee);
        } else {
            System.out.println("Order does not qualify for express shipping.");
        }
    }
}

```
# Unit 4
In **AP Computer Science A**, **Unit 4: Iteration** covers repeating blocks of code using `while` loops, `for` loops, and nested loops. It also tests standard string and number algorithms alongside runtime execution tracing. Every topic below is strictly within the official AP-CSA Java Subset.

---

### Key Takeaways for AP-CSA Unit 4

* **A `while` loop is best for indefinite iteration (when you do not know how many times the loop will run in advance), whereas a `for` loop is best for definite iteration (counting or traversing a known length).**
* **Off-by-one errors happen when loop boundaries use `<` instead of `<=` (or vice versa), causing the loop to run one time too many or one time too few.**
* **To traverse every character in a `String str` without causing a `StringIndexOutOfBoundsException`, loop from `i = 0` to `i < str.length()` and extract single characters with `str.substring(i, i + 1)`.**
* **In nested loops, the inner loop completes all of its iterations for *every single iteration* of the outer loop (`total executions = outer iterations × inner iterations`).**
* **Infinite loops occur when the boolean condition never evaluates to `false`, usually because the loop control variable is not updated or updates in the wrong direction.**

---

### 1. `while` Loops & Standard Numeric Algorithms

A `while` loop evaluates its boolean condition **before** executing the loop body. If the condition is initially `false`, the body runs **0 times**.

#### Analogy: Climbing a Staircase in the Dark

* **`while` Loop (Feeling for the Next Step):** You do not know how many stairs exist. Before each step, you check if there is another stair (`hasNextStep()`). You keep stepping until your foot hits flat ground.
* **`for` Loop (Climbing a 10-Step Ladder):** You know in advance there are exactly 10 rungs. You start at rung `1`, climb while `rung <= 10`, and move up by `1` rung each time.

#### Execution Flow: `while` Loop vs. `for` Loop

```text
WHILE LOOP FLOW                         FOR LOOP FLOW
  [ Initialization ]                      [ 1. Initialization (runs ONCE) ]
          |                                               |
          v                                               v
  +-> ( Condition? ) -- False --> [ Exit ]   +---> ( 2. Condition? ) -- False --> [ Exit ]
  |       |                                  |            |
  |      True                                |           True
  |       |                                  |            |
  |       v                                  |            v
  |   [ Loop Body ]                          |     [ 3. Loop Body ]
  |   [ Update Variable ]                    |            |
  +-------+                                  |            v
                                             |     [ 4. Update Step ]
                                             +------------+

```

#### High-Frequency Numeric Loop Patterns

* **Extracting Digits from an `int n`:**
Use `n % 10` to grab the rightmost digit, and `n /= 10` to chop it off until `n == 0`.
* **Divisibility & Prime Checks:**
Use `num % divisor == 0` to test whether `divisor` divides evenly into `num`.

---

### 2. `for` Loops & `String` Traversal Algorithms

A `for` loop packs initialization, condition, and update into one header:

```java
for (int i = 0; i < str.length(); i++) {
    String letter = str.substring(i, i + 1);
}

```

#### `String` Traversal & Reversal Diagram

```text
String word = "JAVA";    (word.length() == 4)
Indices:       0   1   2   3
Characters:  [ J | A | V | A ]

Forward Traversal:  for (int i = 0; i < word.length(); i++)
  i = 0 --> word.substring(0, 1) --> "J"
  i = 1 --> word.substring(1, 2) --> "A"
  i = 2 --> word.substring(2, 3) --> "V"
  i = 3 --> word.substring(3, 4) --> "A"
  i = 4 --> (4 < 4) is FALSE ------> Loop Terminates Safely

Backward Traversal: for (int i = word.length() - 1; i >= 0; i--)
  Starts at index 3 ("A"), steps down to index 0 ("J"), stops at i = -1.

```

#### Common `String` Loop Traps on AP-CSA

* **Trap 1 — `i <= str.length()` with `substring(i, i + 1)`:** On the final iteration when `i == str.length()`, `i + 1` exceeds the string's length and crashes with `StringIndexOutOfBoundsException`.
* **Trap 2 — Checking Multi-Character Substrings:** If scanning for a 2-letter pattern like `"hi"` using `str.substring(i, i + 2)`, your loop condition **must** stop early: `i < str.length() - 1` (or `i <= str.length() - 2`).

---

### 3. Nested Iteration & Execution Counts

When one loop is placed inside another, the inner loop resets from its starting value on every pass of the outer loop.

#### Trace Table Example: Dependent Nested Loops

```java
for (int row = 1; row <= 3; row++) {
    for (int col = 1; col <= row; col++) {
        System.out.print("*");
    }
    System.out.println();
}

```

| Outer `row` | Inner `col` values executed | Inner Loop Runs | Printed Line |
| --- | --- | --- | --- |
| `1` | `1` | `1` time | `*` |
| `2` | `1, 2` | `2` times | `**` |
| `3` | `1, 2, 3` | `3` times | `***` |
| **Total** |  | **`1 + 2 + 3 = 6` stars** |  |

---

### Practice Programs to Solidify Unit 4

#### Program 1: Digit Analyzer (`while` Loop Digit Extraction)

Counts how many digits are in a positive integer and sums its even digits using `% 10` and `/ 10`.

```java
public class DigitAnalyzer {
    public static void main(String[] args) {
        int num = 48275;
        int temp = num; // Keep a copy so original 'num' isn't destroyed
        int digitCount = 0;
        int evenSum = 0;

        while (temp > 0) {
            int lastDigit = temp % 10; // Extract rightmost digit
            digitCount++;

            if (lastDigit % 2 == 0) {
                evenSum += lastDigit;
            }

            temp /= 10; // Chop off rightmost digit
        }

        System.out.println("Original Number: " + num);
        System.out.println("Total Digits: " + digitCount);   // 5
        System.out.println("Sum of Even Digits: " + evenSum); // 4 + 8 + 2 = 14
    }
}

```

#### Program 2: Substring Counter & Palindrome Checker (`for` Loop `String` Algorithms)

Demonstrates counting multi-character matches safely without out-of-bounds errors and reversing a `String` using a `String` accumulator.

```java
public class StringAlgorithms {
    public static void main(String[] args) {
        // 1. Count occurrences of "ab" without going out of bounds
        String text = "abracadabra";
        int abCount = 0;

        // Stop at length() - 1 because substring(i, i + 2) grabs 2 characters
        for (int i = 0; i < text.length() - 1; i++) {
            if (text.substring(i, i + 2).equals("ab")) {
                abCount++;
            }
        }
        System.out.println("Occurrences of \"ab\": " + abCount); // 2

        // 2. Reverse a String and check if it is a palindrome
        String word = "racecar";
        String reversed = ""; // String accumulator starts empty

        for (int i = word.length() - 1; i >= 0; i--) {
            reversed += word.substring(i, i + 1);
        }

        boolean isPalindrome = word.equals(reversed);
        System.out.println("Reversed: " + reversed);
        System.out.println("Is Palindrome: " + isPalindrome); // true
    }
}

```

#### Program 3: Multiplication Grid & Vowel Stripper (Nested Loops & Filtering)

Demonstrates rectangular nested iteration and removing vowels from a phrase using only AP-CSA `String` methods.

```java
public class NestedAndFilter {
    public static void main(String[] args) {
        // 1. Nested loop 4x4 multiplication table
        for (int r = 1; r <= 4; r++) {
            for (int c = 1; c <= 4; c++) {
                System.out.print((r * c) + "\t");
            }
            System.out.println();
        }

        // 2. Remove all lowercase vowels using indexOf()
        String phrase = "computer science";
        String vowels = "aeiou";
        String result = "";

        for (int i = 0; i < phrase.length(); i++) {
            String currentChar = phrase.substring(i, i + 1);
            // If currentChar is NOT found in "aeiou", indexOf returns -1
            if (vowels.indexOf(currentChar) == -1) {
                result += currentChar;
            }
        }

        System.out.println("Without vowels: " + result); // "cmptr scnc"
    }
}

```
# Unit 5
In **AP Computer Science A**, **Unit 5: Writing Classes** teaches you how to design your own custom blueprints (classes), protect data using encapsulation, overload constructors and methods, distinguish between `static` (class-level) and non-static (instance-level) members, and trace variable scope and parameter passing. Every topic below is strictly within the official AP-CSA Java Subset.

---

### Key Takeaways for AP-CSA Unit 5

* **Encapsulation requires declaring all instance variables `private` and providing `public` constructors, accessor (getter) methods, and mutator (setter) methods.**
* **Overloaded constructors and methods share the same name within a class but must have different parameter lists (different count, types, or order of parameters).**
* **Pass-by-value means Java copies primitive values into parameters (changes inside the method do not affect the caller's variable), whereas for object references, Java copies the memory address (mutating the object inside the method *does* change the original object).**
* **`static` variables and methods belong to the class itself rather than any individual object; `static` methods cannot access instance variables or use the `this` keyword.**
* **The `this` keyword refers to the current object executing the method or constructor, commonly used to resolve variable shadowing between parameters and instance variables.**

---

### 1. Anatomy of a Class & Encapsulation

#### Analogy: A Vending Machine

* **`private` Instance Variables (The Internal Inventory & Cash Box):** Locked behind steel glass so customers cannot reach in and grab snacks or alter inventory counts directly.
* **`public` Constructor (Stocking & Powering On):** Initializes the machine with its starting snack count and item price when installed.
* **`public` Accessor / Getter Methods (The Digital Display):** Lets customers view the item price or remaining stock without changing anything.
* **`public` Mutator / Setter Methods (The Coin Slot & Keypad):** Controlled entry points that validate money inserted before dispensing an item and decrementing stock.

#### Class Structure & Scope Diagram

```text
+-----------------------------------------------------------------------+
| public class BankAccount                                              |
|                                                                       |
|   [ PRIVATE INSTANCE VARIABLES ]  <-- Scope: Entire class             |
|     private String owner;                                             |
|     private double balance;                                           |
|                                                                       |
|   [ PUBLIC OVERLOADED CONSTRUCTORS ]                                  |
|     public BankAccount(String owner, double balance) {                |
|         this.owner = owner;     // 'this.owner' = instance variable   |
|         this.balance = balance; // 'owner' = local parameter          |
|     }                                                                 |
|     public BankAccount(String owner) {                                |
|         this(owner, 0.0);       // Calls 2-argument constructor       |
|     }                                                                 |
|                                                                       |
|   [ PUBLIC ACCESSORS (Getters) & MUTATORS (Setters) ]                 |
|     public double getBalance() { return balance; }                    |
|     public void deposit(double amount) { ... }                        |
+-----------------------------------------------------------------------+

```

---

### 2. Constructors, Overloading & `this` Keyword

* **Constructor Rules:**
* Must have the **exact same name** as the class.
* Has **no return type** (not even `void`).
* **Default Constructor:** If you write *zero* constructors, Java inserts a no-argument constructor automatically. As soon as you write *any* custom constructor, Java removes the automatic default constructor.


* **Method & Constructor Overloading:** Two methods or constructors in the same class can share a name **only if their parameter lists differ** in number, data types, or order. Changing only the return type causes a compile-time error.
* **`this` Keyword:**
* Resolves **shadowing** when a local parameter has the exact same name as an instance variable (`this.balance = balance;`).
* Can pass the current object as an argument to another method (`otherObject.compareWith(this);`).



---

### 3. Pass-by-Value: Primitives vs. Object References

Java is **strictly pass-by-value**. When you call a method, Java copies the contents of the argument box into the parameter box.

```text
1. PASSING A PRIMITIVE (int x = 10)
   Caller's 'x' box: [ 10 ]  ---(copies 10)--->  Parameter 'n' box: [ 10 ]
   If method does n = 99;, 'n' becomes [ 99 ], but caller's 'x' stays [ 10 ]!

2. PASSING AN OBJECT REFERENCE (Student s = new Student("Maya", 90))
   Caller's 's' box: [ 0x3F8 ] --(copies 0x3F8)--> Parameter 'stu' box: [ 0x3F8 ]
                         |                                                 |
                         +-----------------> [ Heap: Student ] <-----------+
                                             [ name: "Maya"  ]
                                             [ grade: 90     ]
   If method calls stu.setGrade(98);, BOTH 's' and 'stu' point to 0x3F8,
   so caller's 's' sees grade = 98!
   HOWEVER, if method does stu = new Student("Leo", 70);, 'stu' points to a new
   address, while caller's 's' STILL points to Maya at 0x3F8!

```

---

### 4. `static` Variables and Methods (Class-Level Members)

| Feature | Instance Members (Non-`static`) | Class Members (`static`) |
| --- | --- | --- |
| **Memory Allocation** | Each object gets its own separate copy. | **One single shared copy** belongs to the class itself. |
| **How to Call** | Called on an object reference (`acc1.deposit(50)`). | Called using the class name (`Ticket.getTotalSold()`). |
| **Access Rules** | Can access both instance variables and `static` variables. | Can **only** access `static` variables/methods; **cannot** access `private` instance variables or `this`. |
| **Common AP-CSA Use** | Object state (`name`, `balance`, `x`, `y`). | Shared counters (`nextId`, `totalObjectsCreated`) or utility methods (`Math.sqrt()`). |

---

### 5. Variable Scope & `toString()`

* **Instance Variables:** Declared inside the class outside all methods; accessible anywhere inside the class for the lifetime of the object.
* **Local Variables & Parameters:** Declared inside a constructor, method, or loop header; exist **only** inside that `{ ... }` block and vanish when the block ends.
* **The `toString()` Method:** Defining `public String toString()` returns a formatted `String` description of an object. Java calls `toString()` automatically whenever an object is passed into `System.out.println(obj)` or concatenated with a `String` (`"Info: " + obj`).

---

### Practice Programs to Solidify Unit 5

#### Program 1: `Ticket` Class (Encapsulation, Overloading, `static` Counter & `toString`)

Demonstrates a complete AP-CSA FRQ-style class with a `static` counter tracking total tickets issued across all objects.

```java
public class Ticket {
    // Private instance variables (each Ticket object gets its own copy)
    private int serialNumber;
    private String eventName;
    private double price;

    // Static variable (shared across ALL Ticket objects)
    private static int totalTicketsSold = 0;

    // Constructor 1: Full parameters
    public Ticket(String eventName, double price) {
        totalTicketsSold++;
        this.serialNumber = totalTicketsSold; // Assigns unique ID: 1, 2, 3...
        this.eventName = eventName;
        this.price = price;
    }

    // Constructor 2: Overloaded constructor for free admission events
    public Ticket(String eventName) {
        totalTicketsSold++;
        this.serialNumber = totalTicketsSold;
        this.eventName = eventName;
        this.price = 0.0;
    }

    // Accessor (Getter) methods
    public double getPrice() {
        return price;
    }

    public int getSerialNumber() {
        return serialNumber;
    }

    // Static accessor method (can only access static variables)
    public static int getTotalTicketsSold() {
        return totalTicketsSold;
    }

    // Mutator (Setter) method with validation
    public void applyDiscount(double percent) {
        if (percent > 0 && percent <= 100) {
            price = price * (1 - percent / 100.0);
        }
    }

    // Automatically called when printing a Ticket object
    public String toString() {
        return "Ticket #" + serialNumber + " [" + eventName + "] - $" + price;
    }
}

```

#### Program 2: `TicketTester` (Testing `static` Calls & Pass-by-Value Mechanics)

Shows how primitives behave differently from object references when passed into helper methods.

```java
public class TicketTester {
    // Helper method demonstrating pass-by-value on primitives vs. objects
    public static void tryToModify(int num, Ticket t) {
        num = 999;              // Modifies local copy only; caller's int is unchanged
        t.applyDiscount(50.0);  // Mutates the actual Ticket object in Heap memory!
        t = new Ticket("Fake", 10.0); // Reassigns local reference copy only; caller unaffected
    }

    public static void main(String[] args) {
        // Before creating any objects, static count is 0
        System.out.println("Tickets sold initially: " + Ticket.getTotalTicketsSold());

        Ticket t1 = new Ticket("Robotics Finals", 40.0);
        Ticket t2 = new Ticket("Science Fair"); // Calls overloaded 1-arg constructor

        int primitiveValue = 10;
        tryToModify(primitiveValue, t1);

        System.out.println("primitiveValue after method: " + primitiveValue); // Still 10!
        System.out.println(t1); // Automatically calls t1.toString() -> Price is now $20.0!
        System.out.println(t2); // Ticket #2 [Science Fair] - $0.0
        System.out.println("Total tickets sold: " + Ticket.getTotalTicketsSold()); // 2
    }
}

```

Please share detailed notes for Unit 1 in AP CSA. Give some programs as well along with the notes, to solidify the learning.
# Ancilliary


In **AP Computer Science A (Unit 4: Iteration)**, terms like **Sentinel**, **Accumulator**, **Counter**, and **Priming Read** are standard vocabulary used to describe common loop design patterns. Knowing these terms makes reading AP Multiple Choice Questions and designing Free Response Question (FRQ) solutions much easier.

---

### Key Takeaways for AP-CSA Loop Vocabulary

* **A Sentinel Value is a special input value (like `-1` or `0`) chosen to signal the end of input and terminate a `while` loop.**
* **An Accumulator is a variable (like `sum` or `total`) initialized before a loop that builds up a combined result across iterations.**
* **A Counter is a variable (like `count`) that increments by `1` each time a loop runs or a specific condition is met.**
* **A Priming Read is the initial input read placed *before* the `while` loop so the condition has a value to test on the very first check.**
* **An Infinite Loop occurs when the loop condition never becomes `false`, usually because the loop control variable is never updated inside the loop.**

---

### Core Concept Breakdown & Analogies

#### 1. Sentinel Value (The Stop Sign)

* **Definition:** A specific marker value that cannot be mistaken for normal data. When the loop detects this value, it stops immediately without processing the sentinel itself into the result.
* **Analogy:** The **"End of Aisle / Next Customer" plastic bar** at a grocery checkout. Items are groceries; the plastic bar is the sentinel telling the cashier to stop scanning.

#### 2. Accumulator (The Snowball / Piggy Bank)

* **Definition:** A variable initialized to a neutral starting value (`0` for addition, `1` for multiplication, `""` for String concatenation) before a loop, which adds or combines new values during every iteration.
* **Analogy:** A **piggy bank**. Every time you get allowance (each loop iteration), you drop the new money inside, and the total amount inside grows (`total += amount`).

#### 3. Counter (The Clicker)

* **Definition:** A specialized accumulator that tracks *how many times* something happens by adding `1` (`count++`).
* **Analogy:** A **security guard's handheld clicker** at a concert entrance. Every time a person walks through the gate, the guard clicks it once (`count++`) regardless of who the person is.

#### 4. Priming Read & Update Read (The Loop Bookends)

* **Definition:** In a sentinel loop, you must read the first piece of data **before** the `while` header (**Priming Read**) and read the next piece of data at the **very bottom** inside the loop (**Update Read**).
* **Analogy:** Checking your fuel gauge **before** starting a road trip (Priming Read), and checking it again **at the end of each highway exit** (Update Read).

---

### ASCII Flow: How All 4 Roles Work Together

```text
int sum = 0;      <--- [ ACCUMULATOR ] (Starts at 0)
int count = 0;    <--- [ COUNTER ]     (Starts at 0)
int num = input;  <--- [ PRIMING READ ] (Gets 1st value before loop)

       +---------------------------------------+
       v                                       |
( num != -1 ? )   <--- [ SENTINEL CHECK ]      | (-1 is the Sentinel)
   |       |                                   |
 False    True                                 |
   |       |                                   |
   |       v                                   |
   |   [ sum += num; ]   (Updates Accumulator) |
   |   [ count++; ]      (Updates Counter)     |
   |   [ num = input; ]  <--- [ UPDATE READ ] -+ (Gets next value)
   |
   v
[ Print sum and count ]

```

---

### Complete AP-CSA Java Example

This example combines all four concepts to calculate the average of test scores entered by a user until `-1` (the sentinel) is entered:

```java
import java.util.Scanner;

public class TestAverage {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        // 1. ACCUMULATOR & COUNTER initialization
        int sum = 0;
        int count = 0;

        // 2. PRIMING READ (before the loop starts)
        System.out.print("Enter a test score (-1 to quit): ");
        int score = input.nextInt();

        // 3. SENTINEL-CONTROLLED LOOP (-1 is the sentinel value)
        while (score != -1) {
            sum += score;   // Accumulator adds the score
            count++;        // Counter tracks how many scores were entered

            // 4. UPDATE READ (at the bottom of the loop)
            System.out.print("Enter a test score (-1 to quit): ");
            score = input.nextInt();
        }

        // Guard against division by zero if user entered -1 immediately
        if (count > 0) {
            double average = (double) sum / count; // Casting for AP-CSA accuracy
            System.out.println("Scores entered: " + count);
            System.out.println("Average score: " + average);
        } else {
            System.out.println("No scores were entered.");
        }

        input.close();
    }
}

```

---

### Summary Table for AP-CSA

| Term | Typical Variable Name | Starting Value | Inside Loop Action | AP-CSA Exam Purpose |
| --- | --- | --- | --- | --- |
| **Sentinel** | `SENTINEL` or literal `-1`, `0` | N/A (Checked in condition) | Tested in `while (val != -1)` | Terminates indefinite input loops cleanly |
| **Accumulator** | `sum`, `total`, `result` | `0` (or `""` for Strings) | `sum += val;` | Computes sums, products, or combined Strings |
| **Counter** | `count`, `numItems` | `0` | `count++;` | Counts iterations or matching elements |
| **Loop Control Variable** | `i`, `num`, `index` | Initial input or `0` | `i++` or `num = nextInput` | Prevents infinite loops by progressing toward exit |

