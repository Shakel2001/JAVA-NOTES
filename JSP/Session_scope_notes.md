
# 🌐 JSP Request, Session, and Application Scope

JSP provides several scopes for storing and sharing data:
- **Request scope**
- **Session scope**
- **Application scope**

Each scope determines the **lifetime** and **visibility** of the data.

---

## 📥 1. Request Scope

### 🧠 Definition:
- Data is accessible during a **single request**.
- Typically used for forwarding data between pages.

### ✅ Syntax:
```jsp
<%
    request.setAttribute("key", "value");
    String val = (String) request.getAttribute("key");
%>
```

### 📝 Example:
**page1.jsp**
```jsp
<%
    request.setAttribute("name", "Shakel");
    RequestDispatcher rd = request.getRequestDispatcher("page2.jsp");
    rd.forward(request, response);
%>
```

**page2.jsp**
```jsp
<%
    String name = (String) request.getAttribute("name");
    out.print("Hello, " + name);
%>
```

### 🔚 Lifetime: Ends after request is completed

---

## 👤 2. Session Scope

### 🧠 Definition:
- Data persists across **multiple requests from the same user**.
- Useful for login, shopping cart, etc.

### ✅ Syntax:
```jsp
<%
    session.setAttribute("key", "value");
    String val = (String) session.getAttribute("key");
    session.removeAttribute("key");
    session.invalidate();  // End session
%>
```

### 📝 Example:
```jsp
<%
    session.setAttribute("username", "Shakel");
%>
```

**Access Later:**
```jsp
<%
    String user = (String) session.getAttribute("username");
%>
```

### 🔚 Lifetime: Ends when user logs out or session times out

---

## 🏢 3. Application Scope

### 🧠 Definition:
- Data is shared **across all users and all sessions**.
- Stored in the **ServletContext** object.

### ✅ Syntax:
```jsp
<%
    application.setAttribute("key", "value");
    String val = (String) application.getAttribute("key");
%>
```

### 📝 Example:
```jsp
<%
    application.setAttribute("visitorCount", 100);
%>

<%
    int count = (Integer) application.getAttribute("visitorCount");
    out.print("Total Visitors: " + count);
%>
```

### 🔚 Lifetime: Until the server is stopped or application is undeployed

---

## ✅ Summary Table

| Scope       | Used For              | Object        | Lifetime             | Shared With         |
|-------------|------------------------|---------------|-----------------------|----------------------|
| Request     | Current request        | `request`     | Single request        | Same request only    |
| Session     | Current user session   | `session`     | Multiple requests     | Same user only       |
| Application | Global app-wide data   | `application` | Entire app lifetime   | All users            |

---

## 🧪 Tip

- Use `request` for temporary transfers (e.g., page to page).
- Use `session` for user tracking (e.g., login).
- Use `application` for global counters or shared data.

---
