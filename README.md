# Exno:1
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
DATA CLEANING
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![1](/1.png)
![2](/2.png)

```
df.isnull().sum()
```
![3](/3.png)

```
df.isnull().any()
```
![4](/4.png)

```
df.dropna()
```
![5](/5.png)

```
df.fillna(0)
```
![6](/6.png)
![7](/7.png)

```
df.fillna(method='ffill')
```
![8](/8.png)
![9](/9.png)

```
df.fillna(method = 'bfill')
```
![10](/10.png)
![11](/11.png)

```
df_dropped=df.dropna()
df_dropped
```
![12](/12.png)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![13](/13.png)
![14](/14.png)

<center><b>IQR(Inter Quartile Range)</b></center>

```
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
```
![15](/15.png)

```
ir.describe()
```
![16](/16.png)

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![17](/17.png)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![18](/18.png)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![19](/19.png)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![20](/20.png)

```
sns.boxplot(x='sepal_width',data=delid)
```
![21](/21.png)

<center><b>Z-SCORE</b></center>

```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![22](/22.png)

```
df = pd.read_csv("/content/heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![23](/23.png)

```
low = q1 - 1.5*iqr
low
```
![24](/24.png)

```
high = q3 + 1.5*iqr
high
```
![25](/25.png)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![26](/26.png)

```
z = np.abs(stats.zscore(df['height']))
z
```
![27](/27.png)

```
df1 = df[z<3]
df1
```
![28](/28.png)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
