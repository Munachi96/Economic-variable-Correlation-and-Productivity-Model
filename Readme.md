``` Python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load the data
usa_m1 = pd.read_excel("C:Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\M1 usa.xlsx", parse_dates=['Year'], index_col='Year')
usa_stock_market = pd.read_excel("C:\Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\stock usa.xlsx", parse_dates=['Year'], index_col='Year')
usa_inflation = pd.read_excel("C:\Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\inflation.xlsx", parse_dates=['Year'], index_col='Year')

nigeria_m1 = pd.read_excel("C:\Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\M1 Nigeria.xlsx", parse_dates=['Year'], index_col='Year')
nigeria_stock_market = pd.read_excel("C:\Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\stock Nig.xlsx", parse_dates=['Year'], index_col='Year')
nigeria_inflation = pd.read_excel("C:\Users\user\OneDrive\Desktop\MY EXCEL WORK\mid-hng\Inflation Nig.xlsx", parse_dates=['Year'], index_col='Year')

# Plot the data
fig, axs = plt.subplots(4, 2, figsize=(15, 10))

axs[0, 0].plot(usa_m1.index, usa_m1['M1'])
axs[0, 0].set_title('USA M1 Money Supply')
axs[0, 1].plot(nigeria_m1.index, nigeria_m1['M1'])
axs[0, 1].set_title('Nigeria M1 Money Supply')

axs[2, 0].plot(usa_stock_market.index, usa_stock_market['Stock Market'])
axs[2, 0].set_title('USA Stock Market Performance')
axs[2, 1].plot(nigeria_stock_market.index, nigeria_stock_market['Stock Market'])
axs[2, 1].set_title('Nigeria Stock Market Performance')

axs[3, 0].plot(usa_inflation.index, usa_inflation['Inflation'])
axs[3, 0].set_title('USA Inflation Rate')
axs[3, 1].plot(nigeria_inflation.index, nigeria_inflation['Inflation'])
axs[3, 1].set_title('Nigeria Inflation Rate')

plt.tight_layout()
plt.show()

# Correlation analysis
usa_data = pd.concat([usa_m1, usa_stock_market, usa_inflation], axis=1).dropna()
nigeria_data = pd.concat([nigeria_m1, nigeria_stock_market, nigeria_inflation], axis=1).dropna()

usa_corr = usa_data.corr()
nigeria_corr = nigeria_data.corr()

print("USA Correlation Matrix")
print(usa_corr)
print("\nNigeria Correlation Matrix")
print(nigeria_corr)

# Time-shifted correlations
lag = 1  # Example lag of 12 months
usa_data_lagged = usa_data.shift(lag)
nigeria_data_lagged = nigeria_data.shift(lag)

usa_corr_lagged = usa_data.corrwith(usa_data_lagged, axis=0)
nigeria_corr_lagged = nigeria_data.corrwith(nigeria_data_lagged, axis=0)

print("\nUSA Time-Shifted Correlations")
print(usa_corr_lagged)
print("\nNigeria Time-Shifted Correlations")
print(nigeria_corr_lagged)

# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Assume data is already loaded into the following DataFrames
# usa_m1, usa_stock_market, usa_inflation
# nigeria_m1, nigeria_stock_market, nigeria_inflation

# Load the data
usa_m1 = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/M1 Usa.xlsx', parse_dates=['Year'], index_col='Year')
usa_stock_market = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Stock Usa.xlsx', parse_dates=['Year'], index_col='Year')
usa_inflation = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Usa Inf.xlsx', parse_dates=['Year'], index_col='Year')

nigeria_m1 = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/M1 Nigeria.xlsx', parse_dates=['Year'], index_col='Year')
nigeria_stock_market = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Stock Nigeria.xlsx', parse_dates=['Year'], index_col='Year')
nigeria_inflation = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Nigeria Inf.xlsx', parse_dates=['Year'], index_col='Year')

# Function to normalize data
def normalize(df, column_name):
    return (df[column_name] - df[column_name].min()) / (df[column_name].max() - df[column_name].min())

# Normalize USA data
usa_m1['M1_normalized'] = normalize(usa_m1, 'M1')
usa_stock_market['Stock_market_normalized'] = normalize(usa_stock_market, 'Stock Market')
usa_inflation['Inflation_normalized'] = normalize(usa_inflation, 'Inflation')

# Normalize Nigeria data
nigeria_m1['M1_normalized'] = normalize(nigeria_m1, 'M1')
nigeria_stock_market['Stock_market_normalized'] = normalize(nigeria_stock_market, 'Stock Market')
nigeria_inflation['Inflation_normalized'] = normalize(nigeria_inflation, 'Inflation')

# Calculate the productivity index for USA
usa_productivity = pd.DataFrame(index=usa_m1.index)
usa_productivity['Productivity'] = (usa_m1['M1_normalized'] + usa_stock_market['Stock_market_normalized'] - usa_inflation['Inflation_normalized']) / 3

# Calculate the productivity index for Nigeria
nigeria_productivity = pd.DataFrame(index=nigeria_m1.index)
nigeria_productivity['Productivity'] = (nigeria_m1['M1_normalized'] + nigeria_stock_market['Stock_market_normalized'] - nigeria_inflation['Inflation_normalized']) / 3

# Plot the productivity index
plt.figure(figsize=(10, 5))

plt.subplot(2, 1, 1)
plt.plot(usa_productivity.index, usa_productivity['Productivity'], label='USA Productivity')
plt.title('USA Productivity Index')
plt.xlabel('Year')
plt.ylabel('Productivity Index')
plt.legend()

plt.subplot(2, 1, 2)
plt.plot(nigeria_productivity.index, nigeria_productivity['Productivity'], label='Nigeria Productivity')
plt.title('Nigeria Productivity Index')
plt.xlabel('Year')
plt.ylabel('Productivity Index')
plt.legend()

plt.tight_layout()
plt.show()

nigeria_productivity['Productivity']

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Sample Data (to be replaced with actual data)
# Assume data is available in the following DataFrames with columns: 'Year', 'Exchange Rate', 'Inflation', 'Productivity'
usa_inflation = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Usa Inf.xlsx', parse_dates=['Year'], index_col='Year')
Productivity_USA =  pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Usa Prod.xlsx', parse_dates=['Year'], index_col='Year')


nigeria_inflation = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Nigeria Inf.xlsx', parse_dates=['Year'], index_col='Year')
nigeria_exchange_rate = pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Exch.xlsx', parse_dates=['Year'], index_col='Year')
Productivity_Nigeria =  pd.read_excel('C:/Users/v v/Desktop/HNG/mid/Nig Prod.xlsx', parse_dates=['Year'], index_col='Year')

usa_data = pd.concat([usa_inflation, Productivity_USA], axis=1).dropna()
nigeria_data = pd.concat([nigeria_inflation, nigeria_exchange_rate, Productivity_Nigeria], axis=1).dropna()

# Merge data for analysis
data = usa_data.merge(nigeria_data, on='Year', suffixes=('_USA', '_Nigeria'))

# Calculate real exchange rate
data['Real_Exchange_Rate'] = data['Exchange Rate'] * (data['Productivity_USA'] / data['Productivity_Nigeria']) * (data['Inflation_Nigeria'] / data['Inflation_USA'])

# Calculate real currency devaluation
data['Real_Devaluation'] = data['Real_Exchange_Rate'].pct_change() * 100  # Percentage change

# Plot the real exchange rate and devaluation
plt.figure(figsize=(12, 5))

plt.subplot(2, 1, 1)
plt.plot(data.index, data['Real_Exchange_Rate'], label='Real Exchange Rate')
plt.title('Real Exchange Rate (Nigeria to USD)')
plt.xlabel('Year')
plt.ylabel('Real Exchange Rate')
plt.legend()

plt.subplot(2, 1, 2)
plt.plot(data.index, data['Real_Devaluation'], label='Real Currency Devaluation')
plt.title('Real Currency Devaluation')
plt.xlabel('Year')
plt.ylabel('Devaluation (%)')
plt.legend()

plt.tight_layout()
plt.show()

```
