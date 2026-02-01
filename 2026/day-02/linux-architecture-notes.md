# Day 02 – Linux Architecture, Processes, and systemd

## Task
Today’s goal is to **understand how Linux works under the hood**.

You will create a short note that explains:
- The core components of Linux (kernel, user space, init/systemd)
Linux has ASK architect - Application, Shell, Kernel (bridge between hardware and application) in center hardware.
Kernel handles - process, memory and device management along with system calls of OS or user. It's the heart of OS.
User space is collection of all code that runs outside of kernel privledge.
init/systemd is 1st process to start in Linux with PID 1 and its responsible for all other process startup, running, shutdown until Linux OS is up.

Boot process of linux powerON system BIOS -> MBR -> GNU GRUB -> Kernel -> init or Systemd PID 1 -> Runlevel -> systemctl

Systemd is the initial process started on linux that remaining running on it until system stop/rebooted.

Everything in Linux is file and folder.

- How processes are created and managed

Every command or activity performed on Linux generates process which has PID which is uniquely generated for it and remain until that process stay in the system.

These PID are similar to task in Windows. We could manage them similar to task manager (Windows). We could kill these process with kill -9

Below are processes, 4 basic state in Linux

Running/Runable (R) - process that is running or working in progress in RUNNING state. Process that could be signaled to execute or perform some task is RUNABLE.
SLEEPING - Process waiting for some resource like I/O, code commit to wake it up. Its of 2 type
INTERRUPTABLE SLEEPING (S) - Process which could be signalled to move further and perform the activity
NONINTERRUPTABLE SLEEPING (D) - Process that could not be moved further and those could only be kill by restart of system.
STOPPED (T) - Process that is stopped by Ctrl+Z. It could then be kill -9 or SIGCONT to continue further.
ZOMBIE (Z) - Ghost processes whose child process been completed or killed by parent process are not released by system and hold resources on it.

top command will give process state in col S.

Few basic command in Linux

ps (process status) - current processes running
ls (list) - to list contents in present directory/folder
cat (concatenate) - to read file in 1 shot
vi (visual editor) - to edit a file
cp (copy), mv (move/rename)
grep - to search a pattern in file or output etc and fetch it out or display
systemctl - system control command to start/stop/check status of process
top - to check running process status/utilisation in CPU/memory usage in real time

- What systemd does and why it matters
systemd is PID 1 which creates other below processes to start different stuff on Linux, without systemd Linux would not boot.

This is the foundation for all troubleshooting you will do as a DevOps engineer.

## Guidelines
Follow these rules while creating your notes:

- Explain **process states** (running, sleeping, zombie, etc.)
- List **5 commands** you would use daily
- Keep it **short and practical** (under 1 page)
- Use bullet points and short headings

---

## Resources
You may refer to:

- Linux `man` pages (`ps`, `top`, `systemctl`)
- Official systemd docs
- Your class notes


## Why This Matters for DevOps
Linux is the base OS for almost every production system.

If you know how processes and systemd work, you can:
- Debug crashed services faster
- Fix CPU/memory issues
- Understand logs and service restarts confidently

This knowledge saves hours during incidents.
