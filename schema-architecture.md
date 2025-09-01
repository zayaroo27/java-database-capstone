# Smart Clinic Management System – Architecture

## Section 1: Architecture Summary

The Smart Clinic Management System is built on **Spring Boot** and follows a **three-tier web architecture**.

- **Presentation Tier** – The system uses **Thymeleaf templates** for Admin and Doctor dashboards, which deliver server-rendered HTML pages, and **REST APIs** for modules like appointments and patient dashboards, which return JSON responses for mobile apps or other clients.
- **Application Tier** – This contains **controllers, services, and business logic**. Controllers handle incoming requests, validate inputs, and delegate operations to the service layer. The service layer enforces rules, coordinates workflows, and manages communication with repositories.
- **Data Tier** – The application uses two databases:
    - **MySQL** (via Spring Data JPA) for structured data such as patients, doctors, appointments, and admin records.
    - **MongoDB** (via Spring Data MongoDB) for flexible, document-based data such as prescriptions.

This dual-database setup leverages the strengths of both relational and non-relational data. Data retrieved from repositories is mapped into Java objects (JPA entities or MongoDB documents). These models are then rendered into HTML through Thymeleaf or returned as JSON in REST responses.

---

## Section 2: Numbered Flow of Data and Control

1. A user interacts with the system through either a **Thymeleaf dashboard** (AdminDashboard, DoctorDashboard) or a **REST API client** (Appointment, PatientDashboard, PatientRecord).
2. The request is routed to the appropriate **controller**. Thymeleaf controllers return HTML templates, while REST controllers return JSON responses.
3. The controller validates the request and forwards it to the **service layer**, keeping business logic separate from request handling.
4. The **service layer** applies business rules and coordinates tasks, such as verifying doctor availability before confirming an appointment.
5. The service layer communicates with the appropriate **repository**:
    - MySQL repositories handle structured relational data.
    - MongoDB repositories manage prescription documents.
6. Repositories query the respective **databases** (MySQL or MongoDB) and return the results.
7. Retrieved data is mapped into **Java model classes**. These models are then:
    - Passed to Thymeleaf templates for **HTML rendering**, or
    - Serialized into JSON for **REST API responses**.

---
