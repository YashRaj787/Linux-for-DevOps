# Compression Commands
## These are the File Permission Commands commonly used in DevOps.
1. zip
2. gunzip
3. tar
4. untar

## 1. `zip`
**What it does:**
- Compresses files into a .zip archive.

**Syntax:**
```
zip [options] archive_name files
```
**Examples:**
```
zip myfiles.zip file1.txt file2.txt      # create zip archive with two files
zip -r myfolder.zip foldername           # compress folder recursively
```
**Notes:**
- -r is needed to compress directories.

- `.zip` files are widely supported across OS (Windows, Linux, Mac).

## 2. `gzip`
**What it does:**
- Compresses a single file using .gz format, replacing the original file by default.

**Syntax:**
```
gzip [options] filename
```
**Examples:**
```
gzip file.txt       # compress file.txt → file.txt.gz
gzip -c file.txt > file.txt.gz   # keep original, create compressed copy
```
**Notes:**
- Works on single files, not directories.
- Often used with `tar` for archiving directories.

## 3. `gunzip`
**What it does:**
- Decompresses `.gz` files.

**Syntax:**
```
gunzip [options] filename.gz
```
**Examples:**
```
gunzip file.txt.gz        # decompress to file.txt
```
**Notes:**
- `gzip -d file.txt.gz` works the same.
- Restores the original file.

## 4. `tar`
**What it does:**
- Creates or extracts tar archives. Can combine multiple files/folders into a single archive. Often used with gzip or bzip2.

**Syntax & Examples:**
**Create a tar archive:**
```
tar -cvf archive.tar file1 file2   # c=create, v=verbose, f=file
tar -czvf archive.tar.gz folder    # c=create, z=gzip, v=verbose, f=file
```
**Extract a tar archive:**
```
tar -xvf archive.tar               # x=extract
tar -xzvf archive.tar.gz           # x=extract + gzip
tar -xjvf archive.tar.bz2          # x=extract + bzip2
```
**Notes:**
- Use `-C` option to extract to a different directory.
- `tar` + gzip (`.tar.gz`) is very common in Linux for backups & downloads.

## 5. `untar`
**What it does:**
- Extracts files from a tar archive (`.tar`, `.tar.gz`, `.tar.bz2`).
**Note:**
- There isn’t a separate `untar` command; we use `tar` with `-x` (extract) option.

**Syntax & Examples:**
**Extract a plain tar file:**
```
tar -xvf archive.tar
```
**Extract a gzip-compressed tar file (.tar.gz or .tgz):**
```
tar -xzvf archive.tar.gz
```
**Extract a bzip2-compressed tar file (.tar.bz2):**
```
tar -xjvf archive.tar.bz2
```
**Options:**

- `-x` → extract
- `-v` → verbose (show files being extracted)
- `-f` → specify file
- `-z` → gzip
- `-j` → bzip2
- `-C /path/to/dir` → extract to specific directory
**Notes:**
- Often called “untar” informally, but it’s actually `tar -x`.
- Can be combined with compression (`.tar.gz`or `.tar.bz2`) to extract in one step.
