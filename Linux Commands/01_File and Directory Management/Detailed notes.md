# Here's the list of commands related to file and direactory management: 
### 1. ls
### 2. cd 
### 3. pwd
### 4. mkdir
### 5. rm, rmdir
### 6. cat, zcat
### 7. touch
### 8. head
### 9. tail, tail -f
### 10. less, more
### 11. cp
### 12. mv
### 13. wc
###14. vi editor
### 15. ln (hard link, soft link)
### 16. cut
### 17. tee
### 18. sort
### 19. clear
### 20. diff

# 1. `ls`
**What it does:**
- Lists the contents of the current directory (files, folders, links, etc.).
---
**Common Options**
| Command | Description |
|---------|-------------|
| `ls -l`   | Long listing (permissions, owner, size, date) |
| `ls -a`   | Include hidden files (those starting with `.`) |
| `ls -lh`  | Human-readable sizes |
| `ls -ltr` | Sort by time, newest last |

---
**Examples**
```bash
ls
ls -la
```
**Notes:**
- Use `ls` to quickly see what is inside a folder.
- Combine options, e.g. `ls -lah` = long + all + human readable.

# 2. `cd`
**What it does:** 
- Changes the current working directory.
**Syntax:**
```
cd <path>
```
**Examples:**
```
cd /home/user/Documents      # go to Documents
cd ..                        # go up one level
cd ~                         # go to home directory
cd -                         # return to previous directory
```
**Notes:**
- '..' means parent directory.
- '.' means current directory.
- '~' is shorthand for your home folder.

# 3. `pwd`
**What it does:**
- Prints the full (absolute) path of the current working directory.
**Example:**
```
pwd
# Output: /home/user/Documents
```
**Notes:**
- Useful to check “Where am I?” in the filesystem.
- Especially handy before running commands that depend on your location.

# 4. `mkdir`
**What it does:** 
- Make Directory.  
**Mainly use:** Create a new folder.
**Syntax:**
```bash
mkdir <directory_name>
```
**Examples:**
```
mkdir test           # create a folder named test
mkdir -p a/b/c       # create parent dirs if they don’t exist
```
**Notes:**
- `p` lets you create nested folders in one go.
- If the folder already exists, `mkdir` throws an error unless `-p` is used.

# 5. `rm` and `rmdir`
**What it does:** 
- Remove files or directories
```
rm file.txt          # delete file
rm -r folder         # delete folder & its contents
rm -i file.txt       # ask before deleting
```
⚠️ Be very careful with `rm -r` because it deletes everything permanently.

`rmdir` – **Remove empty directories**
```
rmdir empty_folder
```
**Notes:**
- Use `rmdir` only if the folder is empty; otherwise, use `rm -r`.
- `rm -rf` = force remove recursively (no confirmation) = **handle with caution**.

# 6️. `cat` **and** `zcat`
**What it does:**
- Displays the contents of a file, or joins multiple files.
**Examples**:
```
cat file.txt
cat file1.txt file2.txt > combined.txt
```
**Notes:**
- Good for viewing small text files quickly.
- Use with `>` or `>>` for redirection.

`zcat`
- Like `cat`, but for compressed files (`.gz`).
- It shows the content of a gzipped file without unzipping it first.
**Example:**
```
zcat log.gz
```
**Notes:**
- Useful for reading compressed logs.
- Works only on `.gz` files.

# 7. `touch`
**What it does:**
- Create a new empty file or update the timestamp of an existing file.
**Syntax:**
```bash
touch <filename>
```
**Examples:**
```touch file.txt                # create an empty file
touch file1.txt file2.txt     # create multiple files
touch -c file.txt             # do not create if it doesn’t exist, just update timestamp
```
**Notes:**
- Useful for quickly creating empty files.
- Also used in scripting to update the “last modified” time of a file.

# 8. `head`
**What it does:**
- View the first few lines of a file.
**Syntax:**
```head <file>
head -n 20 <file>    # show first 20 lines
```
**Examples:**
```
head file.txt
head -n 5 file.txt   # first 5 lines
```
**Notes:**
- Default shows first 10 lines if `-n` is not specified.
- Handy to quickly check the start of logs or large files.

# 9. `tail` and `tail -f`
**What it does:**
- View the last few lines of a file.
**Syntax:**
```tail <file>
tail -n 20 <file>    # last 20 lines
```
**Example:**
```
tail file.txt
```
`tail -f`
- Follow a file in real-time, useful for live logs.
```
tail -f /var/log/syslog
```
**Notes:**
- `tail -f` is commonly used for monitoring log files as new lines are added.
- Exit with `Ctrl + C`.

# 1️0. `less` and `more`

**What it does:**
- View file contents page by page, especially useful for large files.
`more`
- Simple pager. Shows file content one screen at a time.
```
more file.txt
```
**Navigation:**
- Space → next page
- Enter → next line
- `q` → quit
`less`
- More advanced than `more.` Allows scrolling up and down, searching, and better navigation.
```
less file.txt
```
**Navigation:**
- Up/Down arrows → scroll
- `G` → go to end
- `g` → go to start
- `/keyword` → search
- `q` → quit
**Notes:**
- `less` is generally preferred over `more` for logs or big files.
- Works for text and command output piped via `|` (e.g., `cat file.txt | less`).

# 11. `cp`
**What it does:** 
- Copy files or directories.
**Syntax:**
```
cp <source> <destination>
```
**Examples:**
```
cp file1.txt file2.txt          # copy file1.txt to file2.txt
cp file.txt /home/user/Documents/  # copy file to another folder
cp -r folder1 folder2           # copy folder recursively
```
**Notes:**
- `-r` is required to copy directories.
- Can overwrite files if destination exists (use `-i` to ask before overwrite).

# 12. `mv`
**What it does:**
- Move or rename files/directories.
**Syntax:**
```
mv <source> <destination>
```
**Examples:**
```
mv file.txt /home/user/Documents/   # move file to folder
mv oldname.txt newname.txt          # rename file
mv folder1 folder2                  # rename or move folder
```
**Notes:**
- `mv` is safer than `cp + rm` for moving files.
- Overwrites destination file if exists (use `-i` to confirm).


