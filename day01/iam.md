# IAM: Users, Groups, Policies, Roles

Click on each topic to go to the specific section.

<table>
  <tr>
    <th><strong>Topic</strong></th>
    <th><strong>Description</strong></th>
  </tr>
  <tr>
    <td>👤 <a href="iam.md#--iam-users">1. IAM Users</a></td>
    <td>
      <p>- An IAM User is an identity created for an individual to interact with AWS resources.</p>
      <p>- Each user has specific permissions to access AWS services and resources.</p>
      <p>- Users can be part of groups to simplify permissions management.</p>
    </td>
  </tr>
  <tr>
    <td>👥 <a href="iam.md#--iam-groups">2. IAM Groups</a></td>
    <td>
      <p>- IAM Groups are collections of IAM users.</p>
      <p>- You can assign policies to a group, and all users in that group inherit those permissions.</p>
      <p>- Groups help organize users and simplify permissions management.</p>
    </td>
  </tr>
  <tr>
    <td>📜 <a href="iam.md#--iam-policies">3. IAM Policies</a></td>
    <td>
      <p>- IAM Policies define permissions for users, groups, or roles to perform actions on AWS resources.</p>
      <p>- Policies are written in JSON and include actions, resources, and conditions.</p>
      <p>- There are managed policies (AWS pre-defined) and inline policies (user-defined).</p>
    </td>
  </tr>
  <tr>
    <td>🔑 <a href="iam.md#--iam-roles">4. IAM Roles</a></td>
    <td>
      <p>- IAM Roles are identities with permissions to perform actions on AWS resources.</p>
      <p>- Roles are assumed by AWS services, users, or external entities like federated users.</p>
      <p>- Roles allow temporary access to AWS resources, without requiring long-term credentials.</p>
    </td>
  </tr>
</table>

## - IAM Users

An IAM User represents an individual or system that interacts with AWS resources.

### 👤 What are IAM Users?
- IAM Users are entities that represent a person or service who can access AWS services.
- Users can have long-term credentials (passwords, access keys) or temporary credentials (via roles).
- Each user can be assigned different permissions depending on the level of access they require.

### ⚙️ Key Features of IAM Users:
**1. Identity Creation:**
- IAM users are created with a unique username and are assigned permissions to interact with AWS services.

**2. Long-Term & Temporary Credentials:**
- IAM users can have long-term credentials like a password (for the AWS Management Console) or access keys (for AWS CLI or SDKs).
- Temporary credentials can be assigned via IAM roles.

**3. Permissions Management:**
- You can manage access by attaching policies directly to users or assigning them to groups.

### 🌐 Example Use Case:
- A developer can have an IAM user account that grants them permission to launch EC2 instances but restricts access to other AWS resources like RDS or S3.

---

## - IAM Groups

IAM Groups are collections of IAM users, and they allow you to manage permissions for multiple users at once.

### 👥 What are IAM Groups?
- IAM Groups allow you to assign policies to a collection of users rather than individually.
- A group is used to group users who need similar permissions.
- IAM users can be part of multiple groups if needed.

### ⚙️ Key Features of IAM Groups:
**1. Simplified Permission Management:**
- Instead of assigning permissions to individual users, you can assign permissions to the entire group.
- Any user added to a group inherits its permissions.

**2. Organizing Users:**
- Groups help organize users based on roles (e.g., Admins, Developers, ReadOnly) for easier management.

**3. Best Practice:**
- Avoid directly assigning permissions to individual users. Instead, use groups to manage permissions more effectively.

### 🌐 Example Use Case:
- You create an "Admin" group with full access permissions and a "ReadOnly" group with only viewing permissions. Then, you add users to the appropriate groups based on their roles.

---

## - IAM Policies

IAM Policies are JSON documents that define what actions are allowed or denied for a user, group, or role.

### 📜 What are IAM Policies?
- IAM Policies specify the permissions that are granted to a user, group, or role.
- Policies are written in JSON format and can be either managed or inline.

### ⚙️ Key Features of IAM Policies:
**1. Managed Policies:**
- AWS provides pre-defined policies that can be directly attached to users, groups, or roles (e.g., `AdministratorAccess`).

**2. Inline Policies:**
- Inline policies are custom policies created specifically for a user, group, or role. These are directly embedded into the identity.

**3. Permissions Structure:**
- Policies define actions (like `s3:ListBucket`), resources (like `arn:aws:s3:::bucketname`), and conditions (like time of day).

**4. Allow vs. Deny:**
- Policies explicitly allow or deny access. Deny statements override allow statements if both are present.

### 🌐 Example Use Case:
- You create a policy that allows access to an S3 bucket but denies access to any resources in the EC2 service.

---

## - IAM Roles

IAM Roles define a set of permissions that can be assumed by users, applications, or AWS services.

### 🔑 What are IAM Roles?
- IAM Roles are similar to IAM users but are used to delegate access to AWS resources without using long-term credentials.
- Roles are assumed temporarily by entities like EC2 instances, Lambda functions, or federated users.

### ⚙️ Key Features of IAM Roles:
**1. Temporary Access:**
- Roles provide temporary security credentials that grant access to AWS resources.
- These credentials are automatically rotated and expire after a set duration.

**2. Cross-Account Access:**
- Roles can be used to allow access between different AWS accounts without sharing long-term credentials.

**3. Service-Linked Roles:**
- Some AWS services automatically create service-linked roles for their operation, granting necessary permissions.

**4. Trust Policies:**
- A trust policy defines who can assume the role (e.g., EC2 instances, other AWS accounts).

### 🌐 Example Use Case:
- You create a role for an EC2 instance that grants access to an S3 bucket for file storage. The EC2 instance can assume the role and access the bucket, but other instances or users cannot.

---

In summary, IAM is a powerful tool in AWS for managing access to resources. By understanding users, groups, policies, and roles, you can control who can access your AWS environment and what actions they can perform.
