# Git History Cleanup – Removing Sensitive `.env` File

## Overview

This repository demonstrates the process of identifying and removing a sensitive `.env` file that was accidentally committed to version control. The `.env` file contained confidential information such as API keys and database credentials, which posed a critical security risk.

The objective was to completely remove the file from the repository history and implement best practices to prevent similar issues in the future.

---

## Problem Statement

A developer accidentally committed a `.env` file containing sensitive secrets. The security team flagged this as a critical issue. The required tasks were:

1. Identify when the `.env` file was first added to the repository.
2. Remove the `.env` file from **all commits in the Git history**.
3. Ensure the file is permanently deleted and cannot be recovered from previous commits.
4. Add safeguards to prevent future accidental commits of environment files.
5. Provide a template for environment configuration without exposing secrets.
6. Push the cleaned repository to GitHub.

---

## Steps Performed

### 1. Investigated Repository History

Used Git commands to locate the commit where the `.env` file was introduced:

```
git log --diff-filter=A -- .env
```

This identified the exact commit responsible for adding the sensitive file.

---

### 2. Removed `.env` from Entire Git History

Rewrote the repository history using `git filter-repo` to remove the `.env` file from every commit:

```
git filter-repo --path .env --invert-paths
```

This ensured that the secrets were permanently removed from the repository.

---

### 3. Verified Removal

Confirmed that the `.env` file no longer existed in any commit:

```
git log --all -- .env
```

---

### 4. Implemented Preventive Measures

Created a `.gitignore` file and added:

```
.env
```

This prevents environment files from being tracked in future commits.

---

### 5. Added `.env.example`

Created a `.env.example` file containing placeholder values for required environment variables. This allows developers to understand configuration requirements without exposing real credentials.

Example:

```
API_KEY=your_api_key_here
DB_HOST=your_db_host_here
DB_USER=your_db_user_here
DB_PASSWORD=your_db_password_here
```

---

### 6. Committed and Pushed Changes

Committed the cleanup and best-practice files, then force-pushed the rewritten history to GitHub:

```
git push origin main --force
```

---

## Security Note

Even after removing the `.env` file from history, any exposed credentials should always be considered compromised. In real-world scenarios, all secrets must be rotated immediately.

---

## Key Learnings

* Sensitive files should never be committed to version control.
* `.gitignore` is essential for protecting environment configurations.
* Git history can be rewritten to remove confidential data if mistakes occur.
* Providing `.env.example` improves collaboration without risking security.
* Force pushing is required after rewriting Git history.

---

## Repository Purpose

This project serves as a practical demonstration of:

* Git forensic investigation
* Secure repository cleanup
* Version control best practices
* Incident response for exposed secrets

---
