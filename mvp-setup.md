# MVP Setup To-Do (ASP.NET with TDD)

This checklist focuses on preparing the development environment, setting up Test-Driven Development (TDD), and laying the groundwork for our MVP.

---

## âœ… Environment Setup
- [ ] Install **.NET 8 SDK** (or latest stable version)
- [ ] Set up IDE (**Visual Studio 2022** or **Rider / VS Code**)
- [ ] Install **xUnit** or **NUnit** for testing
- [ ] Install **Moq** for mocking dependencies
- [ ] Install **coverlet** for code coverage
- [ ] Configure **Git** and create repository

---

## âœ… Solution Setup
- [ ] Create a new **ASP.NET Web API project**
- [ ] Create a **Class Library project** for core domain logic
- [ ] Create a **Unit Test project**
- [ ] Add project references
- [ ] Setup dependency injection in `Program.cs`
- [ ] Setup `appsettings.json` for environment configs

---

## âœ… TDD Workflow Setup
- [ ] Write first failing test for a **HealthCheck endpoint**
- [ ] Implement the HealthCheck controller to pass the test
- [ ] Refactor code and keep tests green
- [ ] Configure **test pipeline** (dotnet test)

---

## âœ… Use Case: User Event Logging
### Example Flow
- [ ] **Test Case 1**: Save new event (Expected â†’ returns success)
- [ ] **Test Case 2**: Missing fields (Expected â†’ returns validation error)
- [ ] **Test Case 3**: Offline mode save (Expected â†’ stored in local DB)
- [ ] **Test Case 4**: Sync events once online (Expected â†’ data pushed to server)

---

## âœ… CI/CD Initial Setup (Optional for MVP)
- [ ] Setup GitHub Actions or Azure DevOps pipeline
- [ ] Run unit tests on every PR
- [ ] Generate test coverage reports