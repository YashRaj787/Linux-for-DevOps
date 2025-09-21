| **Disk Usage** |                             | **Process Commands**   |
|-----------------------|-----------------------------|------------------------|
| 1) df                 |                             | 1) ps                 |
| 2) du                 |                             | 2) top                |
|                       |                             | 4) fuser              |
|                       |                             | 5) kill               |
|                       |                             | 7) nohup              |
|                       |                             | 8) free               |
|                       |                             | 10) vmstat            |

# Disk usage comamnds:
## 1. `df` — Disk Free
**What it does:**
- Shows disk space usage of mounted filesystems.

**Syntax:**
```
df [options]
```
**Examples:**
```
df                         # show disk usage of all mounted filesystems
df -h                      # human-readable sizes (GB, MB)
df -T                      # show filesystem type
df -i                      # show inode usage
```
**Notes:**
- `df` is great to quickly check available disk space before installing software or moving large files.

## 2. `du` — Disk Usage
**What it does:**
- Shows size of files and directories.

**Syntax:**
```
du [options] <file_or_directory>
```
**Examples:**
```
du file.txt                 # size of a file
du -h /home/user            # human-readable directory sizes
du -sh /home/user           # summarize total size of directory
du -ah /var/log             # list all files + sizes in human-readable form
```
**Notes:**
- `du` is used to analyze which folders/files are consuming the most space.
- Combine `du` with `sort -h` to find largest directories:
```
du -sh * | sort -h
```
# Process Commands:
## 1. `ps` — Process Status
**What it does:** 
- Displays information about the running processes on your system.

**Syntax:**
```
ps [options]
```
**Common options:**
| Option            | Description                           |
| ----------------- | ------------------------------------- |
| `ps`              | Show processes for the current shell  |
| `ps -e` / `ps -A` | Show all processes                    |
| `ps -f`           | Full-format listing                   |
| `ps aux`          | Show all processes with detailed info |

**Examples:**
```
ps                       # processes in current terminal  
ps -ef                   # all processes in full format  
ps aux | grep firefox    # find a specific process
```
**Notes:**
- `ps` is great for snapshots (one-time view) of processes.
- Combine with `grep` to locate a specific process quickly.

 ## 2. `top` — Task Manager in Terminal
 **What it does:**
- Shows real-time information about running processes, CPU, memory, etc.

**Syntax:**
```
top
```
**Key interactions inside top:**
| Key | Action                     |
| --- | -------------------------- |
| `q` | Quit                       |
| `k` | Kill a process (enter PID) |
| `P` | Sort by CPU                |
| `M` | Sort by memory             |
| `h` | Help screen                |

**Notes:**
- Ideal for monitoring system performance.
- Alternatives: `htop` (more user-friendly, if installed).

## 3. `fuser` — Identify Processes Using a File or Socket
**What it does:**
- Shows which processes are using a specific file, directory, or port.

**Syntax:**
```
fuser [options] <file_or_socket>
```

**Examples:**
```
fuser /var/log/syslog        # find processes using syslog
fuser -v /home/user/file.txt # verbose output
fuser -k 8080/tcp            # kill processes using port 8080
```
**Notes:**
- Useful when you get “device or resource busy” errors.
- Great for freeing up ports or checking who is locking a file.

## 4. `kill` — Terminate Processes
**What it does:**
- Send a signal to a process (most often to stop/terminate it).

**Syntax:**
```
kill [options] <PID>
```
**Examples:**
```
kill 1234          # send default TERM signal  
kill -9 1234       # force kill (SIGKILL)  
kill -l            # list all signals
```
**Notes:**
- Use `ps` or `top` to find the PID (process ID).
- `kill -9` is powerful — stops a process without cleanup; use it only if normal `kill` doesn’t work.

## 5. `nohup` — Run Commands Immune to Hangups
**What it does:**
- Runs a command that keeps running even after you log out or close the terminal.

**Syntax:**
```
nohup command [args] &
```
**Examples:**
```
nohup python script.py &        # run script in background  
nohup ./long_task.sh > out.log &
```
**Notes:**
- Output is written to `nohup.out` by default unless redirected.
- Commonly used for long-running jobs on remote servers.

## 6. `free` — Memory Usage Report
**What it does:**
- Displays the amount of free and used RAM/swap in the system.

**Syntax:**
```
free [options]
```
**Examples:**
```
free         # memory in KB  
free -m      # memory in MB  
free -g      # memory in GB  
free -h      # human-readable
```
**Notes:**
- Columns include: `total`, `used`, `free`, `shared`, `buff/cache`, `available`.
- Quick way to check system memory status.

## 7. `vmstat` — Virtual Memory Statistics
**What it does:**
- Reports statistics about processes, memory, I/O, CPU, etc. (system health).

**Syntax:**
```
vmstat [delay] [count]
```
**Examples:**
```
vmstat              # one-time summary  
vmstat 2            # updates every 2 seconds  
vmstat 2 5          # 5 updates, 2 sec apart
```
**Notes:**
- Columns include: `r` (running), `b` (blocked), `swpd` (swap), `free` (free memory), `si/so` (swap in/out), `us` (user CPU), `sy` (system CPU).
- Lightweight alternative to `top` for performance troubleshooting.
