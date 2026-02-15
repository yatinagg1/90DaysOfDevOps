# Day 18 – Shell Scripting: Functions & Slightly Advanced Concepts

---

## Challenge Tasks

### Task 1: Basic Functions
1. Create `functions.sh` with:
   - A function `greet` that takes a name as argument and prints `Hello, <name>!`
   - A function `add` that takes two numbers and prints their sum
   - Call both functions from the script

![alt text](./images/image.png)

- Script called with 3 arguments
- Those arguments are input for the function and observe how arguments changes value when function been called

---

### Task 2: Functions with Return Values
1. Create `disk_check.sh` with:
   - A function `check_disk` that checks disk usage of `/` using `df -h`
   - A function `check_memory` that checks free memory using `free -h`
   - A main section that calls both and prints the results

![alt text](./images/image-1.png)

- Functions been called from another main()
- Usage of awk , how we could use this powerful command in script to fetch a particular information

---

### Task 3: Strict Mode — `set -euo pipefail`
1. Create `strict_demo.sh` with `set -euo pipefail` at the top
2. Try using an **undefined variable** — what happens with `set -u`?
3. Try a command that **fails** — what happens with `set -e`?
4. Try a **piped command** where one part fails — what happens with `set -o pipefail`?

**Document:** What does each flag do?
- `set -e` → Script exits if any command fails
- `set -u` → script exits if try to use a variable which is not defined
- `set -o pipefail` → if any piped commands either 1 or 2 fails example - (command1| command2) , its considered failure for whole line

Output of script execution

![alt text](./images/image-2.png)

Script 

![alt text](./images/image-3.png)

- echo "DONE" - it will be executed if function called in previous step completes without issue/error but here functions are gave error and thus exited the script

---

### Task 4: Local Variables
1. Create `local_demo.sh` with:
   - A function that uses `local` keyword for variables
   - Show that `local` variables don't leak outside the function
   - Compare with a function that uses regular variables

![alt text](./images/image-4.png)

- local variable has limit within the function itself where its defined
- global variable has no limit and returned as value

---

### Task 5: Build a Script — System Info Reporter
Create `system_info.sh` that uses functions for everything:
1. A function to print **hostname and OS info**
2. A function to print **uptime**
3. A function to print **disk usage** (top 5 by size)
4. A function to print **memory usage**
5. A function to print **top 5 CPU-consuming processes**
6. A `main` function that calls all of the above with section headers
7. Use `set -euo pipefail` at the top

Output of the script
![alt text](./images/image-5.png)

Script contents
![alt text](./images/image-6.png)

- Usage of sort in various command and method differently used
- How to automate daily task and get system information quickly

---
