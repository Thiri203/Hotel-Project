
# 📘 Beginner-Friendly R Guide Using the Hotel Booking Project as Reference

This README is designed for someone **new to R and programming**.  
Every code block includes:

✔ What the code does  
✔ How to write it (general pattern)  
✔ Why it matters  
✔ How to reuse it for an individual project  

This ensures you **learn the logic**, not memorize code.

---

# ✨ 1. R LIBRARIES  
Libraries add extra features to R.

### Group Project Example
```r
library(readr)
library(dplyr)
library(tidyverse)
library(ggplot2)
```

### Code Pattern (Formula)
```
library(package_name)
```

### Why it matters  
You must load libraries **before** using their functions.

### For Your Own Project
```r
library(readr)     # reading CSV files
library(ggplot2)   # chart making
```

---

# ✨ 2. READING A CSV FILE  
Loads your dataset into R.

### Group Project Example
```r
hotel_bookings <- read.csv("hotel_bookings.csv", na.strings = "NULL")
```

### Code Pattern
```
object_name <- read.csv("file_name.csv", na.strings = "")
```

### Beginner Explanation
- `object_name` = the name you give your dataset  
- `<-` stores data into a variable  
- `na.strings` converts specified text into NA  

### For Your Own Project
```r
scores <- read.csv("student_scores.csv")
```

---

# ✨ 3. CONVERTING COLUMNS TO NUMERIC  
Needed for calculations and charts.

### Group Project Example
```r
hotel_bookings$adults   <- as.numeric(as.character(hotel_bookings$adults))
hotel_bookings$children <- as.numeric(as.character(hotel_bookings$children))
hotel_bookings$babies   <- as.numeric(as.character(hotel_bookings$babies))
```

### Code Pattern
```
dataset$column <- as.numeric(as.character(dataset$column))
```

### Why this matters  
Numbers stored as text cannot be calculated.

### For Your Own Project
```r
scores$math <- as.numeric(as.character(scores$math))
```

---

# ✨ 4. CONVERTING TEXT INTO DATE FORMAT  
Makes time-related analysis possible.

### Group Project Example
```r
hotel_bookings$reservation_status_date <- 
  as.Date(hotel_bookings$reservation_status_date, format="%Y-%m-%d")
```

### Code Pattern
```
dataset$date_column <- as.Date(dataset$date_column, format="YYYY-MM-DD")
```

---

# ✨ 5. VIEWING UNIQUE VALUES & COUNTING ROWS  
Used for understanding the dataset.

### Group Project Example
```r
unique(hotel_bookings$country)
hotel_bookings %>% count(country)
```

### Code Pattern
```
unique(dataset$column)
dataset %>% count(column)
```

### Why this matters  
- Helps you understand categories  
- Useful for summarizing your dataset  

### For Your Own Project
```r
scores %>% count(class)
```

---

# ✨ 6. COUNTING ROWS THAT MATCH A CONDITION  
Very common in R for data cleaning.

### Group Project Example
```r
zero_guest_count <- sum(hotel_bookings$total_guests == 0)
zero_night_count <- sum(hotel_bookings$total_nights == 0)
```

### Code Pattern
```
sum(dataset$column == value)
```

### For Your Own Project
```r
missing_names <- sum(scores$name == "")
```

---

# ✨ 7. PRINTING RESULTS  
Shows readable messages in the R console.

### Group Project Example
```r
cat("Original rows:", original_rows, "\n")
```

### Code Pattern
```
cat("Your message:", variable, "\n")
```

### For Your Own Project
```r
cat("Number of students:", nrow(scores), "\n")
```

---

# ✨ 8. MAKING BAR PLOTS  
Best for comparing groups.

### Group Project Example
```r
barplot(customer_rate,
        main = "Cancellation Rate by Customer Type",
        ylab = "Cancellation Rate (%)",
        xlab = "Customer Type",
        col = c("lightblue", "tomato", "lightgreen", "grey"))
```

### Code Pattern
```
barplot(values, main="", xlab="", ylab="", col="")
```

### For Your Own Project
```r
barplot(scores$math, main="Math Scores")
```

---

# ✨ 9. GROUPED CALCULATIONS WITH `tapply()`  
Used for multi-category comparisons.

### Group Project Example
```r
grouped_rate <- tapply(hotel_bookings$is_canceled,
                       list(hotel_bookings$hotel, hotel_bookings$customer_type),
                       mean, na.rm = TRUE) * 100
```

### Code Pattern
```
tapply(target, list(group1, group2), function)
```

### For Your Own Project
```r
tapply(scores$math_score, list(scores$gender, scores$class), mean)
```

---

# ✨ 10. BAR PLOT FOR GROUPED DATA  
Visually compares multiple groups.

### Group Project Example
```r
barplot(grouped_rate, beside = TRUE, col = bar_colors)
```

### Code Pattern
```
barplot(table_or_matrix, beside=TRUE, col=colors)
```

---

# 🎓 FINAL TEMPLATE FOR HER INDIVIDUAL PROJECT  

1️⃣ Load dataset  
2️⃣ Clean data  
3️⃣ Convert types  
4️⃣ Summarize (unique, count, sum)  
5️⃣ Create visualizations  
6️⃣ Write insights  

She learns patterns — not memorization.

---

If you want, I can generate:
- a full **individual project template**  
- a guided **worksheet for practice**  
- a starter dataset  
- a polished PDF of this README  

Just ask!
