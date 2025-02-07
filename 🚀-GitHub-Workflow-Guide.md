This document outlines the workflow for development, code review, testing, and deployment using GitHub features like **Pull Requests (PRs)**, **branching**, **issues**, and **GitHub Projects**.

---

## 🌿 Branching Strategy  
- **`main` Branch**: Contains the latest stable version of the code.  
- **`staging` Branch**: Used for testing features before merging into the `main` branch.  
- **Feature Branch**: Created for every new task/issue using the format:  
  **`issueid-issuename`** (e.g., `123-add-login-feature`).

---

## 🛠️ Workflow Steps  

### 1️⃣ Creating a New Feature Branch  
- Create a feature branch from the `main` branch using the naming format:  
  **`issueid-issuename`**  
- Push your changes and commit regularly.  

### 2️⃣ Development and Pull Request (PR)  
- When development is complete, create a **Pull Request (PR)** from the **feature branch** to `main`.  
- Add reviewers for code review.  

### 3️⃣ 🔍 Code Review  
- Reviewers provide feedback on the PR.  
- After incorporating feedback, update the PR if needed.  

### 4️⃣ Merging to Staging for Testing  
- Once the PR is approved, merge the **feature branch** into the **staging branch** (for both backend and frontend).  
- Move the corresponding GitHub Project issue to the **Ready for Testing** column.  

### 5️⃣ 🧪 Testing  
- The testing team or responsible person tests the feature in the staging environment.  
- If the feature passes testing, move the GitHub Project issue to **Ready for Production**.  
- If issues are found, move the task back to **To Do** with comments for fixes.  

### 6️⃣ 🚢 Production Deployment  
- The person with deployment permissions merges the `main` branch into:  
  - **`production` (backend)**  
  - **`deploy` (frontend)**  
- This deploys the code to production.  
- Move the corresponding GitHub Project issue to **Done**.  

---

## 📊 GitHub Project Board Workflow  

### Columns & Status Explanation  

- **🆕 New**: New issues/tasks are added here.  
- **📋 To Do**:  
  - Tasks that need changes after comments.  
  - Reopened issues or tasks that failed in testing.  
- **🚧 In Progress**: Tasks currently being worked on by the developer.  
- **👀 In Review**: PR has been raised for review.  
- **🛠️ Ready for Testing**: After merging the feature branch to `staging`, tasks are moved here for testing.  
- **🔍 In Testing**: The testing team verifies the feature in the staging environment.  
- **✅ Ready for Production**: Tasks that are tested and approved for production deployment.  
- **🏁 Done**: Tasks successfully deployed to production and marked as complete.  

---

## 📑 Summary of Key Steps  

1. **Create a feature branch** from `main`.  
2. **Develop and commit code** on the feature branch.  
3. **Raise a Pull Request** to `main`.  
4. **Code Review** and incorporate feedback.  
5. **Merge to `staging`** for testing.  
6. **Test in the staging environment**.  
7. **Merge to `main`** after successful testing.  
8. **Production Deployment** by merging `main` to `production` (backend) and deploying on `frontend`.  
9. **Mark the issue as Done** in the GitHub Project.  
