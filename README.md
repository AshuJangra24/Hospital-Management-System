Hospital Management System
Overview
This Hospital Management System is designed to manage patients, doctors, and appointments in a hospital setting. It provides basic functionalities such as adding and viewing patients, viewing doctors, and booking appointments. The system uses MySQL as the database and Java for the application logic.

Features
Add Patient: Allows the user to add a new patient with their name, age, and gender.
View Patients: Displays a list of all patients stored in the database.
View Doctors: Displays a list of doctors with their IDs, names, and specializations.
Book Appointment: Allows a patient to book an appointment with a doctor, ensuring that the doctor is available on the selected date.
Requirements
Java 8 or higher.
MySQL Database:
A running instance of MySQL.
A database named hospital with tables patients, doctors, and appointments.
JDBC Driver: Ensure the MySQL JDBC driver is available in the classpath.
Database Schema
patients Table:
sql
Copy
CREATE TABLE patients (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    age INT,
    gender VARCHAR(10)
);
doctors Table:
sql
Copy
CREATE TABLE doctors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    specialization VARCHAR(255)
);
appointments Table:
sql
Copy
CREATE TABLE appointments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,
    FOREIGN KEY (patient_id) REFERENCES patients(id),
    FOREIGN KEY (doctor_id) REFERENCES doctors(id)
);
Classes
Patient
This class manages patient-related operations such as adding a patient to the database, viewing all patients, and checking if a patient exists by ID.

Methods:
addPatient(): Prompts for patient details and inserts them into the patients table.
viewPatients(): Displays all patients stored in the patients table.
getPatientsById(int id): Checks if a patient with the given ID exists in the database.
Doctor
This class manages doctor-related operations, including viewing all doctors and verifying if a doctor exists by ID.

Methods:
viewDoctors(): Displays all doctors and their specializations from the doctors table.
getDoctorById(int doctorId): Checks if a doctor with the given ID exists in the database.
HospitalManagementSystem
This is the main class that ties everything together. It handles user interaction through the command-line interface, providing options for managing patients, doctors, and appointments.

Methods:
main(String[] args): Starts the program and displays a menu for the user.
bookAppointment(Patient patient, Doctor doctor, Connection connection, Scanner scanner): Books an appointment if the selected patient and doctor exist and the doctor is available on the chosen date.
checkDoctorAvailability(int doctorId, String appointmentDate, Connection connection): Checks if the doctor is available on the specified appointment date.
Usage
Database Setup: Ensure your MySQL database is properly set up and the required tables (patients, doctors, and appointments) are created as per the schema provided.

Running the Application:

Compile the Java files.
Make sure the JDBC driver is correctly included in your project.
Run the HospitalManagementSystem class.
Menu Options:

Choose 1 to add a patient.
Choose 2 to view the list of patients.
Choose 3 to view the list of doctors.
Choose 4 to book an appointment (you will need to enter patient ID, doctor ID, and appointment date).
Choose 5 to exit the program.
Example Usage
Add Patient
mathematica
Copy
Enter Patient Name: John
Enter Patient Age: 30
Enter Patient Gender: Male
Patient Added Successfully!
View Patients
diff
Copy
+------------+--------------+------+-----------+
| Patient Id |     Name     |  Age |   Gender  |
+------------+--------------+------+-----------+
| 1          | John         | 30   | Male      |
+------------+--------------+------+-----------+
Book Appointment
mathematica
Copy
Enter Patient Id: 1
Enter Doctor Id: 2
Enter appointment date (YYYY-MM-DD): 2025-01-20
Appointment Booked!
Error Handling
If a doctor or patient ID is invalid, the program will notify the user that the entry does not exist.
If a doctor is already booked on the selected date, the appointment will not be booked, and an error message will be displayed.
