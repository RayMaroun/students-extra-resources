# 🛍️ E-Commerce System - Feature-Based Package Organization

## A Step-by-Step Tutorial for Organizing Java Projects by Features/Modules

---

## 🎯 Project Overview

We're building an E-Commerce System using **Feature-Based Package Organization** (also called Package by Feature or Vertical Slicing). Unlike our previous School System that organized by layers (models, services, utils), this project organizes code by business features. Each feature is self-contained with its own models, services, and controllers - like mini-applications within your application!

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
4. Location: `~/pluralsight/workbook-4` (or `C:/pluralsight/workbook-4` on Windows)
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
        System.out.println("com.company.shop/");
        System.out.println("├── products/");
        System.out.println("│   ├── Product.java");
        System.out.println("│   ├── ProductService.java");
        System.out.println("│   └── ProductController.java");
        System.out.println("├── cart/");
        System.out.println("│   ├── Cart.java");
        System.out.println("│   ├── CartItem.java");
        System.out.println("│   ├── CartService.java");
        System.out.println("│   └── CartController.java");
        System.out.println("└── orders/");
        System.out.println("    ├── Order.java");
        System.out.println("    ├── OrderService.java");
        System.out.println("    └── OrderController.java");
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
   - `com.pluralsight.shop.customers`
   - `com.pluralsight.shop.payment`
   - `com.pluralsight.shop.common` (shared utilities)

Your structure should look like:

```
com/pluralsight/shop/
├── products/     (everything about products)
├── cart/         (everything about shopping cart)
├── orders/       (everything about orders)
├── customers/    (everything about customers)
├── payment/      (everything about payments)
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

import java.math.BigDecimal;

public class Product {
    private String productId;
    private String name;
    private String description;
    private BigDecimal price;
    private int stockQuantity;
    private ProductCategory category;

    public Product(String productId, String name, BigDecimal price, int stockQuantity) {
        this.productId = productId;
        this.name = name;
        this.price = price;
        this.stockQuantity = stockQuantity;
    }

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
            throw new IllegalArgumentException("Not enough stock");
        }
    }

    // Getters and setters
    public String getProductId() { return productId; }
    public String getName() { return name; }
    public String getDescription() { return description; }
    public void setDescription(String description) { this.description = description; }
    public BigDecimal getPrice() { return price; }
    public int getStockQuantity() { return stockQuantity; }
    public ProductCategory getCategory() { return category; }
    public void setCategory(ProductCategory category) { this.category = category; }

    @Override
    public String toString() {
        return String.format("%s - %s ($%.2f) Stock: %d",
            productId, name, price, stockQuantity);
    }
}
```

In the SAME package, create `ProductCategory.java`:

```java
package com.pluralsight.shop.products;

public enum ProductCategory {
    ELECTRONICS("Electronics", 0.15),    // 15% tax
    CLOTHING("Clothing", 0.10),         // 10% tax
    FOOD("Food", 0.05),                 // 5% tax
    BOOKS("Books", 0.0),                 // No tax
    HOME("Home & Garden", 0.10),        // 10% tax
    SPORTS("Sports & Outdoors", 0.10);  // 10% tax

    private final String displayName;
    private final double taxRate;

    ProductCategory(String displayName, double taxRate) {
        this.displayName = displayName;
        this.taxRate = taxRate;
    }

    public String getDisplayName() { return displayName; }
    public double getTaxRate() { return taxRate; }
}
```

In the SAME package, create `ProductService.java`:

```java
package com.pluralsight.shop.products;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class ProductService {
    private Map<String, Product> productDatabase;
    private int nextProductId;

    public ProductService() {
        this.productDatabase = new HashMap<>();
        this.nextProductId = 1000;
        initializeSampleProducts();
    }

    private void initializeSampleProducts() {
        addProduct("Laptop", new BigDecimal("999.99"), 10, ProductCategory.ELECTRONICS);
        addProduct("T-Shirt", new BigDecimal("19.99"), 50, ProductCategory.CLOTHING);
        addProduct("Java Programming Book", new BigDecimal("49.99"), 20, ProductCategory.BOOKS);
        addProduct("Coffee Maker", new BigDecimal("79.99"), 15, ProductCategory.HOME);
        addProduct("Running Shoes", new BigDecimal("89.99"), 25, ProductCategory.SPORTS);
    }

    public Product addProduct(String name, BigDecimal price, int stock, ProductCategory category) {
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

    public List<Product> findByCategory(ProductCategory category) {
        return productDatabase.values().stream()
            .filter(p -> p.getCategory() == category)
            .collect(Collectors.toList());
    }

    public List<Product> findInStock() {
        return productDatabase.values().stream()
            .filter(Product::isInStock)
            .collect(Collectors.toList());
    }

    public List<Product> getAllProducts() {
        return new ArrayList<>(productDatabase.values());
    }

    public BigDecimal calculatePriceWithTax(Product product) {
        if (product.getCategory() == null) {
            return product.getPrice();
        }
        double taxRate = product.getCategory().getTaxRate();
        BigDecimal tax = product.getPrice().multiply(BigDecimal.valueOf(taxRate));
        return product.getPrice().add(tax);
    }

    public boolean checkAndReduceStock(String productId, int quantity) {
        Product product = findById(productId);
        if (product != null && product.hasEnoughStock(quantity)) {
            product.reduceStock(quantity);
            return true;
        }
        return false;
    }
}
```

Create `ProductController.java`:

```java
package com.pluralsight.shop.products;

import java.math.BigDecimal;
import java.util.List;

public class ProductController {
    private ProductService productService;

    public ProductController() {
        this.productService = new ProductService();
    }

    public void displayAllProducts() {
        System.out.println("\n=== ALL PRODUCTS ===");
        List<Product> products = productService.getAllProducts();
        for (Product product : products) {
            BigDecimal priceWithTax = productService.calculatePriceWithTax(product);
            System.out.printf("%s - $%.2f (with tax: $%.2f)%n",
                product, product.getPrice(), priceWithTax);
        }
    }

    public void displayProductsByCategory(ProductCategory category) {
        System.out.println("\n=== " + category.getDisplayName().toUpperCase() + " ===");
        List<Product> products = productService.findByCategory(category);
        if (products.isEmpty()) {
            System.out.println("No products found in this category");
        } else {
            products.forEach(System.out::println);
        }
    }

    public void displayInStockProducts() {
        System.out.println("\n=== IN STOCK PRODUCTS ===");
        productService.findInStock().forEach(System.out::println);
    }

    public ProductService getProductService() {
        return productService;
    }
}
```

**🔍 What's happening? Feature Cohesion:**

**Everything in ONE package:**

- `Product` - The data model
- `ProductCategory` - Related enum
- `ProductService` - Business logic
- `ProductController` - User interface logic

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
import java.math.BigDecimal;

public class CartItem {
    private Product product;
    private int quantity;
    private BigDecimal priceAtAddTime;

    public CartItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
        this.priceAtAddTime = product.getPrice();
    }

    public BigDecimal getSubtotal() {
        return priceAtAddTime.multiply(BigDecimal.valueOf(quantity));
    }

    public void increaseQuantity(int amount) {
        this.quantity += amount;
    }

    public void setQuantity(int quantity) {
        if (quantity <= 0) {
            throw new IllegalArgumentException("Quantity must be positive");
        }
        this.quantity = quantity;
    }

    // Getters
    public Product getProduct() { return product; }
    public int getQuantity() { return quantity; }
    public BigDecimal getPriceAtAddTime() { return priceAtAddTime; }

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
import java.math.BigDecimal;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class Cart {
    private String cartId;
    private List<CartItem> items;
    private LocalDateTime createdAt;
    private LocalDateTime lastModified;

    public Cart(String cartId) {
        this.cartId = cartId;
        this.items = new ArrayList<>();
        this.createdAt = LocalDateTime.now();
        this.lastModified = LocalDateTime.now();
    }

    public void addItem(Product product, int quantity) {
        Optional<CartItem> existingItem = findItemByProduct(product);

        if (existingItem.isPresent()) {
            existingItem.get().increaseQuantity(quantity);
        } else {
            items.add(new CartItem(product, quantity));
        }
        lastModified = LocalDateTime.now();
    }

    public void removeItem(Product product) {
        items.removeIf(item -> item.getProduct().equals(product));
        lastModified = LocalDateTime.now();
    }

    public void updateQuantity(Product product, int newQuantity) {
        Optional<CartItem> item = findItemByProduct(product);
        if (item.isPresent()) {
            if (newQuantity <= 0) {
                removeItem(product);
            } else {
                item.get().setQuantity(newQuantity);
                lastModified = LocalDateTime.now();
            }
        }
    }

    public void clear() {
        items.clear();
        lastModified = LocalDateTime.now();
    }

    public BigDecimal getSubtotal() {
        return items.stream()
            .map(CartItem::getSubtotal)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
    }

    public int getTotalItems() {
        return items.stream()
            .mapToInt(CartItem::getQuantity)
            .sum();
    }

    public boolean isEmpty() {
        return items.isEmpty();
    }

    private Optional<CartItem> findItemByProduct(Product product) {
        return items.stream()
            .filter(item -> item.getProduct().equals(product))
            .findFirst();
    }

    // Getters
    public String getCartId() { return cartId; }
    public List<CartItem> getItems() { return new ArrayList<>(items); }
    public LocalDateTime getCreatedAt() { return createdAt; }
    public LocalDateTime getLastModified() { return lastModified; }
}
```

Create `CartService.java`:

```java
package com.pluralsight.shop.cart;

import com.pluralsight.shop.products.Product;
import com.pluralsight.shop.products.ProductService;
import java.math.BigDecimal;
import java.util.HashMap;
import java.util.Map;

public class CartService {
    private Map<String, Cart> activeCarts;
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

    public BigDecimal calculateCartTotal(String cartId) {
        Cart cart = getCart(cartId);
        if (cart == null) return BigDecimal.ZERO;

        BigDecimal subtotal = cart.getSubtotal();
        BigDecimal tax = calculateTax(cart);
        return subtotal.add(tax);
    }

    private BigDecimal calculateTax(Cart cart) {
        BigDecimal totalTax = BigDecimal.ZERO;
        for (CartItem item : cart.getItems()) {
            Product product = item.getProduct();
            BigDecimal itemTotal = item.getSubtotal();
            if (product.getCategory() != null) {
                double taxRate = product.getCategory().getTaxRate();
                BigDecimal itemTax = itemTotal.multiply(BigDecimal.valueOf(taxRate));
                totalTax = totalTax.add(itemTax);
            }
        }
        return totalTax;
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
        System.out.printf("Tax: $%.2f%n", calculateTax(cart));
        System.out.printf("Total: $%.2f%n", calculateCartTotal(cartId));
        System.out.printf("Total items: %d%n", cart.getTotalItems());
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

**Dependency injection:**

```java
public CartService(ProductService productService) {
    this.productService = productService;
}
```

- CartService needs ProductService
- Passed in constructor (dependency injection)
- Makes testing easier
- Clear what cart depends on

### 🔄 Commit:

1. Press **Ctrl+K** / **Cmd+K**
2. Commit message: `"Added shopping cart feature with product dependency"`
3. Click **Commit and Push**

---

## 💳 Part 5: Orders Feature Module

### Step 6: Create the Orders Feature

In `com.pluralsight.shop.orders`, create `OrderStatus.java`:

```java
package com.pluralsight.shop.orders;

public enum OrderStatus {
    PENDING("Order placed, awaiting payment"),
    PAID("Payment received, preparing for shipment"),
    SHIPPED("Order shipped"),
    DELIVERED("Order delivered"),
    CANCELLED("Order cancelled"),
    REFUNDED("Order refunded");

    private final String description;

    OrderStatus(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }
}
```

Create `OrderItem.java`:

```java
package com.pluralsight.shop.orders;

import java.math.BigDecimal;

public class OrderItem {
    private String productId;
    private String productName;
    private int quantity;
    private BigDecimal unitPrice;
    private BigDecimal subtotal;

    public OrderItem(String productId, String productName, int quantity, BigDecimal unitPrice) {
        this.productId = productId;
        this.productName = productName;
        this.quantity = quantity;
        this.unitPrice = unitPrice;
        this.subtotal = unitPrice.multiply(BigDecimal.valueOf(quantity));
    }

    // Getters (all fields are immutable after creation)
    public String getProductId() { return productId; }
    public String getProductName() { return productName; }
    public int getQuantity() { return quantity; }
    public BigDecimal getUnitPrice() { return unitPrice; }
    public BigDecimal getSubtotal() { return subtotal; }

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

import java.math.BigDecimal;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

public class Order {
    private String orderId;
    private String customerId;
    private List<OrderItem> items;
    private BigDecimal subtotal;
    private BigDecimal tax;
    private BigDecimal total;
    private OrderStatus status;
    private LocalDateTime orderDate;
    private String shippingAddress;

    public Order(String orderId, String customerId) {
        this.orderId = orderId;
        this.customerId = customerId;
        this.items = new ArrayList<>();
        this.status = OrderStatus.PENDING;
        this.orderDate = LocalDateTime.now();
        this.subtotal = BigDecimal.ZERO;
        this.tax = BigDecimal.ZERO;
        this.total = BigDecimal.ZERO;
    }

    public void addItem(OrderItem item) {
        items.add(item);
        recalculateTotals();
    }

    public void setTax(BigDecimal tax) {
        this.tax = tax;
        recalculateTotals();
    }

    private void recalculateTotals() {
        this.subtotal = items.stream()
            .map(OrderItem::getSubtotal)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
        this.total = subtotal.add(tax);
    }

    public void updateStatus(OrderStatus newStatus) {
        // Validate status transitions
        if (this.status == OrderStatus.CANCELLED || this.status == OrderStatus.REFUNDED) {
            throw new IllegalStateException("Cannot change status of cancelled/refunded order");
        }
        this.status = newStatus;
        System.out.println("Order " + orderId + " status updated to: " + newStatus);
    }

    // Getters
    public String getOrderId() { return orderId; }
    public String getCustomerId() { return customerId; }
    public List<OrderItem> getItems() { return new ArrayList<>(items); }
    public BigDecimal getSubtotal() { return subtotal; }
    public BigDecimal getTax() { return tax; }
    public BigDecimal getTotal() { return total; }
    public OrderStatus getStatus() { return status; }
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

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class OrderService {
    private Map<String, Order> orderDatabase;
    private CartService cartService;
    private ProductService productService;
    private int nextOrderId;

    public OrderService(CartService cartService, ProductService productService) {
        this.orderDatabase = new HashMap<>();
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
                return null; // Rollback - in real app would be transaction
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

        // Calculate and set tax
        BigDecimal tax = cartService.calculateCartTotal(cartId)
            .subtract(cart.getSubtotal());
        order.setTax(tax);

        // Store order
        orderDatabase.put(orderId, order);

        // Clear the cart
        cart.clear();

        System.out.println("Order created successfully: " + orderId);
        return order;
    }

    public Order getOrder(String orderId) {
        return orderDatabase.get(orderId);
    }

    public List<Order> getCustomerOrders(String customerId) {
        List<Order> customerOrders = new ArrayList<>();
        for (Order order : orderDatabase.values()) {
            if (order.getCustomerId().equals(customerId)) {
                customerOrders.add(order);
            }
        }
        return customerOrders;
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
        System.out.println("Date: " + order.getOrderDate());
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

import java.util.UUID;
import java.util.concurrent.atomic.AtomicInteger;

public class IdGenerator {
    private static final AtomicInteger customerCounter = new AtomicInteger(1000);
    private static final AtomicInteger transactionCounter = new AtomicInteger(100000);

    private IdGenerator() {
        // Utility class
    }

    public static String generateCustomerId() {
        return "CUST" + customerCounter.incrementAndGet();
    }

    public static String generateTransactionId() {
        return "TXN" + transactionCounter.incrementAndGet();
    }

    public static String generateSessionId() {
        return "SESSION-" + UUID.randomUUID().toString().substring(0, 8).toUpperCase();
    }
}
```

Create `PriceFormatter.java`:

```java
package com.pluralsight.shop.common;

import java.math.BigDecimal;
import java.math.RoundingMode;
import java.text.NumberFormat;
import java.util.Locale;

public class PriceFormatter {
    private static final NumberFormat CURRENCY_FORMAT = NumberFormat.getCurrencyInstance(Locale.US);

    private PriceFormatter() {
        // Utility class
    }

    public static String format(BigDecimal amount) {
        return CURRENCY_FORMAT.format(amount);
    }

    public static String format(double amount) {
        return CURRENCY_FORMAT.format(amount);
    }

    public static BigDecimal roundToTwoDecimalPlaces(BigDecimal amount) {
        return amount.setScale(2, RoundingMode.HALF_UP);
    }

    public static String formatWithLabel(String label, BigDecimal amount) {
        return String.format("%-15s %s", label + ":", format(amount));
    }
}
```

Create `ValidationUtils.java`:

```java
package com.pluralsight.shop.common;

import java.util.regex.Pattern;

public class ValidationUtils {
    private static final Pattern EMAIL_PATTERN =
        Pattern.compile("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$");

    private static final Pattern PHONE_PATTERN =
        Pattern.compile("^\\d{3}-\\d{3}-\\d{4}$");

    private ValidationUtils() {
        // Utility class
    }

    public static boolean isValidEmail(String email) {
        return email != null && EMAIL_PATTERN.matcher(email).matches();
    }

    public static boolean isValidPhone(String phone) {
        return phone != null && PHONE_PATTERN.matcher(phone).matches();
    }

    public static boolean isValidZipCode(String zipCode) {
        return zipCode != null && zipCode.matches("\\d{5}(-\\d{4})?");
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
- Shared exceptions

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
import com.pluralsight.shop.orders.OrderStatus;
import com.pluralsight.shop.products.Product;
import com.pluralsight.shop.products.ProductCategory;
import com.pluralsight.shop.products.ProductController;
import com.pluralsight.shop.products.ProductService;

import java.math.BigDecimal;
import java.util.Scanner;

public class ECommerceApp {
    private static ProductController productController;
    private static ProductService productService;
    private static CartService cartService;
    private static OrderService orderService;
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

        // Create services (dependency injection)
        productController = new ProductController();
        productService = productController.getProductService();
        cartService = new CartService(productService);
        orderService = new OrderService(cartService, productService);

        // Create a customer and cart
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
        System.out.println("      ├── ProductCategory.java (enum)");
        System.out.println("      ├── ProductService.java (logic)");
        System.out.println("      └── ProductController.java (interface)");
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
        System.out.println("      ├── OrderStatus.java");
        System.out.println("      └── OrderService.java");
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
        productController.displayAllProducts();

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
            order.updateStatus(OrderStatus.PAID);
            order.setShippingAddress("123 Main St, Anytown, USA 12345");
            order.updateStatus(OrderStatus.SHIPPED);
        }
    }

    private static void runInteractiveMenu() {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        System.out.println("\n=== INTERACTIVE MENU ===");

        while (running) {
            System.out.println("\n1. View products by category");
            System.out.println("2. Add product to cart");
            System.out.println("3. View cart");
            System.out.println("4. Checkout");
            System.out.println("5. View feature organization");
            System.out.println("6. Exit");
            System.out.print("Choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine();

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
                    checkout();
                    break;
                case 5:
                    demonstrateFeatureOrganization();
                    break;
                case 6:
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
        System.out.println("\nCategories:");
        for (ProductCategory cat : ProductCategory.values()) {
            System.out.println("- " + cat.getDisplayName());
        }
        System.out.print("Enter category: ");
        String catName = scanner.nextLine();

        try {
            ProductCategory category = ProductCategory.valueOf(catName.toUpperCase());
            productController.displayProductsByCategory(category);
        } catch (IllegalArgumentException e) {
            System.out.println("Invalid category!");
        }
    }

    private static void addProductToCart(Scanner scanner) {
        productController.displayInStockProducts();
        System.out.print("\nEnter product ID: ");
        String productId = scanner.nextLine();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();
        scanner.nextLine();

        cartService.addToCart(currentCartId, productId, quantity);
    }

    private static void checkout() {
        Cart cart = cartService.getCart(currentCartId);
        if (cart == null || cart.isEmpty()) {
            System.out.println("Cart is empty!");
            return;
        }

        System.out.println("\n--- CHECKOUT ---");
        cartService.displayCart(currentCartId);

        Order order = orderService.createOrderFromCart(currentCartId, currentCustomerId);
        if (order != null) {
            order.setShippingAddress("Customer Address Here");
            order.updateStatus(OrderStatus.PAID);
            System.out.println("\n✅ Order placed successfully!");
            System.out.println("Order ID: " + order.getOrderId());
            System.out.println("Total: " + PriceFormatter.format(order.getTotal()));

            // Create new cart for next shopping session
            Cart newCart = cartService.createCart();
            currentCartId = newCart.getCartId();
        }
    }
}
```

**🔍 What's happening? Application Structure:**

**Package location:**

- Main app is in root package `com.pluralsight.shop`
- Can see and orchestrate all features
- Acts as the conductor

**Dependency wiring:**

```java
productService = productController.getProductService();
cartService = new CartService(productService);
orderService = new OrderService(cartService, productService);
```

- Main app wires features together
- Clear dependency chain
- Could use dependency injection framework later

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
4. **Dependencies are explicit** - Constructor injection shows what features need
5. **Scales better** - Can grow to hundreds of features without chaos
6. **Team-friendly** - "You work on cart, I'll work on orders"

---

## 💪 Challenge Exercises

1. **Add a Customer feature** - Registration, login, profiles
2. **Add a Reviews feature** - Product ratings and reviews
3. **Add a Shipping feature** - Different shipping methods and tracking
4. **Add a Promotions feature** - Discount codes and sales
5. **Extract Cart to a microservice** - See how easy it is with this structure!

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
