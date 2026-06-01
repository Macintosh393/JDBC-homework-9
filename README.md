# JDBC & H2 Database Integration (Homework 8)

A core Java application demonstrating low-level integration with the **H2 file-based Database** using raw **JDBC** APIs. The project provisions database schemas, populates mock data, and executes several complex analytical SQL queries mapped to dedicated Java Data Transfer Objects (DTOs).

---

## 🛠️ Technologies Used
- **Java SE 11+**: Primary programming language and platform.
- **Gradle**: Build automation and dependency management tool.
- **H2 Database Engine (2.2.224)**: Embedded, file-based SQL database for lightweight persistent storage.
- **JDBC (Java Database Connectivity)**: Standard API for executing SQL scripts, manipulating connections, preparing statement parameters, and handling query result mappings manually.

---

## 📂 Project Structure

```
JDBC-homework-8/
│
├── sql/                             # SQL Script Directory
│   ├── init_db.sql                  # Schema definitions (Tables & Constraints)
│   ├── populate_db.sql              # Mock seed records
│   ├── find_longest_project.sql     # Analytics: Finds projects with the longest duration
│   ├── find_max_projects_client.sql # Analytics: Finds clients with maximum projects
│   ├── find_max_salary_worker.sql   # Analytics: Finds workers earning highest salaries
│   ├── find_youngest_eldest_workers.sql # Analytics: Finds absolute youngest & oldest workers
│   └── print_project_prices.sql     # Analytics: Calculates the cost of each project
│
├── src/main/java/org/example/       # Java Source Directory
│   ├── Database.java                # Singleton managing the active H2 connection
│   ├── DatabaseInitService.java     # Script runner to execute schema generation (init_db.sql)
│   ├── DatabasePopulateService.java # Script runner to populate tables (populate_db.sql)
│   ├── DatabaseQueryService.java    # Analytical client executing custom SQL queries
│   │
│   └── [DTOs]                       # Data Transfer Objects
│       ├── MaxProjectCountClient.java
│       ├── MaxSalaryWorker.java
│       ├── LongestProject.java
│       ├── YoungestEldestWorker.java
│       └── ProjectPrice.java
│
├── build.gradle                     # Gradle configuration with custom Exec tasks
└── .gitignore                       # Keeps H2 cache files (`testdb.*`) out of repository
```

---

## 🚀 How to Use / Execution Instructions

This project includes custom Gradle tasks to easily execute services in order:

### 1. Initialize Database Schema
Execute the following command to parse `sql/init_db.sql` and provision the tables (`worker`, `client`, `project`, `project_worker`):
```bash
./gradlew runInit
```

### 2. Populate Database Seed Data
Execute this command to load `sql/populate_db.sql` and insert dummy records into the tables:
```bash
./gradlew runPopulate
```

### 3. Run Analytical Queries
Execute the following command to run all database queries via the `DatabaseQueryService`. The service reads query files, dynamically prepares statements, and prints clean mapped models to the console:
```bash
./gradlew runQuery
```

---

## ⚙️ Configuration
- The database is stored locally in the root directory under `./testdb` (file `testdb.mv.db`).
- Default credentials: User `sa`, Password ``.
