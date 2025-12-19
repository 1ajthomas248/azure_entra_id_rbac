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

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/94d15e14-5a43-453c-948a-0d4ae374a66a" />

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

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/d5c03ad0-82d2-4f78-8f90-d2fedbc6736d" />

### Step 5: Assign Users to Groups

- Add lab-reader → rg-readers

- Add lab-operator → rg-contributors

## Part 3: Create a Target Resource Group
### Step 6: Create Resource Group

- Resource groups → Create

- Name: rg-entra-rbac-lab

- Region: any

- Create

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/5080569c-daa3-48c0-9ee9-1a9a531de6bd" />

## Part 4: Assign RBAC Roles (The Core)
### Step 7: Assign Reader Role

- Go to Resource groups → rg-entra-rbac-lab

- Access control (IAM) → Add role assignment

- Role: Reader

- Assign access to: User, group, or service principal

- Select: rg-readers

- Assign

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/8608d2b7-3d4a-40ef-ace2-637d1968ea8f" />

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/7d5a5b1b-ef8b-4d57-9ad1-6c82216eb9fd" />

### Step 8: Assign Contributor Role

Repeat:

- Role: Contributor

- Assign to: rg-contributors

## Part 5: Validate Permissions
### Step 9: Sign in as lab-reader

- Open Incognito/Private window

- Log in as lab-reader

- Navigate to Azure Portal

Test actions

- Try to create a resource → ❌ Denied

- Try to delete RG → ❌ Denied

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/8ad68b8d-7f61-43f4-b98e-bc3ce13a6b8b" />

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/3f49ce25-a1ef-4101-a9db-b07c4da84cd0" />

### Step 10: Sign in as lab-operator

- Repeat in a new private window.

Test actions

- Create a resource → ✅ Allowed

- Delete resource → ✅ Allowed

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/b1c42b8d-4c04-4461-be3e-5f62340636b4" />

<img width="512" height="288" alt="image" src="https://github.com/user-attachments/assets/1f512da3-2f63-4aec-9f65-1f66953087f9" />

## Conclusion and Takeways

This lab reinforced the importance of separating identity from authorization and managing access through group-based RBAC rather than individual user assignments. Assigning roles at the resource-group scope demonstrated how least-privilege access can be enforced while still allowing users to perform their required tasks. Validating permissions through real sign-ins highlighted how clearly Azure distinguishes between Reader and Contributor capabilities and emphasized the need to test access rather than assume configuration correctness. Overall, this lab mirrored real enterprise access control patterns and established a strong foundation for implementing more advanced identity and security controls such as Conditional Access and Privileged Identity Management.
