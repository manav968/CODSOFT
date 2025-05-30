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


TASK : 2

import java.util.Scanner;

public class MyGradeCalculator {
    
    public static void main(String[] args) {
        System.out.println("=== My Personal Grade Calculator ===");
        System.out.println("Let's calculate your academic performance!\n");
    
        Scanner inputReader = new Scanner(System.in);

        int subjectCount = getSubjectCount(inputReader);

        int[] subjectMarks = collectSubjectMarks(inputReader, subjectCount);

        int totalScore = calculateTotal(subjectMarks);
        double averagePercent = calculateAverage(subjectCount, totalScore);
        String finalGrade = determineFinalGrade(averagePercent);
        
        showResults(subjectCount, subjectMarks, totalScore, averagePercent, finalGrade);
        
        inputReader.close();
    }

    private static int getSubjectCount(Scanner scanner) {
        System.out.print("How many subjects do you have? ");
        while (!scanner.hasNextInt()) {
            System.out.println("Please enter a whole number!");
            scanner.next();
            System.out.print("How many subjects? ");
        }
        int count = scanner.nextInt();
        while (count <= 0) {
            System.out.print("Please enter a positive number: ");
            count = scanner.nextInt();
        }
        return count;
    }
    private static int[] collectSubjectMarks(Scanner scanner, int count) {
        int[] marks = new int[count];
        System.out.println("\nEnter marks for each subject (out of 100):");
        
        for (int i = 0; i < count; i++) {
            System.out.print("Subject " + (i+1) + " marks: ");
            while (!scanner.hasNextInt()) {
                System.out.println("Numbers only please!");
                scanner.next();
                System.out.print("Subject " + (i+1) + " marks: ");
            }
            marks[i] = scanner.nextInt();

            while (marks[i] < 0 || marks[i] > 100) {
                System.out.print("Marks must be 0-100. Try again: ");
                marks[i] = scanner.nextInt();
            }
        }
        return marks;
    }

    private static int calculateTotal(int[] marks) {
        int sum = 0;
        for (int mark : marks) {
            sum += mark;
        }
        return sum;
    }

    private static double calculateAverage(int count, int total) {
        return (double) total / count;
    }

    private static String determineFinalGrade(double average) {
        if (average >= 95) return "A+ (Excellent)";
        if (average >= 90) return "A (Great job)";
        if (average >= 85) return "A- (Very good)";
        if (average >= 80) return "B+ (Good)";
        if (average >= 75) return "B (Above average)";
        if (average >= 70) return "B- (Average)";
        if (average >= 65) return "C+ (Below average)";
        if (average >= 60) return "C (Needs improvement)";
        if (average >= 50) return "D (Poor)";
        return "F (Failed)";
    }

    private static void showResults(int count, int[] marks, int total, double average, String grade) {
        System.out.println("\n======= YOUR RESULTS =======");

        System.out.println("\nSubject Details:");
        for (int i = 0; i < count; i++) {
            System.out.printf("Subject %2d: %3d/100 %s\n", 
                i+1, marks[i], getPerformanceComment(marks[i]));
        }

        System.out.println("\nPerformance Summary:");
        System.out.println("Total Marks: " + total + "/" + (count * 100));
        System.out.printf("Average Percentage: %.2f%%\n", average);
        System.out.println("Final Grade: " + grade);
        
        // Additional feedback
        System.out.println("\nOverall Performance: " + getOverallComment(average));
    }
 
    private static String getPerformanceComment(int mark) {
        if (mark >= 90) return "[Outstanding!]";
        if (mark >= 80) return "[Very Good]";
        if (mark >= 70) return "[Good]";
        if (mark >= 60) return "[Satisfactory]";
        if (mark >= 50) return "[Needs Work]";
        return "[Concern]";
    }

    private static String getOverallComment(double average) {
        if (average >= 90) return "Exceptional performance! Keep it up!";
        if (average >= 80) return "Strong performance. Well done!";
        if (average >= 70) return "Good work. Room for improvement.";
        if (average >= 60) return "Average. Consider extra study.";
        if (average >= 50) return "Below average. Seek help.";
        return "Serious improvement needed. Please consult your instructor.";
    }
}











