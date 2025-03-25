  QUIZ APPLICATION  BY USING JAVA PROGRAMMING LANGUAGE..



import java.util.*;
public class QuizApplication {
   static Scanner scanner = new Scanner(System.in);
   static int totalEarnings = 0;
   static boolean fiftyFiftyUsed = false, audienceUsed = false, skipUsed = false;
   static boolean fiftyFiftyActive = false;
   static boolean skipActive = false;
   static int[] reducedIndexes = new int[2];
   public static void main(String[] args) {
       System.out.println("\n***************************************");
       System.out.println(" WELCOME TO THE QUIZ APPLICATION ");
       System.out.println("***************************************\n");
      
       displayRules();
      
       System.out.print("Please enter your name: ");
       String playerName = scanner.nextLine();
       System.out.println("Hello, " + playerName + "! Let's begin the quiz! \n");
      
       startQuiz();
   }
   public static void displayRules() {
       System.out.println(" RULES OF THE GAME ");
       System.out.println("1️.Answer correctly to earn money. ");
       System.out.println("2️. Use lifelines wisely! Each lifeline can only be used once. ");
       System.out.println("3️. You can quit anytime and keep your earnings. \n");
       System.out.print("Do you agree to the rules? (yes/no): ");
       if (!scanner.nextLine().equalsIgnoreCase("yes")) {
           System.out.println("Thank you! Come back again. ");
           System.exit(0);
       }
   }
   public static void startQuiz() {
       String[][] questions = {
           {"What is the time complexity of binary search?", "O(n)", "O(log n)", "O(n^2)", "O(1)", "2"},
           {"Which sorting algorithm has the best average case time complexity?", "Bubble Sort", "Insertion Sort", "Merge Sort", "Selection Sort", "3"},
           {"What is the default value of an int variable in Java?", "0", "1", "null", "undefined", "1"},
           {"What is the output of 5 & 3 in Java?", "1", "2", "3", "5", "1"},
           {"What is the derivative of sin(x)?", "cos(x)", "tan(x)", "-cos(x)", "-sin(x)", "1"},
           {"Who directed the movie 'Inception'?", "Christopher Nolan", "Steven Spielberg", "James Cameron", "Martin Scorsese", "1"},
           {"What is the pH value of pure water?", "5", "7", "9", "10", "2"},
           {"What is the value of π (pi) to two decimal places?", "3.12", "3.14", "3.16", "3.18", "2"},
           {"Which gas is known as the 'laughing gas'?", "Nitrous Oxide", "Carbon Dioxide", "Oxygen", "Hydrogen", "1"},
           {"In which movie did Leonardo DiCaprio win his first Oscar?", "The Wolf of Wall Street", "The Revenant", "Titanic", "Inception", "2"}
       };
       for (int i = 0; i < questions.length; i++) {
           fiftyFiftyActive = false;
           reducedIndexes = new int[2];
           skipActive = false;
           System.out.println("\n Question " + (i + 1) + ": " + questions[i][0]);
           for (int j = 1; j <= 4; j++) {
               System.out.println(j + ". " + questions[i][j]);
           }
           boolean answered = false;
           while (!answered) {
               System.out.print("Enter your answer (1-4) or type 'lifeline' to use a lifeline: ");
               String input = scanner.nextLine();
               if (isValidOption(input)) {
                   if (input.equals(questions[i][5])) {
                       if (!skipActive) {
                           System.out.println(" Correct! You earned ₹1000.");
                           totalEarnings += 1000;
                       } else {
                           System.out.println(" Correct! (No earnings since you used Skip Lifeline).\n");
                       }
                   } else {
                       System.out.println(" Wrong answer. The correct answer was: " + questions[i][Integer.parseInt(questions[i][5])]);
                       if (!skipActive) {
                           System.out.println("Game Over. Your total earnings are: ₹" + totalEarnings);
                           return;
                       } else {
                           System.out.println(" Wrong answer! (No penalty since you used Skip Lifeline).\n");
                       }
                   }
                   answered = true;
               } else if (input.equalsIgnoreCase("lifeline")) {
                   showAvailableLifelines(questions[i]);
               } else {
                   System.out.println(" Invalid input! Please enter a number between 1-4 or 'lifeline'.");
               }
           }
           System.out.print("Do you want to quit? (yes/no): ");
           if (scanner.nextLine().equalsIgnoreCase("yes")) {
               System.out.println("You decided to quit. Your total earnings are: ₹" + totalEarnings);
               return;
           }
       }
       System.out.println("\n  Quiz completed! Your total earnings are: ₹" + totalEarnings);
   }
   public static void showAvailableLifelines(String[] question) {
       System.out.println("\n Available Lifelines:");
       if (!fiftyFiftyUsed) System.out.println("1. 50-50");
       if (!audienceUsed) System.out.println("2. Audience Poll");
       if (!skipUsed) System.out.println("3. Skip Question");
       System.out.print("Choose a lifeline (enter the number): ");
       String choice = scanner.nextLine();
       switch (choice) {
           case "1":
               if (!fiftyFiftyUsed) {
                   fiftyFiftyUsed = true;
                   useFiftyFifty(question);
               }
               break;
           case "2":
               if (!audienceUsed) {
                   audienceUsed = true;
                   useAudiencePoll(question);
               }
               break;
           case "3":
               if (!skipUsed) {
                   skipUsed = true;
                   skipActive = true;
                   System.out.println(" You skipped the question, but you still need to answer it.");
               }
               break;
           default:
               System.out.println("❌ Invalid choice. No lifeline used.");
               break;
       }
   }
   public static void useFiftyFifty(String[] question) {
       System.out.println("🔹 50-50 Lifeline Activated! Two incorrect options are removed.");
       Random rand = new Random();
       int correctOption = Integer.parseInt(question[5]);
       int otherOption;
       do {
           otherOption = rand.nextInt(4) + 1;
       } while (otherOption == correctOption);
       reducedIndexes[0] = correctOption;
       reducedIndexes[1] = otherOption;
       System.out.println("Remaining Options:");
       System.out.println(reducedIndexes[0] + ". " + question[reducedIndexes[0]]);
       System.out.println(reducedIndexes[1] + ". " + question[reducedIndexes[1]]);
   }
   public static void useAudiencePoll(String[] question) {
       System.out.println(" Audience Poll Lifeline Activated!");
       System.out.println("Most of the audience chose the correct answer: " + question[Integer.parseInt(question[5])]);
   }
   public static boolean isValidOption(String input) {
       return input.matches("[1-4]");
   }
}





SOFTWARE : ECLIPSE.
