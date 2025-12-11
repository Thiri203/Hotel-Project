
# 📘 Hotel Booking EDA — Annotated Walkthrough (R Project)

This document is written so **you can read the R code and explanation side‑by‑side**, like a guided tour.  
Perfect for beginners in R and for understanding what your teammate actually built.

---

# ⭐ Project Purpose

The script performs:
- Data loading  
- Data cleaning  
- Removal of invalid rows  
- Exploratory Data Analysis (EDA)  
- Visualization of cancellation patterns  

Dataset used: **hotel_bookings.csv**

No machine learning.  
This is a pure **data cleaning + visualization** project.

---

# 🧠 1. Load Required Libraries

```r
library(readr)
library(dplyr)
library(tidyverse)
library(ggplot2)
```

### 💬 What this means:
These packages allow the script to:
- import data  
- transform data  
- clean data  
- create charts  

---

# 🧠 2. Load the Dataset

```r
hotel_bookings <- read.csv("hotel_bookings.csv", na.strings = "NULL")
```

### 💬 Explanation:
Reads the CSV file.  
Any `"NULL"` text is turned into `NA` (missing value).

---

# 🧠 3. Convert Guest Columns to Numeric

```r
hotel_bookings$adults   <- as.numeric(as.character(hotel_bookings$adults))
hotel_bookings$children <- as.numeric(as.character(hotel_bookings$children))
hotel_bookings$babies   <- as.numeric(as.character(hotel_bookings$babies))
```

### 💬 Explanation:
The dataset sometimes stores numbers as text.  
This forces them into actual numeric values so we can compute totals.

---

# 🧠 4. Convert Reservation Date to Date Format

```r
hotel_bookings$reservation_status_date <- 
  as.Date(hotel_bookings$reservation_status_date, format="%Y-%m-%d")
```

### 💬 Explanation:
R needs proper date objects for plotting time or sorting chronologically.

---

# 🧠 5. Explore Countries (Optional Summary)

```r
unique(hotel_bookings$country)
hotel_bookings %>% count(country)
```

### 💬 Explanation:
This lists each country, and counts how many bookings came from each.

---

# 🧠 6. Count Invalid Rows (Zero Guests / Zero Nights)

### Code:

```r
zero_guest_count <- sum(hotel_bookings$total_guests == 0)
zero_night_count <- sum(hotel_bookings$total_nights == 0)

overlap_count <- sum(hotel_bookings$total_guests == 0 & hotel_bookings$total_nights == 0)

total_to_remove <- zero_guest_count + zero_night_count - overlap_count
```

### 💬 Explanation:
- Some rows have **0 guests** (invalid booking)
- Some rows have **0 nights** (also invalid)
- Some rows have **both** (overlap)
- Overlap must not be double-counted  
- They compute how many rows need to be removed

This is basic data cleaning.

---

# 🧠 7. Print Cleaning Summary

```r
cat("Original rows:", original_rows, "
")
cat("Cleaned rows:", nrow(hotel_bookings), "
")
cat("Total rows removed:", original_rows - nrow(hotel_bookings), "
")
```

### 💬 Explanation:
Reports how much data was removed during cleaning.

---

# 🧠 8. Cancellation Rate by Customer Type

```r
barplot(customer_rate,
        main = "Cancellation Rate by Customer Type",
        ylab = "Cancellation Rate (%)",
        xlab = "Customer Type",
        col = c("lightblue", "tomato", "lightgreen", "grey"))
```

### 💬 Explanation:
Creates a bar chart showing which customer groups cancel most.

---

# 🧠 9. Cancellation Rate by Hotel × Customer Type

```r
grouped_rate <- tapply(hotel_bookings$is_canceled,
                       list(hotel_bookings$hotel, hotel_bookings$customer_type),
                       mean, na.rm = TRUE) * 100

barplot(grouped_rate,
        beside = TRUE,
        col = bar_colors)
```

### 💬 Explanation:
- Breaks cancellation rates down by:
  - **Resort Hotel**
  - **City Hotel**
- And customer types  
This allows comparison across categories.

---

# 🧠 10. Cancellation Rate by Deposit Type

```r
barplot(..., xlab = "Deposit Type", col = c("tomato", "lightblue"), ylim = c(0,40))
```

### 💬 Explanation:
Deposit types affect cancellation likelihood.  
For example:
- No Deposit → more cancellations  
- Non-Refund → fewer cancellations  

---

# 🧠 11. Deposit Type × Hotel Type

```r
grouped_rate <- tapply(guest_bookings$is_canceled,
                       list(guest_bookings$hotel, guest_bookings$deposit_type),
                       mean, na.rm = TRUE) * 100
```

### 💬 Explanation:
Shows how cancellation behavior differs between:
- City Hotel vs Resort Hotel  
- and deposit policy  

---

# 🧾 FINAL OVERVIEW

This project’s core flow:

1. Import data  
2. Clean data  
3. Remove invalid rows  
4. Explore descriptive patterns  
5. Visualize cancellation patterns  

It is **beginner-friendly**, uses **only R basics**, and is perfect as a reference for creating a new individual R project.

---

# 🎁 Want me to:  
✔ create an improved version of this script?  
✔ write a full R Markdown report?  
✔ build a new individual project for your friend?  

Just tell me.  
