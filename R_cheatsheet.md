# R Cheatsheet Basic
## Basics
### Datentypen
- Numeric (double) 
- Int 
- Logical (Boolean) 
- Char (Strings) 

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
