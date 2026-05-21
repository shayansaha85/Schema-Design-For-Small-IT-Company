# Database Architecture Documentation

## Database 1: `it_company_internal`

This database manages the company’s internal operations, including employee management, client relationships, project execution, and timesheet tracking.

---

# Module A: Human Resources (HR)

This module manages employees, organizational departments, and reporting structures.

---

## 1. Table: `departments`

Stores the organizational departments within the company.

### Columns

| Column Name  | Data Type    | Constraints                            | Description                                |
| ------------ | ------------ | -------------------------------------- | ------------------------------------------ |
| `id`         | INT          | Primary Key, Auto-Increment            | Unique department identifier               |
| `name`       | VARCHAR(100) | Unique                                 | Department name (e.g., Engineering, Sales) |
| `manager_id` | INT          | Foreign Key → `employees.id`, Nullable | Department manager reference               |

### Dummy Data

| id | name            | manager_id |
| -- | --------------- | ---------- |
| 1  | Engineering     | 2          |
| 2  | Human Resources | NULL       |

---

## 2. Table: `employees`

Stores employee profile and employment information.

### Columns

| Column Name     | Data Type                                | Constraints                    | Description                |
| --------------- | ---------------------------------------- | ------------------------------ | -------------------------- |
| `id`            | INT                                      | Primary Key, Auto-Increment    | Unique employee identifier |
| `first_name`    | VARCHAR(50)                              | NOT NULL                       | Employee first name        |
| `last_name`     | VARCHAR(50)                              | NOT NULL                       | Employee last name         |
| `email`         | VARCHAR(100)                             | Unique                         | Employee email address     |
| `department_id` | INT                                      | Foreign Key → `departments.id` | Associated department      |
| `hire_date`     | DATE                                     | NOT NULL                       | Employee joining date      |
| `status`        | ENUM('Active', 'Terminated', 'On Leave') | NOT NULL                       | Current employment status  |

### Dummy Data

| id | first_name | last_name | email                                       | department_id | hire_date  | status |
| -- | ---------- | --------- | ------------------------------------------- | ------------- | ---------- | ------ |
| 1  | Alice      | Smith     | [alice@itfirm.com](mailto:alice@itfirm.com) | 1             | 2024-01-15 | Active |
| 2  | Bob        | Jones     | [bob@itfirm.com](mailto:bob@itfirm.com)     | 1             | 2023-03-22 | Active |

---

# Module B: CRM & Client Management

This module manages business clients, account ownership, and customer relationship tracking.

---

## 1. Table: `clients`

Stores information about organizations or individuals purchasing company services.

### Columns

| Column Name          | Data Type    | Constraints                  | Description              |
| -------------------- | ------------ | ---------------------------- | ------------------------ |
| `id`                 | INT          | Primary Key, Auto-Increment  | Unique client identifier |
| `company_name`       | VARCHAR(100) | NOT NULL                     | Client organization name |
| `contact_name`       | VARCHAR(100) | NOT NULL                     | Primary point of contact |
| `contact_email`      | VARCHAR(100) | NOT NULL                     | Client contact email     |
| `account_manager_id` | INT          | Foreign Key → `employees.id` | Assigned account manager |

### Dummy Data

| id  | company_name     | contact_name | contact_email                                     | account_manager_id |
| --- | ---------------- | ------------ | ------------------------------------------------- | ------------------ |
| 101 | Acme Retail      | John Doe     | [john@acmeretail.com](mailto:john@acmeretail.com) | 2                  |
| 102 | Zenith Logistics | Clara Oswald | [contact@zenith.log](mailto:contact@zenith.log)   | 2                  |

---

# Module C: Project Management & Timesheets

This module handles software projects, engineering tasks, and time-tracking operations.

---

## 1. Table: `projects`

Stores high-level project information associated with clients.

### Columns

| Column Name  | Data Type     | Constraints                 | Description               |
| ------------ | ------------- | --------------------------- | ------------------------- |
| `id`         | INT           | Primary Key, Auto-Increment | Unique project identifier |
| `client_id`  | INT           | Foreign Key → `clients.id`  | Associated client         |
| `name`       | VARCHAR(150)  | NOT NULL                    | Project name              |
| `budget`     | DECIMAL(12,2) | NOT NULL                    | Allocated project budget  |
| `start_date` | DATE          | NOT NULL                    | Project start date        |
| `end_date`   | DATE          | Nullable                    | Project completion date   |

### Dummy Data

| id  | client_id | name                    | budget   | start_date | end_date   |
| --- | --------- | ----------------------- | -------- | ---------- | ---------- |
| 501 | 101       | E-Commerce Mobile App   | 45000.00 | 2026-02-01 | NULL       |
| 502 | 102       | Cloud Migration Phase 1 | 20000.00 | 2026-01-10 | 2026-04-15 |

---

## 2. Table: `tasks`

Stores project-level tasks, features, issues, or bug tickets.

### Columns

| Column Name   | Data Type                                  | Constraints                            | Description              |
| ------------- | ------------------------------------------ | -------------------------------------- | ------------------------ |
| `id`          | INT                                        | Primary Key, Auto-Increment            | Unique task identifier   |
| `project_id`  | INT                                        | Foreign Key → `projects.id`            | Parent project reference |
| `assigned_to` | INT                                        | Foreign Key → `employees.id`, Nullable | Assigned employee        |
| `title`       | VARCHAR(255)                               | NOT NULL                               | Task title               |
| `status`      | ENUM('To Do', 'In Progress', 'QA', 'Done') | NOT NULL                               | Current task status      |
| `priority`    | ENUM('Low', 'Medium', 'High', 'Critical')  | NOT NULL                               | Task priority level      |

### Dummy Data

| id   | project_id | assigned_to | title                       | status      | priority |
| ---- | ---------- | ----------- | --------------------------- | ----------- | -------- |
| 9001 | 501        | 1           | Setup OAuth2 Authentication | In Progress | High     |
| 9002 | 501        | 2           | Design Database Schema      | Done        | Critical |

---

## 3. Table: `timesheets`

Tracks billable and non-billable engineering work hours.

### Columns

| Column Name    | Data Type    | Constraints                  | Description            |
| -------------- | ------------ | ---------------------------- | ---------------------- |
| `id`           | INT          | Primary Key, Auto-Increment  | Unique timesheet entry |
| `employee_id`  | INT          | Foreign Key → `employees.id` | Employee reference     |
| `task_id`      | INT          | Foreign Key → `tasks.id`     | Related task           |
| `hours_logged` | DECIMAL(4,2) | NOT NULL                     | Hours worked           |
| `work_date`    | DATE         | NOT NULL                     | Work log date          |
| `description`  | TEXT         | Nullable                     | Work summary           |

### Dummy Data

| id    | employee_id | task_id | hours_logged | work_date  | description                     |
| ----- | ----------- | ------- | ------------ | ---------- | ------------------------------- |
| 10001 | 1           | 9001    | 4.50         | 2026-05-20 | Implemented token refresh logic |

---

# Database 2: `it_company_products`

This database manages SaaS offerings, subscription management, and customer support operations.

---

# Module D: Subscriptions & Support

---

## 1. Table: `saas_plans`

Stores SaaS subscription plans offered by the company.

### Columns

| Column Name         | Data Type    | Constraints                 | Description               |
| ------------------- | ------------ | --------------------------- | ------------------------- |
| `id`                | INT          | Primary Key, Auto-Increment | Unique plan identifier    |
| `plan_name`         | VARCHAR(50)  | NOT NULL                    | Subscription plan name    |
| `monthly_price`     | DECIMAL(8,2) | NOT NULL                    | Monthly subscription cost |
| `api_limit_per_day` | INT          | NOT NULL                    | Daily API request limit   |

### Dummy Data

| id | plan_name       | monthly_price | api_limit_per_day |
| -- | --------------- | ------------- | ----------------- |
| 1  | Developer Tier  | 29.00         | 10000             |
| 2  | Enterprise Tier | 499.00        | 1000000           |

---

## 2. Table: `client_subscriptions`

Maps clients to their subscribed SaaS plans.

> **Note:** `client_id` is a logical cross-database reference to `it_company_internal.clients.id`.

### Columns

| Column Name         | Data Type                              | Constraints                   | Description                    |
| ------------------- | -------------------------------------- | ----------------------------- | ------------------------------ |
| `id`                | INT                                    | Primary Key, Auto-Increment   | Unique subscription identifier |
| `client_id`         | INT                                    | Logical Reference             | Reference to internal client   |
| `plan_id`           | INT                                    | Foreign Key → `saas_plans.id` | Selected SaaS plan             |
| `status`            | ENUM('Active', 'Past Due', 'Canceled') | NOT NULL                      | Subscription status            |
| `next_billing_date` | DATE                                   | NOT NULL                      | Upcoming billing date          |

### Dummy Data

| id   | client_id | plan_id | status | next_billing_date |
| ---- | --------- | ------- | ------ | ----------------- |
| 2001 | 101       | 2       | Active | 2026-06-01        |

---

## 3. Table: `support_tickets`

Stores customer support and infrastructure-related issue tickets.

### Columns

| Column Name  | Data Type                                    | Constraints                 | Description                      |
| ------------ | -------------------------------------------- | --------------------------- | -------------------------------- |
| `id`         | INT                                          | Primary Key, Auto-Increment | Unique support ticket identifier |
| `client_id`  | INT                                          | Logical Reference           | Associated client                |
| `subject`    | VARCHAR(200)                                 | NOT NULL                    | Ticket subject                   |
| `severity`   | ENUM('Low', 'Medium', 'High', 'System Down') | NOT NULL                    | Incident severity                |
| `created_at` | TIMESTAMP                                    | NOT NULL                    | Ticket creation timestamp        |

### Dummy Data

| id    | client_id | subject                                    | severity    | created_at          |
| ----- | --------- | ------------------------------------------ | ----------- | ------------------- |
| 40001 | 101       | API endpoints throwing 504 Gateway Timeout | System Down | 2026-05-21 14:20:00 |

---

# Implementation Execution Strategy

To avoid foreign key dependency conflicts during database initialization, follow the execution sequence below.

---

## Step 1: Initialize Databases

Create the databases with `utf8mb4` character encoding support.

```sql
CREATE DATABASE it_company_internal
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;

CREATE DATABASE it_company_products
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
```

---

## Step 2: Build Master Reference Tables

Inside `it_company_internal`, create independent tables first:

* `departments`
* `clients`

At this stage, `manager_id` in `departments` should either remain nullable or be added later through `ALTER TABLE`.

---

## Step 3: Build HR & CRM Dependency Tables

Create the `employees` table and establish its foreign key relationship with `departments.id`.

After populating employee records, safely establish the reverse reference:

```sql
ALTER TABLE departments
ADD CONSTRAINT fk_department_manager
FOREIGN KEY (manager_id)
REFERENCES employees(id);
```

---

## Step 4: Build the Project Management Hierarchy

Create tables in the following dependency order:

1. `projects`
2. `tasks`
3. `timesheets`

This respects the hierarchical structure:

```text
Client → Project → Task → Timesheet
```

---

## Step 5: Deploy Product & Subscription Schema

Switch to the `it_company_products` database and create:

1. `saas_plans`
2. `client_subscriptions`
3. `support_tickets`

The `client_id` field should remain a logical cross-database reference instead of a hard foreign key constraint to maintain schema isolation and improve operational flexibility.
