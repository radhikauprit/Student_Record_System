# Student_Record_System
Student_Record_System is based on student record with using arraylist and object oriented concepts
import java.util.ArrayList;
import java.util.Scanner;

class student {
    private int id;
    private String name;
    private String grade;

    student(int id, String name, String grade) {
        this.id = id;
        this.name = name;
        this.grade = grade;
    }

    public int getid() {
        return id;
    }

    public void setid(int id) {
        this.id = id;
    }

    public String getname() {
        return name;
    }

    public void setname(String name) {
        this.name = name;
    }

    public String getgrade() {
        return grade;
    }

    public void setgrade(String grade) {
        this.grade = grade;
    }

    void dispaly() {
        System.out.println("Id: " + id + " | Name: " + name + " | Grade: " + grade);
    }
}

public class studentmanager {
    private ArrayList<student> students = new ArrayList<>();
    private Scanner scanner = new Scanner(System.in);

    public void start() {
        int choice;
        do {
            System.out.println("\n--- Student Record Management System ---");
            System.out.println("1. Add Student");
            System.out.println("2. View All Students");
            System.out.println("3. Update Student");
            System.out.println("4. Delete Student");
            System.out.println("5. Exit");
            System.out.print("Enter your choice (1 to 5): ");

            choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    addStudent();
                    break;
                case 2:
                    viewStudents();
                    break;
                case 3:
                    updateStudent();
                    break;
                case 4:
                    deleteStudent();
                    break;
                case 5:
                    System.out.println("Exiting program. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 5.");
            }
        } while (choice != 5);
    }

    private void addStudent() {
        System.out.println("\n--- Add New Student ---");
        try {
            System.out.print("Enter Student ID: ");
            int id = scanner.nextInt();
            scanner.nextLine(); // consume newline

            System.out.print("Enter Student Name: ");
            String name = scanner.nextLine();

            System.out.print("Enter Grade: ");
            String grade = scanner.nextLine();

            for (student s : students) {
                if (s.getid() == id) {
                    System.out.println("Student with this ID already exists.");
                    return;
                }
            }

            student newStudent = new student(id, name, grade);
            students.add(newStudent);
            System.out.println("Student added successfully.");
        } catch (Exception e) {
            System.out.println("Invalid input.");
            scanner.nextLine(); // clear buffer
        }
    }

    private void viewStudents() {
        System.out.println("\n--- Student Records ---");
        if (students.isEmpty()) {
            System.out.println("No student records found.");
        } else {
            for (student s : students) {
                s.dispaly();
            }
        }
    }

    private void updateStudent() {
        System.out.println("\n--- Update Student ---");

        System.out.print("Enter Student ID to update: ");
        int id = scanner.nextInt();
        scanner.nextLine(); // consume newline

        student foundstudentid = null;
        for (student s : students) {
            if (s.getid() == id) {
                foundstudentid = s;
                break;
            }
        }

        if (foundstudentid == null) {
            System.out.println("Student with ID " + id + " not found.");
            return;
        }

        System.out.println("Current record:");
        foundstudentid.dispaly();

        System.out.print("Enter new name (leave blank to keep unchanged): ");
        String newname = scanner.nextLine();
        if (!newname.isEmpty()) {
            foundstudentid.setname(newname);
        }

        System.out.print("Enter new grade (leave blank to keep unchanged): ");
        String newgrade = scanner.nextLine();
        if (!newgrade.isEmpty()) {
            foundstudentid.setgrade(newgrade);
        }

        System.out.println("Student record updated.");
    }

    private void deleteStudent() {
        System.out.println("\n--- Delete Student ---");

        System.out.print("Enter Student ID to delete: ");
        int id = scanner.nextInt();
        scanner.nextLine(); // consume newline

        boolean removed = false;
        for (int i = 0; i < students.size(); i++) {
            if (students.get(i).getid() == id) {
                students.remove(i);
                removed = true;
                break;
            }
        }

        if (removed) {
            System.out.println("Student removed.");
        } else {
            System.out.println("Student with ID " + id + " not found.");
        }
    }

    public static void main(String[] args) {
        new studentmanager().start(); // ✅ correct class name
    }
}
