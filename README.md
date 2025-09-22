# API-INTEGRATION-AND-DATA-VISUALIZATION-
import requests
import matplotlib.pyplot as plt


API_KEY = "your_api_key_here"   
CITY = "London"
URL = f"http://api.openweathermap.org/data/2.5/forecast?q={CITY}&appid={API_KEY}&units=metric"

response = requests.get(URL)
data = response.json()


dates = []
temps = []

for forecast in data['list'][:10]:  # first 10 forecast entries
    dates.append(forecast['dt_txt'])
    temps.append(forecast['main']['temp'])


plt.figure(figsize=(10,5))
plt.plot(dates, temps, marker='o', linestyle='-', color='b')
plt.title(f"Weather Forecast for {CITY}")
plt.xlabel("Date & Time")
plt.ylabel("Temperature (°C)")
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
