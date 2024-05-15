### Additional Exercises

#### Exercise 1

Subset the `chicago_air` dataset to only include records where the temperature is below 30 degrees and the pressure is above 1000 hPa. Use the `filter()` function from the `dplyr` package.

<details><summary>Click for Solution</summary>

> Load the `dplyr` package using `library()` and use logical expressions to get records where `temp` is less than 30 and `pressure` is greater than 1000.

```r
library(dplyr)

cold_high_pressure <- filter(chicago_air, temp < 30, pressure > 1000)

cold_high_pressure
```
</details>

---

#### Exercise 2

Create a new column in the `chicago_air` data frame called `ozone_category` that categorizes ozone levels into "Low", "Moderate", and "High". Use the `mutate()` function from the `dplyr` package.

<details><summary>Click for Solution</summary>

> Use `mutate()` to create a new column `ozone_category` based on conditional statements for `ozone` values.

```r
library(dplyr)

chicago_air <- mutate(chicago_air, 
                      ozone_category = case_when(
                        ozone < 0.030 ~ "Low",
                        ozone >= 0.030 & ozone < 0.060 ~ "Moderate",
                        ozone >= 0.060 ~ "High"
                      ))

head(chicago_air)
```
</details>

---

#### Exercise 3

Sort the `chicago_air` data frame by temperature in ascending order and then by pressure in descending order. Use the `arrange()` function from the `dplyr` package.

<details><summary>Click for Solution</summary>

> Use `arrange()` with `temp` and `desc(pressure)` to sort the data frame.

```r
library(dplyr)

sorted_air <- arrange(chicago_air, temp, desc(pressure))

head(sorted_air)
```
</details>

---

#### Exercise 4

Use the `apply()` function to create a vector of the standard deviation values from the numeric columns in the `chicago_air` data frame.

<details><summary>Click for Solution</summary>

> Subset the `chicago_air` data frame to the numeric columns and use the `apply()` function with `sd`.

```r
chicago_numeric <- chicago_air[, c("ozone", "temp", "pressure")]

sd_values <- apply(chicago_numeric, MARGIN = 2, FUN = sd, na.rm = TRUE)

sd_values
```
</details>

---

#### Exercise 5

Write a function called `temp_range` that takes a data frame and returns the difference between the maximum and minimum temperature values.

<details><summary>Click for Solution</summary>

> Define the function `temp_range` and use `max()` and `min()` to calculate the range of temperatures.

```r
temp_range <- function(data) {
  max(data$temp, na.rm = TRUE) - min(data$temp, na.rm = TRUE)
}

temp_range(chicago_air)
```
</details>

---

#### Exercise 6

Create a function named `subset_by_weekday` that takes a data frame and a weekday (as an integer) as arguments and returns a subset of the data frame for that weekday.

<details><summary>Click for Solution</summary>

> Define the function `subset_by_weekday` to filter the data frame based on the `weekday` column.

```r
subset_by_weekday <- function(data, weekday) {
  filter(data, weekday == weekday)
}

subset_by_weekday(chicago_air, 3)
```
</details>

---

#### Exercise 7

Use the `dplyr` package to create a new data frame that groups the `chicago_air` data by month and calculates the average temperature for each month.

<details><summary>Click for Solution</summary>

> Use `group_by()` and `summarize()` to group by `month` and calculate the average `temp`.

```r
library(dplyr)

monthly_avg_temp <- chicago_air %>%
  group_by(month) %>%
  summarize(avg_temp = mean(temp, na.rm = TRUE))

monthly_avg_temp
```
</details>

---

#### Exercise 8

Write a function called `convert_date` that takes a data frame and converts the `date` column from a character to a Date object.

<details><summary>Click for Solution</summary>

> Define the function `convert_date` and use `as.Date()` to convert the `date` column.

```r
convert_date <- function(data) {
  data$date <- as.Date(data$date)
  return(data)
}

chicago_air <- convert_date(chicago_air)
str(chicago_air)
```
</details>

---

#### Exercise 9

Use a `for()` loop to create a vector of average ozone levels for each month in the `chicago_air` data frame.

<details><summary>Click for Solution</summary>

> Loop through each month, filter the data, and calculate the mean ozone level.

```r
average_ozone <- c()

for (month in 1:12) {
  monthly_data <- filter(chicago_air, month == month)
  average_ozone[month] <- mean(monthly_data$ozone, na.rm = TRUE)
}

average_ozone
```
</details>

---

#### Exercise 10

Combine the `warm` and `cool` data frames from the lesson using the `rbind()` function instead of `bind_rows()`.

<details><summary>Click for Solution</summary>

> Use `rbind()` to combine `warm` and `cool` data frames.

```r
recombined_rbind <- rbind(warm, cool)

nrow(recombined_rbind) == nrow(chicago_air)
```
</details>

---

