# File & Directory Management Commands:
| No. | Command(s)            | No. | Command(s)             |
|-----|-----------------------|-----|------------------------|
| 1   | `ls`                  | 11  | `cp`                  |
| 2   | `cd`                  | 12  | `mv`                  |
| 3   | `pwd`                 | 13  | `wc`                  |
| 4   | `mkdir`               | 14  | `vi` editor           |
| 5   | `rm`, `rmdir`         | 15  | `ln` (hard / soft link) |
| 6   | `cat`, `zcat`         | 16  | `cut`                 |
| 7   | `touch`               | 17  | `tee`                 |
| 8   | `head`                | 18  | `sort`                |
| 9   | `tail`, `tail -f`     | 19  | `clear`               |
| 10  | `less`, `more`        | 20  | `diff`                |


## 1. `ls`
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

## 2. `cd`
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

## 3. `pwd`
**What it does:**
- Prints the full (absolute) path of the current working directory.
**Example:**
```
pwd
# Output: /home/user/Documents
```
**Notes:**
- Very Useful to check “Where am I?” in the filesystem.
- Especially handy before running commands that depend on your location.

## 4. `mkdir`
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

## 5. `rm` and `rmdir`
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

## 6️. `cat` **and** `zcat`
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

## 7. `touch`
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

## 8. `head`
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

## 9. `tail` and `tail -f`
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

## 1️0. `less` and `more`
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

## 11. `cp`
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

## 12. `mv`
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

## 13. `wc` — Word Count
**What it does:**
- Counts lines, words, characters, and bytes in a file or from standard input.
```
Syntax:
wc [options] <file>
```
**Examples:**
```
wc file.txt             # shows lines, words, bytes
wc -l file.txt          # count only lines
wc -w file.txt          # count only words
wc -c file.txt          # count only bytes/characters
```
**Notes:**
- Output (by default): lines words bytes
- Combine options (e.g., wc -lw file.txt).

## 14. `vi` Editor (also known as vim in modern systems)
**What it does:**
- A powerful text editor available on almost all Unix/Linux systems.
**Syntax:**
```
vi filename
```
**Modes in `vi`:**
- Command mode (default): navigate, delete, copy, paste, etc.
- Insert mode: for typing text.
- Last-line mode: for saving, quitting, etc.

**Essential keys:**
| Action              | Key           |
| ------------------- | ------------- |
| Enter insert mode   | `i`           |
| Save changes        | `:w`          |
| Quit                | `:q`          |
| Save & quit         | `:wq` or `ZZ` |
| Quit without saving | `:q!`         |
| Delete line         | `dd`          |
| Copy line           | `yy`          |
| Paste line          | `p`           |

**Notes:**
- `vi` is always available, even on minimal servers.
- `vim` (Vi IMproved) adds colors, undo history, etc.

## 15. `ln` — Create Links
**Links** = alternative names/paths to a file.
**Hard Link**
- Another name for the same physical data on disk.
- File & hard link share the same inode.
- If original is deleted, data is still accessible via hard link.
**Syntax:**
```
ln source_file hardlink_name
```
**Example:**
```
ln file.txt file_hardlink
```
**Soft Link (Symbolic Link)**
- Like a shortcut/alias pointing to the original file.
- If the original is deleted, the symlink becomes broken.
**Syntax:**
```
ln -s source_file symlink_name
```
**Example:**
```
ln -s /home/user/file.txt link_to_file
```
**Notes:**
| Type      | Points to    | Survives if original is deleted? | Works across filesystems? |
| --------- | ------------ | -------------------------------- | ------------------------- |
| Hard link | Data (inode) | ✅ Yes                            | ❌ No                      |
| Soft link | File path    | ❌ No                             | ✅ Yes                     |

## 16. `cut`
**What it does:** 
- Extract (cut out) specific sections from each line of a file or output.
**Syntax:**
```
cut [options] <file>
```
**Common options:**
| Option | Meaning                                |
|--------|----------------------------------------|
| `-f`   | Specify field numbers (use with `-d`)  |
| `-d`   | Set delimiter (default is TAB)         |
| `-c`   | Cut by character positions             |

**Examples:**
```
cut -c1-5 file.txt            # first 5 characters of each line  
cut -d',' -f2 file.csv        # 2nd field from comma-separated file  
cut -d':' -f1 /etc/passwd     # usernames from passwd file
```
**Notes:**
- Works line by line.
- Perfect for structured text (CSV, colon-separated configs, logs).

## 17. `tee`
**What id does:** 
- Read from standard input, write to both a file and the screen at the same time.
**Syntax:**
```
command | tee [options] file
```
**Examples:**
```
ls | tee output.txt             # show & save listing  
echo "hi" | tee -a file.txt     # append instead of overwrite
```
**Options:**
- `-a` → append to file (don’t overwrite).
**Notes:**
- Useful in pipelines to save intermediate or final output while still seeing it.
- 
## 18. `sort`
**What it does:**
- Sort lines of text files.
**Syntax:**
```
sort [options] <file>
```
**Common options:**
| Option | Meaning                       |
| ------ | ----------------------------- |
| `-r`   | Reverse order                 |
| `-n`   | Numeric sort                  |
| `-k`   | Sort by a specific key/column |
| `-u`   | Unique (remove duplicates)    |

**Examples:**
```
sort names.txt                # alphabetic  
sort -r names.txt             # reverse order  
sort -n numbers.txt           # numeric sort  
sort -u names.txt             # unique lines only  
sort -t',' -k2 file.csv       # sort by 2nd column (comma separated)
```
**Notes:**
- Default is lexicographic (dictionary) order.
- Combine `-n` and `-r` for reverse numeric sorting.

## 19. `clear`
**What it does:**
- Clears the terminal screen so you get a clean workspace.
**Syntax:**
```
clear
```
**Notes:**
- It doesn’t delete history or close programs — it only scrolls the screen up.
- Shortcut: `Ctrl + L `works the same in most terminals.

## 20. `diff`
**What it does:**
- Compares two text files line-by-line and shows the differences.
**Syntax:**
```
diff [options] file1 file2
```
**Common options:**
| Option | Meaning                                       |
| ------ | --------------------------------------------- |
| `-u`   | Unified format (shows context around changes) |
| `-c`   | Context format                                |
| `-i`   | Ignore case                                   |
| `-w`   | Ignore whitespace                             |

**Examples:**
```
diff file1.txt file2.txt          # basic comparison  
diff -u old.txt new.txt           # unified diff (popular for patches)  
diff -w file1.txt file2.txt       # ignore spaces
```
**Notes:**
- `diff` outputs instructions to make one file like the other.
- Often used with `patch` to apply changes.
- Great for configuration or code changes.

## [Next Page →](Linux%20Commands/02_Disk-Usage-Commands/Detailed-notes.md)
