# Exno:1 - Data Cleaning Process

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
## Data Cleansing
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![Screenshot 2024-08-17 135507](https://github.com/user-attachments/assets/6b99f696-028d-44b0-b932-2222a751c874)

```
df.head()
```
![Screenshot 2024-08-17 135606](https://github.com/user-attachments/assets/df9beecc-d8b0-41c9-9e51-e3645e651b5a)

```
df.head(6)
```
![Screenshot 2024-08-17 135653](https://github.com/user-attachments/assets/a9e1c235-8140-4871-a6c5-94f94bc8e5a7)

```
df.tail()
```
![Screenshot 2024-08-17 135737](https://github.com/user-attachments/assets/a7643b7b-2aff-4031-9bef-0c58f5297a4c)
```
df.isnull()
```

![Screenshot 2024-08-17 135840](https://github.com/user-attachments/assets/ef23e628-2807-483c-8448-5df6715a2d1a)
```
df.notnull()
```

![Screenshot 2024-08-17 135956](https://github.com/user-attachments/assets/05931aa4-576e-4e68-8c4a-7c6867a73b84)
```
df.dropna(axis=0)
```

![Screenshot 2024-08-17 140038](https://github.com/user-attachments/assets/6183401d-e8cd-4d5c-8b41-8b7783f157a8)
```
df.dropna(axis=1)
```


![Screenshot 2024-08-17 140122](https://github.com/user-attachments/assets/75d0e5ff-9668-47b3-b781-93674480b50b)

```
df.fillna(0)
```

![Screenshot 2024-08-17 140215](https://github.com/user-attachments/assets/192047f2-be05-4267-ba5b-bc2ba4a71748)

```
print(df.shape)
```

![Screenshot 2024-08-17 140347](https://github.com/user-attachments/assets/c6a4491e-fe8a-411e-9fdb-e8bbdd28eb71)
```
df.shape
```

![Screenshot 2024-08-17 140347](https://github.com/user-attachments/assets/43dfd142-326a-490e-a9d1-6f37769bb535)

```
df.describe()
```

![Screenshot 2024-08-17 140656](https://github.com/user-attachments/assets/74828f7d-1d70-4ef9-af04-d625f5031c2c)

## IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
```

![Screenshot 2024-08-17 140908](https://github.com/user-attachments/assets/b3fe2566-673f-43e1-b93e-196f232b6baf)
```
ir.describe()
```

![Screenshot 2024-08-17 140946](https://github.com/user-attachments/assets/05d90ce0-13bf-4fb0-973e-5275357b89a8)
```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```

![Screenshot 2024-08-17 141040](https://github.com/user-attachments/assets/8c1c7d64-38ae-405a-b930-8ce81e07809f)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```

![Screenshot 2024-08-17 141132](https://github.com/user-attachments/assets/b5a71ff7-3c4f-4e2b-9509-4faf4b020ac9)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![Screenshot 2024-08-17 141218](https://github.com/user-attachments/assets/9fcb4e19-4434-43f7-9450-4f1907ef8226)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![Screenshot 2024-08-17 141330](https://github.com/user-attachments/assets/bd2fad06-fe33-4635-a875-ccda668aa800)
```
sns.boxplot(x='sepal_width',data=delid)
```

![Screenshot 2024-08-17 141419](https://github.com/user-attachments/assets/2320d014-46d2-4d3a-8e6e-9a3db269f9cb)
## Z-Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```

![Screenshot 2024-08-17 141626](https://github.com/user-attachments/assets/5141e114-2961-418a-8dc2-2c0ae20a3963)
```
df=pd.read_csv("/content/heights.csv")
q1=df['height'].quantile(0.25)
q2=df['height'].quantile(0.5)
q3=df['height'].quantile(0.75)
iqr=q3-q1
iqr
```

![Screenshot 2024-08-17 141843](https://github.com/user-attachments/assets/86880ebb-e70d-48ee-95de-3c611e98e4d0)
```
low=q1-1.5*iqr
low
```

![Screenshot 2024-08-17 141925](https://github.com/user-attachments/assets/bb9c4d85-245e-49ce-8cc0-2e2d6a2ead26)
```
high=q3+1.5*iqr
high
```

![Screenshot 2024-08-17 142043](https://github.com/user-attachments/assets/5e03da44-41fe-4057-b2be-5c6b492705ef)
```
df1=df[((df['height']>=low)&(df['height']<=high))]
df1
```

![Screenshot 2024-08-17 142136](https://github.com/user-attachments/assets/6de26dd4-6afe-4f07-b821-0b26c997e240)
```
z=np.abs(stats.zscore(df['height']))
z
```

![Screenshot 2024-08-17 142226](https://github.com/user-attachments/assets/87ddc494-5730-4764-9263-290090c0115f)
```
df1=df[z<3]
df1
```

![Screenshot 2024-08-17 142312](https://github.com/user-attachments/assets/0da3f59e-1615-4cbf-aec0-b627390683b7)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
