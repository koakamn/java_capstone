# User Stories - Smart Clinic Management System

## 1. Admin User Stories

- **US-A1: Admin Login**
  - **As an** Admin,
  - **I want to** log into the Admin Portal using my username and password,
  - **So that** I can securely manage the clinic's doctors and system settings.
  - **Acceptance Criteria:**
    - Valid credentials return a JWT token and redirect to the Admin Dashboard.
    - Invalid credentials display an authentication error message.

- **US-A2: Add New Doctor**
  - **As an** Admin,
  - **I want to** add a new doctor with their name, specialty, email, phone number, password, and available time slots,
  - **So that** patients can find and book appointments with the new doctor.
  - **Acceptance Criteria:**
    - Duplicate doctor emails are rejected with a conflict message.
    - Newly added doctors appear immediately on the Admin and Patient dashboards.

- **US-A3: View and Filter Doctors**
  - **As an** Admin,
  - **I want to** view all doctors and filter them by name, specialty, or time availability (AM/PM),
  - **So that** I can quickly locate specific doctor profiles.

- **US-A4: Delete Doctor**
  - **As an** Admin,
  - **I want to** remove a doctor from the system,
  - **So that** doctors who are no longer at the clinic cannot be booked.
  - **Acceptance Criteria:**
    - Deleting a doctor removes their profile and associated appointments from the database.

---

## 2. Patient User Stories

- **US-P1: Patient Registration (Sign Up)**
  - **As a** Patient,
  - **I want to** register an account with my name, email, password, phone number, and address,
  - **So that** I can book and manage appointments online.
  - **Acceptance Criteria:**
    - System prevents duplicate registrations with the same email or phone number.

- **US-P2: Patient Login**
  - **As a** Patient,
  - **I want to** log into the Patient Portal using my email and password,
  - **So that** I can access my personalized dashboard and appointments.

- **US-P3: Search and Filter Doctors**
  - **As a** Patient,
  - **I want to** search for doctors by name and filter them by specialty and available time (AM/PM),
  - **So that** I can find the right specialist at a convenient time.

- **US-P4: Book an Appointment**
  - **As a** Patient,
  - **I want to** select an available date and time slot for a doctor and confirm my booking,
  - **So that** I can schedule a consultation.

- **US-P5: View and Filter My Appointments**
  - **As a** Patient,
  - **I want to** view all my booked appointments and filter them by status (past/future) or doctor name,
  - **So that** I can track my upcoming visits and consultation history.

---

## 3. Doctor User Stories

- **US-D1: Doctor Login**
  - **As a** Doctor,
  - **I want to** log into the Doctor Portal with my email and password,
  - **So that** I can manage my daily schedule and patient records.

- **US-D2: View Daily Appointments**
  - **As a** Doctor,
  - **I want to** view a list of all patient appointments for today or any selected date,
  - **So that** I can prepare for my consultations.

- **US-D3: Search Patient Appointments**
  - **As a** Doctor,
  - **I want to** filter my appointments by patient name,
  - **So that** I can quickly find a specific patient's booking and details.

- **US-D4: Add and View Prescriptions**
  - **As a** Doctor,
  - **I want to** create and view digital prescriptions (medication, dosage, doctor notes) for a patient's appointment,
  - **So that** the patient's treatment plan is recorded in the system.
