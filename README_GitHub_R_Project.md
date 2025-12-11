
# 📘 Hotel Booking EDA — Beginner-Friendly Annotated Guide (R Project)
A GitHub‑ready README designed for **students new to R or programming**.  
This version explains **every code block**, what it does, and how to use it to build an individual R project.

---

## 🌟 Project Overview
This project performs **Exploratory Data Analysis (EDA)** on the *Hotel Booking Demand Dataset*.

Main steps:
1. Load dataset  
2. Clean data  
3. Remove impossible values  
4. Analyze patterns in cancellations  
5. Create visual charts with R  

This README is structured so beginners can understand the script and reuse it for their own work.

---

## 📦 1. Required Libraries

```r
library(readr)
library(dplyr)
library(tidyverse)
library(ggplot2)
```

### 📝 What this does  
Loads essential packages used for:
- importing data  
- cleaning data  
- transforming data  
- plotting charts  

### 🧩 Beginner Tip  
Always put library imports at the **top** of your script.

---

## 📂 2. Load the Dataset

```r
hotel_bookings <- read.csv("hotel_bookings.csv", na.strings = "NULL")
```

### 📝 What this does  
Loads the CSV file and converts `"NULL"` values to proper missing values (`NA`).

### 🧩 Beginner Tip  
Use your own file name when doing your individual project.

---

## 🔢 3. Convert Columns to Numeric

```r
hotel_bookings$adults   <- as.numeric(as.character(hotel_bookings$adults))
hotel_bookings$children <- as.numeric(as.character(hotel_bookings$children))
hotel_bookings$babies   <- as.numeric(as.character(hotel_bookings$babies))
```

### 📝 Why this matters  
Sometimes numbers are stored as text. Converting them ensures calculations will work properly.

---

## 📅 4. Convert Date Columns

```r
hotel_bookings$reservation_status_date <- 
  as.Date(hotel_bookings$reservation_status_date, format="%Y-%m-%d")
```

### 📝 Why this matters  
Real date objects allow R to:
- sort by date  
- filter by date ranges  
- create time‑based plots  

---

## 🌍 5. Explore Unique Countries

```r
unique(hotel_bookings$country)
hotel_bookings %>% count(country)
```

### 📝 What this does  
Shows all countries represented in the data and counts the number of bookings per country.

---

## 🚫 6. Detect Invalid Rows

Hotel bookings with:
- **0 guests**  
- **0 nights**  

are impossible and must be removed.

```r
zero_guest_count <- sum(hotel_bookings$total_guests == 0)
zero_night_count <- sum(hotel_bookings$total_nights == 0)

overlap_count <- sum(hotel_bookings$total_guests == 0 &
                     hotel_bookings$total_nights == 0)

total_to_remove <- zero_guest_count + zero_night_count - overlap_count
```

### 📝 Why this matters  
Cleaning invalid rows leads to more accurate charts and analysis.

---

## 📊 7. Print Cleaning Summary

```r
cat("Original rows:", original_rows, "\n")
cat("Cleaned rows:", nrow(hotel_bookings), "\n")
cat("Total rows removed:", original_rows - nrow(hotel_bookings), "\n")
```

### 📝 What this does  
Prints how many rows were removed during the cleaning process.

---

## 📈 8. Visualization: Cancellation Rate by Customer Type

```r
barplot(customer_rate,
        main = "Cancellation Rate by Customer Type",
        ylab = "Cancellation Rate (%)",
        xlab = "Customer Type",
        col = c("lightblue", "tomato", "lightgreen", "grey"))
```

### 📝 Why this matters  
Helps identify which customer groups cancel the most.

---

## 🏨 9. Visualization: Cancellation by Hotel × Customer Type

```r
grouped_rate <- tapply(hotel_bookings$is_canceled,
                       list(hotel_bookings$hotel, hotel_bookings$customer_type),
                       mean, na.rm = TRUE) * 100

barplot(grouped_rate,
        beside = TRUE,
        col = bar_colors)
```

### 📝 What this shows  
Comparison of cancellation rates between:
- City hotel vs. Resort hotel  
- Each customer type  

---

## 💳 10. Visualization: Deposit Type Effects

```r
barplot(deposit_rate,
        main = "Effect of Deposit Type on Cancellation",
        ylab = "Cancellation Rate (%)",
        xlab = "Deposit Type",
        col = c("tomato", "lightblue"),
        ylim = c(0,40))
```

### 📝 Why this matters  
Deposit type strongly influences cancellation behavior.

---

## 🏨💳 11. Visualization: Deposit Type × Hotel Type

```r
grouped_rate <- tapply(guest_bookings$is_canceled, 
                       list(guest_bookings$hotel, guest_bookings$deposit_type),
                       mean, na.rm = TRUE) * 100
```

### 📝 What this shows  
A deeper view of how deposit policies affect different hotel types.

---

## 🎓 For Her Individual R Project  
She can follow the same structure with a different dataset:

### ✔ Step 1 — Choose a dataset  
(e.g., sales, students, weather, products)

### ✔ Step 2 — Clean the data  
Handle missing values  
Convert columns to numeric or date  

### ✔ Step 3 — Summarize the data  
Use `count()`, `summary()`, or grouped calculations  

### ✔ Step 4 — Create visualizations  
Barplots, histograms, boxplots, line charts  

### ✔ Step 5 — Write insights  
Explain what each chart tells you  

---

## 📌 Final Notes  
This README is designed to help beginners:
- Understand the script  
- Reuse the structure  
- Build confidence writing R code  

If you want, I can also generate:
- A full R Markdown (.Rmd) report  
- A PDF version  
- A starter template for her personal project  
- A commented R script she can submit  

Just ask!
