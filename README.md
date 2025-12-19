# Azure Entra ID + RBAC Lab

### Overview
This lab demonstrates the implementation of group-based Role-Based Access Control (RBAC) using Microsoft Entra ID (Azure Active Directory). The goal is to enforce least-privilege access by assigning permissions through security groups at the resource-group scope and validating access through real user sign-ins.

This lab focuses on **authorization** and serves as a foundational identity and access management exercise in Azure.

---

### Objectives
- Create and manage users in Microsoft Entra ID
- Assign users to security groups
- Apply Azure RBAC roles at the resource-group scope
- Validate access differences between Reader and Contributor roles
- Understand the importance of scope and group-based access

---

## Part 1: Create Test Users (Entra ID)
### Step 1: Open Entra ID

- Azure Portal → Microsoft Entra ID

- Go to Users → New user → Create new user

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/6ad41678-a098-4b0e-8576-b774f7bf3625" />

### Step 2: Create User 1 (Read-only)

- Name: lab-reader

- Username: lab-reader@<yourtenant>.onmicrosoft.com

- Password: Auto-generate

- Require password change: Yes

- Create

### Step 3: Create User 2 (Admin-like)

- Name: lab-contributor

- Username: lab-contributor@<yourtenant>.onmicrosoft.com

- Same password settings

- Create

## Part 2: Create Security Groups
### Step 4: Create Groups

- Entra ID → Groups → New group

- Group type: Security

- Group name: rg-readers

- Membership type: Assigned

- Create

Repeat:

- Group name: rg-contributors

### Step 5: Assign Users to Groups

- Add lab-reader → rg-readers

- Add lab-operator → rg-contributors

## Part 3: Create a Target Resource Group
### Step 6: Create Resource Group

- Resource groups → Create

- Name: rg-entra-rbac-lab

- Region: any

- Create

## Part 4: Assign RBAC Roles (The Core)
### Step 7: Assign Reader Role

- Go to Resource groups → rg-entra-rbac-lab

- Access control (IAM) → Add role assignment

- Role: Reader

- Assign access to: User, group, or service principal

- Select: rg-readers

- Assign

### Step 8: Assign Contributor Role

Repeat:

- Role: Contributor

- Assign to: rg-contributors

## Part 5: Validate Permissions
### Step 9: Sign in as lab-reader

- Open Incognito/Private window

- Log in as lab-reader

- Navigate to Azure Portal

- Open rg-entra-rbac-lab

Test actions

- View resources → ✅ Allowed

- Try to create a VM → ❌ Denied

- Try to delete RG → ❌ Denied

### Step 10: Sign in as lab-operator

- Repeat in a new private window.

Test actions

- Create a resource → ✅ Allowed

- Delete resource → ✅ Allowed

- Modify settings → ✅ Allowed
