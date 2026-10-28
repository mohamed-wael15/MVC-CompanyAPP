# Company Management System — ASP.NET Core MVC

An employee and department management web app built with **ASP.NET Core 8 MVC** as a **training project**.
It covers CRUD screens, ASP.NET Core Identity with role-based access, and a layered structure
with a Unit of Work and AutoMapper.

`C#` · `ASP.NET Core 8 MVC` · `Razor` · `EF Core` · `SQL Server` · `ASP.NET Core Identity` · `AutoMapper`

---

## Features

- **Departments** — list, create, view, update, delete
- **Employees** — list with search by name, and create with a profile image upload and a department
- **Accounts** — sign up, log in, log out, forgot / reset password by email
- **Users** *(Admin only)* — list with search, view, update, delete
- **Roles** *(Admin only)* — create, update, delete roles, and add or remove users from a role
- All pages require a logged-in user; users and roles are restricted to the `Admin` role

---

## Architecture

```
Company.Web         → MVC controllers, views, view models, Identity setup
Company.Service     → services for employees and departments, DTOs, AutoMapper profiles, file upload and email helpers
Company.Repository  → generic repository and Unit of Work over EF Core
Company.Data        → entities (Employee, Department, ApplicationUser), DbContext, migrations
```

---

## Running locally

**Prerequisites:** .NET 8 SDK and SQL Server (or LocalDB).

```bash
git clone https://github.com/mohamed-wael15/MVC-CompanyAPP.git
cd MVC-CompanyAPP
```

1. Check the `DefaultConnection` string in `Company.Web/appsettings.json`. It uses a local SQL Server instance with Windows authentication.
2. Create the database:

   ```bash
   dotnet ef database update --project Company.Data --startup-project Company.Web
   ```

   or `Update-Database` from the Package Manager Console in Visual Studio.
3. Run the app:

   ```bash
   dotnet run --project Company.Web
   ```

---

## Notes

- This is a learning project and has no automated tests.
- Employee details, update and delete exist in the service layer but have no screens yet.
- The password-reset email needs SMTP settings. They are left empty in `Company.Service/Helper/EmailSettings.cs`, so that feature will not send emails until they are filled in.
- The admin pages require a user in the `Admin` role, which is not seeded. Assign it to a user in the database first.
