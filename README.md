# Student Attendance Analytics with Pandas

An end-to-end data analysis project in Python using **Pandas** to clean, analyze, feature-engineer, and summarize student attendance data. This workflow handles real-world data issues such as missing values, inconsistent column naming, text extraction, risk modeling, and export automation.

---

## 📌 Project Overview

Maintaining high attendance is crucial for academic success, yet tracking defaulters and patterns across large datasets manually can be challenging. This project processes raw attendance records to automate:
- Data cleaning and standardization.
- Categorization of attendance risk levels.
- Extraction of numerical insights from unstructured status flags.
- Aggregating metrics by student status and performance categories.
- Exporting targeted reports for academic action.

---

## 🛠️ Key Data Transformations & Features

1. **Data Cleaning & Standardization**: 
   - Converted messy column headers into clean, uniform `snake_case`.
   - Handled missing values (`NaN`) and converted date columns into Pandas `datetime` format.
2. **Feature Engineering**:
   - **`attendance_category`**: Classifies students into *Excellent* ($\ge 90\%$), *Good* ($75-89\%$), *Average* ($60-74\%$), and *Poor* ($< 60\%$) using `np.select`.
   - **`attendance_bin`**: Applied `pd.cut()` to bin attendance ranges into *Critical*, *Warning*, *Good*, and *Excellent*.
   - **`risk_score`**: Calculated a custom weighted risk index:
     $$\text{Risk Score} = (\text{Total Absent} \times 0.4) + (\text{Consecutive Absences} \times 0.6)$$
   - **`classes_needed_numeric`**: Extracted numeric values from string status criteria using Regex string matching.
   - **`attendance_flag`**: Used `apply()` with lambda functions to flag "Defaulters" ($<75\%$) vs "Safe" students.
3. **Data Aggregation & Grouping**:
   - Used `.groupby()` and `.agg()` to calculate min, max, average present days, and sum of absences across status groups.
   - Generated cross-tabulations using `pivot_table()` to count students across status and attendance categories.
4. **Data Merging & Exporting**:
   - Performed `inner` joins with supplemental student demographic data (`roll_no`, `branch`, `semester`).
   - Exported critical student lists, status summary statistics, and top 10 risk profiles into separate `.csv` files.

---

## 📁 Repository Structure

```text
├── Project_Student_Attendance_Analytics.ipynb   # Main Jupyter Notebook
├── aids_attendance.xlsx                         # Raw input dataset
├── critical_students.csv                        # Output: Critical risk category students
├── status_summary_statistics.csv                # Output: Aggregated status statistics
├── top_10_risk_students.csv                     # Output: Top 10 high-risk students
└── README.md                                    # Project documentation
