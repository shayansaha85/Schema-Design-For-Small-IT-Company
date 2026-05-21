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

| Column Name  | Data Type    | Constraints                            | Description                  |
| ------------ | ------------ | -------------------------------------- | ---------------------------- |
| `id`         | INT          | Primary Key, Auto-Increment            | Unique department identifier |
| `name`       | VARCHAR(100) | Unique                                 | Department name              |
| `manager_id` | INT          | Foreign Key → `employees.id`, Nullable | Department manager reference |

### Dummy Data

| id | name              | manager_id |
| -- | ----------------- | ---------- |
| 1  | Engineering       | 2          |
| 2  | Human Resources   | 3          |
| 3  | Finance           | 4          |
| 4  | Sales             | 5          |
| 5  | Marketing         | 6          |
| 6  | Operations        | 7          |
| 7  | Legal             | 8          |
| 8  | DevOps            | 9          |
| 9  | Security          | 10         |
| 10 | Product           | 11         |
| 11 | Support           | 12         |
| 12 | Research          | 13         |
| 13 | QA                | 14         |
| 14 | Data Science      | 15         |
| 15 | Cloud Engineering | 16         |
| 16 | Procurement       | 17         |
| 17 | Administration    | 18         |
| 18 | Customer Success  | 19         |
| 19 | Training          | 20         |
| 20 | Analytics         | NULL       |

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

| id | first_name | last_name | email                                             | department_id | hire_date  | status     |
| -- | ---------- | --------- | ------------------------------------------------- | ------------- | ---------- | ---------- |
| 1  | Alice      | Smith     | [alice@itfirm.com](mailto:alice@itfirm.com)       | 1             | 2024-01-15 | Active     |
| 2  | Bob        | Jones     | [bob@itfirm.com](mailto:bob@itfirm.com)           | 1             | 2023-03-22 | Active     |
| 3  | Charlie    | Brown     | [charlie@itfirm.com](mailto:charlie@itfirm.com)   | 2             | 2022-05-10 | On Leave   |
| 4  | David      | Wilson    | [david@itfirm.com](mailto:david@itfirm.com)       | 3             | 2021-11-18 | Active     |
| 5  | Emma       | Taylor    | [emma@itfirm.com](mailto:emma@itfirm.com)         | 4             | 2020-07-09 | Terminated |
| 6  | Frank      | Miller    | [frank@itfirm.com](mailto:frank@itfirm.com)       | 5             | 2023-09-14 | Active     |
| 7  | Grace      | Moore     | [grace@itfirm.com](mailto:grace@itfirm.com)       | 6             | 2022-02-20 | Active     |
| 8  | Henry      | Jackson   | [henry@itfirm.com](mailto:henry@itfirm.com)       | 7             | 2021-12-01 | On Leave   |
| 9  | Isabella   | Martin    | [isabella@itfirm.com](mailto:isabella@itfirm.com) | 8             | 2024-03-11 | Active     |
| 10 | Jack       | White     | [jack@itfirm.com](mailto:jack@itfirm.com)         | 9             | 2020-06-28 | Active     |
| 11 | Karen      | Harris    | [karen@itfirm.com](mailto:karen@itfirm.com)       | 10            | 2022-08-15 | Active     |
| 12 | Liam       | Thompson  | [liam@itfirm.com](mailto:liam@itfirm.com)         | 11            | 2021-01-05 | Terminated |
| 13 | Mia        | Garcia    | [mia@itfirm.com](mailto:mia@itfirm.com)           | 12            | 2024-04-09 | Active     |
| 14 | Noah       | Martinez  | [noah@itfirm.com](mailto:noah@itfirm.com)         | 13            | 2023-10-12 | Active     |
| 15 | Olivia     | Robinson  | [olivia@itfirm.com](mailto:olivia@itfirm.com)     | 14            | 2022-06-30 | On Leave   |
| 16 | Peter      | Clark     | [peter@itfirm.com](mailto:peter@itfirm.com)       | 15            | 2020-09-17 | Active     |
| 17 | Quinn      | Lewis     | [quinn@itfirm.com](mailto:quinn@itfirm.com)       | 16            | 2021-07-25 | Active     |
| 18 | Ryan       | Walker    | [ryan@itfirm.com](mailto:ryan@itfirm.com)         | 17            | 2023-02-19 | Active     |
| 19 | Sophia     | Hall      | [sophia@itfirm.com](mailto:sophia@itfirm.com)     | 18            | 2022-11-08 | Active     |
| 20 | Thomas     | Allen     | [thomas@itfirm.com](mailto:thomas@itfirm.com)     | 19            | 2024-05-01 | Active     |

---

# Module B: CRM & Client Management

## 1. Table: `clients`

### Columns

| Column Name          | Data Type    | Constraints                  | Description              |
| -------------------- | ------------ | ---------------------------- | ------------------------ |
| `id`                 | INT          | Primary Key, Auto-Increment  | Unique client identifier |
| `company_name`       | VARCHAR(100) | NOT NULL                     | Client organization name |
| `contact_name`       | VARCHAR(100) | NOT NULL                     | Primary point of contact |
| `contact_email`      | VARCHAR(100) | NOT NULL                     | Client contact email     |
| `account_manager_id` | INT          | Foreign Key → `employees.id` | Assigned account manager |

### Dummy Data

| id  | company_name      | contact_name     | contact_email                                             | account_manager_id |
| --- | ----------------- | ---------------- | --------------------------------------------------------- | ------------------ |
| 101 | Acme Retail       | John Doe         | [john@acmeretail.com](mailto:john@acmeretail.com)         | 2                  |
| 102 | Zenith Logistics  | Clara Oswald     | [contact@zenith.com](mailto:contact@zenith.com)           | 3                  |
| 103 | Nova Systems      | Ethan Hunt       | [ethan@nova.com](mailto:ethan@nova.com)                   | 4                  |
| 104 | BluePeak Tech     | Sarah Connor     | [sarah@bluepeak.com](mailto:sarah@bluepeak.com)           | 5                  |
| 105 | Delta Networks    | Bruce Wayne      | [bruce@delta.com](mailto:bruce@delta.com)                 | 6                  |
| 106 | FutureVision      | Diana Prince     | [diana@futurevision.com](mailto:diana@futurevision.com)   | 7                  |
| 107 | Alpha Innovations | Peter Parker     | [peter@alpha.com](mailto:peter@alpha.com)                 | 8                  |
| 108 | Matrix Dynamics   | Neo Anderson     | [neo@matrix.com](mailto:neo@matrix.com)                   | 9                  |
| 109 | Quantum Retail    | Steve Rogers     | [steve@quantum.com](mailto:steve@quantum.com)             | 10                 |
| 110 | Horizon Analytics | Natasha Romanoff | [natasha@horizon.com](mailto:natasha@horizon.com)         | 11                 |
| 111 | CloudNest         | Wade Wilson      | [wade@cloudnest.com](mailto:wade@cloudnest.com)           | 12                 |
| 112 | HyperLoop Corp    | Logan Howlett    | [logan@hyperloop.com](mailto:logan@hyperloop.com)         | 13                 |
| 113 | Vertex Solutions  | Clark Kent       | [clark@vertex.com](mailto:clark@vertex.com)               | 14                 |
| 114 | OmniTech          | Barry Allen      | [barry@omnitech.com](mailto:barry@omnitech.com)           | 15                 |
| 115 | Infinity Apps     | Arthur Curry     | [arthur@infinityapps.com](mailto:arthur@infinityapps.com) | 16                 |
| 116 | CyberSphere       | Victor Stone     | [victor@cybersphere.com](mailto:victor@cybersphere.com)   | 17                 |
| 117 | Apex Systems      | Jean Grey        | [jean@apex.com](mailto:jean@apex.com)                     | 18                 |
| 118 | Titan Enterprises | Scott Summers    | [scott@titan.com](mailto:scott@titan.com)                 | 19                 |
| 119 | PixelForge        | Matt Murdock     | [matt@pixelforge.com](mailto:matt@pixelforge.com)         | 20                 |
| 120 | SkyNet Solutions  | Tony Stark       | [tony@skynet.com](mailto:tony@skynet.com)                 | 1                  |

---

# Module C: Project Management & Timesheets

## 1. Table: `projects`

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

| id  | client_id | name                     | budget    | start_date | end_date   |
| --- | --------- | ------------------------ | --------- | ---------- | ---------- |
| 501 | 101       | E-Commerce Platform      | 45000.00  | 2026-01-01 | NULL       |
| 502 | 102       | Cloud Migration          | 25000.00  | 2026-01-10 | 2026-04-15 |
| 503 | 103       | HR Portal                | 18000.00  | 2026-02-01 | NULL       |
| 504 | 104       | CRM Revamp               | 30000.00  | 2026-02-12 | NULL       |
| 505 | 105       | Inventory System         | 55000.00  | 2026-03-01 | NULL       |
| 506 | 106       | Analytics Dashboard      | 42000.00  | 2026-03-15 | NULL       |
| 507 | 107       | Billing Automation       | 37000.00  | 2026-04-01 | NULL       |
| 508 | 108       | AI Recommendation Engine | 95000.00  | 2026-04-10 | NULL       |
| 509 | 109       | Security Monitoring      | 61000.00  | 2026-04-25 | NULL       |
| 510 | 110       | Mobile Banking App       | 80000.00  | 2026-05-01 | NULL       |
| 511 | 111       | Customer Support Portal  | 29000.00  | 2026-05-05 | NULL       |
| 512 | 112       | ERP Integration          | 120000.00 | 2026-05-10 | NULL       |
| 513 | 113       | DevOps Automation        | 48000.00  | 2026-05-15 | NULL       |
| 514 | 114       | Data Warehouse           | 91000.00  | 2026-05-20 | NULL       |
| 515 | 115       | API Gateway              | 67000.00  | 2026-05-25 | NULL       |
| 516 | 116       | Payment Processor        | 76000.00  | 2026-06-01 | NULL       |
| 517 | 117       | Logistics Tracking       | 39000.00  | 2026-06-05 | NULL       |
| 518 | 118       | AI Chatbot               | 44000.00  | 2026-06-10 | NULL       |
| 519 | 119       | Infrastructure Upgrade   | 53000.00  | 2026-06-15 | NULL       |
| 520 | 120       | Blockchain Audit System  | 99000.00  | 2026-06-20 | NULL       |

---

## 2. Table: `tasks`

### Dummy Data

| id   | project_id | assigned_to | title                         | status      | priority |
| ---- | ---------- | ----------- | ----------------------------- | ----------- | -------- |
| 9001 | 501        | 1           | Setup OAuth2 Authentication   | In Progress | High     |
| 9002 | 501        | 2           | Design Database Schema        | Done        | Critical |
| 9003 | 502        | 3           | Configure AWS Infrastructure  | QA          | High     |
| 9004 | 503        | 4           | Build Login Module            | To Do       | Medium   |
| 9005 | 504        | 5           | Implement Payment API         | In Progress | Critical |
| 9006 | 505        | 6           | Create Inventory UI           | QA          | Medium   |
| 9007 | 506        | 7           | Build Dashboard Widgets       | Done        | High     |
| 9008 | 507        | 8           | Setup CI/CD Pipeline          | In Progress | High     |
| 9009 | 508        | 9           | Train ML Recommendation Model | To Do       | Critical |
| 9010 | 509        | 10          | Configure SIEM Alerts         | QA          | High     |
| 9011 | 510        | 11          | Mobile App UI                 | Done        | Medium   |
| 9012 | 511        | 12          | Create Support APIs           | In Progress | High     |
| 9013 | 512        | 13          | ERP Connector                 | To Do       | Critical |
| 9014 | 513        | 14          | Kubernetes Deployment         | QA          | High     |
| 9015 | 514        | 15          | Data ETL Pipeline             | In Progress | High     |
| 9016 | 515        | 16          | API Rate Limiting             | Done        | Medium   |
| 9017 | 516        | 17          | Payment Encryption            | To Do       | Critical |
| 9018 | 517        | 18          | GPS Tracking Integration      | In Progress | High     |
| 9019 | 518        | 19          | NLP Chatbot Training          | QA          | High     |
| 9020 | 519        | 20          | Infrastructure Health Checks  | Done        | Medium   |

---

## 3. Table: `timesheets`

### Dummy Data

| id    | employee_id | task_id | hours_logged | work_date  | description                     |
| ----- | ----------- | ------- | ------------ | ---------- | ------------------------------- |
| 10001 | 1           | 9001    | 4.50         | 2026-05-20 | Implemented token refresh logic |
| 10002 | 2           | 9002    | 7.00         | 2026-05-20 | Completed schema design         |
| 10003 | 3           | 9003    | 5.25         | 2026-05-21 | Configured EC2 instances        |
| 10004 | 4           | 9004    | 6.00         | 2026-05-21 | Built login API                 |
| 10005 | 5           | 9005    | 8.00         | 2026-05-22 | Integrated Stripe payments      |
| 10006 | 6           | 9006    | 4.75         | 2026-05-22 | Created UI wireframes           |
| 10007 | 7           | 9007    | 5.50         | 2026-05-23 | Dashboard graph implementation  |
| 10008 | 8           | 9008    | 7.25         | 2026-05-23 | Jenkins pipeline setup          |
| 10009 | 9           | 9009    | 6.50         | 2026-05-24 | Model training                  |
| 10010 | 10          | 9010    | 5.00         | 2026-05-24 | SIEM rules configuration        |
| 10011 | 11          | 9011    | 7.50         | 2026-05-25 | Mobile app layout               |
| 10012 | 12          | 9012    | 4.25         | 2026-05-25 | REST API creation               |
| 10013 | 13          | 9013    | 8.00         | 2026-05-26 | SAP integration                 |
| 10014 | 14          | 9014    | 6.25         | 2026-05-26 | Kubernetes manifests            |
| 10015 | 15          | 9015    | 5.75         | 2026-05-27 | ETL transformations             |
| 10016 | 16          | 9016    | 4.00         | 2026-05-27 | API throttling                  |
| 10017 | 17          | 9017    | 7.80         | 2026-05-28 | Encryption implementation       |
| 10018 | 18          | 9018    | 5.40         | 2026-05-28 | GPS integration                 |
| 10019 | 19          | 9019    | 6.90         | 2026-05-29 | NLP optimization                |
| 10020 | 20          | 9020    | 3.75         | 2026-05-29 | Health monitoring scripts       |

---

# Database 2: `it_company_products`

# Module D: Subscriptions & Support

## 1. Table: `saas_plans`

### Dummy Data

| id | plan_name    | monthly_price | api_limit_per_day |
| -- | ------------ | ------------- | ----------------- |
| 1  | Starter      | 19.00         | 1000              |
| 2  | Developer    | 29.00         | 10000             |
| 3  | Professional | 79.00         | 50000             |
| 4  | Business     | 199.00        | 100000            |
| 5  | Enterprise   | 499.00        | 1000000           |
| 6  | Growth       | 59.00         | 25000             |
| 7  | Startup      | 39.00         | 15000             |
| 8  | Corporate    | 699.00        | 5000000           |
| 9  | Education    | 9.00          | 500               |
| 10 | Research     | 99.00         | 75000             |
| 11 | Basic        | 14.00         | 800               |
| 12 | Team         | 49.00         | 20000             |
| 13 | Scale        | 149.00        | 85000             |
| 14 | Advanced     | 249.00        | 250000            |
| 15 | Ultimate     | 999.00        | 10000000          |
| 16 | API Plus     | 129.00        | 95000             |
| 17 | Hybrid       | 89.00         | 60000             |
| 18 | Analytics    | 109.00        | 70000             |
| 19 | AI Premium   | 799.00        | 3000000           |
| 20 | Government   | 1499.00       | 50000000          |
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

| id   | client_id | plan_id | status     | next_billing_date |
|------|-----------|---------|-------------|-------------------|
| 2001 | 101       | 1       | Active      | 2026-06-01        |
| 2002 | 102       | 2       | Active      | 2026-06-05        |
| 2003 | 103       | 3       | Past Due    | 2026-06-10        |
| 2004 | 104       | 4       | Active      | 2026-06-15        |
| 2005 | 105       | 5       | Canceled    | 2026-06-20        |
| 2006 | 106       | 6       | Active      | 2026-06-25        |
| 2007 | 107       | 7       | Active      | 2026-07-01        |
| 2008 | 108       | 8       | Past Due    | 2026-07-05        |
| 2009 | 109       | 9       | Active      | 2026-07-10        |
| 2010 | 110       | 10      | Active      | 2026-07-15        |
| 2011 | 111       | 11      | Canceled    | 2026-07-20        |
| 2012 | 112       | 12      | Active      | 2026-07-25        |
| 2013 | 113       | 13      | Active      | 2026-08-01        |
| 2014 | 114       | 14      | Past Due    | 2026-08-05        |
| 2015 | 115       | 15      | Active      | 2026-08-10        |
| 2016 | 116       | 16      | Active      | 2026-08-15        |
| 2017 | 117       | 17      | Active      | 2026-08-20        |
| 2018 | 118       | 18      | Canceled    | 2026-08-25        |
| 2019 | 119       | 19      | Active      | 2026-09-01        |
| 2020 | 120       | 20      | Active      | 2026-09-05        |

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

| id    | client_id | subject                                 | severity    | created_at          |
|-------|-----------|-----------------------------------------|-------------|---------------------|
| 40001 | 101       | API timeout issue                       | High        | 2026-05-21 10:00:00 |
| 40002 | 102       | Login authentication failure            | Medium      | 2026-05-21 11:00:00 |
| 40003 | 103       | Billing mismatch                        | Low         | 2026-05-21 12:00:00 |
| 40004 | 104       | Database connection timeout             | High        | 2026-05-21 13:00:00 |
| 40005 | 105       | Complete service outage                 | System Down | 2026-05-21 14:00:00 |
| 40006 | 106       | Email notifications delayed             | Medium      | 2026-05-21 15:00:00 |
| 40007 | 107       | API rate limit exceeded                 | Low         | 2026-05-21 16:00:00 |
| 40008 | 108       | Kubernetes pod failures                 | High        | 2026-05-21 17:00:00 |
| 40009 | 109       | Payment webhook failures                | High        | 2026-05-21 18:00:00 |
| 40010 | 110       | Slow dashboard performance              | Medium      | 2026-05-21 19:00:00 |
| 40011 | 111       | Incorrect invoice generation            | Low         | 2026-05-21 20:00:00 |
| 40012 | 112       | SSL certificate expired                 | High        | 2026-05-21 21:00:00 |
| 40013 | 113       | Redis cache inconsistency               | Medium      | 2026-05-21 22:00:00 |
| 40014 | 114       | Deployment rollback required            | High        | 2026-05-21 23:00:00 |
| 40015 | 115       | Search indexing failure                 | Medium      | 2026-05-22 00:00:00 |
| 40016 | 116       | Notification queue stuck                | High        | 2026-05-22 01:00:00 |
| 40017 | 117       | Data sync delayed                       | Low         | 2026-05-22 02:00:00 |
| 40018 | 118       | Production memory spike                 | High        | 2026-05-22 03:00:00 |
| 40019 | 119       | VPN connectivity issues                 | Medium      | 2026-05-22 04:00:00 |
| 40020 | 120       | Full infrastructure downtime            | System Down | 2026-05-22 05:00:00 |

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
