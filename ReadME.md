# Optometry Clinic System

This repository contains the desktop release artifacts and documentation for the **Optometry Clinic System**, a Django REST API backend for managing university optometry clinic workflows.

## Overview

The system supports the full patient journey:
- **Registration** → **Appointment** → **Examination** (Visual Acuity, Refraction, Internal/External Observation) → **Diagnosis** → **Management Plan** → **Grading** (for students)

Key features include:
- Real-time appointment updates via WebSockets
- Role-based access (Student, Lecturer, Optometrist, Secretary, Pharmacy, Intern)
- Modular apps for patients, examinations, diagnosis, management, grading, inventory, pharmacy, clinic scheduling, and absence requests
- Robust status machine for workflow management
- Cross-app model resolution for maintainability

## Getting Started

1. **Clone the repository** and install dependencies (see `requirements.txt`).
2. **Run migrations**:
    ```bash
    python manage.py makemigrations && python manage.py migrate
    ```
3. **Create test data and user roles**:
    ```bash
    python test_data.py
    python create_users.py
    ```
4. **Start the development server** (with WebSocket support):
    ```bash
    python manage.py runserver
    ```

## Key Architecture Patterns

- **StatusMachineMixin** for all appointment and workflow status transitions
- **get_model()** helper for cross-app model references
- **Soft deletes** for patient records (never use `.delete()` directly)
- **JWT authentication** with DRF and role-based permissions
- **WebSocket** updates for appointment status (requires Redis)

## Documentation

- See `.github/copilot-instructions.md` for detailed architecture, conventions, and development workflow.
- Refer to `optometry_clinic/settings.py` for configuration details.

## Contributing

Follow the architecture and coding conventions described in the project documentation. All new features should use the established patterns for status management, model inheritance, and API design.
