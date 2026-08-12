# Mohanapriya-Mart-
Introduction 
import java.util.*;

public class PrimeMart {
    static Scanner sc = new Scanner(System.in);

    static String[] products = {
        "Laptop",
        "Mobile Phone",
        "Headphones",
        "Smart Watch",
        "Keyboard"
    };

    static double[] prices = {
        55000,
        25000,
        1500,
        3000,
        1200
    };

    static int[] cart = new int[5];

    public static void main(String[] args) {

        int choice;

        System.out.println("================================");
        System.out.println("       WELCOME TO PRIMEMART");
        System.out.println("   Online Shopping Management");
        System.out.println("================================");

        do {
            System.out.println("\n----- MAIN MENU -----");
            System.out.println("1. Display Products");
            System.out.println("2. Add Product to Cart");
            System.out.println("3. View Cart");
            System.out.println("4. Checkout");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    displayProducts();
                    break;

                case 2:
                    addToCart();
                    break;

                case 3:
                    viewCart();
                    break;

                case 4:
                    checkout();
                    break;

                case 5:
                    System.out.println("\nThank you for shopping with PrimeMart!");
                    break;

                default:
                    System.out.println("Invalid choice! Please try again.");
            }

        } while (choice != 5);

        sc.close();
    }

    // Display available products
    static void displayProducts() {

        System.out.println("\n----- AVAILABLE PRODUCTS -----");

        for (int i = 0; i < products.length; i++) {
            System.out.println(
                (i + 1) + ". " + products[i] +
                " - Rs." + prices[i]
            );
        }
    }

    // Add product to cart
    static void addToCart() {

        displayProducts();

        System.out.print("\nEnter product number: ");
        int product = sc.nextInt();

        if (product >= 1 && product <= products.length) {

            System.out.print("Enter quantity: ");
            int quantity = sc.nextInt();

            if (quantity > 0) {
                cart[product - 1] += quantity;

                System.out.println(
                    quantity + " " + products[product - 1] +
                    "(s) added to cart."
                );
            } else {
                System.out.println("Invalid quantity!");
            }

        } else {
            System.out.println("Invalid product number!");
        }
    }

    // Display cart
    static void viewCart() {

        double total = 0;
        boolean empty = true;

        System.out.println("\n--------- YOUR CART ---------");

        for (int i = 0; i < products.length; i++) {

            if (cart[i] > 0) {

                double amount = cart[i] * prices[i];

                System.out.println(
                    products[i] +
                    " | Quantity: " + cart[i] +
                    " | Amount: Rs." + amount
                );

                total += amount;
                empty = false;
            }
        }

        if (empty) {
            System.out.println("Your cart is empty.");
        } else {
            System.out.println("-----------------------------");
            System.out.println("Total Amount: Rs." + total);
        }
    }

    // Checkout
    static void checkout() {

        double total = 0;

        for (int i = 0; i < products.length; i++) {
            total += cart[i] * prices[i];
        }

        if (total == 0) {
            System.out.println("\nYour cart is empty!");
            return;
        }

        System.out.println("\n--------- CHECKOUT ---------");
        viewCart();

        System.out.println("\n1. Cash on Delivery");
        System.out.println("2. Online Payment");
        System.out.print("Select payment method: ");

        int payment = sc.nextInt();

        if (payment == 1 || payment == 2) {

            System.out.println("\nOrder placed successfully!");
            System.out.println("Total Amount: Rs." + total);
            System.out.println("Payment Method: " +
                    (payment == 1 ? "Cash on Delivery" : "Online Payment"));

            Arrays.fill(cart, 0);

            System.out.println("Thank you for shopping with PrimeMart!");

        } else {
            System.out.println("Invalid payment method!");
        }
    }
}
