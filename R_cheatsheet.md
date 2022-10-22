# R Cheatsheet Basic
## Basics
### Datentypen
- Numeric (double) 
- Int 
- Logical (Boolean) 
- Char (Strings) 

![image](https://user-images.githubusercontent.com/25742415/196103314-00a41e51-c6dd-4ca1-a771-fe464ffc6281.png)

```R
Class(variable) # check which class var belongs to
```
### Vector 
```R
Myvar <- c(var1, var2...) 
Name_column <- c(“spalte1”,”spalte2”) 
Names(myvar) <- name_column # bennent spalten 
Selection_vec <- (myvar > 5) # selecton_vec bekommt nur daten die die condititionen erfüllen 
Myvr[selection_vec] # basically fragt er in den klammer nach der comparison und gibt dann nur die aus die erfüllt sind 
```

### Matrix 
```R
MyMatrix[row,column] 

star_wars_matrix <- matrix(box_office,  
                      nrow = 3, byrow = TRUE,
                      dimnames = list(titles, region)) 
# Nrow = row number; byrow = ob daten per row abgeschnitten werden sollen; Dimnames = liste(x,y) 

MyMatrix <- cbind(matrix1, rowVecotr) # bindet neue column 
MyMatrix <- rbind(matrix1, rowVecotr) # bindet neue row 
```

### Table
Tables aus Datenframes können schnellen Überblick schaffen von Daten (Nominal od. Ordinal) und ihren Proportionen
![image](https://user-images.githubusercontent.com/25742415/196188238-1b1f3789-fc4b-4e50-81e5-86f67ba5bb52.png)
```R
prop.table(mytable, INT) #INT => rows add to 1, column add to 1
```
### Factor levels 
Nominal: Without implied order (Elephant, Giraffe…) 
Ordinal: natural order (School Degree, First Class – Second, …) 

(Nominal) 
```R
Survey_row <- c("M", "F", "F", "M", "M") 

myFactor <- factor(survey_row) #myFactor output: #Levels: F M 

Levels(myFactor) <- c(“Female”, “Male”) #setzt den jeweils ersten und zweiten Factor mit den Namen  
```
(Ordinal) 
```R
factor_speed_vector <- factor(speed_vector, ordered= TRUE, levels = c("slow","medium","fast")) 
```

### Data Frame 
Quasi Matrix nur mit verschiedenen Datentypen 
```R
MyData <- data.frame(name_row1, row2, row3,…) #immer rows und name kommt durch variablen 

MyData[row,column] #column kann auch string sein z.B. “Durchmesser”-Column 

MyData$name_column #genau wie MyData[,”name_column”] 

MyData[“durchmesser”] # gibt column aus und kein vector 

Subset(myData, subset = colname<1) #if colname values < 1 => TRUE, dann in Tabelle) 

Order(mydata$durchmesser) #orders column 
```

Filtering a data frame with filter()
```R
mydata2 <- mydata %>% filter(p-value < 0.05)

# Filter for Asia, add column indicating outliers
gap_asia <- gap2007 %>%
  filter(continent == "Asia") %>%
  mutate(is_outlier = lifeExp < 50)

# Remove outliers, create box plot of lifeExp
gap_asia %>%
  filter(!is_outlier) %>%
  ggplot(aes(x = 1, y = lifeExp)) +
  geom_boxplot()
```
![grafik](https://user-images.githubusercontent.com/25742415/197328708-c5fdf878-7ebc-4997-949b-5231f37dcb1d.png)


### Mutate (adding new Columns by calculating of other columns)
Adds new variables and preserves existing ones; New variables overwrite existing variables of the same name. 
```R
mutate(log_pop = log(pop))
```


## Import Data to R
### Library(read) 
```R
read.table(path, sep = "\t", col.names = c("type", "calories", "sodium"), header=NONE) #sep = seperator
```

### Library(readr - schneller) 
```R
read_delim("potatoes.txt", delim="\t", col_names=properties) 

read_tsv("potatoes.txt", col_types = "cccccccc", col_names = c(“eins”,”zwei”) 

library(data.table - große files) 

fread("potatoes.csv", select=c(6,8)) 
```

### Library(readxl) (EXCEL) 
```R
excel_sheets("urbanpop.xlsx") #zeigt sheets von excel an 

read_excel("urbanpop.xlsx", sheet = 3, col_names=FALSE/c(“erste”,”zweite), skip=2) #ließt excel sheet 3 aus, hat custom column names oder automatische, und skippt die ersten zwei rows)lapply(excel_sheets("data.xlsx"), read_excel, path = "data.xlsx") #ließt alle excel sheets in eine liste 

Library(gdata) (EXCEL, kein xlsx) 

read.xls(“data.xls”, sheet=INT, stringsAsFactors=BOOLEAN) 

na.omit(urban, "NA") #removes values of “NA” 
```

### Library(XLConnect) (EXCEL <-> R) 
```R
my_book <- loadWorkbook("urbanpop.xlsx") #lädt excel file 

getSheets(my_book) #zeigt sheets 

readWorksheet(my_book, sheet=INT) #holt sheets 

createSheet(my_book, "fileName") 

writeWorksheet(my_book, summ, "data_summary") saveWorkbook(my_book, "summary.xlsx") 

renameSheet(my_book, sheet=4,newName="summary") 

saveWorkbook(my_book, file="renamed.xlsx") 
```
## Categorial Data
### Library (dplyr)
Wichtiges Zeichen %>%
Nimmt die Variable des vorherigen Ausdrucks

Beispiel mit Faktoren
Nimmt im ersten den Dataframe comics, nimmt in nächsten Zeile filter() als data comics$align und dann dropt dann leere levels die wir mit dem filter herausgelöscht haben
```R
comics_filtered <- comics %>%
  filter(align != "Reformed Criminals") %>%
  droplevels()
```
# Plotting ggplot2
## Bar Chart
Bar Chart that have Bars not stacked, but besides each other
![image](https://user-images.githubusercontent.com/25742415/196186575-8fe795d5-46f5-4f6a-8a80-29bed9aea959.png)
```R
ggplot(data,aes(x = x_axis_data, fill = y_axis_data)) + 
  geom_bar(position = "dodge")
```
Bar Chart mit proportionalen Daten die den Graph füllen
![image](https://user-images.githubusercontent.com/25742415/196191228-30557431-a941-4675-b34d-ce44742a9c49.png)

```R 
  ggplot(data,aes(x = x_axis_data, fill = y_axis_data)) + 
  geom_bar(position = "fill")+
  ylab("proportion") #ylab => all data proportions should add up to 1
```
Faceting
Takes each Bar and represent it in a single Barchart side-by-side

```R 
  ggplot(comics, aes(x = align)) + geom_bar() + facet_wrap(~ gender)
```
![grafik](https://user-images.githubusercontent.com/25742415/197186141-4d03c1b1-fb05-4d91-ab29-1fccfe5633f0.png)

## Density plot
geom_density

## Data Pipe filtering
```R
mydf %>% 
  filter(column_to_filter < 25000) %>%
  ggplot(aes(x=x_axis_data)) +
  geom_histogram() +
  xlim(c(90, 550)) +
  ggtitle("Title of Diagram")
```

### Statistik
Mean: Durschschnitt Summe/n
Median: Mitte der Daten
Mode: Im Datensatz meist beobachtete Zahl

Var: Rechnet die Abstand die durchschnittlich bei jeden Wert ist. Nimmt ((x - mean)^2)/sum(n). Warum ^2? weil wenn die Werte negativ sind, würde es immer um die 0 schwanken was kein sinn macht. Deshalb hoch zwei um die minus zahlen weg zu bekommen
Standard Deviation: Standartabweichung => sqrt(var) um überhaupt sinn aus Var machen zu können
```R
var() # nur um sd auszurechen
sd() # sqrt von var

IQR()
```

### Group by and summarize
Macht eine Table mit den Daten, columns sind sd, iqr, n()
die var in group_by sollte eine categoriale sein

![grafik](https://user-images.githubusercontent.com/25742415/197330901-0f5baad9-26b6-4f15-be27-7e2df1ae5277.png)

```R
gap2007 %>%
  group_by(continent) %>%
  summarize(sd(lifeExp),
            IQR(lifeExp),
            n())
            
gap2007 %>%
  ggplot(aes(x = lifeExp, fill = continent)) +
  geom_density(alpha = 0.3)
```
