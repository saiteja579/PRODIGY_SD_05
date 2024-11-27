# PRODIGY_SD_05
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Load the dataset (assuming 'US_Accidents_Dataset.csv' is available locally)
df = pd.read_csv('US_Accidents_Dataset.csv')

# Data Cleaning: Select relevant columns and drop rows with missing values
df = df[['Start_Time', 'Weather_Condition', 'Road_Condition', 'Severity']]
df.dropna(inplace=True)

# Extract hour from Start_Time
df['Hour'] = pd.to_datetime(df['Start_Time']).dt.hour

# Plot 1: Accidents by Time of Day (Hourly distribution)
plt.figure(figsize=(10, 6))
sns.countplot(x='Hour', data=df, palette='coolwarm')
plt.title('Accidents by Hour of Day')
plt.xlabel('Hour')
plt.ylabel('Number of Accidents')
plt.show()

# Plot 2: Accidents by Weather Condition
plt.figure(figsize=(12, 8))
sns.countplot(y='Weather_Condition', data=df, order=df['Weather_Condition'].value_counts().iloc[:10].index)
plt.title('Top 10 Weather Conditions Leading to Accidents')
plt.xlabel('Number of Accidents')
plt.ylabel('Weather Condition')
plt.show()

# Plot 3: Severity of Accidents under Different Road Conditions
plt.figure(figsize=(10, 6))
sns.countplot(x='Road_Condition', hue='Severity', data=df)
plt.title('Severity of Accidents by Road Condition')
plt.xlabel('Road Condition')
plt.ylabel('Count')
plt.legend(title='Severity')
plt.show()
