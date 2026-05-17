# HealthCore - Hospital Management System (HMS)

*A modern ASP.NET Core 8 web application for efficient hospital administration and real-time communication.*

![ASP.NET Core](https://img.shields.io/badge/ASP.NET_Core-8.0-blueviolet)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![SQL Server](https://img.shields.io/badge/Database-SQL_Server-red)
![License](https://img.shields.io/badge/License-MIT-green)
---

HealthCore is a comprehensive, data-driven Hospital Management System (HMS) built with ASP.NET Core 8. It provides a centralized web application for hospital administrators to manage patients, doctors, appointments, and departments. The core of the application is a powerful, interactive dashboard that visualizes key performance metrics in real-time.

---

### 🚀 Live Application

Click below GIF to try live project 👇

<a href="https://healthcore.runasp.net" target="_blank">
  <img src="healthcore.gif" alt="HealthCore Demo Video" width="800">
</a>
<br/>

or


🔗 https://healthcore.runasp.net

<br/>

---

### 🔐 Demo Credentials

```text
Username: Admin
Password: Admin@123
```
⚠️ Note: Demo credentials are for evaluation and testing purposes only.


**[▶ Click here to watch the full system walkthrough video on Google Drive](https://drive.google.com/file/d/1F7bn5GGBvKolZCyMcBUZfSyGEP531Bi-/view?usp=sharing)**

---

## 🚀 Core Features

* **Interactive Dashboard:** A business intelligence dashboard with real-time KPIs (Total Patients, Monthly Revenue, etc.), appointment trends, and performance gauges.
* **Data Visualization:** Uses **ApexCharts** to render dynamic line charts, bar charts (Department Performance), and donut charts (Patient Demographics).
* **Data Export:** Features one-click data export functionality for **Excel** (`.xlsx`), **PDF**, and **CSV** files (powered by `ClosedXML` and `iTextSharp`).
* **Patient Management:** Full CRUD (Create, Read, Update, Delete) operations for patient records. Includes search, filtering, and a detailed profile view.
* **Appointment Management:** Schedule, track, and manage all appointments. Features include advanced filtering (by date, doctor, status) and bulk-delete operations.
* **Doctor & Department Management:** Modules to manage doctor profiles, specializations, and hospital departments.
* **User Management:** A secure section for admins to manage all system users, including the ability to update profile images.
* **Modern UI/UX:** A clean, responsive interface built with **Bootstrap 5**, featuring a **Dark Mode / Light Mode** toggle and non-intrusive toast notifications for user actions.

---
## 📂 Project Structure

Here is a high-level overview of the project's folder structure.

```
HealthCore-HMS/
├── Controllers/       # Handles all HTTP requests and business logic
├── HMS_DB/            # Contains all .sql scripts for database setup
├── Hubs/              # SignalR hub for real-time chat
├── Models/            # C# classes representing data (ViewModels)
├── Properties/        # launchSettings.json (IIS/Kestrel configs)
├── Utils/             # Custom utility classes (e.g., CheckAccess filter)
├── Views/             # All .cshtml files (HTML templates)
│   ├── Shared/        # _Layout.cshtml and other shared views
│   └── ...            # Folders for each controller
├── wwwroot/           # All static assets (CSS, JS, images)
│   ├── assets/        # Custom project CSS, JS, and images
│   ├── Profile/       # Default location for user uploads
│   └── vendor/        # [Ignored] Third-party libraries (Bootstrap, etc.)
├── .gitignore         # Specifies files/folders for Git to ignore
├── appsettings.json   # Configuration (e.g., ConnectionString)
├── HMS.csproj         # Project file (dependencies, .NET version)
├── LICENSE.md         # MIT License file
├── Program.cs         # Main application entry point (service registration)
├── README.md          # This file
└── HMS.sln            # Visual Studio solution file
```
---
## ⚡ Feature Spotlight: Real-time Group Chat with SignalR

A standout feature of HealthCore is its built-in, real-time group chat for administrators.

This allows multiple logged-in users to communicate instantly without page refreshes. This functionality is powered by **ASP.NET Core SignalR**, which uses a Hub-based model to push messages from the server to all connected clients immediately.

---

## 🔧 Tech Stack & Architecture

This project is built on a modern .NET 8 stack, using a traditional MVC (Model-View-Controller) pattern with a custom Data Access Layer (DAL).

* **Backend:** .NET 8, ASP.NET Core MVC (Razor Views)
* **Frontend:** Bootstrap 5, ApexCharts.js, HTML5/CSS3, JavaScript
* **Database:** MS SQL Server
* **Data Access:** ADO.NET (`System.Data.SqlClient`) with raw SQL queries and Stored Procedures.
* **Real-time:** ASP.NET Core SignalR
* **Key Libraries:**

  * `ClosedXML`: For Excel data exports.
  * `iTextSharp`: For PDF data exports.
  * `Newtonsoft.Json`: For advanced JSON handling.

---

## 🔐 Authentication: Custom Session Management

HealthCore uses a custom, lightweight authentication approach built on ASP.NET Core's session management.

1. **Login:** Upon successful login, a `UserID` is stored in the `HttpContext.Session`.
2. **Filter:** A custom `CheckAccess` action filter (implementing `IAuthorizationFilter`) is applied to all protected controllers.
3. **Verification:** This filter runs on every request, checking if `Session.GetString("UserID")` exists.
4. **Redirect:** If the `UserID` is not found in the session, the user is immediately redirected to the login page.

---

## 🏁 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

* .NET 8 SDK
* MS SQL Server (or SQL Server Express)
* SSMS (SQL Server Management Studio) or a similar database tool
* A code editor like Visual Studio 2022

### Installation

1. **Clone the repo**

   ```sh
   git clone https://github.com/Yash-Kakadiya/HealthCore-HMS.git
   cd HealthCore-HMS
   ```

2. **Set up the Database**

   * Open SQL Server Management Studio (SSMS).

   * Create a new, empty database. (e.g., `HMS_DB`).

   * Navigate to the `HMS_DB` folder in the cloned project.

   * Execute the following SQL scripts on your new database **in this specific order**:

     1. `tables.sql` - (Creates all table schemas)
     2. `procedure.sql` - (Creates all stored procedures)
     3. `dashboard.sql` - (Creates dashboard-specific procedures)
     4. `initDB.sql` - (Inserts initial data, e.g., an admin user)

   * **Note:** The `deleteAllRecords.sql` script is an optional utility for development that will clear all data from the tables.

3. **Configure the Connection String**

   * Open the `appsettings.json` file in the project.
   * Find the `ConnectionStrings` section and update the `MyCon` value to point to your local SQL Server instance and the database you just created.

   ```json
   "ConnectionStrings": {
     "MyConnectionString": "Data Source=YOUR_SERVER_NAME;Initial Catalog=HMS_DB;Integrated Security=true;Encrypt=false"
   }
   ```

   *(Remember to replace `YOUR_SERVER_NAME` and `HMS_DB` if you used a different name).*

4. **Build and Run**

   * Open the solution (`.sln`) in Visual Studio and hit `F5`.
   * Or, run the following command in your terminal:

   ```sh
   dotnet run
   ```

   The application will launch, and you can navigate to the login page.

---

## 👨‍💻 Author

**Yash Kakadiya** 
<br/>
💼 Computer Science Student | AI & Business Innovation Enthusiast
<br/>
📍 Rajkot, Gujarat, India 
<br/>
🔗 [GitHub Profile](https://github.com/Yash-Kakadiya)

---

## 🔖 License

This project is licensed under the MIT License - see the `LICENSE` file for details.

---

### 🕿️ Keywords

ASP.NET Core MVC, .NET 8, Hospital Management System, SignalR, Real-Time Chat, HealthCare Software, Dashboard, C#, MS SQL Server, Bootstrap
