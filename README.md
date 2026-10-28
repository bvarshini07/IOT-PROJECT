# PowerRoad-AI

PowerRoad-AI is a smart piezoelectric road simulation and prototype project for generating energy from vehicle pressure, monitoring telemetry, and predicting future energy output using a machine learning model.

## Project objective

The project demonstrates:
- piezoelectric energy harvesting concept
- ESP32-style embedded prototype flow
- HC-SR04 vehicle detection logic
- voltage, power, and energy calculations
- CSV-based historical data analysis
- Python ML prediction model
- React dashboard with visual analytics

## Folder structure

- frontend/ — Vite + React dashboard
- backend/ — Flask API and ML pipeline
- hardware/ — ESP32 sketch and Wokwi notes
- docs/ — report and presentation content

## Windows setup

### Quick start in VS Code

1. Install Node.js 22.12 or newer and Python 3.13.
2. In the project root, create the backend environment and install its requirements:

   ```powershell
   python -m venv .venv
   .venv\Scripts\python.exe -m pip install -r backend\requirements.txt
   ```

3. Install the frontend dependencies once:

   ```powershell
   cd frontend
   npm install
   cd ..
   ```

4. In VS Code, choose **Run and Debug → PowerRoad-AI Dashboard**. This starts the backend and Vite dev server, then opens the dashboard. Alternatively, run the **PowerRoad: Start all** task.

The dashboard is at http://localhost:5173 and the backend health check is at http://localhost:5000/api/health.

### Manual startup

```powershell
cd c:\IOT PEOJECT
.\.venv\Scripts\python.exe backend\app.py
```

In a second terminal:

```powershell
cd c:\IOT PEOJECT\frontend
npm run dev
```

## Dashboard controls

- Start Simulation
- Stop Simulation
- Reset Simulation
- Pass Vehicle
- Traffic mode selector
- Export CSV
- Refresh data
- Upload a CSV dataset to retrain the prediction model

The simulation advances once per second while it is running and pauses when stopped. Telemetry history is held in memory and resets when the backend restarts.

### Dataset format

CSV uploads must contain `Time`, `VehicleCount`, `Distance`, `Voltage`, `Power`, `Energy_J`, and `Energy_Wh` columns. The model predicts energy generated during the next interval (the non-negative difference between consecutive cumulative `Energy_J` values); `PreviousEnergyJ` is the previous cumulative reading supplied to the model.

## Academic notes

- The current project uses a software simulation of the piezoelectric voltage signal.
- The ESP32/Wokwi prototype is simulated unless a real serial or MQTT bridge is configured.
- The power equation uses a 50 Ω model for demonstration only and is not a physical proof of real-world output.

## Main execution order

1. Start the backend Python server.
2. Start the frontend dashboard.
3. Use the dashboard to run the simulation and test AI prediction.
4. Export the generated CSV data for academic reporting.
