# Step-by-Step Telco Churn Analysis Guide (Beginner Friendly)

This guide teaches you *how to think and write R code* step-by-step using the Telco Customer Churn dataset.  
Each block includes:

- 🎯 Goal  
- 💻 Code  
- 🧠 Pattern  
- 🧷 Explanation  

So you NEVER have to memorize code.

---

## 🪜 Step 1: Load Libraries

### 🎯 Goal  
Enable R to read files, clean data, and make charts.

### 💻 Code
```r
library(readr)
library(dplyr)
library(ggplot2)
```

### 🧠 Pattern  
`library(package_name)`

### 🧷 Explanation  
- `library()` turns on extra tools for R.  
- These packages give functions like `filter()`, `mutate()`, and plotting.  
- Always load libraries at the top of your R script.

---

## 🪜 Step 2: Read the Dataset

### 🎯 Goal  
Bring the CSV file into R memory.

### 💻 Code
```r
telco <- read.csv("WA_Fn-UseC_-Telco-Customer-Churn.csv",
                  stringsAsFactors = FALSE)
```

### 🧠 Pattern  
`object <- read.csv("file.csv")`

### 🧷 Explanation  
- `telco` is the name of your dataset.  
- `<-` means “store this into this name”.  
- `stringsAsFactors=FALSE` keeps text simple and easy for beginners.

---

## 🪜 Step 3: Explore Dataset Shape & Columns

### 🎯 Goal  
Know what your data looks like.

### 💻 Code
```r
dim(telco)
names(telco)
str(telco)
head(telco, 5)
```

### 🧷 Explanation  
- `dim()` → rows & columns  
- `names()` → column names  
- `str()` → data types  
- `head()` → first few rows  

Essential for ANY project.

---

## 🪜 Step 4: Prepare Target Column (Churn)

### 🎯 Goal  
Convert `Churn` into a category and check counts.

### 💻 Code
```r
telco$Churn <- as.factor(telco$Churn)
levels(telco$Churn)
table(telco$Churn)
prop.table(table(telco$Churn))
```

### 🧠 Pattern
```r
data$column <- as.factor(data$column)
table(data$column)
prop.table(table(data$column))
```

### 🧷 Explanation  
- Factors = categories  
- `table()` shows counts  
- `prop.table()` shows percentages  

---

## 🪜 Step 5: Convert Important Columns to Numeric

### 🎯 Goal  
Fix numeric columns that were read as text.

### 💻 Code
```r
str(telco$Tenure)
str(telco$MonthlyCharges)
str(telco$TotalCharges)

telco$TotalCharges <- as.numeric(telco$TotalCharges)
sum(is.na(telco$TotalCharges))

telco <- telco[!is.na(telco$TotalCharges), ]
```

### 🧠 Pattern
```r
data$col <- as.numeric(data$col)
sum(is.na(data$col))
data <- data[!is.na(data$col), ]
```

### 🧷 Explanation  
- Converting text to numbers sometimes creates `NA`.  
- Remove rows with missing values after conversion.

---

## 🪜 Step 6: Visualize Overall Churn

### 🎯 Goal  
See churn distribution visually.

### 💻 Code
```r
barplot(table(telco$Churn),
        main = "Overall Churn Count",
        xlab = "Churn",
        ylab = "Number of Customers")
```

### 🧷 Explanation  
`table()` groups values → `barplot()` visualizes them.

---

## 🪜 Step 7: Churn by Contract Type

### 🎯 Goal  
Compare churn across contract lengths.

### 💻 Code
```r
telco$Contract <- as.factor(telco$Contract)

contract_churn <- table(telco$Contract, telco$Churn)
prop.table(contract_churn, margin = 1)

barplot(contract_churn,
        beside = TRUE,
        legend = TRUE,
        main = "Churn by Contract Type")
```

### 🧠 Patterns  
- grouped count: `table(group, target)`  
- row percentage: `prop.table(tab, margin = 1)`  
- grouped barplot: `barplot(tab, beside=TRUE)`

### 🧷 Explanation  
Month-to-month usually churns the most.

---

## 🪜 Step 8: Churn vs Tenure

### 🎯 Goal  
Check if new customers churn more.

### 💻 Code
```r
boxplot(tenure ~ Churn, data = telco,
        main = "Tenure by Churn",
        xlab = "Churn", ylab = "Months")
```

### 🧷 Explanation  
Boxplots show median and spread.  
Churned customers usually have lower tenure.

---

## 🪜 Step 9: Churn vs Monthly Charges

### 🎯 Goal  
See if higher monthly charges cause churn.

### 💻 Code
```r
boxplot(MonthlyCharges ~ Churn, data = telco,
        main = "Monthly Charges by Churn")
```

### 🧷 Explanation  
Look for higher charges among churned customers.

---

## 🪜 Step 10: Churn by Payment Method

### 🎯 Goal  
Identify payment methods with high churn.

### 💻 Code
```r
telco$PaymentMethod <- as.factor(telco$PaymentMethod)

payment_churn <- table(telco$PaymentMethod, telco$Churn)
prop.table(payment_churn, margin = 1)

barplot(payment_churn,
        beside = TRUE,
        legend = TRUE,
        las = 2,
        main = "Churn by Payment Method")
```

### 🧷 Explanation  
Electronic check customers tend to churn more.

---

## 🪜 Step 11: Turn Code Into Report Sentences

Examples:

- “26.5% of customers churned overall.”  
- “Month-to-month contracts show the highest churn.”  
- “Customers with shorter tenure churn more.”  
- “Electronic check customers churn at the highest rate.”

---

This guide is everything she needs to follow along and fully understand the Telco Churn analysis.
