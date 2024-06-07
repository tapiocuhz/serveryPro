# This code was created as the final assignment (culminating) for ICS4UA: AP Computer Science.
### Language: Java
An "application" designed to assist staff serving food in school cafeterias to easily create transactions and manage various operations at ease without the use of multiple applications. Culminating project for ICS4UA in Java using Eclipse.
```java
package culminatingProject;

import java.util.ArrayList;
import java.util.Scanner;

public class Culminating {

    public class Stock {

        String productName;
        double productPrice;
        double manufacturerCost;
        int productStock;
        String key;
        int itemNumber;
        String type;

        public Stock(String productName, double productPrice, double manufacturerCost, int productStock, String key, int itemNumber, String type) {
            this.productName = productName;
            this.productPrice = productPrice;
            this.manufacturerCost = manufacturerCost;
            this.productStock = productStock;
            this.key = key;
            this.itemNumber = itemNumber;
            this.type = type;
        }

        public void display() {
            System.out.println(itemNumber + " | " + productName + " => $" + String.format("%.2f", productPrice));
        }
    }

    public static void main(String[] args) {
        double revenue = 0.00;
        double totalCost = 0.00;
        double profit = 0.00;
        int choice = 0;
        Culminating food = new Culminating();
        ArrayList<Stock> stockList = new ArrayList<>();
        stockList.add(food.new Stock("Pizza", 4.00, 1.00, 50, "a", 1, "hot"));
        stockList.add(food.new Stock("Fries", 3.75, 1.75, 50, "b", 2, "hot"));
        stockList.add(food.new Stock("Poutine", 5.00, 2.50, 50, "c", 3, "hot"));
        stockList.add(food.new Stock("Cookie", 1.80, 1.00, 50, "d", 4, "hot"));
        stockList.add(food.new Stock("Bottled Drink", 3.75, 0.50, 50, "e", 5, "beverage"));
        Scanner scanner = new Scanner(System.in);

        ArrayList<String> authorizedEmployees = new ArrayList<>();
        ArrayList<String> authorizedAdministrators = new ArrayList<>();
        ArrayList<String> toDoList = new ArrayList<>();

        authorizedEmployees.add("ayaan.shaikh.107@gmail.ca");
        authorizedEmployees.add("john.doe@gmail.com");
        authorizedEmployees.add("*");

        authorizedAdministrators.add("ayaan.shaikh.107@gmail.ca");
        authorizedAdministrators.add("*");

        String employeePassword = "serverypro123";

        System.out.println("_______  _______  ______    __   __  _______  ______    __   __  ");
        System.out.println("|       ||       ||    _ |  |  | |  ||       ||    _ |  |  | |  |");
        System.out.println("|  _____||    ___||   | ||  |  |_|  ||    ___||   | ||  |  |_|  |");
        System.out.println("| |_____ |   |___ |   |_||_ |       ||   |___ |   |_||_ |       |");
        System.out.println("|_____  ||    ___||    __  ||       ||    ___||    __  ||_     _|");
        System.out.println(" _____| ||   |___ |   |  | | |     | |   |___ |   |  | |  |   |");
        System.out.println("|_______||_______||___|  |_|  |___|  |_______||___|  |_|  |___|");

        System.out.print("\n\nPlease type in your email address: ");
        String email = scanner.nextLine();

        boolean authorizedEmployee = false;
        for (String authorizedEmployee1 : authorizedEmployees) {
            if (email.equals(authorizedEmployee1)) {
                authorizedEmployee = true;
                break;
            }
        }

        if (authorizedEmployee) {
            System.out.print("Please enter the entry password: ");
            String password = scanner.nextLine();

            if (!password.equals(employeePassword)) {
                System.out.println("Unauthorized access. Exiting.");
                return;
            }
        } else {
            System.out.println("Unauthorized access. Exiting.");
            return;
        }

        String firstName = "";
        String localPart = email.split("@")[0];
        firstName = localPart.split("\\.")[0];

        toDoList.add("Stock beverages");
        toDoList.add("Bake cookies");
        toDoList.add("Bake fries");
        toDoList.add("Prepare gravy");
        toDoList.add("Bake pizza");

        while (true) {
            System.out.println("===================================================\nWelcome to the Servery, " + firstName + ".\n\nWhich pathway would you like to go to?\n1 = Register   2 = To-Do   3 = Control Panel   0 = Exit");
            choice = scanner.nextInt();
            scanner.nextLine();

            if (choice == 0) {
                System.out.println("Exiting the system. Goodbye!");
                break;
            } else if (choice == 1) {
                double total = 0;
                boolean complete = false;
                while (!complete) {
                    System.out.println("");
                    for (Stock item : stockList) {
                        item.display();
                    }
                    System.out.println("Type 0 to complete the transaction\n\n");
                    System.out.printf("Current total: $%.2f\n", total);
                    System.out.printf("Item ID: ");

                    int userChoice = scanner.nextInt();
                    scanner.nextLine();
                    if (userChoice == 0) {
                        complete = true;
                        revenue += total;
                        profit = revenue - totalCost;
                    } else if (userChoice >= 1 && userChoice <= stockList.size()) {
                        System.out.print("Enter quantity: ");
                        int quantity = scanner.nextInt();
                        scanner.nextLine();
                        Stock item = stockList.get(userChoice - 1);
                        total += item.productPrice * quantity;
                        totalCost += item.manufacturerCost * quantity;
                    } else {
                        System.out.println("Invalid choice. Please try again.");
                    }
                }

                System.out.printf("Total price: $%.2f\n", total);
                System.out.println("\n\nType 0 to return back to the main page.");
                scanner.nextInt();
                scanner.nextLine();
            } else if (choice == 2) {
                System.out.println("Here are today's to-do tasks:");
                for (String task : toDoList) {
                    System.out.println(task);
                }
                System.out.println("\n\nType 0 to return back to the main page.");
                scanner.nextInt();
                scanner.nextLine();
            } else if (choice == 3) {
                System.out.println("You are entering the control panel. You must have EXPLICIT access.");

                boolean authorizedAdmin = false;
                for (String authorizedAdministrator : authorizedAdministrators) {
                    if (email.equals(authorizedAdministrator)) {
                        authorizedAdmin = true;
                        break;
                    }
                }

                if (authorizedAdmin) {
                    System.out.println("User is authorized, loading control panel.");
                } else {
                    System.out.println("Unauthorized access, closing.");
                    continue;
                }

                if (authorizedAdmin) {
                    System.out.println("========================================================\nWelcome to the Control Panel, " + firstName + ".\n\nWhich pathway would you like to go to?\n4 = Employees   5 = Admins   6 = Finance   7 = Add Employee   \n8 = Edit To-Do List   9 = Add Food Item   0 = Main Menu\n");
                    int adminChoice = scanner.nextInt();
                    scanner.nextLine();

                    if (adminChoice == 4) {
                        for (String authorizedEmployee1 : authorizedEmployees) {
                            System.out.println(authorizedEmployee1);
                        }
                    } else if (adminChoice == 5) {
                        for (String authorizedAdministrator : authorizedAdministrators) {
                            System.out.println(authorizedAdministrator);
                        }
                    } else if (adminChoice == 6) {
                    	System.out.printf("Total revenue: $%.2f\n", revenue);
                    	System.out.printf("Total cost: $%.2f\n", totalCost);
                        double monthlyProfit = revenue - totalCost;
                        System.out.printf("Total profit: $%.2f\n", monthlyProfit);
                    } else if (adminChoice == 7) {
                        System.out.print("Enter new employee email: ");
                        String newEmployeeEmail = scanner.nextLine();
                        authorizedEmployees.add(newEmployeeEmail);
                        System.out.println("Employee added successfully! They can now log in to the system.");
                    } else if (adminChoice == 8) {
                        System.out.println("To-Do List Management:\n1 = View To-Do List   2 = Add To-Do Item   \n3 = Remove To-Do Item   0 = Return to Control Panel\n");
                        int toDoChoice = scanner.nextInt();
                        scanner.nextLine();
                        if (toDoChoice == 1) {
                            System.out.println("To-Do List:");
                            for (String task : toDoList) {
                                System.out.println(task);
                            }
                        } else if (toDoChoice == 2) {
                            System.out.print("Enter new to-do item: ");
                            String newToDoItem = scanner.nextLine();
                            toDoList.add(newToDoItem);
                            System.out.println("To-do item added successfully!");
                        } else if (toDoChoice == 3) {
                            System.out.println("To-Do List:");
                            for (int i = 0; i < toDoList.size(); i++) {
                                System.out.println((i + 1) + ". " + toDoList.get(i));
                            }
                            System.out.print("Enter the number of the task to remove: ");
                            int removeIndex = scanner.nextInt();
                            scanner.nextLine();
                            if (removeIndex > 0 && removeIndex <= toDoList.size()) {
                                toDoList.remove(removeIndex - 1);
                                System.out.println("Task removed successfully!");
                            } else {
                                System.out.println("Invalid task number.");
                            }
                        }
                    } else if (adminChoice == 9) {
                        System.out.print("Enter product name: ");
                        String productName = scanner.nextLine();
                        System.out.print("Enter product price: ");
                        double productPrice = scanner.nextDouble();
                        System.out.print("Enter manufacturer cost: ");
                        double manufacturerCost = scanner.nextDouble();
                        System.out.print("Enter product stock: ");
                        int productStock = scanner.nextInt();
                        scanner.nextLine();
                        System.out.print("Enter product key: ");
                        String key = scanner.nextLine();
                        System.out.print("Enter product type: ");
                        String type = scanner.nextLine();
                        int itemNumber = stockList.size() + 1;
                        Stock newProduct = food.new Stock(productName, productPrice, manufacturerCost, productStock, key, itemNumber, type);
                        stockList.add(newProduct);
                        System.out.println("Added this product to the servery!");
                    } else if (adminChoice == 0) {
                        continue;
                    }

                    System.out.println("\n\nType 0 to return back to the main page.");
                    scanner.nextInt();
                    scanner.nextLine();
                }
            } else {
                System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
```
