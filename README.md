# VAPI Voice Agent - Hospital Appointment System

A backend service for integrating a conversational VAPI voice agent with a hospital appointment management system. The application provides APIs for scheduling, cancelling, and retrieving appointments through voice-driven interactions.

## Overview

This project demonstrates how a voice AI agent can interact with backend services and perform real-world actions through API function calls.

The backend is built with FastAPI and SQLAlchemy, with SQLite used for persistent appointment storage. A Streamlit interface is included for testing and validating the available API workflows.

## Features

* Schedule hospital appointments using patient details, visit reason, and preferred time.
* Cancel appointments for a specific patient and date.
* Retrieve active appointments for a given date.
* Expose backend functions as tools for a VAPI voice agent.
* Persist appointment data using SQLite and SQLAlchemy.
* Test API workflows through a Streamlit dashboard.
* Support structured JSON requests through REST API endpoints.

## Tech Stack

| Technology   | Purpose                               |
| ------------ | ------------------------------------- |
| Python 3.11+ | Application development               |
| FastAPI      | REST API framework                    |
| VAPI         | Voice agent integration               |
| SQLAlchemy   | Database ORM                          |
| SQLite       | Appointment data persistence          |
| Streamlit    | API testing dashboard                 |
| Uvicorn      | ASGI server                           |
| uv           | Dependency and environment management |

## Architecture

```text
User
  |
  v
VAPI Voice Agent
  |
  | Tool / Function Calls
  v
FastAPI Backend
  |
  +-------------------+
  |                   |
  v                   v
Appointment Logic   SQLAlchemy
                        |
                        v
                   SQLite Database
```

## Project Structure

```text
vapi-voice-agent-backend/
├── backend.py          # FastAPI application and API endpoints
├── database.py         # SQLAlchemy models and database configuration
├── dummy_frontend.py   # Streamlit testing interface
├── db_demo.py          # Database query demonstration
├── appointments_db.db  # SQLite database
├── pyproject.toml      # Project configuration and dependencies
├── uv.lock             # Locked dependency versions
└── README.md
```

## API Endpoints

All endpoints accept JSON payloads using HTTP POST requests.

### Schedule Appointment

```http
POST /schedule_appointment/
```

Request:

```json
{
  "patient_name": "Vignesh",
  "reason": "Annual checkup",
  "start_time": "2026-08-25T09:00:00"
}
```

### Cancel Appointment

```http
POST /cancel_appointment/
```

Request:

```json
{
  "patient_name": "Vignesh",
  "date": "2026-08-25"
}
```

### List Appointments

```http
POST /list_appointments/
```

Request:

```json
{
  "date": "2026-08-25"
}
```

## Database Schema

Appointments are stored in SQLite using SQLAlchemy.

| Field          | Type     | Description                     |
| -------------- | -------- | ------------------------------- |
| `id`           | Integer  | Primary key                     |
| `patient_name` | String   | Patient name                    |
| `reason`       | String   | Reason for appointment          |
| `start_time`   | DateTime | Appointment date and time       |
| `canceled`     | Boolean  | Appointment cancellation status |
| `created_at`   | DateTime | Record creation timestamp       |

## VAPI Integration

The backend is designed to act as a tool provider for a VAPI voice assistant.

The following backend functions can be configured as VAPI tools:

```text
schedule_appointment
cancel_appointment
list_appointments
```

This allows the voice agent to interpret a user's request and invoke the appropriate backend function to perform the requested operation.

Example workflow:

```text
User:
"Schedule an appointment for Vignesh tomorrow at 9 AM."

        ↓

VAPI Voice Agent

        ↓

schedule_appointment()

        ↓

FastAPI Backend

        ↓

SQLite Database

        ↓

Appointment Created

        ↓

Voice Agent Response
```

## Installation

### Prerequisites

* Python 3.11 or later
* uv or pip

### Clone the Repository

```bash
git clone https://github.com/AIwithhassan/vapi-voice-agent-backend.git

cd vapi-voice-agent-backend
```

### Using uv

Create and activate the virtual environment:

```bash
uv venv
source .venv/bin/activate
```

Install dependencies:

```bash
uv sync
```

### Using pip

Create and activate a virtual environment:

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install fastapi sqlalchemy streamlit uvicorn
```

## Running the Application

Start the FastAPI server:

```bash
python backend.py
```

The API will be available at:

```text
http://127.0.0.1:4444
```

To launch the Streamlit testing interface:

```bash
streamlit run dummy_frontend.py
```

## Testing

The API can be tested using:

* Streamlit dashboard
* Postman
* FastAPI Swagger documentation
* Direct HTTP requests

FastAPI automatically provides interactive API documentation at:

```text
http://127.0.0.1:4444/docs
```

## Database Utilities

To inspect the SQLite database using the provided utility:

```bash
python db_demo.py
```

## Use Case

The project demonstrates a practical conversational AI workflow where a voice agent is connected to backend APIs and persistent application data.

The architecture can be extended to other domains such as:

* Real-estate lead qualification
* Property inquiries
* Customer support
* Sales follow-ups
* Appointment scheduling
* CRM automation

## Future Improvements

* Add authentication and authorization.
* Add appointment availability and conflict detection.
* Integrate a production-grade database such as PostgreSQL.
* Add logging and monitoring for agent interactions.
* Add automated API and integration tests.
* Deploy the FastAPI backend to a cloud platform.
* Add additional VAPI tools for richer conversational workflows.

