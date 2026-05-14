# Ex-01_DS_Data_Cleansing


## AIM
To read the given data and perform data cleaning and save the cleaned data to a file. 

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. 
Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information. 

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Get the information about the data
### STEP 3
Remove the null values from the data
### STEP 4
Save the Clean data to the file

# CODE and OUTPUT
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt

# Read dataset
df = pd.read_csv("SAMPLEIDS.csv")
df
df.head()
df.tail()
df.info()
df.describe()
df.isnull().sum()
df.isnull().any()

df.dropna()
df.fillna(0)
df.fillna(method='ffill')
df.fillna({'GENDER':'MALE','NAME':'SRI'})

# Iris dataset
ir = pd.read_csv("iris.csv")
ir
ir.describe()

sns.boxplot(x='sepal_width', data=ir)
plt.title("Boxplot Before Removing Outliers")
plt.show()

ir.plot.scatter(x='sepal_length', y='sepal_width', title="Before Removing Outliers")
plt.show()


Q1 = ir.sepal_width.quantile(0.25)
Q3 = ir.sepal_width.quantile(0.75)
IQR = Q3 - Q1
print(IQR)

# Find Outliers
outliers = ir[((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
print("Outliers:\n", outliers['sepal_width'])

# Remove outliers (using ~ to negate the condition)
ran = ir[~((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
print("Cleaned Data (IQR):\n", ran['sepal_width'].head())

# Plot After IQR
sns.boxplot(x='sepal_width', data=ran)
plt.title("Boxplot After IQR")
plt.show()

ran.plot.scatter(x='sepal_length', y='sepal_width', title="After IQR Outlier Removal")
plt.show()

# --- 4. Z-SCORE OUTLIER REMOVAL (petal_length) ---
z = np.abs(stats.zscore(ir['petal_length']))
print("Z-scores:\n", z)

# Keep data where z-score is less than 3
ir1 = ir[z < 3]
print("Cleaned Data (Z-Score):\n", ir1.head())

ir1.plot.scatter(x='petal_length', y='petal_width', title="After Z-score Outlier Removal")
plt.show()

# OUTPUT

<img width="838" height="857" alt="image" src="https://github.com/user-attachments/assets/721a6c5d-9cbc-4b72-a6d4-99f6ad47c8d5" />
<img width="737" height="867" alt="image" src="https://github.com/user-attachments/assets/09012755-32f1-446d-83f5-90b48b051a39" />
<img width="562" height="281" alt="image" src="https://github.com/user-attachments/assets/c3083d84-e6dc-404d-bd10-f730f5fa3c98" />

<img width="780" height="870" alt="image" src="https://github.com/user-attachments/assets/2234472f-d655-466d-b37c-6da17fb1da97" />

<img width="803" height="822" alt="image" src="https://github.com/user-attachments/assets/dfd997f7-c3ee-483e-a913-464a3d87f443" />
