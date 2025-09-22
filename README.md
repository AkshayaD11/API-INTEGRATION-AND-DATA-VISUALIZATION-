# API-INTEGRATION-AND-DATA-VISUALIZATION-
# api_data_visualization.py

import requests
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

url = "https://api.coingecko.com/api/v3/coins/markets"
params = {
    "vs_currency": "usd",   # prices in USD
    "order": "market_cap_desc",
    "per_page": 10,         # top 10 cryptocurrencies
    "page": 1,
    "sparkline": False
}

response = requests.get(url, params=params)
data = response.json()

df = pd.DataFrame(data, columns=[
    "id", "symbol", "name", "current_price", "market_cap",
    "total_volume", "price_change_percentage_24h"
])

print("Top 10 Cryptocurrencies Data:")
print(df.head())

plt.figure(figsize=(15, 10))

plt.subplot(2, 2, 1)
sns.barplot(x="market_cap", y="name", data=df, palette="viridis")
plt.title("Top 10 Cryptos by Market Cap")

plt.subplot(2, 2, 2)
sns.barplot(x="current_price", y="name", data=df, palette="coolwarm")
plt.title("Current Prices (USD)")

plt.subplot(2, 2, 3)
sns.barplot(x="total_volume", y="name", data=df, palette="magma")
plt.title("24h Trading Volume")

plt.subplot(2, 2, 4)
sns.barplot(x="price_change_percentage_24h", y="name", data=df, palette="Spectral")
plt.title("24h Price Change (%)")

plt.tight_layout()
plt.show()
