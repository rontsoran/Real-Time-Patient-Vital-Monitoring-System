Real-Time Patient Monitoring System – Flask API & MATLAB Dashboard

This project implements a real-time medical monitoring system consisting of two main components:

A Flask-based REST API server written in Python – responsible for simulating and managing patient data.

A MATLAB App Designer dashboard – acting as a client that displays real-time patient vitals.

The Postman interface is used to add, update, or remove patients via API requests, while the MATLAB client continuously fetches and visualizes the data. Together, they demonstrate a complete Client–Server architecture suitable for real-time biomedical applications.

Overview

Server (Flask): Simulates patient vitals (SpO₂, heart rate, blood pressure, temperature).
Client (MATLAB App): Displays vitals live, updates automatically, and shows alerts if values are abnormal.
Postman: Used to send POST, GET, and DELETE requests to manage patient records through the API.

System Architecture
        +-------------------+
        |     Postman       |
        |  (Add / Update /  |
        |   Delete Patients)|
        +---------+---------+
                  |
                  |  REST API (JSON)
                  |
     +------------v------------+
     |     Flask Server        |
     |  /patients , /<id> etc. |
     +------------+------------+
                  |
                  |  webread() / webwrite()
                  |
     +------------v------------+
     |   MATLAB Dashboard      |
     |  (Real-Time Monitoring) |
     +-------------------------+

API Endpoints
Method	Endpoint	Description
GET	/patients	Get all patients and their vitals
GET	/patients/<id>	Get a specific patient’s data
POST	/patients	Add or update a patient (JSON body)
DELETE	/patients/<id>	Remove a patient
Example JSON Payload (used in Postman)
{
  "id": "102",
  "name": "Jane Doe",
  "heart_rate": 82,
  "spo2": 96,
  "blood_pressure": "117/75",
  "temperature": 36.6
}

Installation & Setup

Clone the repository:

git clone https://github.com/yourusername/patient-monitoring-system.git
cd patient-monitoring-system


Install dependencies:

pip install -r requirements.txt


Run the Flask API server:

python app.py


Open Postman to send POST / GET requests to http://localhost:5000/patients.

Run the MATLAB App Designer client to view the vitals dashboard in real-time.

Key Features

Real-time JSON API server built with Flask

Seamless integration with MATLAB dashboards

Manage patients via Postman (create, update, delete)

Live data visualization and status indicators

Easy to extend with real sensors or databases

Typical Workflow

Add or update a patient in Postman using POST /patients.

MATLAB App automatically refreshes and shows updated vitals.

Delete or modify patients from Postman as needed.

(Optional) Add alerts for low oxygen, high temperature, etc.

License

This project is released under the MIT License.
Feel free to use it for learning, research, or development purposes.
