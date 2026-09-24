# Student Data Cleaning and Visualization 📊

## 📌 Project Overview

This project demonstrates how to clean, transform, and visualize student data using **Python, Pandas, NumPy, and Matplotlib**.

The dataset contains student information such as:

- Student name
- Roll number
- Subject
- Marks
- Age
- Email ID

The project identifies and corrects incorrect or inconsistent data and then visualizes the students' marks using a bar graph.

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Google Colab

## 📂 Dataset

The project uses a CSV file named:

`schldata.csv`

The dataset contains the following columns:

- `s.no`
- `name`
- `roll no`
- `subject`
- `marks`
- `gmail id`
- `age`

## 🧹 Data Cleaning

The following data-cleaning operations were performed:

1. Created a new `Age` column.
2. Removed the duplicate `age` column.
3. Handled missing/invalid student names.
4. Corrected the missing name as `kirti`.
5. Corrected incorrect roll numbers.
6. Corrected invalid subject values:
   - `102` → `phy`
   - `300` → `cs`
7. Corrected marks greater than 100 by subtracting 30.
8. Created new Gmail addresses using student names.
9. Removed the original invalid Gmail column.
10. Created a bar graph to visualize student marks.

## 📊 Data Visualization

A bar graph is created using **Matplotlib** to display the marks obtained by each student.

- X-axis → Student names
- Y-axis → Marks
- Different colors are used for each student
- Black borders are added to the bars

## 💻 Main Python Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Read CSV file
new = pd.read_csv("schldata.csv")

# Create Age column
new.insert(2, "Age", new["age"])

# Remove old age column
new.drop("age", axis=1, inplace=True, errors="ignore")

# Replace invalid name
new["name"] = new["name"].replace("none", pd.NA)

# Add correct name
new.loc[5, "name"] = "kirti"

# Correct roll numbers
new.loc[4, "roll no"] = 100
new.loc[6, "roll no"] = 106

# Correct subjects
new["subject "] = new["subject "].replace({
    "102": "phy",
    "300": "cs"
})

# Correct marks above 100
new["marks"] = new["marks"].apply(
    lambda x: x - 30 if x > 100 else x
)

# Create Gmail addresses
new.insert(5, "mail", ["@gmail.com"] * len(new))

new["mail"] = new["name"] + new["mail"]

# Remove original Gmail column
new.drop(" gmail id", axis=1, inplace=True)

# Display cleaned data
print(new)
