# File Permission Commands
| #  | Command        | #  | Command        |
|----|----------------|----|----------------|
| 1  | umask          | 4  | chown command  |
| 2  | ls -l          | 5  | chgrp command  |
| 3  | chmod          |    |                |

## 1. `umask`
**What it does:**
- Sets the default permissions for newly created files and directories.

**Syntax:**
```
umask [mask]
```
**Examples:**
```
umask                       # show current mask
umask 022                   # default: files 644, directories 755
umask 077                   # default: files 600, directories 700 (private)
```
**Notes:**
- Default permissions for new files = `666 - umask`
- Default permissions for new directories = `777 - umask`
- Helps control security by restricting access for new files/folders.

## 2. `ls -l`
**What it does:**
- Lists files and directories in long format, showing permissions, owner, group, size, and modification time.

**Syntax:**
```
ls -l [directory]
```
**Example:**
```
ls -l /home/user
```
**Sample Output:**
```
-rw-r--r-- 1 user developers 1024 Sep 21 19:00 file.txt
drwxr-xr-x 2 user developers 4096 Sep 21 18:50 myfolder
```
**Breakdown of Permissions:**
- `-rw-r--r--` → File type + permissions

  - `-`= file, `d` = directory

  - `rw-` = owner can read/write

  - `r--` = group can read

  - `r--` = others can read
**Notes:**
- Use `ls -lh` for human-readable file sizes.
- `ls -la` shows hidden files (`.` and `..` included).

## 3. `chmod`
**What it does:**
- Changes permissions of files and directories.

**Syntax:**
```
chmod [options] mode file
```
**Examples:**
Numeric (octal) method:
```
chmod 644 file.txt   # owner rw-, group r--, others r--
chmod 755 myfolder   # owner rwx, group r-x, others r-x
```
**Symbolic method:**
```
chmod u+x script.sh  # add execute permission to user
chmod g-w file.txt   # remove write permission from group
chmod o=r file.txt   # set others’ permissions to read only
```
**Notes:**
- `r` = read, `w` = write, `x` = execute
- Numeric mode: sum of r=4, w=2, x=1 (e.g., rwx = 7, r-x = 5)
- Use `chmod -R` to recursively change permissions in directories.

## 4. `chown`
**What it does:**
- Changes the owner and optionally the group of a file or directory.

**Syntax:**
```
sudo chown [owner][:group] file_or_directory
```
**Examples:**
```
sudo chown john file.txt             # change owner to john
sudo chown john:developers file.txt  # change owner to john and group to developers
sudo chown -R john:developers /home/john  # recursively change owner/group for directory
```
**Notes:**
- `-R` → recursive, applies to all files/subdirectories.
- Only root or sudo users can change ownership.
- Useful when fixing file permission/ownership issues after copying or extracting files.

## 5. `chgrp`
**What it does:**
- Changes the group ownership of a file or directory.

**Syntax:**
```
sudo chgrp groupname file_or_directory
```
**Examples:**
```
sudo chgrp developers file.txt       # change group to developers
sudo chgrp -R designers /projects    # recursively change group for a directory
```
**Notes:**
- Only root or a member of the target group can change the group.
- Use `chown` if you also need to change the owner.
