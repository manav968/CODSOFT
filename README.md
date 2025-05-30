# CODSOFT
Internship

Task : 1

import java.util.Scanner;
import java.util.Random;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        final int LOWER_BOUND = 1;
        final int UPPER_BOUND = 100;
        final int MAX_ATTEMPTS = 6;

        int score = 0;
        int round = 0;
        boolean playAgain = true;

        System.out.println("Welcome to the Number Guessing Game!");
        System.out.println("I'm thinking of a number between " + LOWER_BOUND + " and " + UPPER_BOUND + ".");

        while (playAgain) {
            int targetNumber = random.nextInt(UPPER_BOUND - LOWER_BOUND + 1) + LOWER_BOUND;
            int attemptsLeft = MAX_ATTEMPTS;
            boolean guessedCorrectly = false;
            round++;

            System.out.println("\n--- Round " + round + " ---");
            System.out.println("You have " + MAX_ATTEMPTS + " attempts to guess the number.");

            while (attemptsLeft > 0) {
                System.out.print("Enter your guess (" + attemptsLeft + " attempts left): ");
                int guess;

                // Handle non-integer input
                if (!scanner.hasNextInt()) {
                    System.out.println("Invalid input. Please enter a number.");
                    scanner.next(); // discard invalid input
                    continue;
                }

                guess = scanner.nextInt();

                if (guess < LOWER_BOUND || guess > UPPER_BOUND) {
                    System.out.println("Your guess must be between " + LOWER_BOUND + " and " + UPPER_BOUND + ".");
                    continue;
                }

                if (guess == targetNumber) {
                    System.out.println("Congratulations! You guessed the correct number!");
                    score++;
                    guessedCorrectly = true;
                    break;
                } else if (guess < targetNumber) {
                    System.out.println("Too low.");
                } else {
                    System.out.println("Too high.");
                }

                attemptsLeft--;
            }

            if (!guessedCorrectly) {
                System.out.println("Sorry, you've used all your attempts. The correct number was: " + targetNumber);
            }

            System.out.println("Current Score: " + score + " out of " + round + " round(s)");

            System.out.print("Do you want to play another round? (yes/no): ");
            scanner.nextLine(); // consume newline
            String response = scanner.nextLine().trim().toLowerCase();

            playAgain = response.equals("yes") || response.equals("y");
        }

        System.out.println("\nGame Over!");
        System.out.println("You scored " + score + " out of " + round + " round(s). Thanks for playing!");

        scanner.close();
    }
}











