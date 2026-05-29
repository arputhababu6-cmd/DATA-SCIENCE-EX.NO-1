#EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

```
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt


df = pd.read_csv("SAMPLEIDS.csv")

print("DATASET:\n")
print(df)
print("\nFIRST 5 ROWS:\n")
print(df.head())

print("\nLAST 5 ROWS:\n")
print(df.tail())
print("\nDATASET INFO:\n")
print(df.info())

print("\nSTATISTICAL SUMMARY:\n")
print(df.describe())

print("\nNULL VALUES COUNT:\n")
print(df.isnull().sum())

print("\nANY NULL VALUES?\n")
print(df.isnull().any())

print("\nDROP NULL VALUES:\n")
print(df.dropna())

print("\nFILL NULL VALUES WITH 0:\n")
print(df.fillna(0))

print("\nFORWARD FILL METHOD:\n")
print(df.fillna(method='ffill'))

print("\nFILL SPECIFIC COLUMNS:\n")
print(df.fillna({'GENDER': 'MALE', 'NAME': 'SRI'}))

ir = pd.read_csv("iris.csv")

print("\nIRIS DATASET:\n")
print(ir)

print("\nIRIS DATASET DESCRIPTION:\n")
print(ir.describe())


sns.boxplot(x='sepal_width', data=ir)

plt.title("Boxplot Before Removing Outliers")
plt.show()


ir.plot.scatter(
    x='sepal_length',
    y='sepal_width',
    title="Before Removing Outliers"
)

plt.show()



Q1 = ir.sepal_width.quantile(0.25)
Q3 = ir.sepal_width.quantile(0.75)

IQR = Q3 - Q1

print("\nIQR VALUE:\n")
print(IQR)


outliers = ir[
    (
        (ir.sepal_width < (Q1 - 1.5 * IQR)) |
        (ir.sepal_width > (Q3 + 1.5 * IQR))
    )
]

print("\nOUTLIERS:\n")
print(outliers['sepal_width'])



ran = ir[
    ~(
        (ir.sepal_width < (Q1 - 1.5 * IQR)) |
        (ir.sepal_width > (Q3 + 1.5 * IQR))
    )
]

print("\nCLEANED DATA USING IQR:\n")
print(ran['sepal_width'].head())

sns.boxplot(x='sepal_width', data=ran)

plt.title("Boxplot After IQR")
plt.show()

ran.plot.scatter(
    x='sepal_length',
    y='sepal_width',
    title="After IQR Outlier Removal"
)

plt.show()

z = np.abs(stats.zscore(ir['petal_length']))

print("\nZ-SCORES:\n")
print(z)


ir1 = ir[z < 3]

print("\nCLEANED DATA USING Z-SCORE:\n")
print(ir1.head())

ir1.plot.scatter(
    x='petal_length',
    y='petal_width',
    title="After Z-score Outlier Removal"
)

plt.show() 

```
<img width="747" height="332" alt="image" src="https://github.com/user-attachments/assets/86212520-8bac-4ddd-aa10-c836ab153444" />
<img width="764" height="329" alt="image" src="https://github.com/user-attachments/assets/3f849689-cd37-4306-9468-fdc4d32be5cc" />
<img width="790" height="323" alt="image" src="https://github.com/user-attachments/assets/f4ad2162-210d-4a27-977d-daed5897d92a" />
<img width="854" height="331" alt="image" src="https://github.com/user-attachments/assets/c0886bb5-a93c-4207-b9c3-4ba8c642eb6d" />
<img width="822" height="335" alt="image" src="https://github.com/user-attachments/assets/f320db3d-6298-4a11-aa0f-0524d68e9a31" />
<img width="833" height="342" alt="image" src="https://github.com/user-attachments/assets/cfcc9645-6554-4a80-94ae-7f78455bb202" />
<img width="739" height="338" alt="image" src="https://github.com/user-attachments/assets/4a723a5e-771d-405d-af46-ec403d9dbbc8" />
<img width="799" height="343" alt="image" src="https://github.com/user-attachments/assets/e4592ef0-9f88-43f0-bc82-a1dab2dc92ce" />
<img width="868" height="328" alt="image" src="https://github.com/user-attachments/assets/721389ab-586f-4f85-95e1-046b987aee9e" />
<img width="742" height="320" alt="image" src="https://github.com/user-attachments/assets/a7f98910-e743-4599-a57c-b6fa81ddf710" />
<img width="705" height="328" alt="image" src="https://github.com/user-attachments/assets/0fa3a4fc-efb5-481d-a521-f60454658f03" />
<img width="724" height="342" alt="image" src="https://github.com/user-attachments/assets/7041ab82-39e4-4785-b983-b426e355bed5" />
<img width="813" height="329" alt="image" src="https://github.com/user-attachments/assets/c73c52b8-872b-4695-9509-a7a1aba1dcc6" />
<img width="528" height="453" alt="image" src="https://github.com/user-attachments/assets/7cf2f464-b58a-4582-9573-ca3e46818196" />
<img width="568" height="453" alt="image" src="https://github.com/user-attachments/assets/70a9957a-5c15-417c-8416-9fbf99fac7f9" />
<img width="785" height="414" alt="image" src="https://github.com/user-attachments/assets/88d4c79c-efa2-4e46-ad85-6a273ce2dbba" />
<img width="520" height="453" alt="image" src="https://github.com/user-attachments/assets/d0b7227a-32c8-43ef-bb75-839c1e9ae339" />
<img width="577" height="453" alt="image" src="https://github.com/user-attachments/assets/92de0bc4-68e6-4c8c-bfac-316475bcd59a" />
<img width="763" height="333" alt="image" src="https://github.com/user-attachments/assets/24ab9935-1d8f-4033-9095-e250e775bafe" />
<img width="567" height="453" alt="image" src="https://github.com/user-attachments/assets/0772b035-145d-455f-8b32-f1360f86fb90" />

# Result
      Thus,the given data is cleaned and the outliers removed using python.
