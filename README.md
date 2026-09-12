# Traffic Volume Prediction

An end-to-end machine learning project that predicts **traffic volume** using weather conditions, time-based features, holidays, and rush-hour information.

The project combines **machine learning model development, a FastAPI backend, and a Streamlit frontend** to provide a complete prediction workflow.

## Project Overview

Traffic volume can vary significantly depending on factors such as time of day, weather conditions, holidays, and rush hours.

This project uses machine learning to estimate traffic volume from these input features.

### Key Components

* **Data Exploration & Model Training** — Jupyter Notebook
* **Machine Learning Pipeline** — Scikit-learn
* **Backend API** — FastAPI
* **Frontend Interface** — Streamlit
* **Model Persistence** — Joblib

## Project Structure

```text
traffic-prediction/
│
├── api.py
├── frontend.py
├── notebook.ipynb
├── traffic_model_pipeline.joblib
├── requirements.txt
├── README.md
│
└── data/
    └── Metro_Interstate_Traffic_Volume.csv
```

## Files

### `notebook.ipynb`

The Jupyter Notebook contains the machine learning workflow.

It includes:

* Data loading and preprocessing
* Exploratory Data Analysis (EDA)
* Feature engineering
* Model training and evaluation
* Creation of time-based features
* Exporting the trained machine learning pipeline

The trained model is saved as:

```text
traffic_model_pipeline.joblib
```

This file is then loaded by the FastAPI backend for making predictions.

### `api.py`

`api.py` contains the FastAPI backend responsible for serving traffic predictions.

The API:

* Loads the trained ML pipeline
* Validates incoming data using Pydantic
* Accepts prediction requests
* Returns the predicted traffic volume

Example input schema:

```python
class TrafficData(BaseModel):
    holiday: str
    temp: float
    rain_1h: float
    snow_1h: float
    clouds_all: int
    weather_main: str
    hour: int
    day_of_week: int
    month: int
    is_rush_hour: int
```

### `frontend.py`

The frontend provides a simple interface for interacting with the prediction API.

If implemented using Streamlit, users can enter weather and time-related information and receive a traffic-volume prediction without directly interacting with the API.

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/traffic-prediction.git
cd traffic-prediction
```

### 2. Create a Virtual Environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## Train the Model

Open the Jupyter Notebook:

```bash
jupyter notebook notebook.ipynb
```

Run the notebook to perform data preprocessing, feature engineering, model training, and evaluation.

After training, the model pipeline will be saved as:

```text
traffic_model_pipeline.joblib
```

## Run the Application

### Start the FastAPI Backend

```bash
uvicorn api:app --reload
```

The API will be available at:

```text
http://127.0.0.1:8000
```

FastAPI also provides interactive API documentation at:

```text
http://127.0.0.1:8000/docs
```

### Start the Streamlit Frontend

In a separate terminal:

```bash
streamlit run frontend.py
```

## API Endpoints

### Health Check

**GET /**

Returns a basic message confirming that the API is running.

Example response:

```json
{
  "message": "Welcome to the Traffic Prediction API. Go to /docs for details."
}
```

### Predict Traffic Volume

**POST /predict**

Accepts weather, time, holiday, and rush-hour information and returns the predicted traffic volume.

#### Request

```json
{
  "holiday": "None",
  "temp": 295.15,
  "rain_1h": 0.0,
  "snow_1h": 0.0,
  "clouds_all": 75,
  "weather_main": "Clouds",
  "hour": 17,
  "day_of_week": 0,
  "month": 6,
  "is_rush_hour": 1
}
```

#### Response

```json
{
  "predicted_traffic_volume": 4720
}
```

## Example API Request

You can also make a prediction using Python and the `requests` library:

```python
import requests

url = "http://127.0.0.1:8000/predict"

data = {
    "holiday": "None",
    "temp": 295.15,
    "rain_1h": 0.0,
    "snow_1h": 0.0,
    "clouds_all": 75,
    "weather_main": "Clouds",
    "hour": 17,
    "day_of_week": 0,
    "month": 6,
    "is_rush_hour": 1
}

response = requests.post(url, json=data)

print(response.json())
```

## Input Features

| Feature        | Description                                        |
| -------------- | -------------------------------------------------- |
| `holiday`      | Holiday information                                |
| `temp`         | Temperature                                        |
| `rain_1h`      | Rainfall during the previous hour                  |
| `snow_1h`      | Snowfall during the previous hour                  |
| `clouds_all`   | Cloud coverage                                     |
| `weather_main` | Main weather condition                             |
| `hour`         | Hour of the day                                    |
| `day_of_week`  | Day of the week                                    |
| `month`        | Month                                              |
| `is_rush_hour` | Indicates whether the input falls within rush hour |

## Tech Stack

* **Python 3.9+**
* **Pandas** — Data processing
* **Scikit-learn** — Machine learning
* **FastAPI** — REST API
* **Pydantic** — Data validation
* **Streamlit** — Frontend interface
* **Joblib** — Model persistence
* **Jupyter Notebook** — Data exploration and experimentation

## Machine Learning Workflow

```text
Raw Dataset
     │
     ▼
Data Preprocessing
     │
     ▼
Exploratory Data Analysis
     │
     ▼
Feature Engineering
     │
     ▼
Model Training
     │
     ▼
Model Evaluation
     │
     ▼
Saved ML Pipeline
     │
     ▼
FastAPI Backend
     │
     ▼
Streamlit Frontend
     │
     ▼
Traffic Volume Prediction
```

## Future Improvements

* Deploy the application using Docker
* Deploy the API to a cloud platform
* Improve the Streamlit UI/UX
* Integrate real-time traffic data
* Add model monitoring
* Implement automated model retraining
* Add more advanced traffic and weather features
* Compare additional machine learning models

## Project Goal

The goal of this project is to demonstrate an end-to-end machine learning workflow, from **data exploration and model development to API deployment and user interaction**.

---

**Developed as part of an AI/ML project by AI Club.**
