# MYSQL-TO-RDS-MIGRATION-USING-EC2

**Author:** Sudarshan Dattatray Bhosale

**Project Type:** AWS Cloud | Database Migration

**Version:** 1.0

**License:** MIT

---

## 🌐 Project Overview

### 👤 About the Author

* **Name:** Sudarshan Dattatray Bhosale
* **Education:** Bachelor of Computer Applications (BCA), Shivaji University
* **Project Experience:** Online Bus Ticket Booking System (PHP & MySQL)
* **Skills:** AWS, EC2, RDS, S3, MySQL, Linux, PHP, Cloud & DevOps Fundamentals
* **Career Goal:** Cloud / DevOps Engineer

This repository demonstrates how to migrate a **MySQL database from an EC2 instance to Amazon RDS (MySQL)**. It includes complete setup steps, commands, folder structure, screenshots suggestions, and best practices.

🔹 **Goal:** Move data securely and efficiently to AWS RDS
🔹 **Tools Used:** EC2, RDS, MySQL, AWS Console, CLI

---

## 🧩 Architecture

```
+--------------------+         +---------------------------+
|    EC2 Instance    |  --->   |     Amazon RDS (MySQL)    |
|  MySQL Installed   |         | Managed DB Service (RDS)  |
+--------------------+         +---------------------------+
```

---

## ⚙️ Tech Stack

| Component              | Description                        |
| ---------------------- | ---------------------------------- |
| ☁️ **AWS EC2**         | Compute instance hosting MySQL     |
| 🗄️ **AWS RDS**        | Managed MySQL database service     |
| 🐬 **MySQL**           | Database engine used for migration |
| 🔐 **Security Groups** | Network rules for EC2 ↔ RDS access |

---

## 🚀 Step-by-Step Setup

## **📌 Step 1 — Launch EC2 Instance & Install MySQL**

Update system packages:

```sh
sudo apt update -y
```

Install MySQL server:

```sh
sudo apt install mysql-server -y
```

Start MySQL service:

```sh
sudo systemctl start mysql
sudo systemctl enable mysql
```

Create a sample database:

```sql
sudo mysql;
CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
  roll_no INT PRIMARY KEY,
  name VARCHAR(100),
  contact VARCHAR(15),
  address VARCHAR(255)
);

INSERT INTO students VALUES (1, "Prasad", "9876543210", "Pune");
INSERT INTO students VALUES (2, "Sudarshan", "9876500000", "Satara");
INSERT INTO students VALUES (3, "Dhiraj", "9645000000", "Kolhapur");
INSERT INTO students VALUES (4, "Shubham", "9004000000", "Sangli");
INSERT INTO students VALUES (5, "Omkar", "8805000000", "Karad");
EXIT;
```

---

## **📌 Step 2 — Export the EC2 MySQL Database**

```sh
sudo mysqldump -u root -p studentdb > mydb.sql
```

This exports your database into a SQL file.

---

## **📌 Step 3 — Create RDS MySQL Instance**

1. AWS Console → RDS → Create Database
2. Standard Create
3. Engine: MySQL
4. Free Tier template
5. DB Identifier: **myrdsdb**
6. Username: **admin**
7. Password: *create your own*
8. Instance Class: `db.t3.micro`
9. Public Access: **Yes** (demo purpose)
10. Port: 3306

Wait until status: **Available**

---

## **📌 Step 4 — Set Security Group for RDS**

Go to **EC2 → Security Groups → RDS-SG → Edit Inbound Rules**

* Type: MySQL/Aurora
* Port: 3306
* Source: EC2 Instance Security Group

This allows EC2 ↔ RDS connection.

---

## **📌 Step 5 — Connect EC2 to RDS**

Install MySQL client (if not present):

```sh
sudo apt install mysql-client -y
```

Test connection:

```sh
mysql -h <rds-endpoint> -u admin -p
```

---

## **📌 Step 6 — Create Database in RDS**

```sql
CREATE DATABASE studentdb;
```

---

## **📌 Step 7 — Import EC2 SQL File into RDS**

```sh
mysql -h <rds-endpoint> -u admin -p studentdb < mydb.sql
```

---

## **📌 Step 8 — Verify the Data Migration**

```sh
mysql -h <rds-endpoint> -u admin -p
USE studentdb;
SELECT * FROM students;
```

✔️ If you see data — **Migration successful!**

---

## 🧠 Common Issues & Fixes

| Issue            | Reason            | Fix                                 |
| ---------------- | ----------------- | ----------------------------------- |
| ❌ Access denied  | Wrong credentials | Use correct admin username/password |
| 🔒 Timeout error | RDS SG not open   | Allow port 3306 from EC2 SG         |
| ⚙️ Import error  | DB missing in RDS | Run `CREATE DATABASE studentdb;`    |

---

## 📁 Folder Structure

```
MYSQL-TO-RDS-MIGRATION-USING-EC2/
│
├── mydb.sql               # Exported database file
├── README.md              # Documentation
└── Images/                # Add screenshots here
```

---

## 📸 Recommended Screenshots

* RDS creation page
* RDS security group inbound rules
* EC2 MySQL connected to RDS
* Output of SELECT * FROM students;

---

## 🧾 Summary

✔️ Created MySQL DB on EC2
✔️ Exported database using mysqldump
✔️ Launched RDS MySQL instance
✔️ Configured network communication
✔️ Imported SQL data into RDS
✔️ Verified migration success

---

## 💡 Key Learning

* Understanding AWS RDS connectivity
* Using mysqldump for backup and migration
* Setting up secure EC2 ↔ RDS communication

---

## 🌐 Connect with Me

👨‍💻 **Sudarshan Dattatray Bhosale**
💼 Cloud & DevOps Enthusiast
🎓 BCA Graduate — Shivaji University

* 🔗 **LinkedIn:** (https://www.linkedin.com/in/sudarshan-bhosale-174477374))
* 🔗 **GitHub:** (https://github.com/Sudarshan-Bhosale145)
  
