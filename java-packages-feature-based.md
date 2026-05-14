# 🛍️ E-Commerce System - Feature-Based Package Organization

## A Step-by-Step Tutorial for Organizing Java Projects by Features/Modules

---

## 🎯 Project Overview

We're building an E-Commerce System using **Feature-Based Package Organization** (also called Package by Feature or Vertical Slicing). Unlike our previous School System that organized by layers (models, services, utils), this project organizes code by business features. Each feature is self-contained with its own models and services - like mini-applications within your application!

**What You'll Master:**

- Feature-based vs Layer-based organization
- When to use each approach
- Self-contained feature modules
- Feature independence and cohesion
- Modern application architecture
- Package by feature best practices

---

## 📚 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `ECommerceSystem`
4. Location: `~/pluralsight/workbook-6` (or `C:/pluralsight/workbook-6` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 1.5: Share to GitHub

1. **VCS → Share Project on GitHub**
2. Repository name: `ECommerceSystem`
3. Description: "Feature-based package organization demo"
4. Click **Share** → **Add**

---

## 🤔 Part 1: Understanding Feature-Based Organization

### Step 2: Create a Comparison Class

First, let's understand the difference. Create a class in `src/main/java`:

```java
public class OrganizationComparison {
    public static void main(String[] args) {
        System.out.println("=== PACKAGE ORGANIZATION STRATEGIES ===\n");

        System.out.println("LAYER-BASED (Previous Project):");
        System.out.println("com.company.school/");
        System.out.println("├── models/");
        System.out.println("│   ├── Student.java");
        System.out.println("│   ├── Teacher.java");
        System.out.println("│   └── Course.java");
        System.out.println("├── services/");
        System.out.println("│   ├── EnrollmentService.java");
        System.out.println("│   └── GradeService.java");
        System.out.println("└── utils/");
        System.out.println("    └── GradeCalculator.java");
        System.out.println("\n✓ Organized by technical layers");
        System.out.println("✓ Similar classes grouped together");
        System.out.println("✗ Feature code scattered across packages");
        System.out.println("✗ High coupling between packages\n");

        System.out.println("FEATURE-BASED (This Project):");
        System.out.println("com.pluralsight.shop/");
        System.out.println("├── products/");
        System.out.println("│   ├── Product.java");
        System.out.println("│   └── ProductService.java");
        System.out.println("├── cart/");
        System.out.println("│   ├── Cart.java");
        System.out.println("│   ├── CartItem.java");
        System.out.println("│   └── CartService.java");
        System.out.println("├── orders/");
        System.out.println("│   ├── Order.java");
        System.out.println("│   ├── OrderItem.java");
        System.out.println("│   └── OrderService.java");
        System.out.println("└── common/");
        System.out.println("    ├── IdGenerator.java");
        System.out.println("    ├── PriceFormatter.java");
        System.out.println("    └── ValidationUtils.java");
        System.out.println("\n✓ Organized by business features");
        System.out.println("✓ Feature code stays together");
        System.out.println("✓ Easy to find and modify features");
        System.out.println("✓ Features can be developed independently");
    }
}
```

**🔍 What's happening? The Philosophy Difference:**

**Layer-Based (Horizontal):**

- Like organizing a closet by clothing type (all shirts together, all pants together)
- Technical grouping
- Good for small projects
- Can lead to "scattered" feature code

**Feature-Based (Vertical):**

- Like organizing by complete outfits (work outfit in one place, gym outfit in another)
- Business grouping
- Scales better for large projects
- Each feature is self-contained

**When to use which?**

- **Layer-based**: Small projects, learning projects, utilities
- **Feature-based**: Large applications, microservices, team projects

**▶️ Run OrganizationComparison** to see the structure comparison!

### 🔄 Commit Your Work:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Initial setup with organization comparison"`
3. Click **Commit and Push**

---

## 📦 Part 2: Creating Feature-Based Package Structure

### Step 3: Delete the Comparison Class and Create Feature Packages

Delete `OrganizationComparison.java` and let's build the real structure.

Create these packages under `src/main/java`:

1. Base package: `com.pluralsight.shop`
2. Feature packages:
   - `com.pluralsight.shop.products`
   - `com.pluralsight.shop.cart`
   - `com.pluralsight.shop.orders`
   - `com.pluralsight.shop.common` (shared utilities)

Your structure should look like:

```
com/pluralsight/shop/
├── products/     (everything about products)
├── cart/         (everything about shopping cart)
├── orders/       (everything about orders)
└── common/       (shared across features)
```

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Created feature-based package structure"`
3. Click **Commit and Push**

---

## 🛍️ Part 3: Products Feature Module

### Step 4: Create the Products Feature

In `com.pluralsight.shop.products`, create `Product.java`:

```java
package com.pluralsight.shop.products;

public class Product {
    private String productId;
    private String name;
    private String description;
    private double price;
    private int stockQuantity;
    private String category; // "ELECTRONICS", "CLOTHING", "FOOD", "BOOKS"

    // Constructor
    public Product(String productId, String name, double price, int stockQuantity) {
        this.productId = productId;
        this.name = name;
        this.price = price;
        this.stockQuantity = stockQuantity;
    }

    // Business logic methods
    public boolean isInStock() {
        return stockQuantity > 0;
    }

    public boolean hasEnoughStock(int quantity) {
        return stockQuantity >= quantity;
    }

    public void reduceStock(int quantity) {
        if (hasEnoughStock(quantity)) {
            stockQuantity -= quantity;
        } else {
            System.out.println("ERROR: Not enough stock for " + name);
        }
    }

    public void addStock(int quantity) {
        stockQuantity += quantity;
    }

    // Calculate tax based on category
    public double getTaxRate() {
        if (category == null) return 0.08; // Default 8%

        switch (category) {
            case "ELECTRONICS":
                return 0.15;  // 15% tax
            case "CLOTHING":
                return 0.10;  // 10% tax
            case "FOOD":
                return 0.05;  // 5% tax
            case "BOOKS":
                return 0.0;   // No tax on books
            default:
                return 0.08;  // Default 8%
        }
    }

    public double getPriceWithTax() {
        return price + (price * getTaxRate());
    }

    // Getters and setters
    public String getProductId() { return productId; }
    public String getName() { return name; }
    public String getDescription() { return description; }
    public void setDescription(String description) { this.description = description; }
    public double getPrice() { return price; }
    public void setPrice(double price) { this.price = price; }
    public int getStockQuantity() { return stockQuantity; }
    public String getCategory() { return category; }
    public void setCategory(String category) { this.category = category; }

    @Override
    public String toString() {
        return String.format("%s - %s ($%.2f) Stock: %d",
            productId, name, price, stockQuantity);
    }
}
```

In the SAME package, create `ProductService.java`:

```java
package com.pluralsight.shop.products;

import java.util.ArrayList;
import java.util.HashMap;

public class ProductService {
    private HashMap<String, Product> productDatabase;
    private int nextProductId;

    public ProductService() {
        this.productDatabase = new HashMap<>();
        this.nextProductId = 1000;
        initializeSampleProducts();
    }

    private void initializeSampleProducts() {
        addProduct("Laptop", 999.99, 10, "ELECTRONICS");
        addProduct("T-Shirt", 19.99, 50, "CLOTHING");
        addProduct("Java Programming Book", 49.99, 20, "BOOKS");
        addProduct("Coffee Maker", 79.99, 15, "ELECTRONICS");
        addProduct("Running Shoes", 89.99, 25, "CLOTHING");
        addProduct("Organic Apples (per lb)", 2.99, 100, "FOOD");
    }

    public Product addProduct(String name, double price, int stock, String category) {
        String productId = "PROD" + nextProductId++;
        Product product = new Product(productId, name, price, stock);
        product.setCategory(category);
        productDatabase.put(productId, product);
        System.out.println("Added product: " + product);
        return product;
    }

    public Product findById(String productId) {
        return productDatabase.get(productId);
    }

    public ArrayList<Product> findByCategory(String category) {
        ArrayList<Product> result = new ArrayList<>();
        for (Product product : productDatabase.values()) {
            if (category.equals(product.getCategory())) {
                result.add(product);
            }
        }
        return result;
    }

    public ArrayList<Product> findInStock() {
        ArrayList<Product> result = new ArrayList<>();
        for (Product product : productDatabase.values()) {
            if (product.isInStock()) {
                result.add(product);
            }
        }
        return result;
    }

    public ArrayList<Product> getAllProducts() {
        return new ArrayList<>(productDatabase.values());
    }

    public boolean checkAndReduceStock(String productId, int quantity) {
        Product product = findById(productId);
        if (product != null && product.hasEnoughStock(quantity)) {
            product.reduceStock(quantity);
            return true;
        }
        return false;
    }

    public void displayAllProducts() {
        System.out.println("\n=== ALL PRODUCTS ===");
        ArrayList<Product> products = getAllProducts();
        for (Product product : products) {
            System.out.printf("%s (Tax: %.0f%%, Total: $%.2f)%n",
                product,
                product.getTaxRate() * 100,
                product.getPriceWithTax());
        }
    }

    public void displayProductsByCategory(String category) {
        System.out.println("\n=== " + category + " PRODUCTS ===");
        ArrayList<Product> products = findByCategory(category);
        if (products.isEmpty()) {
            System.out.println("No products found in this category");
        } else {
            for (Product product : products) {
                System.out.println(product);
            }
        }
    }
}
```

**🔍 What's happening? Feature Cohesion:**

**Everything in ONE package:**

- `Product` - The data model
- `ProductService` - Business logic for products

**Benefits:**

- Want to change products? Look in ONE place
- New developer joins? "Work on products" = one package
- Easy to test - all related code together
- Could extract to microservice easily

**Note about imports:**

- No imports needed between these classes!
- They're all in the same package
- High cohesion, low coupling

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added complete products feature module"`
3. Click **Commit and Push**

---

## 🛒 Part 4: Shopping Cart Feature Module

### Step 5: Create the Cart Feature

In `com.pluralsight.shop.cart`, create `CartItem.java`:

```java
package com.pluralsight.shop.cart;

import com.pluralsight.shop.products.Product;

public class CartItem {
    private Product product;
    private int quantity;
    private double priceAtAddTime;

    public CartItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
        this.priceAtAddTime = product.getPrice();
    }

    public double getSubtotal() {
        return priceAtAddTime * quantity;
    }

    public double getSubtotalWithTax() {
        double subtotal = getSubtotal();
        return subtotal + (subtotal * product.getTaxRate());
    }

    public void increaseQuantity(int amount) {
        this.quantity += amount;
    }

    public void setQuantity(int quantity) {
        if (quantity > 0) {
            this.quantity = quantity;
        } else {
            System.out.println("Quantity must be positive");
        }
    }

    // Getters
    public Product getProduct() { return product; }
    public int getQuantity() { return quantity; }
    public double getPriceAtAddTime() { return priceAtAddTime; }

    @Override
    public String toString() {
        return String.format("%s x%d @ $%.2f = $%.2f",
            product.getName(), quantity, priceAtAddTime, getSubtotal());
    }
}
```

Create `Cart.java`:

```java
package com.pluralsight.shop.cart;

import com.pluralsight.shop.products.Product;
import java.time.LocalDateTime;
import java.util.ArrayList;

public class Cart {
    private String cartId;
    private ArrayList<CartItem> items;
    private LocalDateTime createdAt;
    private LocalDateTime lastModified;

    public Cart(String cartId) {
        this.cartId = cartId;
        this.items = new ArrayList<>();
        this.createdAt = LocalDateTime.now();
        this.lastModified = LocalDateTime.now();
    }

    public void addItem(Product product, int quantity) {
        // Check if product already in cart
        CartItem existingItem = findItemByProduct(product);

        if (existingItem != null) {
            existingItem.increaseQuantity(quantity);
        } else {
            items.add(new CartItem(product, quantity));
        }
        lastModified = LocalDateTime.now();
    }

    public void removeItem(Product product) {
        CartItem itemToRemove = null;
        for (CartItem item : items) {
            if (item.getProduct().equals(product)) {
                itemToRemove = item;
                break;
            }
        }
        if (itemToRemove != null) {
            items.remove(itemToRemove);
            lastModified = LocalDateTime.now();
        }
    }

    public void updateQuantity(Product product, int newQuantity) {
        CartItem item = findItemByProduct(product);
        if (item != null) {
            if (newQuantity <= 0) {
                removeItem(product);
            } else {
                item.setQuantity(newQuantity);
                lastModified = LocalDateTime.now();
            }
        }
    }

    public void clear() {
        items.clear();
        lastModified = LocalDateTime.now();
    }

    public double getSubtotal() {
        double total = 0;
        for (CartItem item : items) {
            total += item.getSubtotal();
        }
        return total;
    }

    public double getTax() {
        double totalTax = 0;
        for (CartItem item : items) {
            double itemSubtotal = item.getSubtotal();
            double itemTax = itemSubtotal * item.getProduct().getTaxRate();
            totalTax += itemTax;
        }
        return totalTax;
    }

    public double getTotal() {
        return getSubtotal() + getTax();
    }

    public int getTotalItems() {
        int total = 0;
        for (CartItem item : items) {
            total += item.getQuantity();
        }
        return total;
    }

    public boolean isEmpty() {
        return items.isEmpty();
    }

    private CartItem findItemByProduct(Product product) {
        for (CartItem item : items) {
            if (item.getProduct().equals(product)) {
                return item;
            }
        }
        return null;
    }

    // Getters
    public String getCartId() { return cartId; }
    public ArrayList<CartItem> getItems() { return new ArrayList<>(items); }
    public LocalDateTime getCreatedAt() { return createdAt; }
    public LocalDateTime getLastModified() { return lastModified; }
}
```

Create `CartService.java`:

```java
package com.pluralsight.shop.cart;

import com.pluralsight.shop.products.Product;
import com.pluralsight.shop.products.ProductService;
import java.util.HashMap;

public class CartService {
    private HashMap<String, Cart> activeCarts;
    private ProductService productService;
    private int nextCartId;

    public CartService(ProductService productService) {
        this.activeCarts = new HashMap<>();
        this.productService = productService;
        this.nextCartId = 1;
    }

    public Cart createCart() {
        String cartId = "CART" + nextCartId++;
        Cart cart = new Cart(cartId);
        activeCarts.put(cartId, cart);
        return cart;
    }

    public Cart getCart(String cartId) {
        return activeCarts.get(cartId);
    }

    public boolean addToCart(String cartId, String productId, int quantity) {
        Cart cart = getCart(cartId);
        if (cart == null) {
            System.out.println("Cart not found: " + cartId);
            return false;
        }

        Product product = productService.findById(productId);
        if (product == null) {
            System.out.println("Product not found: " + productId);
            return false;
        }

        if (!product.hasEnoughStock(quantity)) {
            System.out.println("Not enough stock for " + product.getName());
            return false;
        }

        cart.addItem(product, quantity);
        System.out.printf("Added %d x %s to cart%n", quantity, product.getName());
        return true;
    }

    public void displayCart(String cartId) {
        Cart cart = getCart(cartId);
        if (cart == null || cart.isEmpty()) {
            System.out.println("Cart is empty");
            return;
        }

        System.out.println("\n=== SHOPPING CART ===");
        for (CartItem item : cart.getItems()) {
            System.out.println(item);
        }
        System.out.println("-------------------");
        System.out.printf("Subtotal: $%.2f%n", cart.getSubtotal());
        System.out.printf("Tax: $%.2f%n", cart.getTax());
        System.out.printf("Total: $%.2f%n", cart.getTotal());
        System.out.printf("Total items: %d%n", cart.getTotalItems());
    }

    public void clearCart(String cartId) {
        Cart cart = getCart(cartId);
        if (cart != null) {
            cart.clear();
            System.out.println("Cart cleared");
        }
    }
}
```

**🔍 What's happening? Feature Dependencies:**

**Cross-feature import:**

```java
import com.pluralsight.shop.products.Product;
```

- Cart feature DEPENDS ON Products feature
- This is okay! Features can depend on each other
- But keep dependencies minimal and one-way when possible

**Service needs service:**

```java
public CartService(ProductService productService) {
    this.productService = productService;
}
```

- CartService needs ProductService to look up products
- Passed in through constructor
- Makes the dependency clear and explicit

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added shopping cart feature with product dependency"`
3. Click **Commit and Push**

---

## 💳 Part 5: Orders Feature Module

### Step 6: Create the Orders Feature

In `com.pluralsight.shop.orders`, create `OrderItem.java`:

```java
package com.pluralsight.shop.orders;

public class OrderItem {
    private String productId;
    private String productName;
    private int quantity;
    private double unitPrice;
    private double subtotal;

    public OrderItem(String productId, String productName, int quantity, double unitPrice) {
        this.productId = productId;
        this.productName = productName;
        this.quantity = quantity;
        this.unitPrice = unitPrice;
        this.subtotal = unitPrice * quantity;
    }

    // Getters (all fields are read-only after creation)
    public String getProductId() { return productId; }
    public String getProductName() { return productName; }
    public int getQuantity() { return quantity; }
    public double getUnitPrice() { return unitPrice; }
    public double getSubtotal() { return subtotal; }

    @Override
    public String toString() {
        return String.format("%s x%d @ $%.2f = $%.2f",
            productName, quantity, unitPrice, subtotal);
    }
}
```

Create `Order.java`:

```java
package com.pluralsight.shop.orders;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;

public class Order {
    private String orderId;
    private String customerId;
    private ArrayList<OrderItem> items;
    private double subtotal;
    private double tax;
    private double total;
    private String status; // "PENDING", "PAID", "SHIPPED", "DELIVERED", "CANCELLED"
    private LocalDateTime orderDate;
    private String shippingAddress;

    public Order(String orderId, String customerId) {
        this.orderId = orderId;
        this.customerId = customerId;
        this.items = new ArrayList<>();
        this.status = "PENDING";
        this.orderDate = LocalDateTime.now();
        this.subtotal = 0;
        this.tax = 0;
        this.total = 0;
    }

    public void addItem(OrderItem item) {
        items.add(item);
        recalculateTotals();
    }

    public void setTax(double tax) {
        this.tax = tax;
        recalculateTotals();
    }

    private void recalculateTotals() {
        this.subtotal = 0;
        for (OrderItem item : items) {
            this.subtotal += item.getSubtotal();
        }
        this.total = subtotal + tax;
    }

    public void updateStatus(String newStatus) {
        // Validate status transitions
        if ("CANCELLED".equals(this.status) || "REFUNDED".equals(this.status)) {
            System.out.println("Cannot change status of cancelled/refunded order");
            return;
        }
        this.status = newStatus;
        System.out.println("Order " + orderId + " status updated to: " + newStatus);
    }

    public String getFormattedOrderDate() {
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MMM dd, yyyy HH:mm");
        return orderDate.format(formatter);
    }

    // Status check methods
    public boolean isPending() {
        return "PENDING".equals(status);
    }

    public boolean isPaid() {
        return "PAID".equals(status);
    }

    public boolean isShipped() {
        return "SHIPPED".equals(status);
    }

    // Getters
    public String getOrderId() { return orderId; }
    public String getCustomerId() { return customerId; }
    public ArrayList<OrderItem> getItems() { return new ArrayList<>(items); }
    public double getSubtotal() { return subtotal; }
    public double getTax() { return tax; }
    public double getTotal() { return total; }
    public String getStatus() { return status; }
    public LocalDateTime getOrderDate() { return orderDate; }
    public String getShippingAddress() { return shippingAddress; }
    public void setShippingAddress(String address) { this.shippingAddress = address; }
}
```

Create `OrderService.java`:

```java
package com.pluralsight.shop.orders;

import com.pluralsight.shop.cart.Cart;
import com.pluralsight.shop.cart.CartItem;
import com.pluralsight.shop.cart.CartService;
import com.pluralsight.shop.products.ProductService;

import java.util.ArrayList;
import java.util.HashMap;

public class OrderService {
    private HashMap<String, Order> orderDatabase;
    private HashMap<String, ArrayList<Order>> customerOrders; // customerId -> orders
    private CartService cartService;
    private ProductService productService;
    private int nextOrderId;

    public OrderService(CartService cartService, ProductService productService) {
        this.orderDatabase = new HashMap<>();
        this.customerOrders = new HashMap<>();
        this.cartService = cartService;
        this.productService = productService;
        this.nextOrderId = 10000;
    }

    public Order createOrderFromCart(String cartId, String customerId) {
        Cart cart = cartService.getCart(cartId);

        if (cart == null || cart.isEmpty()) {
            System.out.println("Cannot create order from empty cart");
            return null;
        }

        String orderId = "ORD" + nextOrderId++;
        Order order = new Order(orderId, customerId);

        // Convert cart items to order items and check stock
        for (CartItem cartItem : cart.getItems()) {
            // Check and reduce stock
            boolean stockReduced = productService.checkAndReduceStock(
                cartItem.getProduct().getProductId(),
                cartItem.getQuantity()
            );

            if (!stockReduced) {
                System.out.println("Failed to reserve stock for: " +
                    cartItem.getProduct().getName());
                // In a real app, we'd rollback here
                return null;
            }

            // Create order item
            OrderItem orderItem = new OrderItem(
                cartItem.getProduct().getProductId(),
                cartItem.getProduct().getName(),
                cartItem.getQuantity(),
                cartItem.getPriceAtAddTime()
            );
            order.addItem(orderItem);
        }

        // Set tax from cart
        order.setTax(cart.getTax());

        // Store order
        orderDatabase.put(orderId, order);

        // Track by customer
        if (!customerOrders.containsKey(customerId)) {
            customerOrders.put(customerId, new ArrayList<>());
        }
        customerOrders.get(customerId).add(order);

        // Clear the cart
        cart.clear();

        System.out.println("Order created successfully: " + orderId);
        return order;
    }

    public Order getOrder(String orderId) {
        return orderDatabase.get(orderId);
    }

    public ArrayList<Order> getCustomerOrders(String customerId) {
        ArrayList<Order> orders = customerOrders.get(customerId);
        if (orders == null) {
            return new ArrayList<>();
        }
        return new ArrayList<>(orders);
    }

    public void displayOrder(String orderId) {
        Order order = getOrder(orderId);
        if (order == null) {
            System.out.println("Order not found: " + orderId);
            return;
        }

        System.out.println("\n=== ORDER DETAILS ===");
        System.out.println("Order ID: " + order.getOrderId());
        System.out.println("Customer: " + order.getCustomerId());
        System.out.println("Date: " + order.getFormattedOrderDate());
        System.out.println("Status: " + order.getStatus());
        System.out.println("\nItems:");
        for (OrderItem item : order.getItems()) {
            System.out.println("  " + item);
        }
        System.out.println("-------------------");
        System.out.printf("Subtotal: $%.2f%n", order.getSubtotal());
        System.out.printf("Tax: $%.2f%n", order.getTax());
        System.out.printf("Total: $%.2f%n", order.getTotal());
    }

    public void displayCustomerOrders(String customerId) {
        ArrayList<Order> orders = getCustomerOrders(customerId);

        if (orders.isEmpty()) {
            System.out.println("No orders found for customer: " + customerId);
            return;
        }

        System.out.println("\n=== CUSTOMER ORDER HISTORY ===");
        System.out.println("Customer ID: " + customerId);
        for (Order order : orders) {
            System.out.printf("%s - %s - $%.2f - %s%n",
                order.getOrderId(),
                order.getFormattedOrderDate(),
                order.getTotal(),
                order.getStatus());
        }
    }
}
```

**🔍 What's happening? Feature Orchestration:**

**Multiple dependencies:**

```java
private CartService cartService;
private ProductService productService;
```

- Orders needs BOTH cart and products
- This is the "orchestrator" pattern
- Orders coordinates between features

**Feature flow:**

1. Products feature - manages inventory
2. Cart feature - temporary holding
3. Orders feature - permanent record
4. Each feature has clear responsibility

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added orders feature module with cart and product integration"`
3. Click **Commit and Push**

---

## 🛠️ Part 6: Common/Shared Module

### Step 7: Create Shared Utilities

In `com.pluralsight.shop.common`, create `IdGenerator.java`:

```java
package com.pluralsight.shop.common;

public class IdGenerator {
    private static int customerCounter = 1000;
    private static int transactionCounter = 100000;
    private static int sessionCounter = 1;

    // Private constructor prevents instantiation
    private IdGenerator() {
        // Utility class - should never be instantiated
    }

    public static String generateCustomerId() {
        customerCounter++;
        return "CUST" + customerCounter;
    }

    public static String generateTransactionId() {
        transactionCounter++;
        return "TXN" + transactionCounter;
    }

    public static String generateSessionId() {
        sessionCounter++;
        return "SESSION-" + sessionCounter;
    }
}
```

Create `PriceFormatter.java`:

```java
package com.pluralsight.shop.common;

public class PriceFormatter {

    private PriceFormatter() {
        // Utility class
    }

    public static String formatPrice(double amount) {
        return String.format("$%.2f", amount);
    }

    public static String formatWithLabel(String label, double amount) {
        return String.format("%-15s %s", label + ":", formatPrice(amount));
    }

    public static double roundToTwoDecimalPlaces(double amount) {
        return Math.round(amount * 100.0) / 100.0;
    }
}
```

Create `ValidationUtils.java`:

```java
package com.pluralsight.shop.common;

public class ValidationUtils {

    private ValidationUtils() {
        // Utility class
    }

    public static boolean isValidEmail(String email) {
        if (email == null || email.isEmpty()) {
            return false;
        }
        // Simple email validation
        return email.contains("@") &&
               email.contains(".") &&
               email.indexOf("@") < email.lastIndexOf(".");
    }

    public static boolean isValidPhone(String phone) {
        if (phone == null || phone.isEmpty()) {
            return false;
        }
        // Simple phone validation (format: 555-555-5555)
        String cleaned = phone.replaceAll("[^0-9]", "");
        return cleaned.length() == 10;
    }

    public static boolean isValidZipCode(String zipCode) {
        if (zipCode == null || zipCode.isEmpty()) {
            return false;
        }
        // US zip code validation (5 digits or 5+4)
        return zipCode.matches("\\d{5}") || zipCode.matches("\\d{5}-\\d{4}");
    }

    public static boolean isNotEmpty(String str) {
        return str != null && !str.trim().isEmpty();
    }
}
```

**🔍 What's happening? Common Module:**

**Why a common package?**

- Some utilities are used by MULTIPLE features
- Don't want to duplicate code
- Central place for shared functionality

**What goes in common?**

- ID generators
- Formatters
- Validators
- Constants

**What does NOT go in common?**

- Business logic (belongs in features)
- Feature-specific utilities
- Models/entities (belong to features)

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added common utilities module for shared functionality"`
3. Click **Commit and Push**

---

## 🏃‍♂️ Part 7: Main Application

### Step 8: Create the Application Entry Point

In `com.pluralsight.shop`, create `ECommerceApp.java`:

```java
package com.pluralsight.shop;

import com.pluralsight.shop.cart.Cart;
import com.pluralsight.shop.cart.CartService;
import com.pluralsight.shop.common.IdGenerator;
import com.pluralsight.shop.common.PriceFormatter;
import com.pluralsight.shop.orders.Order;
import com.pluralsight.shop.orders.OrderService;
import com.pluralsight.shop.products.Product;
import com.pluralsight.shop.products.ProductService;

import java.util.ArrayList;
import java.util.Scanner;

public class ECommerceApp {
    // Services that features need
    private static ProductService productService;
    private static CartService cartService;
    private static OrderService orderService;

    // Current session data
    private static String currentCustomerId;
    private static String currentCartId;

    public static void main(String[] args) {
        System.out.println("╔════════════════════════════════════════╗");
        System.out.println("║    E-COMMERCE SYSTEM                  ║");
        System.out.println("║    Feature-Based Organization Demo    ║");
        System.out.println("╚════════════════════════════════════════╝\n");

        initializeSystem();
        demonstrateFeatureOrganization();
        runShoppingDemo();
        runInteractiveMenu();
    }

    private static void initializeSystem() {
        System.out.println("=== INITIALIZING SYSTEM ===");

        // Create services (wiring features together)
        productService = new ProductService();
        cartService = new CartService(productService);
        orderService = new OrderService(cartService, productService);

        // Create a customer and cart for this session
        currentCustomerId = IdGenerator.generateCustomerId();
        Cart cart = cartService.createCart();
        currentCartId = cart.getCartId();

        System.out.println("Customer ID: " + currentCustomerId);
        System.out.println("Cart ID: " + currentCartId);
        System.out.println("System ready!\n");
    }

    private static void demonstrateFeatureOrganization() {
        System.out.println("=== FEATURE-BASED ORGANIZATION ===");
        System.out.println("Each feature is self-contained:");
        System.out.println();
        System.out.println("📦 PRODUCTS FEATURE");
        System.out.println("  └── Everything about products in ONE place");
        System.out.println("      ├── Product.java (model)");
        System.out.println("      └── ProductService.java (business logic)");
        System.out.println();
        System.out.println("🛒 CART FEATURE");
        System.out.println("  └── Complete cart functionality together");
        System.out.println("      ├── Cart.java");
        System.out.println("      ├── CartItem.java");
        System.out.println("      └── CartService.java");
        System.out.println();
        System.out.println("📋 ORDERS FEATURE");
        System.out.println("  └── All order-related code in one package");
        System.out.println("      ├── Order.java");
        System.out.println("      ├── OrderItem.java");
        System.out.println("      └── OrderService.java");
        System.out.println();
        System.out.println("🔧 COMMON MODULE");
        System.out.println("  └── Shared utilities used by all features");
        System.out.println("      ├── IdGenerator.java");
        System.out.println("      ├── PriceFormatter.java");
        System.out.println("      └── ValidationUtils.java");
        System.out.println();
        System.out.println("Benefits:");
        System.out.println("✓ Easy to locate feature code");
        System.out.println("✓ Features can be developed independently");
        System.out.println("✓ Clear boundaries between features");
        System.out.println("✓ Easier to extract into microservices");
        System.out.println();
    }

    private static void runShoppingDemo() {
        System.out.println("=== SHOPPING DEMONSTRATION ===\n");

        // Display products
        productService.displayAllProducts();

        // Add items to cart
        System.out.println("\n--- Adding items to cart ---");
        cartService.addToCart(currentCartId, "PROD1000", 1);  // Laptop
        cartService.addToCart(currentCartId, "PROD1001", 2);  // T-Shirts
        cartService.addToCart(currentCartId, "PROD1002", 1);  // Book

        // Display cart
        cartService.displayCart(currentCartId);

        // Create order
        System.out.println("\n--- Creating order from cart ---");
        Order order = orderService.createOrderFromCart(currentCartId, currentCustomerId);

        if (order != null) {
            orderService.displayOrder(order.getOrderId());

            // Simulate order processing
            System.out.println("\n--- Processing order ---");
            order.updateStatus("PAID");
            order.setShippingAddress("123 Main St, Anytown, USA 12345");
            order.updateStatus("SHIPPED");
        }
    }

    private static void runInteractiveMenu() {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        System.out.println("\n=== INTERACTIVE MENU ===");

        while (running) {
            System.out.println("\n--- Main Menu ---");
            System.out.println("1. View products by category");
            System.out.println("2. Add product to cart");
            System.out.println("3. View cart");
            System.out.println("4. Checkout");
            System.out.println("5. View my orders");
            System.out.println("6. Show feature organization");
            System.out.println("7. Exit");
            System.out.print("Choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    viewProductsByCategory(scanner);
                    break;
                case 2:
                    addProductToCart(scanner);
                    break;
                case 3:
                    cartService.displayCart(currentCartId);
                    break;
                case 4:
                    checkout(scanner);
                    break;
                case 5:
                    orderService.displayCustomerOrders(currentCustomerId);
                    break;
                case 6:
                    demonstrateFeatureOrganization();
                    break;
                case 7:
                    running = false;
                    System.out.println("Thank you for shopping!");
                    break;
                default:
                    System.out.println("Invalid choice!");
            }
        }

        scanner.close();
    }

    private static void viewProductsByCategory(Scanner scanner) {
        System.out.println("\nAvailable categories:");
        System.out.println("1. ELECTRONICS");
        System.out.println("2. CLOTHING");
        System.out.println("3. FOOD");
        System.out.println("4. BOOKS");
        System.out.print("Enter choice (1-4) or category name: ");
        String input = scanner.nextLine().trim();

        // Map numeric choice to category, or let the user type the name directly
        String category;
        switch (input) {
            case "1":
                category = "ELECTRONICS";
                break;
            case "2":
                category = "CLOTHING";
                break;
            case "3":
                category = "FOOD";
                break;
            case "4":
                category = "BOOKS";
                break;
            default:
                category = input.toUpperCase();
                break;
        }

        productService.displayProductsByCategory(category);
    }

    private static void addProductToCart(Scanner scanner) {
        // Show available products
        ArrayList<Product> products = productService.findInStock();
        System.out.println("\n=== AVAILABLE PRODUCTS ===");
        for (Product product : products) {
            System.out.println(product);
        }

        System.out.print("\nEnter product ID (e.g., PROD1000): ");
        String productId = scanner.nextLine();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        boolean added = cartService.addToCart(currentCartId, productId, quantity);
        if (added) {
            System.out.println("Item added to cart!");
        }
    }

    private static void checkout(Scanner scanner) {
        Cart cart = cartService.getCart(currentCartId);
        if (cart == null || cart.isEmpty()) {
            System.out.println("Cart is empty! Add some items first.");
            return;
        }

        System.out.println("\n--- CHECKOUT ---");
        cartService.displayCart(currentCartId);

        System.out.print("\nConfirm order? (yes/no): ");
        String confirm = scanner.nextLine();

        if ("yes".equalsIgnoreCase(confirm)) {
            Order order = orderService.createOrderFromCart(currentCartId, currentCustomerId);
            if (order != null) {
                order.setShippingAddress("Customer Address Here");
                order.updateStatus("PAID");
                System.out.println("\n✅ Order placed successfully!");
                System.out.println("Order ID: " + order.getOrderId());
                System.out.println("Total: " + PriceFormatter.formatPrice(order.getTotal()));

                // Create new cart for next shopping session
                Cart newCart = cartService.createCart();
                currentCartId = newCart.getCartId();
                System.out.println("New cart created for next purchase");
            }
        } else {
            System.out.println("Order cancelled");
        }
    }
}
```

**🔍 What's happening? Application Structure:**

**Package location:**

- Main app is in root package `com.pluralsight.shop`
- Can see and orchestrate all features
- Acts as the conductor

**Wiring features together:**

```java
productService = new ProductService();
cartService = new CartService(productService);
orderService = new OrderService(cartService, productService);
```

- Main app connects features
- Clear dependency chain
- Each service gets what it needs

**Feature independence:**

- Each feature package could be its own project
- Only main app knows about all features
- Features don't know about main app

**🔍 A note on the interactive menu:**

Two details in this menu are easy to get wrong, and worth a moment of attention:

1. **One Scanner for the whole session.** The menu opens a single `Scanner` on `System.in` in `runInteractiveMenu()` and passes it down to `viewProductsByCategory(scanner)`, `addProductToCart(scanner)`, and `checkout(scanner)`. Never open a second `Scanner` on `System.in` inside one of these helpers — it can swallow input or block unpredictably because two scanners are sharing the same underlying stream.

2. **The category menu accepts both numbers and names.** The menu shows a numbered list (`1. ELECTRONICS`, `2. CLOTHING`, …), but the underlying category is a string. A small `switch` maps `"1"` → `"ELECTRONICS"`, etc., and falls back to `input.toUpperCase()` so typing `electronics` or `Books` still works. This is a useful pattern any time a menu shows numbered options but the underlying value is a string.

### 🔄 Final Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added main application with complete feature integration"`
3. Click **Commit and Push**

---

## 📊 Comparison: Feature-Based vs Layer-Based

### When to Use Feature-Based:

✅ **Use when:**

- Large applications with many features
- Multiple teams working on different features
- Planning to extract microservices
- Business functionality is more important than technical similarity
- Want to minimize merge conflicts in team development

✅ **Benefits:**

- Easy to find all code for a feature
- Can assign entire features to developers
- Lower coupling between features
- Easier to delete/extract features
- Natural microservice boundaries

### When to Use Layer-Based:

✅ **Use when:**

- Small to medium applications
- CRUD applications with simple logic
- Learning projects
- Shared utilities and libraries
- Technical organization is more important

✅ **Benefits:**

- Similar code grouped together
- Easy to see all models/services at once
- Good for simple applications
- Familiar to most developers
- Easier to apply cross-cutting changes

---

## 🎯 Key Takeaways

1. **Feature-based = Vertical slices** - Each package is a complete feature
2. **Self-contained features** - Everything about a feature in ONE place
3. **Clear boundaries** - Easy to see where features start and end
4. **Dependencies are explicit** - Constructor parameters show what features need
5. **Scales better** - Can grow to hundreds of features without chaos
6. **Team-friendly** - "You work on cart, I'll work on orders"

---

## 💪 Challenge Exercises

1. **Add a Customer feature** - Customer class, CustomerService for registration
2. **Add a Reviews feature** - ProductReview class, ReviewService
3. **Add a Search feature** - SearchService that searches across products
4. **Add a Discount feature** - DiscountCode class, DiscountService
5. **Add inventory alerts** - Notify when products are low on stock

---

## 🎉 Congratulations!

You now understand BOTH major ways to organize Java projects:

**Layer-Based (Previous tutorial):**

- Technical organization
- Good for small projects
- Traditional approach

**Feature-Based (This tutorial):**

- Business organization
- Good for large projects
- Modern approach
- Microservice-ready

**Real-world advice:**

- Start with layer-based for learning
- Move to feature-based as projects grow
- Many projects use a hybrid approach
- The key is CONSISTENCY within a project

You're now equipped to organize Java projects like a professional developer! 🚀
