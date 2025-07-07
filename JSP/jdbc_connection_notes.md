
# 🔗 JDBC Connection in Java

**JDBC (Java Database Connectivity)** is a Java API that allows Java programs to connect and execute queries with databases.

---

## 📦 Required Packages

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.sql.PreparedStatement;
import java.sql.SQLException;
```

---

## 🔄 Steps to Establish JDBC Connection

| Step | Description                                |
|------|--------------------------------------------|
| 1️⃣   | Load and register the JDBC driver          |
| 2️⃣   | Establish a connection to the database     |
| 3️⃣   | Create a statement                         |
| 4️⃣   | Execute the query                          |
| 5️⃣   | Process the results                        |
| 6️⃣   | Close the connection                       |

---

## ✅ Example: JDBC MySQL Connection

```java
import java.sql.*;

public class JdbcExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/dbname";
        String user = "root";
        String password = "yourpassword";

        try {
            // 1. Load MySQL JDBC Driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Create Connection
            Connection con = DriverManager.getConnection(url, user, password);

            // 3. Create Statement
            Statement stmt = con.createStatement();

            // 4. Execute Query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            // 5. Process Result
            while (rs.next()) {
                System.out.println(rs.getInt(1) + " " + rs.getString(2));
            }

            // 6. Close Connection
            con.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## 🛠️ Common JDBC Interfaces

| Interface        | Description                              |
|------------------|------------------------------------------|
| `DriverManager`  | Manages the database drivers              |
| `Connection`     | Establishes connection with DB            |
| `Statement`      | Used to execute SQL queries               |
| `PreparedStatement` | Used for precompiled parameterized queries |
| `ResultSet`      | Holds data retrieved from DB              |

---

## 🧪 Using PreparedStatement

```java
PreparedStatement pst = con.prepareStatement("INSERT INTO students VALUES (?, ?)");
pst.setInt(1, 1);
pst.setString(2, "Shakel");
pst.executeUpdate();
```

---

## ❌ Exception Handling

Always use try-catch blocks to catch:
- `ClassNotFoundException`
- `SQLException`

---

## 📌 JDBC Driver Types

| Type | Description                      |
|------|----------------------------------|
| Type 1 | JDBC-ODBC bridge                |
| Type 2 | Native API driver               |
| Type 3 | Network Protocol driver         |
| Type 4 | Thin driver (pure Java)         |

✅ Most commonly used: **Type 4**

---

## 🧹 Best Practices

- Always close `Connection`, `Statement`, and `ResultSet`
- Use `try-with-resources` from Java 7+
- Avoid hardcoding credentials in code
- Use `PreparedStatement` to prevent SQL injection

---

## 📝 Sample Table

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

---

## ✅ Summary

| Step             | Method/Class Used               |
|------------------|----------------------------------|
| Load Driver      | `Class.forName()`               |
| Connect          | `DriverManager.getConnection()` |
| Query Execution  | `Statement` or `PreparedStatement` |
| Read Data        | `ResultSet`                     |
| Close Connection | `con.close()`                   |

---
