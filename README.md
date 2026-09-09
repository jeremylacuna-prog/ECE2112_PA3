# **ECE2112_PA3**
**Jeremy Rafael G. Lacuna | 2ECE-C**
*This repository contains three programming problems which covers **Module 3 - Pandas**.* <br>
<br>
**Objectives:**
1. Load a CSV dataset into a Pandas DataFrame;
2. Select rows and columns using positional and label-based indexing;
3. Filter records using conditions on a DataFrame column; and
4. Extract a well-defined subset of data without changing the source data.
## A. **Positional and Label-Based Slicing**
After loading `cars`, complete the following operations. <br>
**a.** **Display** the **shape** and complete **list** of column names of `cars`. <br>
**b.** Using **positional slicing**, create `cars_6_to_10` containing **rows 6 through 10** of the dataset, where the first data row is row 1. <br>
**c.** From `cars_6_to_10`, display only the columns **Model**, **mpg**, **cyl**, **hp**, and **gear**, in that order. <br>

**Requirement:** The row selection in part **(b)** must use `iloc`; the column selection in part **(c)** must use column labels.

Functions used for this problem:

- **pd.read_csv()**: Used to **load the CSV file into a Pandas DataFrame**.
- **.shape & .columns**: **Returns** both the **dimensions** and the **names of all the columns** in the DataFrame.
- **.iloc[]**: Used to **select rows and columns** from a DataFrame **by their numerical position.**
- **Label-based Selection (`[['Model', 'mpg', ...]]`)**: **Extracts** and returns **specific columns by their names** in the DataFrame.
### **Code:**
```python
import pandas as pd

def pos_and_label_slice():
    cars = pd.read_csv('cars.csv')

    shape = cars.shape
    columns = list(cars.columns)

    cars_6_to_10 = cars.iloc[5:9]

    sliced_cols = cars_6_to_10[['Model', 'mpg', 'cyl', 'hp', 'gear']]

    return shape, columns, cars_6_to_10, sliced_cols
```
#### **Test Cases:**
```python
shape, columns, cars_6_to_10, sliced_cols = pos_and_label_slice()
```
```python
print("Shape of cars:", shape)
```
Output: ```Shape of cars: (32, 12)```
```python
print("Column names:", columns)
```
Output: ```Column names: ['Model', 'mpg', 'cyl', 'disp', 'hp', 'drat', 'wt', 'qsec', 'vs', 'am', 'gear', 'carb']```
```python
print("\ncars_6_to_10:\n", cars_6_to_10)
```
Output: <br>
```
cars_6_to_10:
         Model   mpg  cyl   disp   hp  drat    wt   qsec  vs  am  gear  carb
5     Valiant  18.1    6  225.0  105  2.76  3.46  20.22   1   0     3     1
6  Duster 360  14.3    8  360.0  245  3.21  3.57  15.84   0   0     3     4
7   Merc 240D  24.4    4  146.7   62  3.69  3.19  20.00   1   0     4     2
8    Merc 230  22.8    4  140.8   95  3.92  3.15  22.90   1   0     4     2
```
```python
print("\nSelected Columns (Model, mpg, cyl, hp, gear):\n", sliced_cols)
```
Output: <br>
```
Selected Columns (Model, mpg, cyl, hp, gear):
         Model   mpg  cyl   hp  gear
5     Valiant  18.1    6  105     3
6  Duster 360  14.3    8  245     3
7   Merc 240D  24.4    4   62     4
8    Merc 230  22.8    4   95     4
```
## **B. Model Lookup**
Use Boolean indexing on the **Model** column to answer both requests. <br>
**a.** **Display** the complete **row** for **Toyota Corolla**. <br>
**b.** For **Pontiac Firebird**, **display** only **Model**, **mpg**, **hp**, and **wt**. <br>
**Store** the two results in `toyota` and `pontiac`, respectively. **Do not use a hard-coded row number to locate either model.**

Functions used for this problem:
- **Boolean indexing (`cars['Model'] == ...`)**: **Filters** data based on the Model of the car.
- **Label Subsetting (`[['Model', 'mpg', 'hp', 'wt']]`)**: **Creates** a new DataFrame **based on the specified columns.**
### **Code:**
```python
def model_lookup():
    cars = pd.read_csv('cars.csv')

    toyota = cars[cars['Model'] == 'Toyota Corolla']

    pontiac = cars[cars['Model'] == 'Pontiac Firebird'][['Model', 'mpg', 'hp', 'wt']]

    return toyota, pontiac
```
#### **Test Cases:**
```python
toyota, pontiac = model_lookup()
```
```python
print("toyota:\n", toyota)
```
Output: <br>
```
toyota:
              Model   mpg  cyl  disp  hp  drat     wt  qsec  vs  am  gear  carb
19  Toyota Corolla  33.9    4  71.1  65  4.22  1.835  19.9   1   1     4     1
```
```python
print("\npontiac:\n", pontiac)
```
Output: <br>
```
pontiac:
                Model   mpg   hp     wt
24  Pontiac Firebird  19.2  175  3.845
```
## **C. Multi-Model Subsetting**
Create a DataFrame named `selected_cars` containing only the records for three models: **Datsun 710**, **Lotus Europa**, and **Ferrari Dino**.
For these records, **retain** only **Model**, **mpg**, **cyl**, **hp**, and **gear**. **Select** the rows by their **model values** rather than by row numbers. **Display selected cars and its shape.** <br>

**Required check:** The final DataFrame **must** contain exactly three rows and five columns.

Functions used for this problem:
- **.isin()**: **Checks** whether elements in a DataFrame **exist within a specified sequence of values**.
- **.shape**: **Returns** the **shape of the extracted subset** of the DataFrame
### **Code:**
```python
def multi_subset():
    cars = pd.read_csv('cars.csv')

    target_models = ['Datsun 710', 'Lotus Europa', 'Ferrari Dino']
    target_columns = ['Model', 'mpg', 'cyl', 'hp', 'gear']

    selected_cars = cars[cars['Model'].isin(target_models)][target_columns]

    return selected_cars, selected_cars.shape
```
#### **Test Cases:**
```python
selected_cars, shape = multi_subset()
```
```python
print("selected_cars:\n", selected_cars)
```
Output: <br>
```
selected_cars:
            Model   mpg  cyl   hp  gear
2     Datsun 710  22.8    4   93     4
27  Lotus Europa  30.4    4  113     5
29  Ferrari Dino  19.7    6  175     5
```

To view and test the code:
- Download ```'Lacuna_PA - 2.ipynb'``` that is located in the repository
- Download ```'cars.csv'``` that is located in the repository
- **Note:** Both ```'Lacuna_PA - 2.ipynb'``` and ```'cars.csv'``` **must** be in the **same file directory**
- Open the file via Jupyter Notebook
- Click on the file and click 'Run'

**README File Version History:**

```September 2, 2026``` - README.md output uploaded. <br>
