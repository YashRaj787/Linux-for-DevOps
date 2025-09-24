# Advanced Linuc commands which mostly used in linux
1. awk
2. sed
3. grep
4. find

## 1. `awk` — Advanced Text Processing
**What it does:**
- Reads text line by line, splits lines into fields (columns), and performs operations.
- Can do filtering, calculations, formatting, and reporting.
**Key Features:**
- `$1, $2…` → represent columns.
- `NR` → current line number.
- `NF` → number of fields in current line.
- `BEGIN` / `END` blocks → run before/after processing input.
**Advanced Examples:**
```
# Print 1st and 3rd columns of /etc/passwd
awk -F: '{print $1, $3}' /etc/passwd

# Sum the values in the 2nd column
awk '{sum+=$2} END {print "Total =", sum}' numbers.txt

# Print lines where 3rd column > 50
awk '$3 > 50 {print $0}' data.txt

# Format output nicely
awk 'BEGIN {print "Name\tScore"} {print $1 "\t" $2}' students.txt
```
**Notes:**
- Extremely powerful for log parsing, CSV/TSV files, reports.
- Often used in combination with `grep` or `sed` for pipelines.

## 2. `sed` — Stream Editor
**What it does:**
- Edits text in-place or streams, applies pattern-based transformations, using regular expressions.
**Key Features:**
- `s/old/new/` → substitution.
- `-i` → edit file directly.
- `-n` → suppress automatic printing.
- Line addressing: `1,5` or `/pattern/`.
**Advanced Examples:**
```
# Replace all "foo" with "bar" in file
sed -i 's/foo/bar/g' file.txt

# Delete lines containing "error"
sed -i '/error/d' logfile.txt

# Print only lines 10-20
sed -n '10,20p' file.txt

# Replace only on lines matching a pattern
sed '/^INFO/s/old/new/' logfile.txt
```
**Notes:**
- Ideal for automated editing, configuration changes, batch replacements.
- Supports complex regex and multi-line patterns.

## 3. `grep` — Pattern Searching
**What it does:**
- Searches for strings or regex patterns in files/output.
- Can highlight matches, filter lines, and combine with other commands.
**Key Features:**
- `-i` → case-insensitive.
- `-v` → invert match (exclude pattern).
- `-r` → recursive.
- `-n` → show line numbers.
- `-E` → extended regex (allow `+`, `?`, `|`).
**Advanced Examples:**
```
# Find "ERROR" in all logs recursively
grep -r "ERROR" /var/log/

# Count occurrences of a word
grep -c "failed" logfile.txt

# Show lines not containing "INFO"
grep -v "INFO" logfile.txt

# Highlight matches
grep --color=auto "pattern" file.txt

# Use regex to match IP addresses
grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' access.log
```
**Notes:**
- Frequently combined in pipes:
```
cat logfile | grep "ERROR" | awk '{print $1,$2}'
```

## 4. `find` — Advanced File Searching
**What it does:**
- Locates files/directories based on name, type, size, permissions, modification time, and can perform actions on them.
**Key Features:**
- `-name`, `-type` → match file or directory names.
- `-mtime`, `-atime` → find by modification/access time.
- `-size` → find by file size.
- `-perm` → find by permissions.
- `-exec` → run command on found files.

**Advanced Examples:**
```
# Find all .log files in /var/log
find /var/log -type f -name "*.log"

# Find directories named "backup"
find /home -type d -name "backup"

# Files modified in last 7 days
find /home/user -mtime -7

# Files larger than 100MB
find / -type f -size +100M

# Execute command on found files (delete all .tmp files)
find /tmp -type f -name "*.tmp" -exec rm -f {} \;

# Find files with specific permissions (e.g., 777)
find / -type f -perm 777
```
**Notes:**
- Combine with xargs for efficiency:
```
find . -name "*.log" | xargs grep "ERROR"
```
- Extremely useful for system maintenance, backups, automation, and security audits.
