# EXTRA-credit-CI-CD

## Branching Strategy – GitFlow

*Overview*  
We use GitFlow to manage our code releases and ensure production stability.

*Branch Types*  
**Main Branches**  
- **main**: Production-ready code only. Every commit here should be deployable.  
- **develop**: Integration branch where features come together for testing.

**Supporting Branches**  
- **feature/***: New features and non-emergency bug fixes  
  - Branch from: **develop**  
  - Merge to: **develop**  
  - Naming: `feature/description-of-feature`

- **release/***: Prepare new production releases  
  - Branch from: **develop**  
  - Merge to: **main** and **develop**  
  - Naming: `release/version-number`

- **hotfix/***: Emergency fixes for production  
  - Branch from: **main**  
  - Merge to: **main** and **develop**  
  - Naming: `hotfix/critical-issue-description`

*Workflow Process*  
1. **For New Features**  
   - Create `feature/...` branch from **develop**  
   - Develop and test your feature locally  
   - Open a Pull Request → **develop**  
   - Code review (≥1 approval) + CI must pass  
   - Merge into **develop** and delete the `feature/...` branch  

2. **For Releases**  
   - Create `release/...` from **develop**  
   - Final testing & bug fixes on `release/...`  
   - Open a Pull Request → **main** (CI + ≥1 approval required)  
   - Merge into **main** with a version tag  
   - Merge **main** back into **develop**  
   - Delete the `release/...` branch  
   - Deploy from **main**  

3. **For Hotfixes**  
   - Create `hotfix/...` from **main**  
   - Fix the bug, commit, and push  
   - Open a Pull Request → **main** (CI + ≥1 approval required)  
   - Merge into **main** (now production is fixed)  
   - Tag a new hotfix release on **main** (e.g., `v1.2.1`)  
   - Merge **main** back into **develop** so the fix lives in future releases  
   - Delete the `hotfix/...` branch  

*Protection Rules*  
- **main** and **develop** are protected branches.  
  - All changes must go through Pull Requests.  
  - CI/CD pipeline must pass before merge.  
  - Minimum one reviewer approval required.  
