# Here is the list of commands related to file and direactory management: 
1. ls 
2. cd 
3. pwd
4. mkdir
5. rm, rmdir
6. cat, zcat
7. touch
8. head
9. tail, tail -f
10. less, more
11. cp
12. mv
13. wc
14. vi editor
15. ln (hard link, soft link)
16. cut
17. tee
18. sort
19. clear
20. diff

# 1. `ls`
**What it does:**
- Lists the contents of the current directory (files, folders, links, etc.).
---
### Common Options
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
**Usage:**
```
cd <path>
```
Examples:
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
Example:
```
pwd
# Output: /home/user/Documents
```
**Notes:**
- Useful to check “Where am I?” in the filesystem.
- Especially handy before running commands that depend on your location.

# 4. `mkdir`
**Meaning:** “Make Directory.”  
**Use:** Create a new folder.
### Syntax
```bash
mkdir <directory_name>
```
Examples:
```
mkdir test           # create a folder named test
mkdir -p a/b/c       # create parent dirs if they don’t exist
```
**Notes:**
- `p` lets you create nested folders in one go.
- If the folder already exists, `mkdir` throws an error unless `-p` is used.

# 5. `rm` and `rmdir`
`rm` – **Remove files or directories**
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
`cat` **(Concatenate)**
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
