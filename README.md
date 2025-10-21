# Real-Time Patient Vital Monitoring System – Python & Flask

This project is a **JSON-based API server** built with **Python and Flask** for **real-time monitoring of patient vitals**. It simulates data for oxygen saturation, heart rate, blood pressure, and temperature, and is easily extendable to connect to real sensors. The system demonstrates **API design, JSON data handling, and real-time server updates**, making it a practical example for building fast, interactive backend systems.

## Features

. JSON-based API server allows apps, dashboards, or sensors to communicate seamlessly  
. Real-time updates for fast, live monitoring of vital signs  
. Simulated data provides sample patient vitals for testing and demonstration  
. Ready for real sensors, easily extendable to handle actual inputs  
. Automatic alerts for abnormal values (optional extension)

## Technologies

. Python 3.x  
. Flask  
. JSON  
. Postman (for testing API requests)

## API Endpoints

. GET /patients retrieves all patient vitals  
. GET /patients/<id> retrieves vitals for a specific patient  
. POST /patients adds or updates patient vitals (JSON payload)  
. DELETE /patients/<id> removes a patient record  

> Example GET request in Postman retrieves simulated vitals. The server output can be viewed in PyCharm or any Python console.

## Installation & Setup

Clone the repository: `git clone https://github.com/yourusername/your-repo.git`  
Navigate to the project folder: `cd your-repo`  
Install dependencies: `pip install -r requirements.txt`  
Run the server: `python app.py`  
Test API endpoints via Postman or any HTTP client

## Usage

Simulated patient vitals are automatically generated and served through the API. The live dashboard (if integrated) updates automatically with new data. The system is ready to integrate with physical sensors for real-time monitoring in clinical or experimental setups.

## Contributing

Feel free to fork the project, submit issues, or create pull requests to add features such as advanced alerting for abnormal vitals, integration with real-time sensor data streams, or dashboard improvements.

## License

This project is licensed under the MIT License.
