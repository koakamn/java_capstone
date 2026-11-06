# Database Schema Design - Smart Clinic Management System

## Overview
The Smart Clinic Management System uses a hybrid database architecture:
1. **MySQL Relational Database (`cms`)** for structured core entities (`admin`, `doctor`, `doctor_available_times`, `patient`, `appointment`).
2. **MongoDB Document Database (`prescriptions`)** for flexible clinical documents (`prescription`).

---

## 1. MySQL Database Schema

### Table: `admin`
Stores administrator credentials for managing the clinic portal.

| Column | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `BIGINT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Unique identifier for the admin |
| `username` | `VARCHAR(100)` | `NOT NULL`, `UNIQUE` | Admin login username |
| `password` | `VARCHAR(255)` | `NOT NULL` | Admin login password |

```sql
CREATE TABLE admin (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);
```

---

### Table: `doctor`
Stores doctor profile details and contact information.

| Column | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `BIGINT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Unique identifier for the doctor |
| `name` | `VARCHAR(100)` | `NOT NULL` | Full name of the doctor (3–100 chars) |
| `specialty` | `VARCHAR(50)` | `NOT NULL` | Medical specialization (e.g., Cardiologist) |
| `email` | `VARCHAR(100)` | `NOT NULL`, `UNIQUE` | Doctor's email address |
| `password` | `VARCHAR(255)` | `NOT NULL` | Doctor's portal password (min 6 chars) |
| `phone` | `VARCHAR(10)` | `NOT NULL` | 10-digit contact phone number |

```sql
CREATE TABLE doctor (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    specialty VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(10) NOT NULL
);
```

---

### Table: `doctor_available_times`
Stores the available time slots (`@ElementCollection`) associated with each doctor.

| Column | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `doctor_id` | `BIGINT` | `NOT NULL`, `FOREIGN KEY (doctor.id)` | Reference to the doctor |
| `available_times` | `VARCHAR(50)` | `NOT NULL` | Time slot string (e.g., `09:00-10:00`) |

```sql
CREATE TABLE doctor_available_times (
    doctor_id BIGINT NOT NULL,
    available_times VARCHAR(50) NOT NULL,
    FOREIGN KEY (doctor_id) REFERENCES doctor(id) ON DELETE CASCADE
);
```

---

### Table: `patient`
Stores registered patient information.

| Column | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `BIGINT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Unique identifier for the patient |
| `name` | `VARCHAR(100)` | `NOT NULL` | Full name of the patient (3–100 chars) |
| `email` | `VARCHAR(100)` | `NOT NULL`, `UNIQUE` | Patient's email address |
| `password` | `VARCHAR(255)` | `NOT NULL` | Patient's portal password (min 6 chars) |
| `phone` | `VARCHAR(10)` | `NOT NULL`, `UNIQUE` | 10-digit contact phone number |
| `address` | `VARCHAR(255)` | `NOT NULL` | Residential address |

```sql
CREATE TABLE patient (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(10) NOT NULL UNIQUE,
    address VARCHAR(255) NOT NULL
);
```

---

### Table: `appointment`
Stores scheduled and completed appointments linking doctors and patients.

| Column | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `BIGINT` | `PRIMARY KEY`, `AUTO_INCREMENT` | Unique identifier for the appointment |
| `doctor_id` | `BIGINT` | `NOT NULL`, `FOREIGN KEY (doctor.id)` | Assigned doctor |
| `patient_id` | `BIGINT` | `NOT NULL`, `FOREIGN KEY (patient.id)` | Assigned patient |
| `appointment_time` | `DATETIME` | `NOT NULL` | Scheduled date and start time |
| `status` | `INT` | `NOT NULL` | `0` = Scheduled, `1` = Completed |

```sql
CREATE TABLE appointment (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    doctor_id BIGINT NOT NULL,
    patient_id BIGINT NOT NULL,
    appointment_time DATETIME NOT NULL,
    status INT NOT NULL DEFAULT 0,
    FOREIGN KEY (doctor_id) REFERENCES doctor(id) ON DELETE CASCADE,
    FOREIGN KEY (patient_id) REFERENCES patient(id) ON DELETE CASCADE
);
```

---

## 2. MongoDB Collection Schema

### Collection: `prescriptions`
Stores prescriptions issued during an appointment.

```json
{
  "_id": "ObjectId('661d9a2b3f4e5a6b7c8d9e0f')",
  "patientName": "John Smith",
  "appointmentId": 1,
  "medication": "Atorvastatin",
  "dosage": "20mg once daily",
  "doctorNotes": "Take after dinner for 30 days. Follow up in 1 month."
}
```
