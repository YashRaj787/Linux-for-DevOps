# System-level Commands
| #  | Command   | #  | Command  |
|----|-----------|----|----------|
| 1  | uname     | 11 | apt      |
| 2  | uptime    | 12 | yum      |
| 3  | date      | 13 | dnf      |
| 4  | who       | 14 | pacman   |
| 5  | whoami    | 15 | portage  |
| 6  | which     |    |          |
| 7  | id        |    |          |
| 8  | sudo      |    |          |
| 9  | shutdown  |    |          |
| 10 | reboot    |    |          |

## 1. `uname`
**What it does:**
- Displays basic information about the system/kernel.

**Syntax:**
```
uname [options]
```
**Examples & Options:**

| Option   | Description                                         | Example    |
| -------- | --------------------------------------------------- | ---------- |
| *(none)* | Prints kernel name                                  | `uname`    |
| `-a`     | Show all system info (kernel, version, machine, OS) | `uname -a` |
| `-r`     | Kernel release                                      | `uname -r` |
| `-s`     | Kernel name                                         | `uname -s` |
| `-m`     | Machine hardware (e.g., x86\_64)                    | `uname -m` |

**Notes:**
- `uname -a` is most commonly used to get a quick summary of system info.

## 2. `uptime`
**What it does:**
- Shows how long the system has been running and the load average.

**Syntax:**
```
uptime
```
**Sample Output:**
```
19:05:32 up 3 days,  2:17,  2 users,  load average: 0.00, 0.01, 0.05
```
**Breakdown:**
- Current time
- How long the system has been running
- Number of logged-in users
- Load average (system workload over 1, 5, 15 min)
**Notes:**
- Helps check server stability and performance.
- “Load average” shows how busy the CPU has been.

## 3. `date`
**What it does:**
- Displays or sets the system date & time.

**Syntax:**
```
date [options]
```
**Examples:**
```
date                     # show current date and time
date "+%Y-%m-%d %H:%M:%S"    # custom format
sudo date -s "2025-09-21 19:10:00"   # set system date/time (root)
```
**Formatting Options:**
| Code | Meaning           |
| ---- | ----------------- |
| `%Y` | Year (e.g., 2025) |
| `%m` | Month (01–12)     |
| `%d` | Day               |
| `%H` | Hour (24h)        |
| `%M` | Minute            |
| `%S` | Seconds           |

**Notes:**
- Changing the system time usually requires root privileges.
- `date` is also handy inside shell scripts for timestamps.

## 4. `who` & `whoami`
### `who`
**What it does:**
- Shows who is currently logged in on the system.

**Syntax:**
```
who
```
**Sample Output:**
```
user1   tty7   2025-09-21 09:15 (:0)
user2   pts/0  2025-09-21 19:05 (192.168.1.5)
```
**Notes:**
- Shows usernames, terminals (tty/pts), login time, and source (local/IP).
- Good for checking active sessions.

`whoami`
**What it does:**
- Displays the current effective username of the person running the command.

**Syntax:**
```
whoami
```
**Notes:**
- Quick way to confirm which account you’re using (esp. after sudo).

## 5. `which`
**What it does:**
- Shows the full path of the executable a shell will run for a command.

**Syntax:**
```
which <command>
```
**Examples:**
```
which python3
which ls
```
**Notes:**
- Helps you identify which version of a program is being used when multiple versions are installed.
- If it returns nothing, the command isn’t in your `$PATH`.

## 6. `id`
**What it does:**
- Displays your user ID (UID), group ID (GID), and group memberships.

**Syntax:**
```
id [username]
```
**Examples:**
```
id             # info about yourself  
id root        # info about another user
```
**Sample Output:**
```
uid=1000(user) gid=1000(user) groups=1000(user),27(sudo)
```
**Notes:**
- Useful for checking privileges or debugging permission problems.
- Combine with groups to see group memberships only.

## 7. `sudo` — Superuser Do
**What it does:**
- Run commands with administrative (root) privileges.

**Syntax:**
```
sudo <command>
```
**Examples:**
```
sudo apt update              # run with admin rights
sudo vi /etc/hosts           # edit system file
```
**Notes:**
- Prompts for your password (if you’re in the sudoers list).
- Use only when necessary → protects system from accidental damage.
- `sudo -i` → start a root shell.
- `sudo !!` → repeat the last command with sudo.

## 8. `shutdown`
**What it does:**
- Safely power off or schedule a shutdown for the system.

**Syntax:**
```
shutdown [options] [time] [message]
```
**Examples:**
```
sudo shutdown now            # shutdown immediately
sudo shutdown +10            # shutdown after 10 min
sudo shutdown -h 20:30 "Maintenance"   # halt at 8:30 PM with message
```
**Options:**
| Option | Meaning                   |
| ------ | ------------------------- |
| `-h`   | halt/power off            |
| `-r`   | reboot instead of halt    |
| `-c`   | cancel scheduled shutdown |

**Notes:**
- Always use sudo because it’s a privileged action.
- shutdown ensures all processes stop cleanly before power-off.

## 9. `reboot`
**What it does:**
- Restart the system immediately.

**Syntax:**
```
sudo reboot
```
**Notes:**
- Similar to `shutdown -r now`, but shorter.
- Requires admin rights.
- Useful after kernel updates or major configuration changes.

## 10. `apt` – Advanced Package Tool
***(Debian / Ubuntu and derivatives)***
**What it does:**
- Install, update, upgrade, and remove software packages on Debian-based systems.
**Common usage:**
```
sudo apt update                 # refresh package index  
sudo apt upgrade                # upgrade installed packages  
sudo apt install nginx          # install a package  
sudo apt remove nginx           # remove package (keep configs)  
sudo apt purge nginx            # remove package + configs  
sudo apt autoremove             # remove unneeded deps
```
**Notes:**
- Always run `sudo apt update` before installing to get the latest package list.
- `apt` is newer and more user-friendly than the older `apt-get` interface.

## 11. `yum` – Yellowdog Updater, Modified
***(CentOS, RHEL 7, older Fedora)***

**What it does:**
- Package manager for RPM-based distributions (Red Hat family).
**Examples:**
```
sudo yum update            # update all packages  
sudo yum install httpd     # install Apache  
sudo yum remove httpd      # remove package  
sudo yum search mysql      # search for a package
```
**Notes:**
- Replaced by `dnf` in newer Fedora/CentOS Stream versions.
- `yum` keeps backward compatibility scripts for older systems.

## 12. `dnf` – Dandified YUM
***(Fedora, RHEL 8+, CentOS Stream)***

**What it does:**
- Modern replacement for yum; better performance and dependency handling.
**Examples:**
```
sudo dnf update            # refresh + update packages  
sudo dnf install nginx     # install  
sudo dnf remove nginx      # uninstall  
sudo dnf search python     # search package
```
**Notes:**
- Command syntax is almost identical to `yum`.
- Recommended on all modern RHEL/Fedora-based distributions.

## 14. `pacman` – Package Manager for Arch Linux
**What it does:**
- Install, remove, and manage software packages on Arch Linux and derivatives (Manjaro, EndeavourOS).

**Syntax & Examples:**
```
sudo pacman -Syu           # update package database & upgrade all packages
sudo pacman -S package_name # install a package
sudo pacman -R package_name # remove a package
sudo pacman -Ss keyword     # search for a package
sudo pacman -Qi package_name # info about a package
```
**Notes:**
- `pacman` uses `.pkg.tar.zst` packages.
- `-S` = sync, `-R` = remove, `-U` = install from local file.
- Combines features of apt/yum in a simple interface.

## 15. `portage` – Package Manager for Gentoo Linux
**What it does:**
- Gentoo’s source-based package management system, where software is compiled from source.

**Command tool:** `emerge`

**Examples:**
```
sudo emerge --sync             # sync package tree
sudo emerge package_name       # install a package
sudo emerge --update --deep @world  # update system
sudo emerge --search keyword   # search for package
```
**Notes:**
- Gentoo emphasizes optimization and customization.
- Packages are compiled, which can take longer but allows optimization for your hardware.
- USE flags control optional features during compilation.
  
