# User & Group Management Commands
## These are the User & Group Management Commands commonly used in DevOps.
| #  | Command     | #  | Command       |
|----|-------------|----|---------------|
| 1  | sudo        | 6  | userdel       |
| 2  | useradd     | 7  | groupadd      |
| 3  | whoami      | 8  | gpasswd -a,-m |
| 4  | su          | 9  | groupdel      |
| 5  | passwd      |    |               |

## 1. `sudo` — Superuser Do
**What it does:**
- Run commands with administrative (root) privileges.

**Syntax:**
```
sudo <command>
```
**Examples:**
```
sudo apt update           # run with admin rights
sudo vi /etc/hosts        # edit system file
sudo systemctl restart nginx  # restart a service
```
**Notes:**
- Prompts for your password (if your user is in the sudoers list).
- Use carefully — running dangerous commands as root can harm the system.
- Shortcuts: 
  - `sudo !!` → repeat last command with sudo
   - `sudo -i` → start a root shell
 ## 2. useradd
 **What it does:**
- Create a new user on the system.

**Syntax:**
```
sudo useradd [options] username
```
**Common Options:**
| Option | Meaning                          |
| ------ | -------------------------------- |
| `-m`   | Create home directory            |
| `-s`   | Specify default shell            |
| `-c`   | Add comment (e.g., full name)    |
| `-G`   | Add user to supplementary groups |

**Examples:**
```
sudo useradd -m -s /bin/bash john      # create user john with home & bash shell
sudo useradd -m -s /bin/bash -G sudo jane  # create user jane with sudo rights
```
**Notes:**
- After `useradd`, you usually set a password:
```
sudo passwd john
```
- `adduser` is a friendlier alternative on Debian/Ubuntu.

## 3. `whoami`
**What it does:**
- Displays the current effective username of the person running the command.

**Syntax:**
```
whoami
```
**Notes:**
- Quick way to confirm which account you’re using (esp. after sudo).

## 4. `su` — Switch User
**What it does:**
- Switch to another user account or root temporarily.

**Syntax:**
```
su [username]
```
**Examples:**
```
su                        # switch to root (requires root password)
su john                   # switch to user john
su -                      # switch to root and load root environment
```
**Notes:**
- Unlike `sudo`, `su` requires the target user’s password, not your own.
- Use `exit` or `Ctrl+D` to return to your previous account.

## 5. `passwd`
**What it does:**
- Sets or changes a user’s password.

**Syntax:**
```
passwd [username]
```
**Examples:**
```
passwd                   # change password of current user
sudo passwd john         # set/change password for user john
```
**Notes:**
- Prompts for the new password twice.
- Can also expire passwords or enforce password policies with options (`-e`, `-l`, etc.).

## 6. `userdel`
**What it does:**
- Deletes a user from the system.

**Syntax:**
```
sudo userdel [options] username
```
**Examples:**
```
sudo userdel john             # delete user john (home folder not removed)
sudo userdel -r jane          # delete user jane and remove home directory
```
**Notes:**
- `-r` is important if you want to remove the user’s home folder and mail spool.
- Always double-check before deleting a user to avoid data loss.

## 7. `groupadd`
**What it does:**
- Creates a new group on the system.

**Syntax:**
```
sudo groupadd [options] groupname
```
**Examples:**
```
sudo groupadd developers      # create a group named developers
sudo groupadd -g 1010 designers  # create group with specific GID
```
**Notes:**
- Groups are used to manage permissions for multiple users.
- Combine with `usermod -aG groupname username` to add users to a group.

## 8. `gpasswd -a`
**What it does:**
- Adds a user to a group.

**Syntax:**
```
sudo gpasswd -a username groupname
```
**Example:**
```
sudo gpasswd -a john developers   # add user john to group developers
```
**Notes:**
- Changes take effect after the user logs out and logs back in.
- Useful for managing group permissions easily.

## 9. `gpasswd -m`
**What it does:**
- Removes a user from a group.

**Syntax:**
```
sudo gpasswd -d username groupname
```
**Example:**
```
sudo gpasswd -d jane developers   # remove user jane from group developers
```
**Notes:**
- Ensure you don’t remove users from groups required for system access.
- Often used for cleaning up group membership.

**Note:** `-m` is not standard; the standard option to remove is `-d`.

## 10. `groupdel`
**What it does:**
- Deletes a group from the system.

**Syntax:**
```
sudo groupdel groupname
```
**Example:**
```
sudo groupdel designers          # delete the group designers
```
**Notes:**
- The group must not have any logged-in users.
- Removing a group does not delete users from the system — only removes the grou
