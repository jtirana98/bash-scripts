- `grep 'text' \<file-name\>: Get a list of the lines that have 'text'`
- For each file inside the folder print the number of lines that include the 'phrase' text.
Print it as a list where is line contains: the file's name, Count
```
for file in $(ls *.log); do
    count=$(grep -o 'phrase' "$file" | wc -l)
    echo "File: $file, Count: $count"
done
```
- Assuming that you have a file like the following:
```
hello 0
1
2
3
4
hello 4
5
6
7
hello 0
9
10
11
hello 6
12
14
22
```
And you want to get the lines 1,2,3,4 and 9,10,11, i.e., the content under a "hello 0" block
You can retrieve these lines with the following command:

`awk '/hello 0/ {p=1; print; next} /hello [0-9]+/ && p==1 {p=0} p' test.log`

Explanation:

* /hello 0/: This pattern matches lines containing "hello 0".
* {p=1; print; next}: If a line matches the pattern above, set variable p to 1 (true) print line and the next line.
* /hello[0-9]+/: This pattern matches lines containing "hello" followed by one or more digits.
* {p=0}: If a line matches the pattern above, set variable p to 0 (false).
* p: If p is true (i.e., 1), it prints the line.

In case you want the lines that follow hello x, at the first argument change hello 0 to hello x
