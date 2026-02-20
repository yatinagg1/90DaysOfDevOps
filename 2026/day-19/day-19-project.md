# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Task
Apply scripting knowledge in real-world mini projects.

- Write a **log rotation** script
- Write a **server backup** script
- Schedule them with **crontab**

---

## Challenge Tasks

### Task 1: Log Rotation Script
Create `log_rotate.sh` that:
1. Takes a log directory as an argument (e.g., `/var/log/myapp`)
2. Compresses `.log` files older than 7 days using `gzip`
3. Deletes `.gz` files older than 30 days
4. Prints how many files were compressed and deleted
5. Exits with an error if the directory doesn't exist

Output of script
![alt text](./images/image.png)

Script:
![alt text](./images/image-1.png)
---

### Task 2: Server Backup Script
Create `backup.sh` that:
1. Takes a source directory and backup destination as arguments
2. Creates a timestamped `.tar.gz` archive (e.g., `backup-2026-02-08.tar.gz`)
3. Verifies the archive was created successfully
4. Prints archive name and size
5. Deletes backups older than 14 days from the destination
6. Handles errors — exit if source doesn't exist

Output of script:
![alt text](./images/image-2.png)

Script:
![alt text](./images/image-3.png)

Error Handling

![alt text](./images/image-5.png)

---

### Task 3: Crontab
1. Read: `crontab -l` — what's currently scheduled?

Nothing for user - yatin and root both

![alt text](./images/image-4.png)

2. Understand cron syntax:
   ```
   * * * * *  command
   │ │ │ │ │
   │ │ │ │ └── Day of week (0-7)
   │ │ │ └──── Month (1-12)
   │ │ └────── Day of month (1-31)
   │ └──────── Hour (0-23)
   └────────── Minute (0-59)
   ```
3. Write cron entries for:
   - Run `log_rotate.sh` every day at 2 AM
   - Run `backup.sh` every Sunday at 3 AM
   - Run a health check script every 5 minutes

crontab -e - used to edit the crontab and make entry into the file

![alt text](./images/image-6.png)

![alt text](./images/image-7.png)

---

### Task 4: Combine — Scheduled Maintenance Script
Create `maintenance.sh` that:
1. Calls your log rotation function
2. Calls your backup function
3. Logs all output to `/var/log/maintenance.log` with timestamps
4. Write the cron entry to run it daily at 1 AM


Output of /var/log/maintenance.log file

![alt text](./images/image-8.png)

Script:

![alt text](./images/image-9.png)

Crontab addition
![alt text](./images/image-10.png)
---

### What I Learned
- Usage of [ ! -d $dir ] - To validate if directory exists of not
- Arguments $1, $2, $#, $? - usage in scripts
- File handling and cleanup with -mtime
- crontab entry and usage
- How to combine scripts or functions to redirect output to single location