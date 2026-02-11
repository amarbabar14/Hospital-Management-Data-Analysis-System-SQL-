
CREATE DATABASE HospitalDB;
use  HospitalDB;

# Departments Table
CREATE TABLE Departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

# Doctors Table
CREATE TABLE Doctors (
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(100),
    specialization VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id)
);

# Patients Table
CREATE TABLE Patients (
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(100),
    gender VARCHAR(10),
    age INT,
    phone VARCHAR(15)
);

# Appointments Table
CREATE TABLE Appointments (
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,
    status VARCHAR(50),
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);

# Admissions Table
CREATE TABLE Admissions (
    admission_id INT PRIMARY KEY,
    patient_id INT,
    ward VARCHAR(50),
    admission_date DATE,
    discharge_date DATE,
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id)
);

# Treatments Table
CREATE TABLE Treatments (
    treatment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    treatment_description VARCHAR(200),
    treatment_cost DECIMAL(10,2),
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);

# Billing Table
CREATE TABLE Billing (
    bill_id INT PRIMARY KEY,
    patient_id INT,
    total_amount DECIMAL(10,2),
    payment_status VARCHAR(50),
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id)
);


# ---- Insert Sample Data ----- #
INSERT INTO Departments VALUES
(1, 'Cardiology'),
(2, 'Neurology'),
(3, 'Orthopedics'),
(4, 'General Medicine'),
(5, 'Pediatrics'),
(6, 'Dermatology'),
(7, 'Gynecology'),
(8, 'Oncology'),
(9, 'ENT'),
(10, 'Psychiatry');

INSERT INTO Doctors VALUES
(1, 'Dr. Sharma', 'Cardiologist', 1),
(2, 'Dr. Mehta', 'Neurologist', 2),
(3, 'Dr. Patil', 'Orthopedic', 3),
(4, 'Dr. Khan', 'Physician', 4),
(5, 'Dr. Rao', 'Pediatrician', 5),
(6, 'Dr. Iyer', 'Dermatologist', 6),
(7, 'Dr. Singh', 'Gynecologist', 7),
(8, 'Dr. Verma', 'Oncologist', 8),
(9, 'Dr. Desai', 'ENT Specialist', 9),
(10, 'Dr. Kulkarni', 'Psychiatrist', 10);

INSERT INTO Patients VALUES
(1, 'Amit Joshi', 'Male', 35, '9876543210'),
(2, 'Neha Patil', 'Female', 28, '9876501234'),
(3, 'Rahul Singh', 'Male', 42, '9876512345'),
(4, 'Priya Shah', 'Female', 30, '9876523456'),
(5, 'Rohan More', 'Male', 25, '9876534567'),
(6, 'Sneha Kulkarni', 'Female', 32, '9876545678'),
(7, 'Vikas Gupta', 'Male', 50, '9876556789'),
(8, 'Anjali Nair', 'Female', 27, '9876567890'),
(9, 'Karan Malhotra', 'Male', 45, '9876578901'),
(10, 'Pooja Deshmukh', 'Female', 38, '9876589012');

INSERT INTO Appointments VALUES
(1, 1, 1, '2025-01-10', 'Completed'),
(2, 2, 2, '2025-01-12', 'Completed'),
(3, 3, 3, '2025-01-15', 'Pending'),
(4, 4, 4, '2025-01-18', 'Completed'),
(5, 5, 5, '2025-01-20', 'Completed'),
(6, 6, 6, '2025-01-22', 'Cancelled'),
(7, 7, 7, '2025-01-25', 'Completed'),
(8, 8, 8, '2025-01-28', 'Pending'),
(9, 9, 9, '2025-02-01', 'Completed'),
(10, 10, 10, '2025-02-03', 'Completed');

INSERT INTO Admissions VALUES
(1, 1, 'Ward A', '2025-01-10', '2025-01-15'),
(2, 2, 'Ward B', '2025-01-12', '2025-01-14'),
(3, 3, 'Ward C', '2025-01-15', NULL),
(4, 4, 'Ward A', '2025-01-18', '2025-01-20'),
(5, 5, 'Ward D', '2025-01-20', '2025-01-23'),
(6, 6, 'Ward E', '2025-01-22', NULL),
(7, 7, 'Ward F', '2025-01-25', '2025-01-30'),
(8, 8, 'Ward B', '2025-01-28', '2025-02-02'),
(9, 9, 'Ward C', '2025-02-01', NULL),
(10, 10, 'Ward D', '2025-02-03', '2025-02-06');

INSERT INTO Treatments VALUES
(1, 1, 1, 'Heart Surgery', 150000),
(2, 2, 2, 'Brain MRI', 25000),
(3, 3, 3, 'Knee Replacement', 80000),
(4, 4, 4, 'General Checkup', 2000),
(5, 5, 5, 'Child Vaccination', 5000),
(6, 6, 6, 'Skin Allergy Treatment', 7000),
(7, 7, 7, 'Delivery Procedure', 60000),
(8, 8, 8, 'Cancer Therapy', 120000),
(9, 9, 9, 'Ear Surgery', 30000),
(10, 10, 10, 'Mental Health Therapy', 15000);

INSERT INTO Billing VALUES
(1, 1, 160000, 'Paid'),
(2, 2, 25000, 'Paid'),
(3, 3, 80000, 'Unpaid'),
(4, 4, 2000, 'Paid'),
(5, 5, 5000, 'Paid'),
(6, 6, 7000, 'Unpaid'),
(7, 7, 60000, 'Paid'),
(8, 8, 120000, 'Unpaid'),
(9, 9, 30000, 'Paid'),
(10, 10, 15000, 'Paid');


#--Queries--#

#(1) Show Department Performance
SELECT 
    d.department_name,
    COUNT(DISTINCT a.patient_id) AS Total_Patients,
    SUM(t.treatment_cost) AS Total_Revenue
FROM Departments d
JOIN Doctors doc ON d.department_id = doc.department_id
JOIN Treatments t ON doc.doctor_id = t.doctor_id
JOIN Appointments a ON a.doctor_id = doc.doctor_id
GROUP BY d.department_name
ORDER BY Total_Revenue DESC;

#(2) Show Total Hospital Revenue
SELECT 
    SUM(total_amount) AS Total_Hospital_Revenue
FROM Billing;

#(3) Show Unpaid Bills
SELECT 
    p.patient_name,
    b.total_amount,
    b.payment_status
FROM Billing b
JOIN Patients p ON b.patient_id = p.patient_id
WHERE b.payment_status = 'Unpaid';

#(4) Show Doctor Workload
SELECT 
    d.doctor_name,
    COUNT(a.appointment_id) AS Total_Appointments
FROM Doctors d
JOIN Appointments a ON d.doctor_id = a.doctor_id
GROUP BY d.doctor_name
ORDER BY Total_Appointments DESC;

#(5) Show Admission Trends (Monthly)
SELECT 
    FORMAT(admission_date, 'yyyy-MM') AS Admission_Month,
    COUNT(admission_id) AS Total_Admissions
FROM Admissions
GROUP BY FORMAT(admission_date, 'yyyy-MM')
ORDER BY Admission_Month;


#(6) Average Treatment Cost by Department
SELECT 
    d.department_name,
    AVG(t.treatment_cost) AS Avg_Treatment_Cost
FROM Departments d
JOIN Doctors doc ON d.department_id = doc.department_id
JOIN Treatments t ON doc.doctor_id = t.doctor_id
GROUP BY d.department_name;
