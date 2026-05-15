# Authentication and Authorization: Learn about Pyramid's security features to implement user login systems, permissions, and more.

## Authentication and Authorization in Pyramid

Pyramid security has **two** main ideas:

```text
Authentication = Who are you?
Authorization  = What are you allowed to do?
```

Pyramid provides an optional security system that can identify the current user and check whether that user has access to certain resources. ([Pylons Project][1])

---

## 1. Authentication: “Who is the user?”

`Authentication` means checking the user’s identity.

Example:

```text
User enters email + password
        ↓
Pyramid checks user information
        ↓
If correct, user becomes logged in
```

Real-life example:

```text
University ID card check = Authentication
```

In a Pyramid app, authentication is used for things like:

```text
Login
Logout
Current logged-in user
Session/cookie-based user identity
```

Simple web app example:

```text
Rakib logs in
        ↓
System confirms: This is Rakib
        ↓
Now Pyramid knows the request belongs to Rakib
```

---

## 2. Authorization: “What can this user do?”

Authorization means checking permission.

Example:

```text
Rakib is logged in
        ↓
Can Rakib access admin dashboard?
        ↓
If yes → allow
If no → deny
```

Real-life example:

```text
You may enter university building,
but you may not enter the exam controller room.
```

So:

```text
Login successful ≠ access to everything
```

Authentication only proves identity.
Authorization decides access level.

---

## 3. Authentication vs Authorization

| Topic          | Meaning                    | Example                                    |
| -------------- | -------------------------- | ------------------------------------------ |
| Authentication | Checks who you are         | Login with email/password                  |
| Authorization  | Checks what you can access | Admin can delete users, normal user cannot |

Easy memory:

```text
Authentication = Identity
Authorization = Permission
```

---

## 4. Pyramid Security Flow

When a user visits a protected page, Pyramid security works like this:

```text
User Request
    ↓
Pyramid receives request
    ↓
Security policy checks user identity
    ↓
Pyramid checks required permission
    ↓
If allowed → view runs
    ↓
If denied → forbidden response
```

In Pyramid 2.0, older separate authentication and authorization policies were merged into one **security policy** system. The older policy style still works for compatibility, but it is deprecated. ([Pylons Project][2])

---

## 5. What is a Security Policy?

A **security policy** tells Pyramid how to handle user identity and access decisions.

Simple meaning:

```text
Security policy = rule system for login identity + permission checking
```

It answers questions like:

```text
Who is the current user?
Is the user logged in?
Is this user allowed to access this page?
```

In modern Pyramid, you configure security with APIs like `set_security_policy()`, and Pyramid also provides `request.identity` for accessing the current user identity. ([Pylons Project][2])

---

## 6. What is Permission?

A permission is a named access rule.

Example permissions:

```text
view
edit
delete
admin
create_post
manage_users
```

Example:

```text
Blog reader → view
Blog writer → view + create_post + edit
Admin       → view + create_post + edit + delete + manage_users
```

So in Pyramid, you can protect a view using a permission idea:

```text
Only users with "edit" permission can open the edit page.
```

---

## 7. What is ACL?

**ACL** means:

```text
Access Control List
```

**It is a list of rules that says who can do what.**

Example:

```text
Everyone can view public pages
Logged-in users can create posts
Only admin can delete posts
```

In Pyramid, ACL-based authorization checks permissions against rules attached to a context/resource, and Pyramid has helpers for ACL-style authorization. ([Pylons Project][3])

Simple ACL thinking:

```text
Allow Everyone → view
Allow Authenticated user → comment
Allow Admin → delete
Deny others → restricted
```

---

## 8. Everyone vs Authenticated

Pyramid commonly uses these **two** ideas:

```text
Everyone = any visitor, even not logged in
Authenticated = user who is logged in
```

Pyramid documentation describes `Everyone` and `Authenticated` as built-in principals used in Pyramid applications, especially in ACL-style security examples. ([Pylons Project][4])

Example:

```text
Home page → Everyone can view
Profile page → Only Authenticated users can view
Admin page → Only admin role can view
```

---

## 9. Role-Based Access

For real apps, we often use roles.

Example roles:

```text
admin
teacher
student
editor
user
guest
```

Example permission design:

| Role   | Access                         |
| ------ | ------------------------------ |
| Guest  | View homepage only             |
| User   | View profile, edit own account |
| Editor | Create and edit content        |
| Admin  | Manage users and delete data   |

Pyramid’s official tutorial shows role-style permissions such as users having roles like `editor` or `basic`, often represented as role principals like `role:editor`. ([Pylons Project][4])

---

## 10. Login System Flow in Pyramid

A normal login system works like this:

```text
User opens login page
        ↓
User submits username/password
        ↓
View checks database
        ↓
If correct, Pyramid stores user identity in session/cookie
        ↓
User becomes logged in
        ↓
Protected pages become accessible
```

Logout flow:

```text
User clicks logout
        ↓
Pyramid clears session/cookie identity
        ↓
User becomes anonymous again
```

---

## 11. Full Security Architecture

```text
Browser Request
      ↓
Route
      ↓
Security Policy
      ↓
Check Identity
      ↓
Check Permission
      ↓
View Function
      ↓
Response
```

More detailed:

```text
User visits /admin
      ↓
Pyramid checks route
      ↓
Route says: admin_view needs "admin" permission
      ↓
Security policy checks current user
      ↓
User role = normal user
      ↓
Permission denied
      ↓
403 Forbidden response
```

---

## 12. Example Scenario: Student Management App

Suppose we build a Pyramid Student Management System.

Pages:

```text
/login
/students
/students/add
/students/edit/1
/students/delete/1
/admin/users
```

Security design:

```text
Everyone:
- Can open login page

Student:
- Can view own profile

Teacher:
- Can view student list
- Can add marks

Admin:
- Can add/edit/delete students
- Can manage users
```

Flow:

```text
Admin logs in
      ↓
Admin opens /students/delete/1
      ↓
Pyramid checks permission
      ↓
Admin has delete permission
      ↓
Delete view runs
```

But:

```text
Normal student opens /students/delete/1
      ↓
Pyramid checks permission
      ↓
Student does not have delete permission
      ↓
Access denied
```

---

## 13. Why Pyramid Security is Flexible

Pyramid does not force only one login style.

You can build:

```text
Session-based login
Cookie-based login
Database user login
Role-based permission
ACL-based permission
JWT token-based API login
Custom security policy
```

This flexibility is one reason Pyramid is useful for both small and large applications. Pyramid’s security system is optional and declarative, meaning you add security rules when your app needs them. ([Pylons Project][1])

---

# Main Summary

```text
Authentication = checks user identity
Authorization = checks user permission
Security Policy = controls identity + access rules
Permission = named access right
ACL = list of allow/deny rules
Role = user category like admin, editor, student
```

Best memory line:

```text
In Pyramid, authentication tells who the user is, and authorization decides what that user can access.
```

For our future project, the best simple security plan will be:

```text
User login
Admin role
Normal user role
Protected dashboard
CRUD permission control
```

[1]: https://docs.pylonsproject.org/projects/pyramid/en/latest/narr/security.html?utm_source=chatgpt.com "Security — The Pyramid Web Framework v2.1"
[2]: https://docs.pylonsproject.org/projects/pyramid/en/latest/whatsnew-2.0.html?utm_source=chatgpt.com "What's New in Pyramid 2.0"
[3]: https://docs.pylonsproject.org/projects/pyramid/en/latest/api/authorization.html?utm_source=chatgpt.com "pyramid.authorization — The Pyramid Web Framework v2.1"
[4]: https://docs.pylonsproject.org/projects/pyramid/en/latest/tutorials/wiki2/authorization.html?utm_source=chatgpt.com "Adding authorization — The Pyramid Web Framework v2.1"
