[This code serves as the teaching baseline for **Lecture 6: The Repository Pattern & Abstraction Layers**...](https://docs.google.com/document/d/1ICmy-4ladY91_VkwT9jGZWudQPdG6CUK_uyOCEr3mNs/edit?usp=sharing)
***
>NOTE
> >this code was based on lab-4-starter
# Bookstore CLI - Lecture 6 (Winter 2026)
> **Baseline Codebase for Lecture 6: The Repository Pattern & Abstraction Layers**

This repository represents the transition from raw JPA persistence (Lecture 5) to a professional **Tiered Architecture**. It demonstrates how to decouple application logic from database "plumbing" using the **Repository Design Pattern**.

## 🎯 Lecture 6 Learning Objectives
* **Abstraction:** Hiding the `EntityManager` and `EntityTransaction` behind a clean interface.
* **Generics:** Using `IRepository<T>` to create a reusable data access contract.
* **The "Upsert" Strategy:** Implementing `save()` logic that automatically handles both `persist` (Insert) and `merge` (Update).
* **Tiered Architecture:** Separating the **Presentation Layer** (`App.java`) from the **Data Access Layer** (`ProductRepository.java`).

## 🛠 Key Architectural Changes
1. **New Package: `csd214.bookstore.repositories`**
    * `IRepository.java`: The generic contract defining CRUD operations.
    * `ProductRepository.java`: The concrete JPA implementation that encapsulates all transaction logic.
2. **Refactored `App.java`**
    * The `EntityManager` has been removed.
    * The UI now interacts exclusively with the `IRepository` interface.
3. **Repository Demo: `RepositoryApp.java`**
    * A simplified standalone script used in class to demonstrate how clean client code becomes when using repositories.

## 🚀 In-Class Exercises Included
This codebase is pre-configured to support the Lecture 6 exercises:
* **Exercise 1 (Aggregate Queries):** The `count()` method in the repository for high-performance inventory counting.
* **Exercise 2 (Bulk Operations):** The `deleteAll()` method (Menu Option 6: "System Reset") to demonstrate `executeUpdate()` and the performance risks of the N+1 problem.

---

## 📋 Prerequisites
* **Java JDK:** 24
* **Maven:** 3.9+
* **Docker:** Required to run the MySQL database.

## 🚦 Getting Started

### 1. Start the Database
The application requires the MySQL container defined in `docker-compose.yml`.
```bash
docker-compose up -d
```

### 2. Compile and Run
To run the main Bookstore application (Presentation Layer):
```bash
mvn clean compile
mvn exec:java -Dexec.mainClass="csd214.bookstore.Main"
```

To run the standalone Repository Demo:
```bash
mvn exec:java -Dexec.mainClass="csd214.bookstore.repositories.RepositoryApp"
```

---

## 🏗 Project Structure
```text
src/main/java/csd214/bookstore/
├── App.java                 # Presentation Layer (UI Logic)
├── Main.java                # Entry Point
├── entities/                # JPA Database Models (The "Vault")
├── pojos/                   # Data Transfer Objects (DTOs / UI Logic)
└── repositories/            # Data Access Layer (Abstraction Layer)
    ├── IRepository.java     # The Contract
    └── ProductRepository.java # The Implementation
```

## ⚖️ License
Educational use for CSD214 - Sault College.