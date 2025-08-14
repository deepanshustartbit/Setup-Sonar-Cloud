# 🛠️ Setup SonarCloud for .NET Projects

This repository provides a complete step-by-step guide to:

- ✅ **Creating a new .NET project**
- ☁️ **Setting up SonarCloud.io** for code analysis
- 📊 **Enabling code coverage reporting** and quality checks

> 📁 A complete document is available in the `File` folder — you can download and refer to it for your convenience.

---

## 📌 How to Set Up a Sonar Project on SonarCloud

### ✅ Create a .NET Project

1. Open **Visual Studio** and create a new project.
2. Select your project type (e.g., **MVC**).
3. Enter the **project name** and choose the appropriate **.NET version**.
4. Click **Create** to generate the project.

---

### ✅ Add Unit Test Project

1. In **Solution Explorer**, right-click on the solution → `Add > New Project`.
2. Select **xUnit Test Project**.
3. Name the project ending with `.Tests` (e.g., `SampleApp.Tests`).
4. The unit test project will now appear in the solution.

---

### ✅ Create a Method and Unit Test

1. Create a method in `HomeController.cs` in your main project.
2. In the test project, create a folder named `Controllers`.
3. Inside it, create a file `HomeControllerTest.cs`.
4. Add a reference from the test project to the main project:
   - Right-click test project → `Add > Reference...` → Select main project.

---

### ✅ Install Required NuGet Package

Install the following package in the test project:

```bash
dotnet add package coverlet.msbuild --version 6.0.4
```

---

### ✅ Write a Test Using `[Fact]`

Example structure of a unit test:

```csharp
[Fact]
public void Index_ReturnsCorrectView()
{
    // Arrange

    // Act

    // Assert
}
```

Use `[Fact]` for simple test methods, and `[Theory]` for tests with multiple inputs and conditions.

---

## ☁️ Setup Project on SonarCloud.io

### 1. **Create an Account and Organization**

- Go to [SonarCloud.io](https://sonarcloud.io) and log in with **GitHub** or manually.
- Click **My Organization** → **Create**.
- Choose your plan (free trial is available).
- Click **Analyze a New Project**.

### 2. **Create a New Project**

- Enter your project display name.
- Set the new code condition (e.g., "Previous Version").
- Click **Create Project**.

---

## 🔧 Configure and Run SonarCloud Analysis

### 1. **Install Coverlet**

```bash
dotnet add package coverlet.msbuild --version 6.0.4
```

### 2. **Generate Coverage File**

```bash
dotnet test YourProject.Tests/YourProject.Tests.csproj `
  /p:CollectCoverage=true `
  /p:CoverletOutput=../TestResults/ `
  /p:CoverletOutputFormat=opencover
```

> 🔁 Replace `YourProject.Tests` with your actual test project name.

---

### 3. **Run SonarScanner Begin Command**

```bash
dotnet sonarscanner begin `
  /k:"your_project_key" `
  /o:"your_organization_key" `
  /d:sonar.login="your_generated_token" `
  /d:sonar.cs.opencover.reportsPaths="TestResults/coverage.opencover.xml"
```

> 🔑 Generate your **SonarCloud token** from:  
> **My Organization → Security → Generate Token**

---

### 4. **Build and Test the Project**

```bash
dotnet build
```

```bash
dotnet test YourProject.Tests/YourProject.Tests.csproj `
  /p:CollectCoverage=true `
  /p:CoverletOutput=../TestResults/ `
  /p:CoverletOutputFormat=opencover
```

---

### 5. **Run SonarScanner End Command**

```bash
dotnet sonarscanner end /d:sonar.login="your_generated_token"
```

---

### ✅ Done!

- Go to your project on [SonarCloud.io](https://sonarcloud.io).
- You will now see your **code quality analysis** and **coverage report**.

---

## 📄 Screenshots

Add screenshots of the setup or reports here for clarity (optional):

```markdown
![SonarCloud Setup](assets/sonarcloud-setup.png)
```

