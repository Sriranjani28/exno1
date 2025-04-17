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
import pandas as pd

df=pd.read_csv("/content/SAMPLEIDS.csv")

df

df.isnull()
<img width="473" alt="ds ss01" src="https://github.com/user-attachments/assets/6f8f7e73-065c-4c09-a978-64f775a5f1f5" />

df.notnull()
<img width="496" alt="ds ss02" src="https://github.com/user-attachments/assets/fe9df29c-81c2-49f5-a8a4-535ad875c1e3" />


df.dropna(axis=1)
<img width="488" alt="ds ss03" src="https://github.com/user-attachments/assets/c6a9f916-abfb-4814-b935-8e500b4fd0f2" />


df.dropna(axis=0)
<img width="194" alt="ds ss04" src="https://github.com/user-attachments/assets/58adced2-9038-47f4-a777-5947598e9483" />


dfs=df[df['TOTAL']>270]
<img width="524" alt="ds ss05" src="https://github.com/user-attachments/assets/03dd75e9-4bfe-481d-b0ea-9121aa17a1d4" />


dfs

dfs=df[df['NAME'].str.startswith(('A','C'))&(df['TOTAL']>250)]

<img width="461" alt="ds ss06" src="https://github.com/user-attachments/assets/7502635b-8512-4e1c-9b46-be444f148623" />


dfs


df.iloc[:4]
<img width="321" alt="ds ss07" src="https://github.com/user-attachments/assets/3474844e-be7d-4f92-9b9f-df61c2d367f1" />


df.iloc[0:4,1:4]
<img width="454" alt="ds ss08" src="https://github.com/user-attachments/assets/c151d5b1-d6b2-4bd7-b570-e2d148e94b80" />


df.iloc[[1,3,5],[1,3]]
<img width="208" alt="ds ss09" src="https://github.com/user-attachments/assets/c4a65f46-0ad1-4f7f-b743-5c06738d0f09" />


df
<img width="145" alt="ds ss10" src="https://github.com/user-attachments/assets/4ae2549c-db51-4f90-b6ed-f7fbc7735a90" />


dff=df.fillna(0)
<img width="494" alt="ds ss11" src="https://github.com/user-attachments/assets/c8d335bb-b1df-4a6b-b4db-9da6d4e7b03f" />


dff

df['TOTAL'].fillna(value=df['TOTAL'].mean())
<img width="533" alt="ds ss12" src="https://github.com/user-attachments/assets/437c43c9-2cd3-4fe3-bea6-20661597af57" />


df.fillna(method='ffill')
<img width="117" alt="ds ss13" src="https://github.com/user-attachments/assets/d4793cdb-69e6-45ca-b92d-1c58b80d65aa" />


df.fillna(method='bfill')
<img width="698" alt="ds ss14" src="https://github.com/user-attachments/assets/fd599fa6-99b3-467b-a8d0-4cf7da174ee5" />


df['TOTAL'].fillna(value=df['TOTAL'].mean(),inplace=True)
<img width="716" alt="ds ss15" src="https://github.com/user-attachments/assets/0d15d1f3-e60d-47a2-bd4c-9b45d21c2ba2" />


df
<img width="931" alt="ds ss16" src="https://github.com/user-attachments/assets/786785c0-e1ba-4aae-851b-b77c102c7d28" />


import pandas as pd
import seaborn as sns
import numpy as np

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]

af=pd.DataFrame(age)

af

sns.boxplot(af)
<img width="95" alt="ds ss17" src="https://github.com/user-attachments/assets/23e0396f-74c0-47f6-b463-c8b0f8a33274" />


sns.scatterplot(data=af)
<img width="358" alt="ds ss18" src="https://github.com/user-attachments/assets/28499a47-3c1e-4ba2-91c5-5dd48ba427ca" />


q1=af.quantile(0.25)
<img width="350" alt="ds ss19" src="https://github.com/user-attachments/assets/72fe8f23-6bb9-49c5-98fe-3275e95fe914" />

q2=af.quantile(0.5)

q3=af.quantile(0.75)

iqr=q3-q1

iqr

Q1=np.percentile(af,25)
<img width="88" alt="ds ss20" src="https://github.com/user-attachments/assets/e542f38b-4bc4-4d88-84e0-0289fc884712" />

Q3=np.percentile(af,75)

IQR=Q3-Q1

IQR

lower_bound=Q1-1.5*IQR
<img width="516" alt="ds ss21" src="https://github.com/user-attachments/assets/5c1d5892-b89c-4d24-b651-60fac6efd5ec" />


upper_bound=Q3+1.5*IQR

lower_bound

upper_bound
<img width="393" alt="ds ss22" src="https://github.com/user-attachments/assets/3c045475-2ad1-4df9-91fd-2f18077cfd57" />


outliers=[x for x in age if x<lower_bound or x>upper_bound]
<img width="388" alt="ds ss23" src="https://github.com/user-attachments/assets/9c01c96b-e881-46e1-bb99-2d41316edb15" />


print("Q1:",Q1)

print("Q3:",Q3)

print("IQR:",IQR)

print("Lower bound:",lower_bound)

print("Upper bound:",upper_bound)

print("Outliers:",outliers)

af=af[((af>=lower_bound)&(af<=upper_bound))]
<img width="166" alt="ds ss24" src="https://github.com/user-attachments/assets/c9155401-5e9a-45da-84aa-f7cae23c2ad4" />

af

af.dropna()
<img width="96" alt="ds ss25" src="https://github.com/user-attachments/assets/ed995662-1965-4835-9a3f-e13f9c0760c8" />


sns.boxplot(data=af)
<img width="101" alt="ds ss26" src="https://github.com/user-attachments/assets/98f90b64-3531-4b3f-bf2e-db367965cd18" />


sns.scatterplot(data=af)
<img width="338" alt="ds ss27" src="https://github.com/user-attachments/assets/882f81e0-5873-42b4-bef5-3c57c609395c" />


data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,1,2]
<img width="323" alt="ds ss28" src="https://github.com/user-attachments/assets/e561b579-502a-4ab9-aea5-0610fccdebcc" />

mean=np.mean(data)

std=np.std(data)

print('mean of the dataset is',mean)

print('std. deviation is',std)

threshold=3
<img width="299" alt="ds ss29" src="https://github.com/user-attachments/assets/1d6eb1d5-4744-49be-9b58-56247f9ebe87" />

outlier=[]

for i in data:

  z=(i-mean)/std
  
  if z>threshold:
  
    outlier.append(i)
    
  print('outlier in dataset is',outlier)
<img width="155" alt="ds ss30" src="https://github.com/user-attachments/assets/eb836f99-ef2b-4272-a570-8c81dc605cc2" />

import pandas as pd

import numpy as np

import seaborn as sns

import pandas as pd

from scipy import stats

data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,83,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df

<img width="55" alt="ds ss31" src="https://github.com/user-attachments/assets/20cdf67c-4ed5-4783-af10-dac2173c1177" />

# Result
            Thus we have read and learned the data and also removed the outliers by detection using IQR and Z-score method.
