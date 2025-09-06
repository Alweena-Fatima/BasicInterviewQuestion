## 📊 What is Data Manipulation and Analysis?

---
### 🧹 **Data Manipulation**

- **Definition:**  
  Changing, organizing, or preparing data to make it useful and easier to understand.

- **Goal:**  
  To clean, transform, and structure raw data for better usability.

- **Examples:**
  - **Organizing a Grocery List:**  
    Sorting random items into categories like *"Fruits"* or *"Dairy"*.
  - **Fixing Errors in a Student Record:**  
    Correcting missing or wrong grades.

---

### 🔍 **Data Analysis**

- **Definition:**  
  Extracting patterns, trends, and insights from the data to solve problems or make decisions.

- **Goal:**  
  To answer questions or identify trends using the data.

- **Examples:**
  - **Analyzing Sales Trends:**  
    Finding the month with the highest revenue.
  - **Tracking Fitness Progress:**  
    Analyzing daily steps and calories for activity levels.

---
#### 🔄 Key Differences Between Data Manipulation and Data Analysis

| **Aspect**  | **Data Manipulation**                    | **Data Analysis**                          |
| ----------- | ---------------------------------------- | ------------------------------------------ |
| **Focus**   | Preparing and cleaning data              | Extracting insights from prepared data     |
| **Goal**    | Organize and structure raw data          | Find patterns, trends, and solve problems  |
| **Example** | Fixing errors in a student’s grade sheet | Analyzing which student scored the highest |

---

### 🐼 What is Pandas?

- **Pandas** is a powerful and popular Python library designed for:
  - **Data Manipulation**: cleaning, transforming, and structuring data
  - **Data Analysis**: finding patterns, trends, and insights

- It simplifies working with structured datasets like:
  - Tables  
  - Spreadsheets  
  - Time-series data
#### 📌 Real-World Use Cases of Pandas

Pandas is widely used across industries for real-world data processing and analysis. Below are some practical examples of how it's used:

---
##### 1. **Retail and E-Commerce**
**Use:** Analyze sales, customer behavior, and inventory data  
**Example Tasks:**
- Reading Excel/CSV sales reports
- Grouping by month to find top-selling products
- Filtering returns and customer complaints
---

##### 2. **Healthcare**
**Use:** Manage patient data and hospital records  
**Example Tasks:**
- Cleaning missing diagnosis codes
- Merging patient visits with lab results
- Time-series analysis of patient vitals

---
#####  3. **Marketing and Customer Analytics**
**Use:** Understand customer demographics and campaign performance  
**Example Tasks:**
- Filtering leads based on engagement
- Segmenting customers by region or spending
- Analyzing conversion rates

---
##### 🧪 4. **Data Science and Machine Learning**
**Use:** Prepare data for model training  
**Example Tasks:**
- Feature engineering (e.g. extracting date parts)
- Handling missing/outlier values
- One-hot encoding categorical variables
##### 📅 5. **NRM (Net Revenue Management) at Fractal**
**Use:** Automate and analyze Excel-based datasets  
**Example Tasks:**
- Filtering large Excel files using Python
- Generating automated Excel reports
- Cleaning and restructuring raw sales data

#### Install 
Go to your Terminal use pip (Python Package Installer)
```python 
pip install pandas
```
Import Pandas to your code 
``` python
import pandas as pd
```
---
### Reading Files in Pandas

Pandas can load data from various file formats like CSV, Excel, and JSON.
##### CSV

```python
import pandas as pd
df = pd.read_csv('data.csv')
print(df)
```
---
##### Excel
```python
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')
```
📌 Install dependency (once):
```bash
pip install openpyxl
```
---
##### JSON

```python
df = pd.read_json('data.json')
```

--- 
#### Basic Data Structures in Pandas

Pandas provides two main classes to work with structured data:
**1️⃣ Series**
- ✅ **Definition**: A one-dimensional **labeled** array.
- ✅ **Data Types**: Can store integers, floats, strings, Python objects, etc.
- ✅ **Label**: Each element has a label called an **index**.

 🔹 Example:

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])
print(s)
```

📤 **Output**:
```
0    10
1    20
2    30
3    40
dtype: int64
```

---
 **2️⃣ DataFrame**
-  **Definition**: A **two-dimensional** table-like structure with rows and columns.
-  Think of it like an **Excel sheet** or a **SQL table**.
-  Each column is actually a **Series**.
-  It consists of rows and columns where 
        Row have indices (labels)
        Columns have names

Example:

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
}

df = pd.DataFrame(data)
print(df)
```

**Output**:
```
     Name  Age
0   Alice   25
1     Bob   30
2  Charlie  35
```
---
### Saving Data in Pandas
After modifying your DataFrame, use the functions below to save it to a file.

---
**Save to CSV**

```python
df.to_csv('modified_data.csv', index=False)
```
📌 `index=False` avoids saving row numbers.

---
**Save to Excel**
```python
df.to_excel('modified_data.xlsx', index=False)
```
📌 Install dependency if needed:
```bash
pip install openpyxl
```
---
**Save to JSON**
```python
df.to_json('modified_data.json', orient='records')
```
---
```python
import pandas as pd
data={
    "Name":["Alweena","Armaghan","Azhan"],
    "Age" :[21,19,14],
    "city":["Delhi","GopalGanj","GopalGanj"]
}
df=pd.DataFrame(data)
df.to_csv("Mydata.csv",index=False) #if you dont want that 0 1 ... indexing
df.to_excel("Mydata.xlsx",index=False)
```
<img width="840" height="658" alt="image" src="https://github.com/user-attachments/assets/737cbc03-7961-4179-8c73-d636f34673f6" />


---
A step-by-step process to understand and clean your dataset using Pandas.
- Understanding the data 
- identifying the problems (missing data, incorrect data , duplicate data etc....)
- Plan to clean the data 
##### 1️⃣ Understand the Data/ Pandas Data Inspection Commands

**df.head(n)**

- Shows the **first 5 rows** by default.
- Use `n` to show the first `n` rows.

```python
df.head()       # first 5 rows
df.head(10)     # first 10 rows
```

**df.tail(n)**
- Shows the **last 5 rows** by default.
- Use `n` to show the last `n` rows.

```python
df.tail()       # last 5 rows
df.tail(3)      # last 3 rows
```
**df.shape**

- Returns the **dimensions** of the DataFrame.
- Output is a tuple: `(no. of rows,no. of columns)`

```python
df.shape
# Example: (100, 6)
---
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("No. of rows and columns ")
print(dataframe.shape)
--
No. of rows and columns 
(6, 5)
```

 **df.info()**
- Gives a **summary** of the DataFrame:
  - Number of rows/columns
  - Column names
  - Data types
  - Non-null counts
  - Memory usage

```python
df.info()
---
import pandas as pd
df=pd.read_csv("Mydata.csv")
print(df.info())
```
![[Pasted image 20250615232126.png]]
**df.describe()**
- Returns **summary statistics** for numeric columns:
  - Count, mean, std, min, 25%, 50%, 75%, max (of numeric column only)

```python
df.describe()
----
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Sample DataFrame")
print(dataframe)
print("Descriptive stats of Data ")
print(dataframe.describe())

| Name     | Age |     City     | Grade | Salary  |
|----------|-----|--------------|-------|---------|
| Alweena  | 21  | Delhi        | A     | 100000  |
| Armaghan | 19  | GopalGanj    | A+    | 100000  |
| Azhan    | 14  | GopalGanj    | A+    | 100000  |
| Nagma    | 41  | GopalGanj    | A+    | 50000   |
| Sabir    | 46  | Saudi        | A+    | 120000  |
| ABC      | 22  | Hyd          | A+    | 150000  |

## 📈 Descriptive Stats (Numeric Columns)

| Metric   | Age     | Salary     |
|----------|---------|------------|
| Count    | 6       | 6          |
| Mean     | 27.17   | 103333.33  |
| Std Dev  | 13.04   | 32659.86   |
| Min      | 14      | 50000      |
| 25%      | 19.5    | 100000     |
| 50%      | 21.5    | 100000     |
| 75%      | 36.25   | 115000     |
| Max      | 46      | 150000     |

---

📌 Use `include='all'` to see stats for non-numeric data too.
```python
df.describe(include='all')
```

**df.columns**

- Lists all the **column names** in the DataFrame.

```python
df.columns
# Output: Index(['Name', 'Age', 'Salary'], dtype='object')
---
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print(dataframe.columns)
---
Index(['Name', 'Age', 'city', 'Grade', 'salary'], dtype='object')
```
---



#####2️⃣ Identify Problems

Missing Data     [[6. Handling Missing Data]]

```python
df.isnull().sum()     # Count of nulls per column
```
Incorrect Data Types

```python
df.dtypes              # Check current data types
```
✅ Example Fix:
```python
df['Age'] = df['Age'].astype(int)
```
Duplicate Entries
```python
df.duplicated().sum()     # Total duplicates
```
✅ Drop them:
```python
df.drop_duplicates(inplace=True)
```

---
##### 3️⃣ Plan to Clean the Data

- ✅ Fill or drop missing data
  ```python
  df['column'].fillna('Unknown', inplace=True)
  df.dropna(inplace=True)
  ```

- ✅ Fix incorrect types
  ```python
  df['Date'] = pd.to_datetime(df['Date'])
  ```

- ✅ Remove duplicates
  ```python
  df.drop_duplicates(inplace=True)
  ```


---
When working with data, focus on **3 key operations**:

**1️⃣ Select Columns**
- returns 
- - a series 
- - data frame multiple columns of data
```python
df['column_name']         # Select single column (as Series)
df[['col1', 'col2','....' ]]      # Select multiple columns (as DataFrame)
```

Example:
```python
----------------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Selecting column")
print(dataframe["Age"])
print(dataframe[["Age","Grade"]])
------------------------------------------------------------------------
Selecting column
0    21
1    19
2    14
3    41
4    46
5    22
Name: Age, dtype: int64
Selecting column
   Age Grade
0   21     A
1   19    A+
2   14    A+
3   41    A+
4   46    A+
5   22    A+
```

**2️⃣ Filter Rows (Single Condition)**

```python
filterrows= df[df['Age'] > 25]        # Filter rows where Age > 25
new=df[df['city'] == 'Delhi'] # Filter rows where city is Delhi
--------------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Show the row based on condition provided ")
print(df[df["Age"]>19])
---------------------------------------------------------------------------
      Name  Age       city Grade  salary
0  Alweena   21      Delhi     A  100000
3    Nagma   41  GopalGanj    A+   50000
4    Sabir   46      Saudi    A+  120000
5      ABC   22   Hydrabad    A+  150000
```
**3️⃣ Filter Rows (Multiple Conditions)**

Use `&` for AND, `|` for OR 

```python
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Show the row based on the multiple condition")
print(df[(df["Age"]>20) & (df["salary"]>100000)])
---------------------------------------------------------------------------
Show the row based on the multiple condition
    Name  Age      city Grade  salary
4  Sabir   46     Saudi    A+  120000
5    ABC   22  Hydrabad    A+  150000
```

🧠 Tip: Always use parentheses around each condition due to operator precedence.


---
#### 1️⃣ Add a New Column

Add a column with constant or calculated values:
- direct assignment via []
- using insert method (provide adv of add columns at specific position)
**a) direct** 
```python
df['new_col'] = 0                  # Constant value
df['bonus'] = df['salary'] * 0.10 # Derived from existing columns
----------------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
dataframe["Bonus"]=[100,900,9000,1200,90,900]
dataframe["New_Salary"]=dataframe["Bonus"]*10+dataframe["salary"]
print(dataframe)
# Save the updated DataFrame back to CSV
dataframe.to_csv("Mydata.csv", index=False)
---------------------------------------------------------------------------
Display The DataFrame
       Name  Age       city Grade  salary
0   Alweena   21      Delhi     A  100000
1  Armaghan   19  GopalGanj    A+  100000
2     Azhan   14  GopalGanj    A+  100000
3     Nagma   41  GopalGanj    A+   50000
4     Sabir   46      Saudi    A+  120000
5       ABC   22   Hydrabad    A+  150000
----
       Name  Age       city Grade  salary  Bonus  New_Salary
0   Alweena   21      Delhi     A  100000    100      101000
1  Armaghan   19  GopalGanj    A+  100000    900      109000
2     Azhan   14  GopalGanj    A+  100000   9000      190000
3     Nagma   41  GopalGanj    A+   50000   1200       62000
4     Sabir   46      Saudi    A+  120000     90      120900
5       ABC   22   Hydrabad    A+  150000    900      159000
```

**b) using insert** 

```python
   df.insert(loc,column,value)
- `loc`: index where to insert the column (0 for first column)
- `column`: name of the new column
- `value`: list/series of values to insert
----------------------------------------------------------------------------
dataframe.insert(2,"weight",[49,55,35,65,75,63])
print(dataframe)
# Save the updated DataFrame back to CSV
dataframe.to_csv("Mydata.csv", index=False)
----------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary  Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000    100      101000
1  Armaghan   19      55  GopalGanj    A+  100000    900      109000
2     Azhan   14      35  GopalGanj    A+  100000   9000      190000
3     Nagma   41      65  GopalGanj    A+   50000   1200       62000
4     Sabir   46      75      Saudi    A+  120000     90      120900
5       ABC   22      63   Hydrabad    A+  150000    900      159000
```
---

#### 2️⃣ Update Values

**Update single value:**
```python
df.at[row_index, 'column'] = new_value
df.loc[row_index, 'column'] = new_value #
```

✅ Example:
```python
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
# assume you want to update the Grade of row 2(Azhan) from A+ to A
#and the salary of row 3 from 50k to 60k
df.loc[2,'Grade']='A'
df.at[3,'salary']=60000
print(dataframe)
# Save the updated DataFrame back to CSV
dataframe.to_csv("Mydata.csv", index=False)
------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary  Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000    100      101000
1  Armaghan   19      55  GopalGanj    A+  100000    900      109000
2     Azhan   14      35  GopalGanj     A  100000   9000      190000
3     Nagma   41      65  GopalGanj    A+   60000   1200       62000
4     Sabir   46      75      Saudi    A+  120000     90      120900
5       ABC   22      63   Hydrabad    A+  150000    900      159000
```

**Update multiple rows based on condition:**
```python
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
# now want to update the multiple col using condition
df.loc[df['Age'] > 20, 'Bonus'] = 2000
print(dataframe)
# Save the updated DataFrame back to CSV
# dataframe.to_csv("Mydata.csv", index=False)
--------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary  Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   2000      101000
1  Armaghan   19      55  GopalGanj    A+  100000    900      109000
2     Azhan   14      35  GopalGanj     A  100000   9000      190000
3     Nagma   41      65  GopalGanj    A+   60000   2000       62000
4     Sabir   46      75      Saudi    A+  120000   2000      120900
5       ABC   22      63   Hydrabad    A+  150000   2000      159000
```

---

#### 3️⃣ Remove Column

**Drop a column (permanently with `inplace=True`):**
```python
df.drop(column=['column_name'], axis=1, inplace=True)
-------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
df.drop(columns=['New_Salary'], inplace=True)
print(df)
------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary  Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000    100      101000
1  Armaghan   19      55  GopalGanj    A+  100000    900      109000
2     Azhan   14      35  GopalGanj     A  100000   9000      190000
3     Nagma   41      65  GopalGanj    A+   60000   1200       62000
4     Sabir   46      75      Saudi    A+  120000     90      120900
5       ABC   22      63   Hydrabad    A+  150000    900      159000
---------
       Name  Age  weight       city Grade  salary  Bonus
0   Alweena   21      49      Delhi     A  100000    100
1  Armaghan   19      55  GopalGanj    A+  100000    900
2     Azhan   14      35  GopalGanj     A  100000   9000
3     Nagma   41      65  GopalGanj    A+   60000   1200
4     Sabir   46      75      Saudi    A+  120000     90
5       ABC   22      63   Hydrabad    A+  150000    900
```

**Drop multiple columns:**
```python
df.drop(['col1', 'col2'], axis=1, inplace=True)
--------------------------------------------------------------------------
df.drop(columns=['New_Salary','weight'], inplace=True)
       Name  Age       city Grade  salary  Bonus
0   Alweena   21      Delhi     A  100000    100
1  Armaghan   19  GopalGanj    A+  100000    900
2     Azhan   14  GopalGanj     A  100000   9000
3     Nagma   41  GopalGanj    A+   60000   1200
4     Sabir   46      Saudi    A+  120000     90
5       ABC   22   Hydrabad    A+  150000    900
```

---
Missing data refers to the absence of a value in a DataFrame or Series. It can affect the accuracy and reliability of data analysis if not handled properly.

---
#### 🧾 Representation of Missing Data

1. **NaN** (Not a Number)  
   - Comes from NumPy  
   - Commonly used for missing numerical values  

2. **None**  
   - Python’s built-in null object  
   - Often used for missing object/string data
---
#### Detecting Missing Data

**🔍isnull()**
Returns a **boolean DataFrame**:
- `True` → Value is missing
- `False` → Value is present

```python
df.isnull()
---------------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
#check if missing
print(df.isnull())
--------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000     NaN         NaN
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
-------------------------------------------------------------------------
    Name    Age  weight   city  Grade  salary  Bonus  New_Salary
0  False  False   False  False  False   False  False       False
1  False  False   False   True  False   False  False       False
2  False  False   False  False  False   False   True        True
3  False  False   False  False  False   False  False       False
4  False  False   False  False  False   False  False       False
5  False  False   False  False  False   False  False       False

```
**isnull().sum()**
- it will count the total number of none values
```python
df.isnull().sum()
----------------------------------------------------------------------
print(df.isnull().sum())
------------------------------------------------------------------
Name          0
Age           0
weight        0
city          1
Grade         0
salary        0
Bonus         1
New_Salary    1
```

#### 🛠️ Handle Missing Value

You can either:
- ❌ **Remove** the missing values
- ✅ **Fill** or replace them with valid values

---

**Removing the Missing Value**

You can remove rows or columns that contain missing values using `dropna()`.

#### 📌 Remove Rows with Missing Data

```python
df_cleaned = df.dropna(axis=1,inplace=True) #asix=1 (droping the missing value of the columns ) axis=0 (droping the missing value of tthe rows)
------------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
dataframe.dropna(axis=0,inplace=True)
print(dataframe)
--------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000     NaN         NaN
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
---
      Name  Age  weight       city Grade  salary   Bonus  New_Salary
0  Alweena   21      49      Delhi     A  100000   100.0    101000.0
3    Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4    Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5      ABC   22      63   Hydrabad    A+  150000   900.0    159000.0

dataframe.dropna(axis=1,inplace=True)
       Name  Age  weight Grade  salary
0   Alweena   21      49     A  100000
1  Armaghan   19      55    A+  100000
2     Azhan   14      35     A  100000
3     Nagma   41      65    A+   60000
4     Sabir   46      75    A+  120000
5       ABC   22      63    A+  150000

```
#### 🟢 Filling the Missing Value
Instead of dropping rows or columns, you can **fill in** the missing values using the `fillna()` method.

---
**Fill with a Constant Value**

Replace all missing values with a fixed value:

```python
df_filled = df.fillna(value , inplace) # missing data will be replace by given value 
---------------------------------------------------------------------
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
# dataframe.dropna(axis=0,inplace=True)
dataframe.fillna(0,inplace=True)
print(dataframe)
-------------------------------------------------------------------------
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000     NaN         NaN
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
-----
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55          0    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000     0.0         0.0
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
```
**Fill with the calculated value** 
```python 
import pandas as pd
df=pd.read_csv("Mydata.csv")
dataframe=pd.DataFrame(df)
print("Display The DataFrame")
print(dataframe)
#fill with calculated value
#in bonus fill with means of bonus
df['Bonus'].fillna(df['Bonus'].mean(),inplace=True)
print(df)
-----------------------------------------------------------
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000   638.0         NaN
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
```
#### 📈 Interpolation (For Numerical Columns)

**Interpolation** is a technique used to fill missing values by **estimating** them from the existing values based on a pattern or trend.
- linear 
- polynomial
- time

---
###### 📌 Why Use Interpolation?

- ✅ Preserves **data integrity**
- ✅ Maintains **smooth trends** in data
- ✅ Helps **avoid data loss** without blindly filling or dropping values
---
```python
df_interpolated = df.interpolate(method="linear/poly/time",axis=0, inplace=true)
------------------------------------------------------------------------
df_interpolated = df.interpolate(method="linear")
print(df_interpolated)
----------------------------------------------------------------------
Display The DataFrame
       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000     NaN         NaN
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0

       Name  Age  weight       city Grade  salary   Bonus  New_Salary
0   Alweena   21      49      Delhi     A  100000   100.0    101000.0
1  Armaghan   19      55        NaN    A+  100000   900.0    109000.0
2     Azhan   14      35  GopalGanj     A  100000  1050.0     85500.0
3     Nagma   41      65  GopalGanj    A+   60000  1200.0     62000.0
4     Sabir   46      75      Saudi    A+  120000    90.0    120900.0
5       ABC   22      63   Hydrabad    A+  150000   900.0    159000.0
```


