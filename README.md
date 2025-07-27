# 🔥 AI-Based Wildfire Prediction System

A low-power, edge-AI wildfire prediction system built using the **Renesas RA6E2 microcontroller**, environmental sensors, and machine learning to detect early wildfire risks and send real-time alerts.

## 📦 Features

- Real-time monitoring of **temperature, humidity, and AQI**
- **Random Forest + ULSTM** hybrid model for fire risk prediction
- **Edge inference** on Renesas MCU
- **Wi-Fi connectivity** with Adafruit IO for cloud backup
- **Streamlit GUI** for visualization and user registration
- **WhatsApp alerts** using Twilio API and MySQL backend

## 🧠 System Architecture

- **Sensors**: PMOD HS001 (temp & humidity), ZMOD 4510 (AQI)
- **Microcontroller**: Renesas RA6E2 (Cortex-M33)
- **Connectivity**: DA16600 Wi-Fi module (MQTT)
- **AI**: Random Forest (training) + dynamic risk scaling
- **Cloud**: Adafruit IO for real-time dashboard
- **Frontend**: Streamlit-based GUI
- **Alerts**: WhatsApp via Node.js + SQL trigger

## 🚀 Deployment Flow

1. Sensor data collected by Renesas board
2. Data analyzed locally with hybrid ML model
3. Results published to Adafruit IO (MQTT)
4. Dashboard shows real-time risk on Streamlit
5. When threshold crossed, WhatsApp alerts sent

## 📊 Risk Calculation Logic

```python
# Temperature-Humidity interaction
th_interact = temp * (100 - humidity)

# Temperature-AQI interaction
tp_interact = temp * AQI

# Dynamic threshold scaling
if temp > 35:
    risk *= min(1.5, 1 + 0.05 * (temp - 35))

# Trigger alert
if temp > 50:
    alert_threshold = 0.15
else:
    alert_threshold = 0.40

if risk > alert_threshold:
    send_alert()
