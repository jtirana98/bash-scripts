- grep 'text' \<file-name\>: Get a list of the lines that have 'text'
- 

For each file inside the folder print the number of lines that include the 'phrase' text.
Print it as a list where is line contains: file-name, Count
```
for file in $(ls *.log); do
    count=$(grep -o 'phrase' "$file" | wc -l)
    echo "File: $file, Count: $count"
done
```
