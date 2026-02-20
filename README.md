🏥 Hospital Management System (SQL Project)
📌 Project Overview

The Hospital Management System is a structured relational database project built using MySQL.
This project demonstrates database design, table relationships, data insertion, and advanced SQL queries for real-world hospital operations analysis.

It includes modules for:
Departments
Doctors
Patients
Appointments
Admissions
Treatments
Billing

🛠️ Tech Stack
Database: MySQL
Query Language: SQL
Tool Used: MySQL Workbench

🗂️ Database Name
HospitalDB

📊 Database Structure
🔹 Tables Created
Departments
Doctors
Patients
Appointments
Admissions
Treatments
Billing
All tables are properly connected using Primary Keys and Foreign Keys to maintain relational integrity.

🔗 Entity Relationship Flow

Departments
→ Doctors
→ Appointments
→ Patients
→ Admissions
→ Treatments
→ Billing

This ensures proper tracking of hospital operations.

📈 Key Business Queries Implemented
1️⃣ Department Performance

Total patients handled
Total revenue generated
Department-wise revenue ranking

2️⃣ Total Hospital Revenue

Overall revenue calculation from billing table

3️⃣ Unpaid Bills Report

List of patients with pending payments

4️⃣ Doctor Workload Analysis

Number of appointments handled by each doctor

5️⃣ Monthly Admission Trends

Total admissions per month

6️⃣ Average Treatment Cost by Department

Department-wise cost analysis

📌 Sample Business Insights

Identify highest revenue generating department
Track unpaid bills for financial management
Analyze doctor performance
Monitor hospital growth trends
Understand patient admission patterns

🎯 Learning Outcomes
Through this project, I learned:
Database normalization
Creating relational schemas
Implementing primary & foreign keys
Writing complex JOIN queries
Using GROUP BY, ORDER BY, Aggregate functions
Performing business data analysis using SQL

🚀 How to Run This Project

Open MySQL Workbench

Create database:
CREATE DATABASE HospitalDB;

Use the database:
USE HospitalDB;
Run the table creation scripts

Insert the sample data
Execute analytical queries

📌 Author
Amar Babar
Aspiring Data Analyst Using SQL Developer

⭐ If You Like This Project

Give it a ⭐ on GitHub and connect with me!

