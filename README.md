# 💧 Water Quality Monitoring System

A comprehensive **AI + IoT Early Warning System** that monitors water parameters (pH, turbidity, temperature) and predicts contamination using Machine Learning.

![Status](https://img.shields.io/badge/status-ready-success)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![React](https://img.shields.io/badge/frontend-HTML/CSS/JS-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🎯 Features

### Core Functionality

- ✅ **ML-Powered Predictions** - Random Forest classifier (100% accuracy)
- ✅ **Real-Time Dashboard** - Live monitoring with charts and gauges
- ✅ **Automatic Sensor Simulation** - Continuous data generation
- ✅ **Data Logging** - All readings stored in JSON format
- ✅ **Water Quality Index (WQI)** - Calculated score (0-100)
- ✅ **Early Warning System** - Color-coded alerts (Green/Yellow/Red)

### User Interface

- ✅ **Professional Dashboard** - HTML/CSS/Chart.js interface
- ✅ **Beautiful Homepage** - Landing page with feature cards
- ✅ **Dark Mode Toggle** - Light/dark theme support
- ✅ **Auto-Refresh** - Updates every 3 seconds
- ✅ **Browser Notifications** - Alerts for unsafe water
- ✅ **Responsive Design** - Works on all devices

### Advanced Features

- ✅ **Trend Prediction** - Forecast next hour values
- ✅ **Threshold Configuration** - Adjust WHO guidelines
- ✅ **Sensor Simulator** - Test with realistic data
- ✅ **Historical Data** - View past 10 readings
- ✅ **API Endpoints** - RESTful API for integration

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Node.js 14+ (for React frontend, optional)
- Modern web browser

### Installation

#### 1. Backend Setup

```bash

# Navigate to backend directory

cd backend

# Install Python dependencies

pip install -r requirements.txt

# Generate training dataset

python data_generator.py

# Train ML model

python train_model.py

# Start Flask server

python app.py

```

✅ Backend will run on `http://localhost:5000`

#### 2. Frontend Setup

### Option A: HTML Dashboard (Simple)

- Open `frontend/dashboard.html` in your browser
- Or open `frontend/index.html` for homepage

### Option B: React Dashboard (Advanced)

```bash
cd frontend
npm install
npm run dev

```

✅ Frontend will run on `http://localhost:3000`

---

## 📖 Usage Guide

### Start the System

1. **Start Backend** (Terminal 1):

   ```bash
   cd backend
   python app.py

   ```

2. **Open Dashboard** (Browser):
   - Go to `frontend/index.html` (homepage)
   - Or directly to `frontend/dashboard.html` (dashboard)

3. **Start Sensor Simulation** (Optional):
   - Go to `frontend/sensor-controls.html`
   - Click "Start Simulation"
   - Data will be automatically generated every 3 seconds

### View Dashboard

- **Status Cards** - Current water quality status
- **Circular Gauges** - Visual representation of pH, turbidity, temperature
- **Trend Charts** - Historical data visualization
- **Latest Readings Table** - Past 10 measurements
- **WQI Score** - Water Quality Index (0-100)

### Make Predictions

### Via Dashboard:

- Dashboard auto-refreshes every 3 seconds
- Shows predictions in real-time

### Via API:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

```

---

## 📡 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/login` | POST | User authentication |
| `/predict` | POST | Predict water quality |
| `/latest` | GET | Get last 10 readings |
| `/future-trend` | POST | Predict next hour trends |
| `/get-thresholds` | GET | Get WHO thresholds |
| `/set-thresholds` | POST | Update thresholds |
| `/simulate` | POST | Start sensor simulation |
| `/simulate/stop` | POST | Stop simulation |
| `/simulate/status` | GET | Check simulation status |

**Full API Documentation**: See [API_DOCUMENTATION.md](API_DOCUMENTATION.md)

---

## 🔐 Login Credentials

### Admin:

- Username: `admin`
- Password: `admin123`

### User:

- Username: `user`
- Password: `user123`

---

## 🏗️ Project Structure

```text
water_quality_system/
├── backend/
│   ├── app.py                 # Flask API server
│   ├── data_generator.py      # Generate training dataset
│   ├── preprocessing.py       # Data preprocessing pipeline
│   ├── train_model.py         # Train ML model
│   ├── sensor_simulator.py    # Sensor simulation
│   ├── models/
│   │   ├── model.pkl          # Trained ML model
│   │   └── scaler.pkl         # Feature scaler
│   ├── logs.json              # Data logs
│   ├── thresholds.json        # WHO thresholds
│   └── requirements.txt       # Python dependencies
│
├── frontend/
│   ├── index.html             # Homepage
│   ├── dashboard.html         # Main dashboard
│   ├── sensor-controls.html   # Simulation control
│   ├── style.css              # Styles
│   ├── script.js              # Dashboard logic
│   └── src/                   # React components (optional)
│
└── README.md                  # This file

```

---

## 🤖 Machine Learning Model

### Model Details

- **Algorithm**: Random Forest Classifier
- **Features**: pH, Turbidity, Temperature
- **Output**: Safe/Unsafe classification
- **Accuracy**: 100% (on test set)
- **Training Data**: 1000 samples (70% safe, 30% unsafe)

### Model Training

```bash
cd backend
python data_generator.py  # Generate 1000 samples
python train_model.py     # Train model

```

Model is automatically loaded when Flask server starts.

---

## 📊 Water Quality Index (WQI)

WQI is calculated using weighted parameters:

- **pH** (40% weight): Optimal range 6.5-8.5
- **Turbidity** (35% weight): Optimal < 5 NTU
- **Temperature** (25% weight): Optimal 15-25°C

### Alert Levels:

- 🟢 **Green** (WQI ≥ 70): Safe water
- 🟡 **Yellow** (50 ≤ WQI < 70): Caution
- 🔴 **Red** (WQI < 50): Unsafe water

---

## 🔧 Configuration

### WHO Thresholds

Default thresholds can be adjusted:

- pH: 6.5 - 8.5
- Turbidity: 0 - 5 NTU
- Temperature: 15 - 25°C

Update via:

- Dashboard admin panel
- API: `POST /set-thresholds`

### Sensor Simulation

Configure simulation:

- **Interval**: 1-60 seconds (default: 3)
- **Mode**: normal or mixed (includes unsafe readings)

---

## 🧪 Testing

### Test Backend

```bash

# Health check

curl http://localhost:5000/health

# Make prediction

curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

# Get latest readings

curl http://localhost:5000/latest

```

### Test Frontend

1. Open `frontend/index.html` in browser
2. Check backend connection status
3. Navigate to dashboard
4. Start sensor simulation
5. Monitor real-time updates

---

## 🐛 Troubleshooting

### Backend Issues

### "Model not loaded"

```bash
cd backend
python train_model.py  # Retrain model

```

### Port 5000 already in use

- Change port in `app.py`: `app.run(port=5001)`
- Or stop other services using port 5000

### CORS errors

- CORS is enabled for all origins
- Restart Flask server if issues persist

### Frontend Issues

### "Cannot connect to backend"

- Ensure Flask server is running on port 5000
- Check firewall settings
- Verify CORS is enabled

### Charts not displaying

- Check browser console for errors
- Ensure Chart.js is loaded (CDN)
- Verify data format from API

---

## 📈 Performance

- **Prediction Time**: < 10ms
- **Dashboard Refresh**: 3 seconds (configurable)
- **Data Logging**: Real-time (saves to logs.json)
- **Model Accuracy**: 100% on test set

---

## 🔒 Security Notes

- **Development Only**: Current implementation is for development
- **Production**: Implement proper authentication, HTTPS, rate limiting
- **Sensitive Data**: Add encryption for logs and user data

---

## 📝 License

MIT License - See LICENSE file for details

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📞 Support

For issues, questions, or contributions:

- Check documentation in `API_DOCUMENTATION.md`
- Review troubleshooting section
- Open an issue on GitHub

---

## 🎉 Acknowledgments

- WHO Guidelines for water quality thresholds
- scikit-learn for ML algorithms
- Chart.js for data visualization
- Flask for backend framework

---

### Built with ❤️ for water quality monitoring

Last Updated: November 2024


---

Additional notes (Nov 23, 2025):

- The backend now serves the frontend files. When the Flask server is running you can open:
   - `http://127.0.0.1:5000/dashboard` — serves `frontend/dashboard.html` plus its assets (`script.js`, `style.css`) from the backend host.

- There is a convenient testing endpoint:
   - `GET /simulate/once` — returns a single simulated reading with `prediction`, `wqi`, and `alert_color` and also saves it to `backend/logs.json`.

If you prefer to serve frontend files separately, you can still run a quick server in the `frontend/` folder:

```powershell
cd frontend
python -m http.server 8000
# open http://localhost:8000/dashboard.html
```



A comprehensive **AI + IoT Early Warning System** that monitors water parameters (pH, turbidity, temperature) and predicts contamination using Machine Learning.

![Status](https://img.shields.io/badge/status-ready-success)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![React](https://img.shields.io/badge/frontend-HTML/CSS/JS-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🎯 Features

### Core Functionality

- ✅ **ML-Powered Predictions** - Random Forest classifier (100% accuracy)
- ✅ **Real-Time Dashboard** - Live monitoring with charts and gauges
- ✅ **Automatic Sensor Simulation** - Continuous data generation
- ✅ **Data Logging** - All readings stored in JSON format
- ✅ **Water Quality Index (WQI)** - Calculated score (0-100)
- ✅ **Early Warning System** - Color-coded alerts (Green/Yellow/Red)

### User Interface

- ✅ **Professional Dashboard** - HTML/CSS/Chart.js interface
- ✅ **Beautiful Homepage** - Landing page with feature cards
- ✅ **Dark Mode Toggle** - Light/dark theme support
- ✅ **Auto-Refresh** - Updates every 3 seconds
- ✅ **Browser Notifications** - Alerts for unsafe water
- ✅ **Responsive Design** - Works on all devices

### Advanced Features

- ✅ **Trend Prediction** - Forecast next hour values
- ✅ **Threshold Configuration** - Adjust WHO guidelines
- ✅ **Sensor Simulator** - Test with realistic data
- ✅ **Historical Data** - View past 10 readings
- ✅ **API Endpoints** - RESTful API for integration

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Node.js 14+ (for React frontend, optional)
- Modern web browser

### Installation

#### 1. Backend Setup

```bash

# Navigate to backend directory

cd backend

# Install Python dependencies

pip install -r requirements.txt

# Generate training dataset

python data_generator.py

# Train ML model

python train_model.py

# Start Flask server

python app.py

```

✅ Backend will run on `http://localhost:5000`

#### 2. Frontend Setup

### Option A: HTML Dashboard (Simple)

- Open `frontend/dashboard.html` in your browser
- Or open `frontend/index.html` for homepage

### Option B: React Dashboard (Advanced)

```bash
cd frontend
npm install
npm run dev

```

✅ Frontend will run on `http://localhost:3000`

---

## 📖 Usage Guide

### Start the System

1. **Start Backend** (Terminal 1):

   ```bash
   cd backend
   python app.py

   ```

2. **Open Dashboard** (Browser):
   - Go to `frontend/index.html` (homepage)
   - Or directly to `frontend/dashboard.html` (dashboard)

3. **Start Sensor Simulation** (Optional):
   - Go to `frontend/sensor-controls.html`
   - Click "Start Simulation"
   - Data will be automatically generated every 3 seconds

### View Dashboard

- **Status Cards** - Current water quality status
- **Circular Gauges** - Visual representation of pH, turbidity, temperature
- **Trend Charts** - Historical data visualization
- **Latest Readings Table** - Past 10 measurements
- **WQI Score** - Water Quality Index (0-100)

### Make Predictions

### Via Dashboard:

- Dashboard auto-refreshes every 3 seconds
- Shows predictions in real-time

### Via API:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

```

---

## 📡 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/login` | POST | User authentication |
| `/predict` | POST | Predict water quality |
| `/latest` | GET | Get last 10 readings |
| `/future-trend` | POST | Predict next hour trends |
| `/get-thresholds` | GET | Get WHO thresholds |
| `/set-thresholds` | POST | Update thresholds |
| `/simulate` | POST | Start sensor simulation |
| `/simulate/stop` | POST | Stop simulation |
| `/simulate/status` | GET | Check simulation status |

**Full API Documentation**: See [API_DOCUMENTATION.md](API_DOCUMENTATION.md)

---

## 🔐 Login Credentials

### Admin:

- Username: `admin`
- Password: `admin123`

### User:

- Username: `user`
- Password: `user123`

---

## 🏗️ Project Structure

```text
water_quality_system/
├── backend/
│   ├── app.py                 # Flask API server
│   ├── data_generator.py      # Generate training dataset
│   ├── preprocessing.py       # Data preprocessing pipeline
│   ├── train_model.py         # Train ML model
│   ├── sensor_simulator.py    # Sensor simulation
│   ├── models/
│   │   ├── model.pkl          # Trained ML model
│   │   └── scaler.pkl         # Feature scaler
│   ├── logs.json              # Data logs
│   ├── thresholds.json        # WHO thresholds
│   └── requirements.txt       # Python dependencies
│
├── frontend/
│   ├── index.html             # Homepage
│   ├── dashboard.html         # Main dashboard
│   ├── sensor-controls.html   # Simulation control
│   ├── style.css              # Styles
│   ├── script.js              # Dashboard logic
│   └── src/                   # React components (optional)
│
└── README.md                  # This file

```

---

## 🤖 Machine Learning Model

### Model Details

- **Algorithm**: Random Forest Classifier
- **Features**: pH, Turbidity, Temperature
- **Output**: Safe/Unsafe classification
- **Accuracy**: 100% (on test set)
- **Training Data**: 1000 samples (70% safe, 30% unsafe)

### Model Training

```bash
cd backend
python data_generator.py  # Generate 1000 samples
python train_model.py     # Train model

```

Model is automatically loaded when Flask server starts.

---

## 📊 Water Quality Index (WQI)

WQI is calculated using weighted parameters:

- **pH** (40% weight): Optimal range 6.5-8.5
- **Turbidity** (35% weight): Optimal < 5 NTU
- **Temperature** (25% weight): Optimal 15-25°C

### Alert Levels:

- 🟢 **Green** (WQI ≥ 70): Safe water
- 🟡 **Yellow** (50 ≤ WQI < 70): Caution
- 🔴 **Red** (WQI < 50): Unsafe water

---

## 🔧 Configuration

### WHO Thresholds

Default thresholds can be adjusted:

- pH: 6.5 - 8.5
- Turbidity: 0 - 5 NTU
- Temperature: 15 - 25°C

Update via:

- Dashboard admin panel
- API: `POST /set-thresholds`

### Sensor Simulation

Configure simulation:

- **Interval**: 1-60 seconds (default: 3)
- **Mode**: normal or mixed (includes unsafe readings)

---

## 🧪 Testing

### Test Backend

```bash

# Health check

curl http://localhost:5000/health

# Make prediction

curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

# Get latest readings

curl http://localhost:5000/latest

```

### Test Frontend

1. Open `frontend/index.html` in browser
2. Check backend connection status
3. Navigate to dashboard
4. Start sensor simulation
5. Monitor real-time updates

---

## 🐛 Troubleshooting

### Backend Issues

### "Model not loaded"

```bash
cd backend
python train_model.py  # Retrain model

```

### Port 5000 already in use

- Change port in `app.py`: `app.run(port=5001)`
- Or stop other services using port 5000

### CORS errors

- CORS is enabled for all origins
- Restart Flask server if issues persist

### Frontend Issues

### "Cannot connect to backend"

- Ensure Flask server is running on port 5000
- Check firewall settings
- Verify CORS is enabled

### Charts not displaying

- Check browser console for errors
- Ensure Chart.js is loaded (CDN)
- Verify data format from API

---

## 📈 Performance

- **Prediction Time**: < 10ms
- **Dashboard Refresh**: 3 seconds (configurable)
- **Data Logging**: Real-time (saves to logs.json)
- **Model Accuracy**: 100% on test set

---

## 🔒 Security Notes

- **Development Only**: Current implementation is for development
- **Production**: Implement proper authentication, HTTPS, rate limiting
- **Sensitive Data**: Add encryption for logs and user data

---

## 📝 License

MIT License - See LICENSE file for details

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📞 Support

For issues, questions, or contributions:

- Check documentation in `API_DOCUMENTATION.md`
- Review troubleshooting section
- Open an issue on GitHub

---

## 🎉 Acknowledgments

- WHO Guidelines for water quality thresholds
- scikit-learn for ML algorithms
- Chart.js for data visualization
- Flask for backend framework

---

### Built with ❤️ for water quality monitoring

Last Updated: November 2024

A comprehensive **AI + IoT Early Warning System** that monitors water parameters (pH, turbidity, temperature) and predicts contamination using Machine Learning.

![Status](https://img.shields.io/badge/status-ready-success)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![React](https://img.shields.io/badge/frontend-HTML/CSS/JS-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🎯 Features

### Core Functionality

- ✅ **ML-Powered Predictions** - Random Forest classifier (100% accuracy)
- ✅ **Real-Time Dashboard** - Live monitoring with charts and gauges
- ✅ **Automatic Sensor Simulation** - Continuous data generation
- ✅ **Data Logging** - All readings stored in JSON format
- ✅ **Water Quality Index (WQI)** - Calculated score (0-100)
- ✅ **Early Warning System** - Color-coded alerts (Green/Yellow/Red)

### User Interface

- ✅ **Professional Dashboard** - HTML/CSS/Chart.js interface
- ✅ **Beautiful Homepage** - Landing page with feature cards
- ✅ **Dark Mode Toggle** - Light/dark theme support
- ✅ **Auto-Refresh** - Updates every 3 seconds
- ✅ **Browser Notifications** - Alerts for unsafe water
- ✅ **Responsive Design** - Works on all devices

### Advanced Features

- ✅ **Trend Prediction** - Forecast next hour values
- ✅ **Threshold Configuration** - Adjust WHO guidelines
- ✅ **Sensor Simulator** - Test with realistic data
- ✅ **Historical Data** - View past 10 readings
- ✅ **API Endpoints** - RESTful API for integration

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Node.js 14+ (for React frontend, optional)
- Modern web browser

### Installation

#### 1. Backend Setup

```bash

# Navigate to backend directory

cd backend

# Install Python dependencies

pip install -r requirements.txt

# Generate training dataset

python data_generator.py

# Train ML model

python train_model.py

# Start Flask server

python app.py

```

✅ Backend will run on `http://localhost:5000`

#### 2. Frontend Setup

### Option A: HTML Dashboard (Simple)

- Open `frontend/dashboard.html` in your browser
- Or open `frontend/index.html` for homepage

### Option B: React Dashboard (Advanced)

```bash
cd frontend
npm install
npm run dev

```

✅ Frontend will run on `http://localhost:3000`

---

## 📖 Usage Guide

### Start the System

1. **Start Backend** (Terminal 1):

   ```bash
   cd backend
   python app.py

   ```

2. **Open Dashboard** (Browser):
   - Go to `frontend/index.html` (homepage)
   - Or directly to `frontend/dashboard.html` (dashboard)

3. **Start Sensor Simulation** (Optional):
   - Go to `frontend/sensor-controls.html`
   - Click "Start Simulation"
   - Data will be automatically generated every 3 seconds

### View Dashboard

- **Status Cards** - Current water quality status
- **Circular Gauges** - Visual representation of pH, turbidity, temperature
- **Trend Charts** - Historical data visualization
- **Latest Readings Table** - Past 10 measurements
- **WQI Score** - Water Quality Index (0-100)

### Make Predictions

### Via Dashboard:

- Dashboard auto-refreshes every 3 seconds
- Shows predictions in real-time

### Via API:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

```

---

## 📡 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/login` | POST | User authentication |
| `/predict` | POST | Predict water quality |
| `/latest` | GET | Get last 10 readings |
| `/future-trend` | POST | Predict next hour trends |
| `/get-thresholds` | GET | Get WHO thresholds |
| `/set-thresholds` | POST | Update thresholds |
| `/simulate` | POST | Start sensor simulation |
| `/simulate/stop` | POST | Stop simulation |
| `/simulate/status` | GET | Check simulation status |

**Full API Documentation**: See [API_DOCUMENTATION.md](API_DOCUMENTATION.md)

---

## 🔐 Login Credentials

### Admin:

- Username: `admin`
- Password: `admin123`

### User:

- Username: `user`
- Password: `user123`

---

## 🏗️ Project Structure

```text
water_quality_system/
├── backend/
│   ├── app.py                 # Flask API server
│   ├── data_generator.py      # Generate training dataset
│   ├── preprocessing.py       # Data preprocessing pipeline
│   ├── train_model.py         # Train ML model
│   ├── sensor_simulator.py    # Sensor simulation
│   ├── models/
│   │   ├── model.pkl          # Trained ML model
│   │   └── scaler.pkl         # Feature scaler
│   ├── logs.json              # Data logs
│   ├── thresholds.json        # WHO thresholds
│   └── requirements.txt       # Python dependencies
│
├── frontend/
│   ├── index.html             # Homepage
│   ├── dashboard.html         # Main dashboard
│   ├── sensor-controls.html   # Simulation control
│   ├── style.css              # Styles
│   ├── script.js              # Dashboard logic
│   └── src/                   # React components (optional)
│
└── README.md                  # This file

```

---

## 🤖 Machine Learning Model

### Model Details

- **Algorithm**: Random Forest Classifier
- **Features**: pH, Turbidity, Temperature
- **Output**: Safe/Unsafe classification
- **Accuracy**: 100% (on test set)
- **Training Data**: 1000 samples (70% safe, 30% unsafe)

### Model Training

```bash
cd backend
python data_generator.py  # Generate 1000 samples
python train_model.py     # Train model

```

Model is automatically loaded when Flask server starts.

---

## 📊 Water Quality Index (WQI)

WQI is calculated using weighted parameters:

- **pH** (40% weight): Optimal range 6.5-8.5
- **Turbidity** (35% weight): Optimal < 5 NTU
- **Temperature** (25% weight): Optimal 15-25°C

### Alert Levels:

- 🟢 **Green** (WQI ≥ 70): Safe water
- 🟡 **Yellow** (50 ≤ WQI < 70): Caution
- 🔴 **Red** (WQI < 50): Unsafe water

---

## 🔧 Configuration

### WHO Thresholds

Default thresholds can be adjusted:

- pH: 6.5 - 8.5
- Turbidity: 0 - 5 NTU
- Temperature: 15 - 25°C

Update via:

- Dashboard admin panel
- API: `POST /set-thresholds`

### Sensor Simulation

Configure simulation:

- **Interval**: 1-60 seconds (default: 3)
- **Mode**: normal or mixed (includes unsafe readings)

---

## 🧪 Testing

### Test Backend

```bash

# Health check

curl http://localhost:5000/health

# Make prediction

curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

# Get latest readings

curl http://localhost:5000/latest

```

### Test Frontend

1. Open `frontend/index.html` in browser
2. Check backend connection status
3. Navigate to dashboard
4. Start sensor simulation
5. Monitor real-time updates

---

## 🐛 Troubleshooting

### Backend Issues

### "Model not loaded"

```bash
cd backend
python train_model.py  # Retrain model

```

### Port 5000 already in use

- Change port in `app.py`: `app.run(port=5001)`
- Or stop other services using port 5000

### CORS errors

- CORS is enabled for all origins
- Restart Flask server if issues persist

### Frontend Issues

### "Cannot connect to backend"

- Ensure Flask server is running on port 5000
- Check firewall settings
- Verify CORS is enabled

### Charts not displaying

- Check browser console for errors
- Ensure Chart.js is loaded (CDN)
- Verify data format from API

---

## 📈 Performance

- **Prediction Time**: < 10ms
- **Dashboard Refresh**: 3 seconds (configurable)
- **Data Logging**: Real-time (saves to logs.json)
- **Model Accuracy**: 100% on test set

---

## 🔒 Security Notes

- **Development Only**: Current implementation is for development
- **Production**: Implement proper authentication, HTTPS, rate limiting
- **Sensitive Data**: Add encryption for logs and user data

---

## 📝 License

MIT License - See LICENSE file for details

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📞 Support

For issues, questions, or contributions:

- Check documentation in `API_DOCUMENTATION.md`
- Review troubleshooting section
- Open an issue on GitHub

---

## 🎉 Acknowledgments

- WHO Guidelines for water quality thresholds
- scikit-learn for ML algorithms
- Chart.js for data visualization
- Flask for backend framework

---

### Built with ❤️ for water quality monitoring

Last Updated: November 2024



A comprehensive **AI + IoT Early Warning System** that monitors water parameters (pH, turbidity, temperature) and predicts contamination using Machine Learning.

![Status](https://img.shields.io/badge/status-ready-success)
![Python](https://img.shields.io/badge/python-3.8+-blue)
![React](https://img.shields.io/badge/frontend-HTML/CSS/JS-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 🎯 Features

### Core Functionality

- ✅ **ML-Powered Predictions** - Random Forest classifier (100% accuracy)
- ✅ **Real-Time Dashboard** - Live monitoring with charts and gauges
- ✅ **Automatic Sensor Simulation** - Continuous data generation
- ✅ **Data Logging** - All readings stored in JSON format
- ✅ **Water Quality Index (WQI)** - Calculated score (0-100)
- ✅ **Early Warning System** - Color-coded alerts (Green/Yellow/Red)

### User Interface

- ✅ **Professional Dashboard** - HTML/CSS/Chart.js interface
- ✅ **Beautiful Homepage** - Landing page with feature cards
- ✅ **Dark Mode Toggle** - Light/dark theme support
- ✅ **Auto-Refresh** - Updates every 3 seconds
- ✅ **Browser Notifications** - Alerts for unsafe water
- ✅ **Responsive Design** - Works on all devices

### Advanced Features

- ✅ **Trend Prediction** - Forecast next hour values
- ✅ **Threshold Configuration** - Adjust WHO guidelines
- ✅ **Sensor Simulator** - Test with realistic data
- ✅ **Historical Data** - View past 10 readings
- ✅ **API Endpoints** - RESTful API for integration

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Node.js 14+ (for React frontend, optional)
- Modern web browser

### Installation

#### 1. Backend Setup

```bash

# Navigate to backend directory

cd backend

# Install Python dependencies

pip install -r requirements.txt

# Generate training dataset

python data_generator.py

# Train ML model

python train_model.py

# Start Flask server

python app.py

```

✅ Backend will run on `http://localhost:5000`

#### 2. Frontend Setup

### Option A: HTML Dashboard (Simple)

- Open `frontend/dashboard.html` in your browser
- Or open `frontend/index.html` for homepage

### Option B: React Dashboard (Advanced)

```bash
cd frontend
npm install
npm run dev

```

✅ Frontend will run on `http://localhost:3000`

---

## 📖 Usage Guide

### Start the System

1. **Start Backend** (Terminal 1):

   ```bash
   cd backend
   python app.py

   ```

2. **Open Dashboard** (Browser):
   - Go to `frontend/index.html` (homepage)
   - Or directly to `frontend/dashboard.html` (dashboard)

3. **Start Sensor Simulation** (Optional):
   - Go to `frontend/sensor-controls.html`
   - Click "Start Simulation"
   - Data will be automatically generated every 3 seconds

### View Dashboard

- **Status Cards** - Current water quality status
- **Circular Gauges** - Visual representation of pH, turbidity, temperature
- **Trend Charts** - Historical data visualization
- **Latest Readings Table** - Past 10 measurements
- **WQI Score** - Water Quality Index (0-100)

### Make Predictions

### Via Dashboard:

- Dashboard auto-refreshes every 3 seconds
- Shows predictions in real-time

### Via API:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

```

---

## 📡 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/login` | POST | User authentication |
| `/predict` | POST | Predict water quality |
| `/latest` | GET | Get last 10 readings |
| `/future-trend` | POST | Predict next hour trends |
| `/get-thresholds` | GET | Get WHO thresholds |
| `/set-thresholds` | POST | Update thresholds |
| `/simulate` | POST | Start sensor simulation |
| `/simulate/stop` | POST | Stop simulation |
| `/simulate/status` | GET | Check simulation status |

**Full API Documentation**: See [API_DOCUMENTATION.md](API_DOCUMENTATION.md)

---

## 🔐 Login Credentials

### Admin:

- Username: `admin`
- Password: `admin123`

### User:

- Username: `user`
- Password: `user123`

---

## 🏗️ Project Structure

```text
water_quality_system/
├── backend/
│   ├── app.py                 # Flask API server
│   ├── data_generator.py      # Generate training dataset
│   ├── preprocessing.py       # Data preprocessing pipeline
│   ├── train_model.py         # Train ML model
│   ├── sensor_simulator.py    # Sensor simulation
│   ├── models/
│   │   ├── model.pkl          # Trained ML model
│   │   └── scaler.pkl         # Feature scaler
│   ├── logs.json              # Data logs
│   ├── thresholds.json        # WHO thresholds
│   └── requirements.txt       # Python dependencies
│
├── frontend/
│   ├── index.html             # Homepage
│   ├── dashboard.html         # Main dashboard
│   ├── sensor-controls.html   # Simulation control
│   ├── style.css              # Styles
│   ├── script.js              # Dashboard logic
│   └── src/                   # React components (optional)
│
└── README.md                  # This file

```

---

## 🤖 Machine Learning Model

### Model Details

- **Algorithm**: Random Forest Classifier
- **Features**: pH, Turbidity, Temperature
- **Output**: Safe/Unsafe classification
- **Accuracy**: 100% (on test set)
- **Training Data**: 1000 samples (70% safe, 30% unsafe)

### Model Training

```bash
cd backend
python data_generator.py  # Generate 1000 samples
python train_model.py     # Train model

```

Model is automatically loaded when Flask server starts.

---

## 📊 Water Quality Index (WQI)

WQI is calculated using weighted parameters:

- **pH** (40% weight): Optimal range 6.5-8.5
- **Turbidity** (35% weight): Optimal < 5 NTU
- **Temperature** (25% weight): Optimal 15-25°C

### Alert Levels:

- 🟢 **Green** (WQI ≥ 70): Safe water
- 🟡 **Yellow** (50 ≤ WQI < 70): Caution
- 🔴 **Red** (WQI < 50): Unsafe water

---

## 🔧 Configuration

### WHO Thresholds

Default thresholds can be adjusted:

- pH: 6.5 - 8.5
- Turbidity: 0 - 5 NTU
- Temperature: 15 - 25°C

Update via:

- Dashboard admin panel
- API: `POST /set-thresholds`

### Sensor Simulation

Configure simulation:

- **Interval**: 1-60 seconds (default: 3)
- **Mode**: normal or mixed (includes unsafe readings)

---

## 🧪 Testing

### Test Backend

```bash

# Health check

curl http://localhost:5000/health

# Make prediction

curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"ph": 7.2, "turbidity": 3.4, "temperature": 25.8}'

# Get latest readings

curl http://localhost:5000/latest

```

### Test Frontend

1. Open `frontend/index.html` in browser
2. Check backend connection status
3. Navigate to dashboard
4. Start sensor simulation
5. Monitor real-time updates

---

## 🐛 Troubleshooting

### Backend Issues

### "Model not loaded"

```bash
cd backend
python train_model.py  # Retrain model

```

### Port 5000 already in use

- Change port in `app.py`: `app.run(port=5001)`
- Or stop other services using port 5000

### CORS errors

- CORS is enabled for all origins
- Restart Flask server if issues persist

### Frontend Issues

### "Cannot connect to backend"

- Ensure Flask server is running on port 5000
- Check firewall settings
- Verify CORS is enabled

### Charts not displaying

- Check browser console for errors
- Ensure Chart.js is loaded (CDN)
- Verify data format from API

---

## 📈 Performance

- **Prediction Time**: < 10ms
- **Dashboard Refresh**: 3 seconds (configurable)
- **Data Logging**: Real-time (saves to logs.json)
- **Model Accuracy**: 100% on test set

---

## 🔒 Security Notes

- **Development Only**: Current implementation is for development
- **Production**: Implement proper authentication, HTTPS, rate limiting
- **Sensitive Data**: Add encryption for logs and user data

---

## 📝 License

MIT License - See LICENSE file for details

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📞 Support

For issues, questions, or contributions:

- Check documentation in `API_DOCUMENTATION.md`
- Review troubleshooting section
- Open an issue on GitHub

---

## 🎉 Acknowledgments

- WHO Guidelines for water quality thresholds
- scikit-learn for ML algorithms
- Chart.js for data visualization
- Flask for backend framework

---

### Built with ❤️ for water quality monitoring

Last Updated: November 2024




