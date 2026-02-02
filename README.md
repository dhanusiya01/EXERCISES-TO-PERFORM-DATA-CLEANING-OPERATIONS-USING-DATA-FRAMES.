# EXERCISES-TO-PERFORM-DATA-CLEANING-OPERATIONS-USING-DATA-FRAMES.
Pip install pandas
Pip instal numpy 
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler
df = pd.DataFrame({
    'Date': ['2023-01-01', '02-01-2023', 'Invalid'],
    'Category': ['Apple', 'apple', 'Banana'],
    'Value': [10, 1500, 20],
    'Missing': [1, np.nan, 3]
})

print("Original Data:\n", df)
df.drop_duplicates(inplace=True)
df['Missing'] = df['Missing'].fillna(df['Missing'].mean())
df['Date'] = pd.to_datetime(df['Date'], errors='coerce')
df['Date'] = df['Date'].ffill()
df['Category'] = df['Category'].str.lower()
df['Value'] = df['Value'].clip(upper=100)
scaler = MinMaxScaler()
df['Value_norm'] = scaler.fit_transform(df[['Value']])

print("\nCleaned Data:\n", df)

Output:

Original Data:
          Date Category  Value  Missing
0  2023-01-01    Apple     10      1.0
1  02-01-2023    apple   1500      NaN
2     Invalid   Banana     20      3.0

Cleaned Data:
         Date Category  Value  Missing  Value_norm
0 2023-01-01    apple     10      1.0    0.000000
1 2023-01-01    apple    100      2.0    1.000000
2 2023-01-01   banana     20      3.0    0.111111


