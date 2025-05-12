import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

  System.out.println("Welcome to the Online Exam System");
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

  if ("a".equals(username) && "1".equals(password)) {
            System.out.println("Login successful!");
            ExamController examController = new ExamController();
            examController.startExam(scanner);
        } else {
            System.out.println("Invalid credentials.");
        }

  scanner.close();
    }
}

class ExamController {
    private int currentQuestion = 0;
    private int score = 0;
    private int timeLeft = 120; // Time in seconds

  private final String[][] questions = {
        {"Choose the best answer: What is 12 * 8?", "96", "88", "108", "112", "1"},
        {"Choose the best answer: If x = 2 and y = 3, what is x^2 + y^2?", "13", "12", "10", "9", "1"},
        {"Choose the best answer: Which number is divisible by 9?", "123", "153", "124", "145", "2"},
        {"Choose the best answer: What is the average of 10, 20, 30?", "15", "20", "25", "30", "2"},
        {"Choose the best answer: Find the missing number in the series: 2, 4, 8, 16, ?", "20", "24", "32", "40", "3"},
        {"Choose the best answer: How many sides does a pentagon have?", "4", "5", "6", "8", "2"},
        {"Choose the best answer: If a car travels 60 km in 1.5 hours, what is its speed?", "30 km/h", "40 km/h", "45 km/h", "50 km/h", "3"},
        {"Choose the best answer: Find the odd one out: 2, 3, 5, 9, 11", "3", "5", "9", "11", "3"},
        {"Choose the best answer: What is 15% of 200?", "25", "30", "35", "40", "2"},
        {"Choose the best answer: If 6x = 42, what is x?", "6", "7", "8", "9", "2"}
    };

   public void startExam(Scanner scanner) {
        long startTime = System.currentTimeMillis();
        long endTime = startTime + (timeLeft * 1000);
        while (currentQuestion < questions.length && System.currentTimeMillis() < endTime) {
            loadQuestion(scanner);
        }
        showResult();
    }
    private void loadQuestion(Scanner scanner) {
        if (currentQuestion < questions.length) {
            System.out.println("\n" + questions[currentQuestion][0]);
            System.out.println("1. " + questions[currentQuestion][1]);
            System.out.println("2. " + questions[currentQuestion][2]);
            System.out.println("3. " + questions[currentQuestion][3]);
            System.out.println("4. " + questions[currentQuestion][4]);

  System.out.print("Select an option (1-4): ")
            int selected = scanner.nextInt();
      if (String.valueOf(selected).equals(questions[currentQuestion][5])) {
                score++;
            }
            currentQuestion++;
        }
    }
    private void showResult() {
        System.out.println("\nExam over! Your score is: " + score + "/" + questions.length);
    }
}
