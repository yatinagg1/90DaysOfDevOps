# Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide

| Topic | Key Syntax | Example |
|-------|-----------|---------|
| Variable | `VAR="value"` | `NAME="DevOps"` |
| Argument | `$1`, `$2` `$#` `$@` `#?` | `./script.sh arg1` |
| If | `if [ condition ]; then` | `if [ -f file ]; then` |
| For loop | `for i in list; do` | `for i in 1 2 3; do` |
| Function | `name() { ... }` | `greet() { echo "Hi"; }` |
| Grep | `grep pattern file` | `grep -i "error" log.txt` |
| Awk | `awk '{print $1}' file` | `awk -F: '{print $1}' /etc/passwd` |
| Sed | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt` |
| Make Executable | `chmod +x file.sh` | `chmod +x script.sh` |
| Run Script | `./file.sh` | ` ./script.sh` |
| Comment |	`# comment` |	`echo "Hi" # inline comment` |
| Use Variable | `$VAR` | `echo $NAME` |
| Read Input |	`read VAR` |	`read USER` |
| String Compare |	`[ "$a" = "$b" ]` |	`[ "$name" = "Linux" ]` |
| Integer Compare |	`[ $a -gt 10 ]`  | `[ $num -eq 5 ]` |
| File Test |	`[ -f file ]` | 	`[ -d /home ]` |
| Case Statement |	`case $v in ... esac`	 | `case $1 in start) echo run ;; esac` |
| AND |	`cmd1 && cmd2` |	`mkdir test && cd test` |
| OR |	`cmd1  cmd2` |	`cd dir  pwd` |
| C-Style For |	`for ((i=1;i<=3;i++))` |	`for ((i=1;i<=3;i++)); do touch f$i; done` |
| While Loop |	`while [ cond ]; do` |	`while [ $a -lt 5 ]; do echo $a; done` |
| Until Loop |	`until [ cond ]; do` |	`until ping -c1 google.com; do sleep 2; done` |
| Break	 | `break` |	`if [ $i -eq 5 ]; then break; fi` |
| Continue |	`continue`	 | `if [ $i -eq 2 ]; then continue; fi` |
| Function Arg |	`$1 inside function` |	`add(){ echo $(($1+$2)); }` |
| Return Status |	`return 0` |	`return 1` |
| Capture Output |	`result=$(func)` |	`val=$(date)` |
| Local Variable |	`local var=value`	| `local count=10` |
| cut |	`cut -d: -f1 file` |	`cut -d: -f1 /etc/passwd` |
| sort |	`sort file` |  `sort -n numbers.txt` |
| uniq |	`sort file  uniq` |	`sort file  uniq -c` |
| tr |	`tr 'a-z' 'A-Z'` |	`echo hi  tr 'a-z' 'A-Z'` |
| wc |	`wc -l file` |	`wc -w file.txt` |
| head |	`head -n 5 file` |	`head -n 10 log.txt` |
| tail |	`tail -f file` |	`tail -f app.log` |


### Task 1: Basics
1. Shebang (`#!/bin/bash`) —

It tells the script to execute in which shell so that script could work properly without this line script would be executed in default shell of the user.

```
#!/bin/bash
echo "Hello, World"
```


2. Running a script — 
`chmod +x` - makes the file executable without it script could not be executed/run 

`./script.sh` - method to execute the script of the path/directory where its been kept

`bash script.sh` - method to execute the script with bash shell

3. Comments — single line (`#`) and inline

Comments are used to make it readable and understandable script for others and later on could be understood easily to edit in future. We could use `#` to comment everything after this as comment.

4. Variables — declaring, using, and quoting (`$VAR`, `"$VAR"`, `'$VAR'`)

```
VAR=4
echo $VAR                   # print value of VAR thats 4
echo "Value of VAR - $VAR"  # output would be Value of VAR - 4
echo 'Value of VAR - $VAR'  # output would be Balue of VAR - $VAR
```

5. Reading user input — `read`

Used to get input from the user
```
read -p "Enter a number - " $x
```

6. Command-line arguments — 

`$0` - Script name

`$1` - 1st argument passed to the script, so on `$2` . `$3` etc if any

`$#` - Count number of arguments pass to the scripts

`$@` - All Arguments

`$?` - Last command status, used to check if it was successful or not so to take next action accordingly


---

### Task 2: Operators and Conditionals

1. String comparisons — 
`=` - Check 2 strings are equal or not

`!=` - Check 2 strings are not equal

`-z` - check if string is empty

`-n`-  Checks if a string is not empty (contains characters)

2. Integer comparisons — 

`-eq` - check 2 numbers are equal

`-ne` - Check 2 numbers are not equal

`-lt` - check 3 is less than 5 or not

`-gt` - check 5 is greater than 3 or not

`-le` - check 3 is less than or equal to 5 too

`-ge` - check 3 is greater than or equal too

3. File test operators — 

`-f`- check if file exists or not

`-d`- check for if path exists and is a directory or not

`-e` - check if file or directory exists

`-r`- check if file has read permission

`-w`- check if file has write permission

`-x` - check if file has executable permission

`-s` - check if file is not empty

4. `if` - used to check 1st condition then enter the loop 
  
   `elif` - check 2nd condition then enter it to perform task , looping if then else
  
   `else` - if no conditions satisfied then enter this as default task to be performed

5. Logical operators — 

`&&` - logical AND operator, used to execute 1st and 2nd command and return success only if both are successful

`||` - logical OR operator, used to return success if either of 1st or 2nd command successful

`!`  - negation operator, used to return opposite of condition

```
if [ ! -f test.txt ] - this checks test.txt should not be file
```

6. Case statements — `case ... esac` - used to handle multiple statement conditions instead of using many if then elif then else 

```
#!/bin/bash

echo "Enter your command (start, stop, or status):"
read command

case "$command" in
    start)
        echo "Starting service..."
        systemctl start <servicename>
        ;;
    stop)
        echo "Stopping service..."
        systemctl stop <servicename>
        ;;
    status)
        echo "Checking status..."
        systemctl status <servicename>
        ;;
    *)
        echo "Invalid input. Choices are start, stop, or status."
        exit 1
        ;;
esac

```


---

### Task 3: Loops

1. `for` loop — 

a. list-based - to iterate for each item in list

```
for FRUIT in apple banana cherry
do
    echo "I like to eat $FRUIT"
done
```

b. C-style - numeric counter loop based with initialization, condition, iteration

```
for (( i=0; i<5; i++ )); do
    echo "Value of $i."
done

would print / output
0
1
2
3
4
```

2. `while` loop - repeats the loop until it remains true
```
while read LINE; do
    echo "$LINE"
done < /etc/hostname
```

3. `until` loop - repeats the loop until condition becomes true
```
until ping -c 1 google.com; do
    echo "The internet is still down."
    echo "I will try again in 3 seconds..."
    sleep 3
done
```

4. Loop control — 

`break`- come out of loop immediately
```
for FILE in *.log; do
    if [ "$FILE" = "error.log" ]; then
        break
    fi
    echo "$FILE"
done
```

`continue` - skips the iteration and move to next loop

```
count=0
while [ "$x" -lt 5 ]; do
    ((x++))
    if [ "$x" -eq 3 ]; then
        continue # Skip the echo statement
    fi
    echo "X is: $x"
done


output
X is: 1
X is: 2
X is: 4
X is: 5
```

5. Looping over files — `for file in *.log` - iterate each file matching the pattern .log in a currect directory
```
for file in *.log; do
  ./MyProgram.sh "$file"  #pass each file as argument to a script named MyProgram.sh
done
```

6. Looping over command output — `while read line` - is the safest and most memory-efficient way to process the output of a shell command line-by-line
```
ls *.txt | while read LINE; do
    echo "File: $LINE"
done
```
---

### Task 4: Functions
1. Defining a function — `function_name() { ... }`
```
say_hello() {
    
    echo "Hello!"
}
```

2. Calling a function - called directly as function name
```
say_hello
```

3. Passing arguments to functions — `$1`, `$2` inside functions
```
say_hello() {
    echo "Hello, $1!"
}
say_hello Yatin

Output
Hello, Yatin!
```

4. Return values — `return` vs `echo` - 

`return` used to return a value (0-255) by a function to calling function and exit the function.

`echo` is print statement or value on screen or file

```
check_service() {
    systemctl is-active --quiet "$1"
    if [ $? -eq 0 ]; then
        return 0    # service is running
    else
        return 1    # service is not running
    fi
}

check_service nginx
if [ $? -eq 0 ]; then
    echo "nginx is running"
else
    echo "nginx is not running"
fi
echo $?
```

```
get_disk_usage() {
    du -sh "$1" | awk '{print $1}'
}

usage=$(get_disk_usage /var/log)
echo "Disk usage of /var/log: $usage"
```

5. Local variables — 
`local` - defination of variable inside a function only. `local` keyword before the variable is important else by default variables are global

```
count_files() {
    local total=$(ls "$1" | wc -l)   # local variable named total
    echo "Total files in $1: $total"  # would print number of files inside /var/log
}

count_files /var/log

echo $total   # empty, because 'total' is local as globally total is not defined
```


---

### Task 5: Text Processing Commands
1. `grep` — search patterns,
 
 `-i` - ignore case does not care of uppercase or lowercase, as by default it's case sensitive `grep -i ERROR test.txt`
 
 `-r` - recursive search in currect directory and subdirectories `grep -r "todo"`
 
 `-c` - count matching lines `grep -c error test.txt`
 
 `-n` - show line numbers for matching word/phrase line `grep -n ERROR test.log`
 
 `-v` - lines that don't match `grep -v error test.log`
 
 `-E` - searches multiple patterns with extended regex `grep -E "Error|Failed" test.log`

2. `awk` — Process and extract text from files or input,especially by columns/fields.

print columns - Extract and display specific columns from text.
```
awk '{print $1, $2}' file
awk '{print $1}' /etc/passwd
``` 

field separator -  Specify a custom delimiter instead of default spaces/tabs.
```
awk -F ":" '{print $1, $3}' file
awk -F ":" '{print $1, $3}' /etc/passwd
```

patterns - Perform actions only on lines matching a pattern.
```
awk '/pattern/ { action }' file
awk '/root/ {print }' /etc/passwd
```

`BEGIN/END` - Execute actions before or after processing the file
```
awk 'BEGIN { ... } { ... } END { ... }' file
awk -F ":" 'BEGIN {print "Users list:"} {print $1} END {print "Done"}' /etc/passwd
```

3. `sed` — to search and replace operator in a text , it can also delete, insert, append text in files or piped input

substitution - Substitute first match in a line
```
sed 's/pattern/replacement/' file
sed 's/error/ERROR/' file.txt
```

delete lines - delete a line
```
sed 'Nd' file
sed '2d' file.txt
```

in-place edit - Modify the file directly instead of just printing output.
```
sed -i 's/pattern/replacement/g' file
sed -i 's/error/ERROR/g' file.txt
```

4. `cut` — extract columns by delimiter - extract specific sections from each line of input based on bytes (-b), characters (-c), or fields (-f)
```
echo "Hello World" | cut -c 1-5
# Output: Hello

echo "Hello World" | cut -c 7-
# Output: World

echo "0123456789" | cut -c 2,5,8
# Output: 147

echo "apple banana cherry" | cut -d ' ' -f 1
# Output: apple

cut -d: -f1,7 /etc/passwd
# This displays the username (field 1) and shell (field 7) for each user.

echo "field1,field2,field3,field4" | cut -d, -f 1-3
# Output: field1,field2,field3

echo "ID,Name,Age" | cut -d, -f 1 --complement
# Output: Name,Age
```

5. `sort` — arrange lines in a file alphabetically, number in ascending or descending order and remove duplicates
alphabetical - 
```
sort fruits.txt

if fruits.txt
bananas,2
apples,1
oranges,20
kiwis,3

output 
apples,1
bananas,2
kiwis,3
oranges,20
```

numerical
```
 sort -n numbers.txt

if numbers.txt
4
90
9
10

Output
4
9
10
90
```
reverse
```
sort -r fruits.txt

output
oranges,20
kiwis,3
bananas,2
apples,1
```
unique
```
sort -u list.txt

The -u option sorts the file and keeps only one copy of each unique line.
```

Sorted output to a new file
```
# Redirect to a new file
sort fruits.txt > sorted_fruits.txt

# Overwrite the original file with sorted content (guaranteed safe in GNU sort)
sort -o fruits.txt fruits.txt
```

6. `uniq` — Removes consecutive duplicate lines,also count occurrences.

 deduplicate
```
# Sample file content (apple.txt):
# apple
# orange
# orange
# apple
# apple
# banana
# apple
# banana
# watermelon


sort apple.txt | uniq

Output
apple
banana
orange
watermelon
```

count - 
```
sort apple.txt | uniq -c

Output
      4 apple
      2 banana
      2 orange
      1 watermelon

      sort apple.txt | uniq -u

Output
watermelon 

```


7. `tr` — translate/delete characters

```
 echo "hello"     | tr 'a-z' 'A-Z'   # convert to uppercase

    Output
    HELLO

 echo "hello 123" | tr -d '0-9'  # delete digits

    Output
    hello
```

8. `wc` — line/word/char count

```
    wc -l file.txt    # count number of lines in file.txt
    wc -w file.txt    # count word in file.txt
    wc -c file.txt    # count character in file.txt
```

9. `head` / `tail` — first/last N (Default 10) lines, follow mode
```
    head -n 5 file.txt                  # first 5 lines
    tail -n 5 file.txt                  # last 5 lines
    tail -f /var/log/nginx/access.log   # live updates from the file to screen
```

---

### Task 6: Useful Patterns and One-Liners

- Find and delete files older than N days
```
find /var/log -type f -name "*.log" -mtime +15 -exec rm -f {} \;
```

- Count lines in all `.log` files
```
wc -l /var/log/*.log
```

- Replace a string across multiple files
```
sed 's/apple/orange/g' fruits.txt  # Replace all occurrences (global) of "apple" with "orange" on each line
```

- Check if a service is running
```
systemctl is-active --quiet docker && echo "Running" || echo "Stopped"
```

- Monitor disk usage with alerts
```
df -h | awk '$5+0 > 80 {print $0}' | mail -s "Disk Usage Alert on $(hostname)" your.email@example.com
```

- Parse CSV or JSON from command line
```
awk -F',' '{print $2}' filename.csv
```

- Tail a log and filter for errors in real time
```
tail -f /var/log/syslog | grep -E 'ERROR|CRITICAL'
```

---

### Task 7: Error Handling and Debugging

1. Exit codes — 
`$?` - stores previous run command/script/function exit status

`exit 0` - store success for the function or script

`exit 1` - terminate the script or function immediately with failure

2. `set -e` — exit on error - Exit immediately if a command fails

3. `set -u` — treat unset variables as error - Error if using an unset variable

4. `set -o pipefail` — catch errors in pipes - 	Fail if any command in a pipeline fails

5. `set -x` — debug mode (trace execution) - Debug mode (show commands before running)

6. Trap — `trap 'cleanup' EXIT` - Run cleanup function when script exits

```
set -e
false → script stops immediately

set -u
echo $name → error if name is not set

set -o pipefail
false | true → returns failure

set -x
echo "Hello" → prints + echo Hello

	trap 'cleanup' EXIT
cleanup() { echo "Cleaning up..."; } → runs on exit
```

---

