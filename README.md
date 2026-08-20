# Real-Time Patient Monitoring System – Flask API & MATLAB Dashboard

A real-time medical monitoring system with two components:

- **Server** — a Flask REST API (`oxmonitor`) that simulates and manages patient vitals.
- **Client** — a MATLAB App Designer dashboard (`medicalsimulator`) that polls the API and displays vitals live, with alerts on abnormal readings.

Patients are managed via HTTP requests (e.g. through Postman), while the MATLAB client continuously fetches and visualizes the data — together demonstrating a full client–server architecture for a biomedical application.

## Overview

- **Server (Flask):** simulates patient vitals (SpO₂, heart rate, blood pressure, temperature) for a set of seeded patients, updating every 5 seconds, and prints alerts when a value goes outside a safe range.
- **Client (MATLAB App):** displays vitals live, refreshes automatically, and shows a status lamp/alerts if values are abnormal.
- **Postman (or curl):** used to add, update, delete, and query patient records through the API.

## System Architecture

```
+-------------------+
|      Postman       |
| (Add / Update /    |
|  Delete Patients)  |
+---------+-----------+
          |
          |  REST API (JSON)
          v
+--------------------------+
|      Flask Server        |
|  /patients/, /<id>, etc. |
+------------+-------------+
             |
             |  webread() / webwrite()
             v
+--------------------------+
|    MATLAB Dashboard      |
|  (Real-Time Monitoring)  |
+--------------------------+
```

## API Endpoints

| Method | Endpoint                    | Description                                |
|--------|------------------------------|--------------------------------------------|
| GET    | `/`                          | List available endpoints (docs)             |
| GET    | `/patients/`                 | Get all patients and their vitals           |
| GET    | `/patients/<id>`             | Get a specific patient's data               |
| POST   | `/patients/`                 | Add a new patient (JSON body, see below)    |
| PUT    | `/patients/<id>`             | Replace a patient's fields                  |
| PATCH  | `/patients/<id>`             | Update some of a patient's fields           |
| DELETE | `/patients/<id>`             | Remove a patient                            |
| POST   | `/patients/<id>/update`      | Push new vitals from an external sensor     |
| GET    | `/patients/count`            | Get the total number of patients            |

### Example: add a patient (`POST /patients/`)

```json
{
  "name": "Jane Doe",
  "age": 34,
  "gender": "female",
  "heart_rate": 82,
  "blood_pressure_systolic": 117,
  "blood_pressure_diastolic": 75,
  "temperature": 36.6,
  "oxygen_saturation": 96,
  "weight_kg": 62,
  "city": "New York"
}
```

`id` is assigned automatically by the server; all other fields above are required.

## Installation & Setup

**Prerequisites:** Python 3.9+, `flask`, and MATLAB with App Designer (for the client).

1. Clone the repository:
   ```bash
   git clone https://github.com/rontsoran/Real-Time-Patient-Vital-Monitoring-System.git
   cd Real-Time-Patient-Vital-Monitoring-System
   ```

2. Install dependencies:
   ```bash
   pip install flask
   ```

3. Run the Flask API server:
   ```bash
   python oxmonitor
   ```
   The server listens on `http://127.0.0.1:5000`.

4. Use Postman (or curl) to send GET / POST / PUT / PATCH / DELETE requests to `http://127.0.0.1:5000/patients/`.

5. Open `medicalsimulator` in MATLAB App Designer and run it to view the live dashboard. On first run, update the `BASE_URL` property to `http://127.0.0.1:5000` (it defaults to a placeholder URL).

## Key Features

- Real-time JSON API server built with Flask, backed by an in-memory patient list with a background simulation thread.
- Automatic alerts (console-logged) when a patient's oxygen, heart rate, blood pressure, or temperature falls outside safe thresholds.
- Full CRUD over patients via Postman or any HTTP client.
- Live MATLAB dashboard that polls the API and visualizes vitals with status indicators.
- Easy to extend with real sensors (via `POST /patients/<id>/update`) or a persistent database.

## Typical Workflow

1. Add or update a patient via `POST /patients/` in Postman.
2. The MATLAB app automatically refreshes and shows the updated vitals.
3. Delete or modify patients from Postman as needed.
4. (Optional) Extend the alert thresholds or add new vital signs.

## Notes / Known Limitations

- Patient data is stored in memory only — it resets whenever the server restarts.
- The server runs without authentication and is intended for local/demo use, not production deployment.

## License

This project is released under the MIT License. Feel free to use it for learning, research, or development purposes.
