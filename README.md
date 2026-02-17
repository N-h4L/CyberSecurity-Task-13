# Task 13: Secure API Testing & Authorization Validation

## Overview

This task demonstrates Secure API Testing and Authorization Validation using Postman and cURL in a Kali Linux environment. The objective was to analyze REST API security by testing authentication, authorization, input validation, and rate limiting controls.

API security testing is essential because APIs are commonly used in web and mobile applications and are frequent targets for cyber attacks.

---

## Objective

- Understand REST API functionality and HTTP methods (GET, POST, DELETE)
- Test API endpoints using Postman
- Identify authentication and authorization weaknesses
- Perform input validation testing
- Test for broken authorization vulnerabilities (IDOR)
- Perform rate limiting testing
- Map findings to OWASP API Security Top 10

---

## Tools Used

- Postman – API testing tool
- cURL – Command-line HTTP testing tool
- Kali Linux – Testing operating system
- VirtualBox – Virtualization platform
- JSONPlaceholder API – Public testing API

---

## Testing Environment

- Host OS: Windows 11
- Virtual Machine: VirtualBox
- Guest OS: Kali Linux
- API Tool: Postman
- Network Configuration: NAT

---

## API Endpoint Used

Base URL:

```
https://jsonplaceholder.typicode.com
```

Endpoints Tested:

```
GET /users/1
POST /users
DELETE /users/1
GET /users/2
GET /users/3
```

---

## Testing Methodology

### 1. GET Request Testing

Purpose: Retrieve user information from the API.

Request:

```
GET https://jsonplaceholder.typicode.com/users/1
```

Result:

- Status Code: 200 OK
- User data successfully retrieved
- No authentication required

Security Observation:

- API allows access without authentication

---

### 2. POST Request Testing

Purpose: Test resource creation and input handling.

Request:

```
POST https://jsonplaceholder.typicode.com/users
```

Request Body:

```json
{
  "name": "Nihal",
  "role": "Cyber Security Intern"
}
```

Result:

- Status Code: 201 Created
- Resource successfully created

Security Observation:

- API accepts input without authentication validation

---

### 3. Authorization Testing (IDOR Test)

Purpose: Test access control by modifying user IDs.

Requests Tested:

```
GET /users/1
GET /users/2
GET /users/3
```

Result:

- All user records accessible
- No authorization enforcement

Security Observation:

- Broken Object Level Authorization vulnerability

---

### 4. DELETE Request Testing

Purpose: Test function-level authorization.

Request:

```
DELETE https://jsonplaceholder.typicode.com/users/1
```

Result:

- Status Code: 200 OK
- Delete request accepted

Security Observation:

- API allows sensitive operations without authentication

---

### 5. Input Validation Testing

Purpose: Test handling of malicious input.

Request Body:

```json
{
  "name": "<script>alert('XSS')</script>",
  "role": "' OR 1=1 --"
}
```

Result:

- Status Code: 201 Created
- Malicious input accepted

Security Observation:

- Lack of input validation controls

---

### 6. Missing Authentication Testing

Purpose: Verify authentication enforcement.

Observation:

- API endpoints accessible without authentication headers

Security Observation:

- Broken Authentication vulnerability

---

### 7. Rate Limiting Testing

Command used:

```bash
for i in {1..50}; do curl https://jsonplaceholder.typicode.com/users/1; done
```

Result:

- All requests processed successfully
- No blocking or rate limiting

Security Observation:

- No rate limiting implemented

---

## OWASP API Security Top 10 Mapping

| Vulnerability | OWASP Category | Description |
|--------------|----------------|-------------|
| No authentication required | API2: Broken Authentication | API allows access without verifying identity |
| Access to other user IDs | API1: Broken Object Level Authorization | Unauthorized access to resources |
| DELETE allowed without auth | API5: Broken Function Level Authorization | Sensitive operations allowed |
| Malicious input accepted | API10: Unsafe Consumption of APIs | Improper input validation |
| No rate limiting | API4: Unrestricted Resource Consumption | Vulnerable to DoS attacks |

---

## Security Risks Identified

- Broken Authentication
- Broken Object Level Authorization
- Broken Function Level Authorization
- Lack of Input Validation
- Missing Rate Limiting Controls

---

## Conclusion

This task demonstrated practical API security testing using Postman and Kali Linux. Multiple security weaknesses were identified, including lack of authentication, authorization flaws, and missing rate limiting controls.

This exercise helped develop hands-on skills in:

- API security testing
- Vulnerability identification
- OWASP API risk mapping
- Security analysis and documentation

These skills are essential for Cyber Security Analysts, SOC Analysts, and Penetration Testers.

---

## Screenshots

Screenshots of all test cases are available in the screenshots folder.

---

## Author

Mohammed Nihal  
Cyber Security Intern  
Kali Linux | Postman | API Security Testing
