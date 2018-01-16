# Compilation of one liners : awk 
#### print the simple average of rows in a column
```
awk '{ sum += $12 } END { if (NR>0) print sum / NR }' < input.file
```
 - here sum is automatically assigned to 0 by awk
 - dollar sign is used to denote the column number, here it is 12
 - NR is an inbuilt tool to count the number of lines in the column
 - if there was atleast one line in the column, it will print the average with `print` command
