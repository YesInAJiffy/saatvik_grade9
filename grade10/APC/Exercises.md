# Unit 4 Practice problems

Your program is a **Sentinel-Controlled `while` Loop** (AP-CSA Unit 4: Iteration) designed to read integers and accumulate their sum until `0` is entered. It has **3 compile-time syntax errors** caused by capitalization and variable naming typos, though its loop logic is solid.


```java
// Import the Scanner class from the java.util package to read console input
import java.util.Scanner;

public class Program1 {
    public static void main(String[] args) {
        // Instantiate a Scanner object named 'keyboard' connected to standard input (System.in)
        Scanner keyboard = new Scanner(System.in);

        // PRIMING READ: Prompt and read the first integer BEFORE the loop starts
        // so the while-loop condition has an initial value to evaluate
        System.out.print("Enter a number or 0 to quit: ");
        int number = keyboard.nextInt();

        // ACCUMULATOR: Initialize 'sum' to 0 before the loop to store the running total
        int sum = 0;

        // SENTINEL-CONTROLLED LOOP: Continue looping as long as 'number' is not the sentinel value (0)
        // If the user enters 0 on the priming read, this loop body executes 0 times
        while (number != 0) {
            // Update the accumulator by adding the current valid input to 'sum'
            sum += number;

            // UPDATE READ: Read the next integer at the bottom of the loop
            // Updates the loop control variable ('number') to prevent an infinite loop
            System.out.print("Enter a number or 0 to quit: ");
            number = keyboard.nextInt();
        }

        // Loop terminates once 'number == 0'; print the final accumulated total (excluding 0)
        System.out.println("Sum: " + sum);

        // Close the Scanner resource to prevent memory/resource leaks
        keyboard.close();
    }
}

```

## Two

Your program is a **Number Guessing Game** combining **AP-CSA Unit 2 (`Math.random()`)**, **Unit 3 (`if-else if-else` selection)**, and **Unit 4 (`while` loops and counters)**. It currently has **12 compile-time and logic errors** that prevent it from compiling or running properly.


```java
// Import the Scanner class to read user guesses from the console
import java.util.Scanner;

public class Program2 {
    public static void main(String[] args) {
        // Instantiate a Scanner object to read keyboard input
        Scanner input = new Scanner(System.in);

        // UNIT 2 CONCEPT: Generate a random integer from 1 to 100 (inclusive)
        // Math.random() returns [0.0, 1.0) -> * 100 gives [0.0, 100.0) -> (int) gives 0..99 -> + 1 gives 1..100
        int secretNumber = (int) (Math.random() * 100) + 1;

        // PRIMING READ: Prompt and read the user's first guess BEFORE the loop starts
        System.out.print("Guess a number between 1 and 100: ");
        int guess = input.nextInt();

        // COUNTER: Initialize 'count' to 1 because the user has already made their first guess
        int count = 1;

        // UNIT 4 CONCEPT: Sentinel-style while loop continues until 'guess' equals 'secretNumber'
        while (guess != secretNumber) {
            // UNIT 3 CONCEPT: Use if-else inside the loop to give directional feedback
            if (guess > secretNumber) {
                System.out.println("Too high!");
            } else {
                System.out.println("Too low!");
            }

            // UPDATE READ & COUNTER INCREMENT: Read the next guess and add 1 to the attempt counter
            System.out.print("Guess again: ");
            guess = input.nextInt();
            count++;
        }

        // Loop exits only when (guess == secretNumber) is true
        System.out.println("You got it!");
        System.out.println("It took you " + count + " guesses.");

        // Close the Scanner resource
        input.close();
    }
}

```

## Three
