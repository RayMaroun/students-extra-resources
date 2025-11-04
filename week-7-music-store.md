# 🎵 Music Store Management System

## A Step-by-Step Tutorial for Advanced OOP: Interfaces, Generics, Lambdas & Streams

---

## 🎯 Project Overview

We're building a Music Store Management System that teaches all the Advanced OOP concepts from Workbook 6a. You'll learn interfaces with default methods, generic classes and methods, bounded generics, lambda expressions, and the essential Stream API methods. This project shows how modern Java features make code cleaner and more powerful!

**What You'll Learn:**

- Interfaces and multiple implementation
- Default methods in interfaces
- Generic classes with type parameters
- Generic methods
- Bounded generics (limiting types)
- Lambda expressions basics
- Stream methods: filter, map, reduce, forEach, sorted, count, collect

---

## 📝 Project Setup

### Step 1: Create Your Project

1. Open IntelliJ IDEA
2. Click **File → New → Project**
3. Name it: `MusicStoreSystem`
4. Location: `~/pluralsight/workbook-6` (or `C:/pluralsight/workbook-6` on Windows)
5. Select **Java** as language
6. Select **Maven** as build system
7. Choose **corretto-17** as JDK
8. Check ✅ **Create Git repository**
9. Click **Create**

### Step 2: Share to GitHub

1. Go to **VCS → Share Project on GitHub**
2. Repository name: Keep as `MusicStoreSystem`
3. Description: "Advanced OOP concepts with Music Store"
4. Click **Share**
5. Click **Add** in the next dialog

### Step 3: Create Package

1. Right-click on `src/main/java`
2. Select **New → Package**
3. Name it: `com.pluralsight.music`
4. Click **OK**

---

## 🔌 Part 1: Understanding Interfaces

### Step 4: Create Your First Interface

Create `Playable` interface:

```java
package com.pluralsight.music;

// Interface = a contract that says "anything that implements me CAN do these things"
public interface Playable {
    // All methods in interfaces are public abstract by default
    void play();
    void pause();
    void stop();
    double getDuration();  // in minutes
}
```

**🔍 What's happening?**

- **Interface** = Like a promise or contract
- Classes that implement this MUST provide these methods
- Think of it like: "If you're Playable, you MUST be able to play, pause, stop"
- No method bodies - just signatures (what, not how)

### Step 5: Create Interface with Default Method

Create `Sellable` interface:

```java
package com.pluralsight.music;

public interface Sellable {
    double getPrice();
    void setPrice(double price);
    int getStock();
    void reduceStock(int quantity);

    // Default method - has implementation!
    // Classes can use this or override it
    default double calculateDiscountPrice(double discountPercent) {
        return getPrice() * (1 - discountPercent / 100);
    }

    // Another default method
    default boolean isInStock() {
        return getStock() > 0;
    }
}
```

**🔍 What's happening?**

- **Default methods** = Methods WITH implementation in the interface
- Classes get these "for free" - don't have to implement them
- But they CAN override if they want different behavior
- Added in Java 8 to allow interfaces to evolve

### Step 6: Implement Multiple Interfaces

Create `Song` class:

```java
package com.pluralsight.music;

// A class can implement MULTIPLE interfaces!
public class Song implements Playable, Sellable {
    private String title;
    private String artist;
    private double duration;  // in minutes
    private double price;
    private int stock;

    public Song(String title, String artist, double duration, double price, int stock) {
        this.title = title;
        this.artist = artist;
        this.duration = duration;
        this.price = price;
        this.stock = stock;
    }

    // Implement Playable interface methods
    @Override
    public void play() {
        System.out.println("♪ Playing: " + title + " by " + artist);
    }

    @Override
    public void pause() {
        System.out.println("⏸ Paused: " + title);
    }

    @Override
    public void stop() {
        System.out.println("⏹ Stopped: " + title);
    }

    @Override
    public double getDuration() {
        return duration;
    }

    // Implement Sellable interface methods
    @Override
    public double getPrice() {
        return price;
    }

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public int getStock() {
        return stock;
    }

    @Override
    public void reduceStock(int quantity) {
        if (stock >= quantity) {
            stock -= quantity;
        } else {
            System.out.println("Not enough stock!");
        }
    }

    // Song-specific methods
    public String getTitle() {
        return title;
    }

    public String getArtist() {
        return artist;
    }

    @Override
    public String toString() {
        return title + " by " + artist;
    }
}
```

### Step 7: Create Another Implementation

Create `Album` class:

```java
package com.pluralsight.music;

public class Album implements Playable, Sellable {
    private String name;
    private String artist;
    private int numberOfSongs;
    private double totalDuration;
    private double price;
    private int stock;

    public Album(String name, String artist, int numberOfSongs,
                 double totalDuration, double price, int stock) {
        this.name = name;
        this.artist = artist;
        this.numberOfSongs = numberOfSongs;
        this.totalDuration = totalDuration;
        this.price = price;
        this.stock = stock;
    }

    // Playable methods
    @Override
    public void play() {
        System.out.println("📀 Playing album: " + name + " (" + numberOfSongs + " songs)");
    }

    @Override
    public void pause() {
        System.out.println("⏸ Album paused: " + name);
    }

    @Override
    public void stop() {
        System.out.println("⏹ Album stopped: " + name);
    }

    @Override
    public double getDuration() {
        return totalDuration;
    }

    // Sellable methods
    @Override
    public double getPrice() {
        return price;
    }

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public int getStock() {
        return stock;
    }

    @Override
    public void reduceStock(int quantity) {
        if (stock >= quantity) {
            stock -= quantity;
        }
    }

    public String getName() {
        return name;
    }

    public String getArtist() {
        return artist;
    }
}
```

### Step 8: Heterogeneous Collections

Create test class showing different types in same collection:

```java
package com.pluralsight.music;

import java.util.ArrayList;
import java.util.List;

public class InterfaceDemo {
    public static void main(String[] args) {
        System.out.println("=== INTERFACE DEMONSTRATION ===\n");

        // Create different types
        Song song1 = new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100);
        Song song2 = new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50);
        Album album1 = new Album("Divide", "Ed Sheeran", 12, 45.5, 9.99, 20);
        Album album2 = new Album("After Hours", "The Weeknd", 14, 56.0, 12.99, 15);

        // Heterogeneous collection - different types in same list!
        System.out.println("--- Heterogeneous Collection (Playable) ---");
        List<Playable> playlist = new ArrayList<>();
        playlist.add(song1);
        playlist.add(song2);
        playlist.add(album1);
        playlist.add(album2);

        // Process all as Playable (even though they're different types!)
        for (Playable item : playlist) {
            item.play();
            System.out.println("Duration: " + item.getDuration() + " minutes");
        }

        // Another heterogeneous collection with Sellable
        System.out.println("\n--- Inventory (Sellable) ---");
        List<Sellable> inventory = new ArrayList<>();
        inventory.add(song1);
        inventory.add(song2);
        inventory.add(album1);
        inventory.add(album2);

        // Calculate total inventory value
        double totalValue = 0;
        for (Sellable item : inventory) {
            totalValue += item.getPrice() * item.getStock();
        }
        System.out.println("Total inventory value: $" + totalValue);

        // Using default methods
        System.out.println("\n--- Using Default Methods ---");
        System.out.println(song1 + " with 20% discount: $" +
                          song1.calculateDiscountPrice(20));
        System.out.println("Is " + album1.getName() + " in stock? " +
                          album1.isInStock());
    }
}
```

**🔍 What's happening?**

- **Heterogeneous collection** = Different types in same list
- Both Song and Album can be in a `List<Playable>` because they implement Playable
- We can treat them all as Playable, even though they're different classes
- This is the power of interfaces!

### Step 9: Commit Your Work

1. Click **Commit** button
2. Message: "Add interfaces with multiple implementations"
3. Click **Commit and Push**

---

## 🔷 Part 2: Understanding Generics

### Step 10: Why We Need Generics

Create a class showing the problem:

```java
package com.pluralsight.music;

public class WhyGenerics {
    public static void main(String[] args) {
        System.out.println("=== WHY WE NEED GENERICS ===\n");

        // Without generics (old Java way)
        System.out.println("--- Without Generics (Problems) ---");
        ArrayList oldList = new ArrayList();  // No type specified
        oldList.add("Hello");
        oldList.add(123);      // Can add ANY type - dangerous!
        oldList.add(true);

        // Need casting - error prone!
        String text = (String) oldList.get(0);  // Must cast
        // String wrong = (String) oldList.get(1);  // ClassCastException at runtime!

        // With generics (modern Java)
        System.out.println("\n--- With Generics (Type Safety) ---");
        ArrayList<String> safeList = new ArrayList<>();  // Type specified
        safeList.add("Hello");
        safeList.add("World");
        // safeList.add(123);  // Compile error - can't add wrong type!

        String safe = safeList.get(0);  // No casting needed!

        System.out.println("Generics give us:");
        System.out.println("1. Type safety at compile time");
        System.out.println("2. No casting needed");
        System.out.println("3. Clear code intent");
    }
}
```

### Step 11: Create a Generic Class

Create `MusicBox` generic class:

```java
package com.pluralsight.music;

// Generic class - T is a placeholder for any type
public class MusicBox<T> {
    private T content;
    private String label;

    public MusicBox(String label) {
        this.label = label;
        this.content = null;
    }

    public void store(T item) {
        this.content = item;
        System.out.println("Stored in " + label + ": " + item);
    }

    public T retrieve() {
        T temp = content;
        content = null;
        return temp;
    }

    public T peek() {
        return content;
    }

    public boolean isEmpty() {
        return content == null;
    }

    public String getLabel() {
        return label;
    }
}
```

**🔍 What's happening?**

- **`<T>`** = Type parameter (like a variable for types)
- T can be ANY type when we create the MusicBox
- Once we say `MusicBox<Song>`, T becomes Song everywhere
- No casting needed - compiler knows the type!

### Step 12: Generic Class with Fixed Size (from workbook)

Create `FixedList` generic class:

```java
package com.pluralsight.music;

import java.util.ArrayList;
import java.util.List;

// Generic class that limits the number of items
public class FixedList<T> {
    private List<T> items;
    private int maxSize;

    public FixedList(int maxSize) {
        this.maxSize = maxSize;
        this.items = new ArrayList<>();
    }

    public boolean add(T item) {
        if (items.size() >= maxSize) {
            System.out.println("List is full! Cannot add: " + item);
            return false;
        }
        items.add(item);
        return true;
    }

    public T get(int index) {
        if (index >= 0 && index < items.size()) {
            return items.get(index);
        }
        return null;
    }

    public List<T> getItems() {
        return new ArrayList<>(items);  // Return copy for safety
    }

    public int size() {
        return items.size();
    }

    public boolean isFull() {
        return items.size() >= maxSize;
    }
}
```

### Step 13: Generic Methods

Create utility class with generic methods:

```java
package com.pluralsight.music;

import java.util.List;
import java.util.Random;

public class MusicUtils {

    // Generic method - can work with ANY type
    public static <T> void swap(T[] array, int i, int j) {
        T temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    // Generic method that returns a value
    public static <T> T pickRandom(List<T> list) {
        if (list == null || list.isEmpty()) {
            return null;
        }
        Random random = new Random();
        return list.get(random.nextInt(list.size()));
    }

    // Generic method with two type parameters
    public static <K, V> void printKeyValue(K key, V value) {
        System.out.println("Key: " + key + ", Value: " + value);
    }
}
```

**🔍 What's happening?**

- **`<T>`** before return type declares this is a generic method
- T is decided when method is called
- Can have multiple type parameters (K, V)
- Static methods can be generic too!

### Step 14: Bounded Generics (Limiting Types)

Create class with bounded generics:

```java
package com.pluralsight.music;

import java.util.ArrayList;
import java.util.List;

// T must extend Playable - limits what types can be used
public class Playlist<T extends Playable> {
    private String name;
    private List<T> tracks;

    public Playlist(String name) {
        this.name = name;
        this.tracks = new ArrayList<>();
    }

    public void addTrack(T track) {
        tracks.add(track);
    }

    // Can call Playable methods because T extends Playable!
    public void playAll() {
        System.out.println("Playing playlist: " + name);
        for (T track : tracks) {
            track.play();  // We know T has play() method!
        }
    }

    public double getTotalDuration() {
        double total = 0;
        for (T track : tracks) {
            total += track.getDuration();  // We know T has getDuration()!
        }
        return total;
    }

    public List<T> getTracks() {
        return new ArrayList<>(tracks);
    }
}
```

**🔍 What's happening?**

- **`<T extends Playable>`** = T must be Playable or implement Playable
- This limits what types can be used
- BUT it lets us call Playable methods on T
- Can't create `Playlist<String>` - String doesn't extend Playable!

### Step 15: Test Generics

```java
package com.pluralsight.music;

import java.util.Arrays;
import java.util.List;

public class GenericsDemo {
    public static void main(String[] args) {
        System.out.println("=== GENERICS DEMONSTRATION ===\n");

        // Generic class with different types
        System.out.println("--- Generic MusicBox ---");
        MusicBox<Song> songBox = new MusicBox<>("Song Storage");
        MusicBox<Album> albumBox = new MusicBox<>("Album Storage");

        Song song = new Song("Hello", "Adele", 4.5, 1.29, 50);
        Album album = new Album("25", "Adele", 11, 48.0, 9.99, 10);

        songBox.store(song);
        albumBox.store(album);
        // songBox.store(album);  // Compile error! Type safety!

        // FixedList generic
        System.out.println("\n--- FixedList Generic ---");
        FixedList<Song> top5Songs = new FixedList<>(5);
        top5Songs.add(new Song("Song 1", "Artist 1", 3.0, 0.99, 10));
        top5Songs.add(new Song("Song 2", "Artist 2", 3.5, 0.99, 20));
        top5Songs.add(new Song("Song 3", "Artist 3", 4.0, 1.29, 15));
        top5Songs.add(new Song("Song 4", "Artist 4", 3.2, 0.99, 25));
        top5Songs.add(new Song("Song 5", "Artist 5", 3.8, 1.29, 30));
        top5Songs.add(new Song("Song 6", "Artist 6", 3.1, 0.99, 5)); // Will fail!

        // Generic methods
        System.out.println("\n--- Generic Methods ---");
        String[] genres = {"Rock", "Pop", "Jazz", "Classical"};
        System.out.println("Before swap: " + Arrays.toString(genres));
        MusicUtils.swap(genres, 0, 2);
        System.out.println("After swap: " + Arrays.toString(genres));

        List<String> artists = Arrays.asList("Beatles", "Queen", "ABBA", "Eagles");
        System.out.println("Random artist: " + MusicUtils.pickRandom(artists));

        MusicUtils.printKeyValue("Favorite Genre", "Rock");
        MusicUtils.printKeyValue(1, "First Place");

        // Bounded generics
        System.out.println("\n--- Bounded Generics ---");
        Playlist<Song> songPlaylist = new Playlist<>("My Favorites");
        songPlaylist.addTrack(new Song("Song A", "Artist A", 3.5, 0.99, 10));
        songPlaylist.addTrack(new Song("Song B", "Artist B", 4.0, 1.29, 5));

        songPlaylist.playAll();
        System.out.println("Total duration: " + songPlaylist.getTotalDuration() + " minutes");

        // This also works because Album extends Playable
        Playlist<Album> albumPlaylist = new Playlist<>("Best Albums");
        albumPlaylist.addTrack(album);

        // Playlist<String> stringPlaylist = new Playlist<>("Invalid");  // Compile error!
    }
}
```

### Step 16: Commit

1. Click **Commit** button
2. Message: "Add generics with bounded types and generic methods"
3. Click **Commit and Push**

---

## 🎭 Part 3: Lambda Expressions (Quick Introduction for Streams)

### Step 17: Understanding Lambdas for Streams

Create a simple demo:

```java
package com.pluralsight.music;

import java.util.*;

public class LambdaIntro {
    public static void main(String[] args) {
        System.out.println("=== LAMBDA EXPRESSIONS INTRO ===\n");

        List<Song> songs = Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Bad Guy", "Billie Eilish", 3.2, 1.29, 90)
        );

        // OLD WAY - Before Java 8 (verbose!)
        System.out.println("--- Old Way (Anonymous Class) ---");
        Collections.sort(songs, new Comparator<Song>() {
            @Override
            public int compare(Song s1, Song s2) {
                return s1.getTitle().compareTo(s2.getTitle());
            }
        });
        System.out.println("Sorted with anonymous class");

        // NEW WAY - Lambda expression (clean!)
        System.out.println("\n--- New Way (Lambda) ---");
        // Lambda = short way to write a function
        // (parameters) -> expression
        Collections.sort(songs, (s1, s2) -> s1.getTitle().compareTo(s2.getTitle()));
        System.out.println("Sorted with lambda - much cleaner!");

        // We'll mainly use lambdas with streams
        System.out.println("\n--- Lambda with Streams (Preview) ---");

        // Lambda in filter: song -> song.getPrice() < 1.00
        // This means: "given a song, return true if price < 1.00"
        long cheapSongs = songs.stream()
            .filter(song -> song.getPrice() < 1.00)
            .count();

        System.out.println("Cheap songs found: " + cheapSongs);

        // That's it! Lambdas make streams possible
        System.out.println("\nLambdas are just a cleaner way to write functions!");
        System.out.println("We'll use them throughout streams.");
    }
}
```

**🔍 What's happening?**

- **Lambda** = Short way to write a function
- Syntax: `(parameters) -> expression`
- Example: `song -> song.getPrice() < 1.00` means "given a song, check if price is less than 1.00"
- Makes code cleaner and easier to read
- Essential for using streams effectively!

### Step 18: Commit

1. Click **Commit** button
2. Message: "Add lambda introduction for streams"
3. Click **Commit and Push**

---

## 🌊 Part 4: Java Streams (Only What's in Workbook)

### Step 19: Stream Basics with filter() and collect()

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class StreamBasics {
    public static void main(String[] args) {
        System.out.println("=== STREAMS - FILTER & COLLECT ===\n");

        List<Song> songs = createMusicLibrary();

        // Traditional way with loop
        System.out.println("--- Traditional Loop ---");
        List<Song> cheapSongs = new ArrayList<>();
        for (Song song : songs) {
            if (song.getPrice() < 1.00) {
                cheapSongs.add(song);
            }
        }
        System.out.println("Cheap songs (loop): " + cheapSongs.size());

        // Stream way with filter and collect
        System.out.println("\n--- Stream with filter() ---");
        List<Song> cheapSongsStream = songs.stream()
            .filter(song -> song.getPrice() < 1.00)
            .collect(Collectors.toList());

        System.out.println("Cheap songs (stream): " + cheapSongsStream.size());
        cheapSongsStream.forEach(s -> System.out.println("  " + s));
    }

    private static List<Song> createMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Someone You Loved", "Lewis Capaldi", 3.0, 0.79, 60),
            new Song("Bad Guy", "Billie Eilish", 3.2, 1.29, 90),
            new Song("Circles", "Post Malone", 3.6, 0.99, 80),
            new Song("Memories", "Maroon 5", 3.1, 0.69, 70)
        );
    }
}
```

**🔍 What's happening?**

- **Stream** = A pipeline for processing data
- **`.stream()`** = Converts collection to stream
- **`.filter()`** = Keeps only items matching condition
- **`.collect()`** = Gathers results back into collection
- Think of it like a conveyor belt with filters!

### Step 20: forEach() and count()

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class StreamForEachCount {
    public static void main(String[] args) {
        System.out.println("=== STREAMS - FOREACH & COUNT ===\n");

        List<Song> songs = createMusicLibrary();

        // forEach - do something with each element
        System.out.println("--- forEach() ---");
        System.out.println("All Ed Sheeran songs:");
        songs.stream()
            .filter(song -> song.getArtist().contains("Ed Sheeran"))
            .forEach(song -> System.out.println("  ♪ " + song.getTitle()));

        // Method reference version
        System.out.println("\nUsing method reference:");
        songs.stream()
            .filter(song -> song.getPrice() < 1.00)
            .forEach(System.out::println);  // Same as: song -> System.out.println(song)

        // count - count matching elements
        System.out.println("\n--- count() ---");
        long expensiveSongs = songs.stream()
            .filter(song -> song.getPrice() >= 1.00)
            .count();

        System.out.println("Number of songs $1.00 or more: " + expensiveSongs);

        long shortSongs = songs.stream()
            .filter(song -> song.getDuration() <= 3.0)
            .count();

        System.out.println("Number of short songs (≤ 3 min): " + shortSongs);
    }

    private static List<Song> createMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Perfect", "Ed Sheeran", 4.2, 1.29, 120),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Someone You Loved", "Lewis Capaldi", 3.0, 0.79, 60),
            new Song("Bad Guy", "Billie Eilish", 2.8, 1.29, 90)
        );
    }
}
```

### Step 21: sorted()

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class StreamSorted {
    public static void main(String[] args) {
        System.out.println("=== STREAMS - SORTED ===\n");

        List<Song> songs = createMusicLibrary();

        // sorted() - natural order (needs Comparable)
        System.out.println("--- sorted() by Title ---");
        songs.stream()
            .sorted((s1, s2) -> s1.getTitle().compareTo(s2.getTitle()))
            .forEach(s -> System.out.println("  " + s.getTitle()));

        // sorted with filter
        System.out.println("\n--- Cheap songs sorted by artist ---");
        List<Song> sortedCheapSongs = songs.stream()
            .filter(song -> song.getPrice() < 1.00)
            .sorted((s1, s2) -> s1.getArtist().compareTo(s2.getArtist()))
            .collect(Collectors.toList());

        sortedCheapSongs.forEach(s ->
            System.out.println("  " + s.getArtist() + " - " + s.getTitle()));
    }

    private static List<Song> createMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Someone You Loved", "Lewis Capaldi", 3.0, 0.79, 60),
            new Song("Bad Guy", "Billie Eilish", 3.2, 0.99, 90)
        );
    }
}
```

### Step 22: map()

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class StreamMap {
    public static void main(String[] args) {
        System.out.println("=== STREAMS - MAP ===\n");

        List<Song> songs = createMusicLibrary();

        // map() - transform each element
        System.out.println("--- map() to get titles ---");
        List<String> titles = songs.stream()
            .map(song -> song.getTitle())  // Transform Song to String
            .collect(Collectors.toList());

        System.out.println("All titles: " + titles);

        // Method reference version
        List<String> artists = songs.stream()
            .map(Song::getArtist)  // Same as: song -> song.getArtist()
            .distinct()  // Remove duplicates
            .collect(Collectors.toList());

        System.out.println("\nUnique artists: " + artists);

        // Map to calculate prices with tax
        System.out.println("\n--- map() to calculate prices with tax ---");
        List<Double> pricesWithTax = songs.stream()
            .map(song -> song.getPrice() * 1.08)  // Add 8% tax
            .collect(Collectors.toList());

        System.out.println("Prices with tax: " + pricesWithTax);

        // Chaining map operations
        System.out.println("\n--- Chaining maps ---");
        List<Integer> titleLengths = songs.stream()
            .map(Song::getTitle)        // Song -> String
            .map(String::length)         // String -> Integer
            .collect(Collectors.toList());

        System.out.println("Title lengths: " + titleLengths);
    }

    private static List<Song> createMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Perfect", "Ed Sheeran", 4.2, 1.29, 120),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Bad Guy", "Billie Eilish", 3.2, 0.99, 90)
        );
    }
}
```

**🔍 What's happening?**

- **`map()`** = Transform each element to something else
- Song → String (get title)
- Song → Double (get price)
- Can chain maps: Song → String → Integer
- Like a factory line transforming items!

### Step 23: reduce()

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class StreamReduce {
    public static void main(String[] args) {
        System.out.println("=== STREAMS - REDUCE ===\n");

        List<Song> songs = createMusicLibrary();

        // reduce() - combine all elements into one result
        System.out.println("--- reduce() to sum prices ---");

        // Sum all prices
        double totalValue = songs.stream()
            .map(Song::getPrice)  // Get prices
            .reduce(0.0, (sum, price) -> sum + price);  // Add them up

        System.out.println("Total value of all songs: $" + totalValue);

        // Sum with method reference
        double totalDuration = songs.stream()
            .map(Song::getDuration)
            .reduce(0.0, Double::sum);  // Same as: (a, b) -> a + b

        System.out.println("Total duration: " + totalDuration + " minutes");

        // Find max price
        Optional<Double> maxPrice = songs.stream()
            .map(Song::getPrice)
            .reduce((price1, price2) -> price1 > price2 ? price1 : price2);

        maxPrice.ifPresent(price -> System.out.println("Most expensive: $" + price));

        // Concatenate all titles
        String allTitles = songs.stream()
            .map(Song::getTitle)
            .reduce("", (result, title) ->
                result.isEmpty() ? title : result + ", " + title);

        System.out.println("All titles: " + allTitles);

        // Calculate average using reduce (sum / count)
        double sum = songs.stream()
            .map(Song::getPrice)
            .reduce(0.0, Double::sum);

        long count = songs.stream().count();
        double average = sum / count;

        System.out.println("Average price: $" + average);
    }

    private static List<Song> createMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Someone You Loved", "Lewis Capaldi", 3.0, 0.79, 60),
            new Song("Bad Guy", "Billie Eilish", 3.2, 1.29, 90)
        );
    }
}
```

**🔍 What's happening?**

- **`reduce()`** = Combine all elements into ONE result
- Takes initial value and combination function
- `(sum, price) -> sum + price` = Keep adding to sum
- Can find sum, max, min, concatenate strings, etc.
- Like folding paper - many become one!

### Step 24: Complete Example Using All Stream Methods

```java
package com.pluralsight.music;

import java.util.*;
import java.util.stream.*;

public class CompleteStreamExample {
    public static void main(String[] args) {
        System.out.println("=== COMPLETE STREAM EXAMPLE ===\n");

        List<Song> musicLibrary = createLargeMusicLibrary();

        // Example 1: Find and display Ed Sheeran songs under $1
        System.out.println("--- Ed Sheeran songs under $1 ---");
        musicLibrary.stream()
            .filter(song -> song.getArtist().equals("Ed Sheeran"))
            .filter(song -> song.getPrice() < 1.00)
            .sorted((s1, s2) -> s1.getTitle().compareTo(s2.getTitle()))
            .forEach(song -> System.out.println("  " + song.getTitle() + " - $" + song.getPrice()));

        // Example 2: Calculate total value of inventory for songs with stock > 50
        System.out.println("\n--- Total value of well-stocked songs ---");
        double totalValue = musicLibrary.stream()
            .filter(song -> song.getStock() > 50)
            .map(song -> song.getPrice() * song.getStock())
            .reduce(0.0, Double::sum);

        System.out.println("Total value: $" + totalValue);

        // Example 3: Get list of all unique artists
        System.out.println("\n--- All unique artists ---");
        List<String> artists = musicLibrary.stream()
            .map(Song::getArtist)
            .distinct()
            .sorted()
            .collect(Collectors.toList());

        artists.forEach(artist -> System.out.println("  • " + artist));

        // Example 4: Find average duration of songs under $1
        System.out.println("\n--- Average duration of budget songs ---");
        double totalDuration = musicLibrary.stream()
            .filter(song -> song.getPrice() < 1.00)
            .map(Song::getDuration)
            .reduce(0.0, Double::sum);

        long budgetSongCount = musicLibrary.stream()
            .filter(song -> song.getPrice() < 1.00)
            .count();

        if (budgetSongCount > 0) {
            double avgDuration = totalDuration / budgetSongCount;
            System.out.println("Average duration: " + avgDuration + " minutes");
        }

        // Example 5: Process songs by specific artist
        System.out.println("\n--- Process Billie Eilish songs ---");
        List<String> billieEilishTitles = musicLibrary.stream()
            .filter(song -> song.getArtist().equals("Billie Eilish"))
            .map(Song::getTitle)
            .sorted()
            .collect(Collectors.toList());

        System.out.println("Billie Eilish songs: " + billieEilishTitles);
    }

    private static List<Song> createLargeMusicLibrary() {
        return Arrays.asList(
            new Song("Shape of You", "Ed Sheeran", 3.5, 1.29, 100),
            new Song("Perfect", "Ed Sheeran", 4.2, 0.89, 120),
            new Song("Castle on the Hill", "Ed Sheeran", 4.2, 0.79, 80),
            new Song("Blinding Lights", "The Weeknd", 3.2, 0.99, 50),
            new Song("Save Your Tears", "The Weeknd", 3.6, 1.29, 60),
            new Song("Dance Monkey", "Tones and I", 3.3, 0.89, 75),
            new Song("Someone You Loved", "Lewis Capaldi", 3.0, 0.79, 60),
            new Song("Bad Guy", "Billie Eilish", 3.2, 1.29, 90),
            new Song("Everything I Wanted", "Billie Eilish", 4.0, 0.99, 70),
            new Song("Circles", "Post Malone", 3.6, 0.99, 85),
            new Song("Memories", "Maroon 5", 3.1, 0.69, 95),
            new Song("Senorita", "Shawn Mendes", 3.1, 0.89, 110)
        );
    }
}
```

### Step 25: Final Commit

1. Click **Commit** button
2. Message: "Complete Music Store System with all stream operations"
3. Click **Commit and Push**

---

## 🎯 Challenge Exercises

Try these to practice what you learned:

1. **Create a FixedList for top 10 songs** - Use the generic FixedList class
2. **Filter songs by multiple criteria** - Songs under $1 AND over 3 minutes
3. **Create a Playlist interface** - With methods like shuffle(), repeat()
4. **Use reduce to find shortest song** - Find the song with minimum duration
5. **Map songs to "Title by Artist" format** - Transform to display strings
6. **Sort songs by price, then by title** - Multi-level sorting
7. **Count songs per artist** - Use streams to group and count
8. **Calculate total inventory value** - Price × Stock for all items

---

## 📚 Key Takeaways

### What You Learned:

✅ **Interfaces** - Contracts that define what classes can do  
✅ **Default methods** - Methods with implementation in interfaces  
✅ **Multiple implementation** - One class can implement many interfaces  
✅ **Heterogeneous collections** - Different types in same list via interfaces

✅ **Generic classes** - Type-safe containers with `<T>`  
✅ **Generic methods** - Methods that work with any type  
✅ **Bounded generics** - Limiting types with `extends`  
✅ **Type safety** - No casting needed, errors caught at compile time

✅ **Lambda expressions** - Short way to write functions  
✅ **Method references** - Even shorter with `::`

✅ **Stream operations:**

- `filter()` - Keep matching elements
- `map()` - Transform elements
- `reduce()` - Combine into one result
- `forEach()` - Do something with each
- `sorted()` - Sort elements
- `count()` - Count elements
- `collect()` - Gather results

---

## 🎉 Congratulations!

You've mastered Advanced OOP concepts! You built a complete Music Store System using:

- Interfaces for flexible design
- Generics for type-safe code
- Lambdas for cleaner syntax
- Streams for powerful data processing

**Remember:**

- Interfaces = What things CAN DO
- Generics = Type safety without casting
- Lambdas = Short functions
- Streams = Data processing pipelines

Keep practicing these concepts - they're used everywhere in modern Java!

Keep coding, keep learning, and keep building! 🚀
