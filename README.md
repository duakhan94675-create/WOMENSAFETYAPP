# WOMENSAFETYAPP
import java.util.Scanner;
import java.util.ArrayList;
// OOP Concept: 1. Encapsulation & Custom Class for Contact
class EmergencyContact {
    private String details; // Private variable (Data Hiding)

    // Constructor to initialize object
    public EmergencyContact(String details) {
        this.details = details;
    }
    // Getter Method to access private data safely
    public String getDetails() {
        return details;
    }
}
// OOP Concept: 2. Abstraction & Modularity (App Manager Class)
class SafetyAppManager {
    private Scanner sc = new Scanner(System.in);
    private final String username = "dua khan";
    private final String password = "0987654321";
    
    // Storing Objects of EmergencyContact class instead of plain Strings
    private ArrayList<EmergencyContact> contactsList = new ArrayList<>();

    // LOGIN SYSTEM
    public boolean login() {
        int attempts = 3;
        while (attempts > 0) {
            System.out.print("Enter Username: ");
            String u = sc.nextLine();
            System.out.print("Enter Password: ");
            String p = sc.nextLine();

            if (u.equals(username) && p.equals(password)) {
                System.out.println("Login Successful!\n");
                return true;
            } else {
                attempts--;
                System.out.println("Wrong credentials. Attempts left: " + attempts);
            }
        }
        return false;
    }

    // MAIN MENU
    public void menu() {
        int choice;
        do {
            System.out.println("\n========= MAIN MENU =========");
            System.out.println("1. Add Emergency Contact");
            System.out.println("2. View Contacts");
            System.out.println("3. SOS Alert");
            System.out.println("4ps");
            System.out.println("6. My Location (Demo)");
            System.out.println("0. Exit");
            System.out.print("Enter choice: ");

            choice = sc.nextInt();
            sc.nextLine(); // Clear buffer

            switch (choice) {
                case 1: addContact(); break;
                case 2: viewContacts(); break;
                case 3: sosAlert(); break;
                case 4: fakeCall(); break;
                case 5: safetyTips(); break;
                case 6: showLocation(); break;
                case 0: System.out.println("Exiting App... Stay Safe!"); break;
                default: System.out.println("Invalid Choice!");
            }
        } while (choice != 0);
    }

    // ADD CONTACT (OOP Object Creation)
    private void addContact() {
        System.out.print("Enter contact name/number: ");
        String input = sc.nextLine();
        
        // Creating an Object of EmergencyContact
        EmergencyContact newContact = new EmergencyContact(input);
        contactsList.add(newContact); 
        System.out.println("Contact Saved Successfully!");
    }

    // VIEW contacts
    private void viewContacts() {
        System.out.println("\n--- Emergency Contacts ---");
        if (contactsList.isEmpty()) {
            System.out.println("No contacts added yet.");
        } else {
            for (int i = 0; i < contactsList.size(); i++) {
                // Calling getter method of object
                System.out.println((i + 1) + ". " + contactsList.get(i).getDetails());
            }
        }
    }

    // SOS ALERT
    private void sosAlert() {
        System.out.println("\n🚨 SOS ALERT ACTIVATED 🚨");
        System.out.println("Sending emergency message to contacts...");

        if (contactsList.isEmpty()) {
            System.out.println("No contacts available!");
        } else {
            for (EmergencyContact c : contactsList) {
                System.out.println("Message sent to: " + c.getDetails());
            }
        }
        System.out.println("ALERT: Emergency services notified (simulation)");
    }

    // FAKE CALL FEATURE
    private void fakeCall() {
        System.out.println("Unknown Caller: 'Mom Calling...'");
        System.out.println("Press any key to disconnect...");
        sc.nextLine();
        System.out.println("Call Ended.");
    }

    // SAFETY TIPS
    private void safetyTips() {
        System.out.println("\n--- SAFETY TIPS ---");
        System.out.println("1. Share live location with trusted contacts.");
        System.out.println("2. Avoid dark isolated areas.");
        System.out.println("3. Keep emergency numbers saved.");
        System.out.println("4. Trust your instincts.");
        System.out.println("5. Use SOS feature in danger.");
    }
    // LOCATION (DEMO ONLY)
    private void showLocation() {
        System.out.println("\nYour Current Location (Demo):");
        System.out.println("City: Nawabshah");
        System.out.println("Latitude: 26.2442 N");
        System.out.println("Longitude: 68.4100 E");
    }
}
// MAIN CLASS (Sirf execution ke liye)
public class WomenSafetyApp {
    public static void main(String[] args) {
        System.out.println("=====================================");
        System.out.println("   WOMEN SAFETY APPLICATION (JAVA)   ");
        System.out.println("=====================================");

        // OOP Concept: Creating object of the App Manager to run the app
        SafetyAppManager app = new SafetyAppManager();
        
        if (app.login()) {
            app.menu();
        } else {
            System.out.println("Too many failed attempts. Exiting...");
        }
    }
