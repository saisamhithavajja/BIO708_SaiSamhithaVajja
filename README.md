This study explores the intricate interplay of sexual selection, allometry, and intralocus sexual conflict in shaping the evolution of sexual dimorphism in Drosophila wing shape and size. Contradictory findings regarding the stability of sexual shape dimorphism in Drosophila prompt a closer examination of allometry's contribution to the evolution of wing shape dimorphism. The study delves into the complex relationship between intersexual genetic correlation, intralocus sexual conflict, and the constraints they impose on the evolution of sexual dimorphism. The evidence suggests that shared genetic architecture between males and females limits the evolutionary response of wing shape dimorphism, highlighting the role of intralocus sexual conflict. Furthermore, the study explores the potential resolution of such conflicts by evolving condition-dependent traits.
The concept of condition dependence is investigated in the context of Drosophila wing size and shape, revealing a link between nutrition, mating success, and the observed sexual dimorphism. The study extends its focus to interspecific patterns, exploring how the degree of sexual shape and size dimorphism correlates with condition dependence across a phylogeny of flies. The findings suggest that species with more pronounced sexual dimorphism exhibit stronger condition dependence for sexually selected traits.

The objective of this study will be to look at the cell counts in the wings of different Drsophila species and how sexually dimorphic the cell counts are in the species of Drosophila. The biological questions we would like to answer are as follows;

1) Condition dependence difference in the cell counts in the wings of different Drosophila species. 
2) Within the same species, how dimorphic is the condition dependent cell count in the wings.


Following below, I have written some initial analysis as well as explaination of what the code is doing. 

1) Load Packages:
   ```ruby
   library(tidyverse)
   library(ggplot2)
   ```
The code loads the tidyverse package, which includes a collection of packages for data manipulation (dplyr), data visualization (ggplot2), and other useful tools.

2) Load Data:
```ruby
data <- read.csv("data/MP_SpeciesStarvation_Cell_count_data.csv")
```
Reads a CSV file ("MP_SpeciesStarvation_Cell_count_data.csv") into a dataframe named data.

3) Explore Data Structure:
```ruby
str(data)
```
Prints the structure of the data, showing the types and first few values of each column.

4) Check for Missing Values:
``ruby
missing_values <- data %>%
  summarise_all(~ sum(is.na(.)))
```
Computes the sum of missing values in each column and stores the result in the missing_values dataframe.

5) Drop Rows with Missing Values:
```ruby
data <- data %>%
  drop_na()
```
Removes rows with missing values from the dataframe.

6) Extract Sex Information:
```ruby
data <- data %>%
  mutate(Sex = ifelse(str_detect(Label, "_F_"), "Female", "Male"))
```
Creates a new column Gender based on whether the "Label" column contains "F" (Female) or not.

7) Show Unique Entries in Columns:
```ruby
unique_entries <- data %>%
  distinct(Label, Wing_Area)
print(unique_entries)
```
Prints unique entries in the "Label" and "Wing_Area" columns.

8) Create a New Column "Species":
```ruby
data <- data %>%
  mutate(Species = case_when(
    ... # species mapping rules
  ))
```
Creates a new column "Species" based on patterns in the "Label" column using the case_when function.

9) Print Updated Data:
```ruby
print(data)
```
Prints the updated dataframe with the new "Species" column.

10) Filter Data and Create Plots:
```ruby
# ... (code for creating boxplot, violin plot, t-test, etc.)
```
Filters the data, creates boxplots, violin plots, and performs a t-test for a comparative analysis.

10) Basic Summary Statistics:
``ruby
summary_stats <- data %>%
  group_by(Species, Gender) %>%
  summarise(
    mean_cell_count = mean(Count),
    sd_cell_count = sd(Count),
    min_cell_count = min(Count),
    max_cell_count = max(Count),
    total_count = n()
)
```
Computes basic summary statistics by grouping data based on "Species" and "Gender."

11) Visualize Mean Cell Count:
```ruby
ggplot(summary_stats, aes(x = Species, y = mean_cell_count, fill = Gender)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "Mean Cell Count by Species and Gender",
       x = "Species",
       y = "Mean Cell Count")
```
Creates a bar plot to visualize the mean cell count by species and gender.

12) Boxplot for Cell Counts by Species and Gender:
```ruby
ggplot(data, aes(x = Species, y = Count, fill = Gender)) +
  geom_boxplot() +
  labs(title = "Cell Counts by Species and Gender",
       x = "Species",
       y = "Cell Count")
```
Creates a boxplot to compare cell counts by species and gender.

13) Scatter Plot: Cell Count vs. Wing Disc:
```ruby
ggplot(data, aes(x = Wing_Area, y = Count, color = Species)) +
  geom_point() +
  labs(title = "Cell Count vs. Wing Disc",
       x = "Wing Disc",
       y = "Cell Count",
       color = "Species")
```
Creates a scatter plot to visualize the relationship between cell count and wing disc size.

14) Correlation between Cell Count and Wing Disc:
```ruby
correlation_result <- data %>%
  group_by(Wing_Area) %>%
  summarise(correlation = cor(Count))
print(correlation_result)
```
Computes the correlation between cell count and wing disc size, grouping by "Wing_Area."

This code is a comprehensive analysis pipeline for exploring and visualizing cell count data in Drosophila species. It includes data preprocessing, visualization, statistical testing, and summary statistics. The specific details of the analysis depend on the content of the dataset and the research questions being addressed.

Some of the Results: 

1) Visualize mean cell count by Species and Gender
   ![image](https://github.com/saisamhithavajja/QMEE/assets/96578069/9c6eea9a-78f2-4869-adf3-5c00c49a9ae0)

2) Box plots for cell counts by species and Gender
   ![image](https://github.com/saisamhithavajja/QMEE/assets/96578069/c0ab432f-44d7-4460-9293-056ee822b39a)

3) Scatter Plot: Cell Count vs. Wing Disc
   ![image](https://github.com/saisamhithavajja/QMEE/assets/96578069/fdaefc1c-4485-486d-8195-a887ccf19936)




