# 🎓 3-Tier RESTful Student API with DB

## Overview

This project implements a **3-Tier RESTful Student API** architecture that demonstrates professional software design patterns. It provides complete CRUD operations for student management with a clean separation of concerns across three distinct layers: Data Access, Business Logic, and API Controller layers.

## Architecture

### 1. Data Access Layer (StudentData.cs)

The Data Access Layer handles all direct database interactions using SQL Server. It encapsulates database connectivity and SQL operations, protecting the rest of the application from database-specific details.

**Key Responsibilities:**
- 🔗 Manages SQL Server connections using `SqlConnection`
- 🛠️ Executes stored procedures for all database operations
- 📦 Returns `StudentDTO` objects to higher layers
- 📋 Implements methods for: GetAllStudents, GetPassedStudents, GetAverageGrade, GetStudentById, AddStudent, UpdateStudent, DeleteStudent

**Database Connection:**
- 🔒 Uses stored procedures for secure and optimized database access
- 🌐 Connection string configured for SQL Server with proper authentication

### 2. Business Logic Layer (StudentAPIBusinessLayer)

The Business Logic Layer acts as the intermediary between the API Controller and Data Access Layer. It enforces business rules, validates data, and coordinates operations.

**Key Responsibilities:**
- 📏 Implements business rules and validation logic
- 🔄 Converts between `StudentDTO` (data layer) and `Student` (business objects)
- ⚙️ Orchestrates complex operations across the data layer
- ✅ Ensures data consistency and integrity
- 📡 Provides a clean interface for the API layer to consume

**Design Benefits:**
- 🔄 Decouples API controllers from database details
- 🛠️ Centralizes business logic for easier maintenance
- 🔄 Allows business rule changes without modifying API code

### 3. API Controller Layer (StudentsController.cs)

The API Controller Layer exposes RESTful endpoints for client applications. It handles HTTP requests, delegates operations to the business layer, and returns appropriate responses.

**API Endpoints:**
- 📜 `GET /api/Students/All` - Retrieve all students
- 🎓 `GET /api/Students/Passed` - Retrieve students who passed (Grade ≥ 50)
- 📊 `GET /api/Students/AverageGrade` - Get average grade across all students
- 🔍 `GET /api/Students/{id}` - Retrieve a specific student
- ➕ `POST /api/Students` - Create a new student
- 🔄 `PUT /api/Students/{id}` - Update student information
- ❌ `DELETE /api/Students/{id}` - Delete a student

**Response Handling:**
- 📜 Uses `ProducesResponseType` attributes for OpenAPI documentation
- 📈 Returns appropriate HTTP status codes (200, 201, 400, 404)
- ✅ Implements input validation before business layer delegation

## User Manual

### Prerequisites
- **.NET 8.0+** or compatible version
- **SQL Server** (LocalDB or full instance)
- **Visual Studio 2022** or VS Code with C# extensions
- **Git** for cloning the repository

### Step-by-Step Installation & Setup

#### 1. Clone the Repository
```bash
git clone <repository-url>
cd "3-Tier RESTful Student API with DB"
```

#### 2. Database Setup
- 🛠️ Open SQL Server Management Studio (SSMS)
- 📦 Create a new database named `StudentsDB`
- 📋 Create the `Students` table and required stored procedures:
    - `SP_GetAllStudents`
    - `SP_GetPassedStudents`
    - `SP_GetAverageGrade`
    - `SP_GetStudentById`
    - `SP_AddStudent`
    - `SP_UpdateStudent`
    - `SP_DeleteStudent`

#### 3. Configure Connection String
- 🔍 Open `StudentData.cs` in the Data Access Layer
- ✏️ Update the `_connectionString` with your SQL Server instance details
- 🔑 Ensure credentials match your local SQL Server setup

#### 4. Build the Solution
```bash
dotnet build
```

#### 5. Run the API Server
```bash
cd StudentRestAPI
dotnet run
```

The API will be accessible at `https://localhost:5001` or `http://localhost:5000`

#### 6. Test the API
- 🧪 Use **Postman**, **Thunder Client**, or **curl** to test endpoints
- 📖 The API provides Swagger/OpenAPI documentation at `/swagger`
- 🔍 Example GET request: `GET https://localhost:5001/api/Students/All`

### Troubleshooting
- ❗ **Connection Issues:** Verify SQL Server is running and credentials are correct
- ⚠️ **Port Conflicts:** Check if ports 5000/5001 are available
- ❌ **Missing Stored Procedures:** Ensure all required SPs exist in the database
