import java.util.ArrayList;
import java.util.List;

public class User {
    private String name;
    private int age;
    private List<Workout> workouts;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
        this.workouts = new ArrayList<>();
    }

    public void addWorkout(Workout workout) {
        workouts.add(workout);
    }

    public List<Workout> getWorkouts() {
        return workouts;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", workouts=" + workouts +
                '}';
    }
}

public class Workout {
    private String type;          // Type of workout (e.g., Running, Cycling)
    private int duration;         // Duration in minutes
    private int caloriesBurned;   // Calories burned

    public Workout(String type, int duration, int caloriesBurned) {
        this.type = type;
        this.duration = duration;
        this.caloriesBurned = caloriesBurned;
    }

    public String getType() {
        return type;
    }

    public int getDuration() {
        return duration;
    }

    public int getCaloriesBurned() {
        return caloriesBurned;
    }

    @Override
    public String toString() {
        return "Workout{" +
                "type='" + type + '\'' +
                ", duration=" + duration +
                " minutes, caloriesBurned=" + caloriesBurned +
                '}';
    }
}

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class FitnessApp {
    private Map<String, User> users;

    public FitnessApp() {
        users = new HashMap<>();
    }

    public void addUser(String name, int age) {
        users.put(name, new User(name, age));
    }

    public User getUser(String name) {
        return users.get(name);
    }

    public void trackWorkout(String userName, String type, int duration, int caloriesBurned) {
        User user = getUser(userName);
        if (user != null) {
            Workout workout = new Workout(type, duration, caloriesBurned);
            user.addWorkout(workout);
            System.out.println("Workout tracked for " + userName + ": " + workout);
        } else {
            System.out.println("User not found.");
        }
    }

    public void displayUserWorkouts(String userName) {
        User user = getUser(userName);
        if (user != null) {
            System.out.println(user.getName() + "'s Workouts:");
            for (Workout workout : user.getWorkouts()) {
                System.out.println(workout);
            }


        } else {
            System.out.println("User not found.");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        FitnessApp app = new FitnessApp();

        while (true) {
            System.out.println("1. Add User");
            System.out.println("2. Track Workout");
            System.out.println("3. Display User Workouts");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter user name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter age: ");
                    int age = scanner.nextInt();
                    app.addUser(name, age);
                    System.out.println("User added: " + name);
                    break;

                case 2:
                    System.out.print("Enter user name: ");
                    String userName = scanner.nextLine();
                    System.out.print("Enter workout type: ");
                    String type = scanner.nextLine();
                    System.out.print("Enter duration (in minutes): ");
                    int duration = scanner.nextInt();
                    System.out.print("Enter calories burned: ");
                    int calories = scanner.nextInt();
                    app.trackWorkout(userName, type, duration, calories);
                    break;

                case 3:
                    System.out.print("Enter user name: ");
                    String uName = scanner.nextLine();
                    app.displayUserWorkouts(uName);
                    break;

                case 4:
                    System.out.println("Exiting the application.");
                    scanner.close();
                    return;

                default:
                    System.out.println("Invalid option. Please choose again.");
            }
        }
    }
}
