# File Transfer Commands
## These are the File Transfer Commands commonly used in DevOps.
## 1. `scp` — Secure Copy
**What it does:**
- Copies files or directories securely over SSH between local and remote machines.

**Syntax:**
```
scp [options] source destination
```
**Examples:**
```
# Copy local file to remote server
scp file.txt user@remote:/home/user/

# Copy remote file to local machine
scp user@remote:/home/user/file.txt /local/path/

# Copy entire directory (use -r)
scp -r myfolder user@remote:/home/user/
```
**Notes:**
- Uses SSH for authentication and encryption.
- `-P` lets you specify a custom SSH port (uppercase P).
- Slower than `rsync` for large/changed files because it copies everything.

## 2. `rsync` — Remote Sync
**What it does:**
- Synchronizes files/directories between locations, locally or over SSH. Efficient for incremental backups.

**Syntax:**
```
rsync [options] source destination
```
**Examples:**
```
# Sync a local folder to remote server
rsync -avz myfolder/ user@remote:/home/user/

# Sync remote folder back to local
rsync -avz user@remote:/home/user/myfolder/ /local/path/

# Mirror directory, delete removed files
rsync -avz --delete /src/ /dst/
```
**Options (commonly used):**
| Option       | Meaning                                                     |
| ------------ | ----------------------------------------------------------- |
| `-a`         | Archive mode (preserves permissions, times, symlinks)       |
| `-v`         | Verbose output                                              |
| `-z`         | Compress data during transfer                               |
| `--progress` | Show progress of transfer                                   |
| `--delete`   | Remove files from destination if they don’t exist in source |

**Notes:**
- Only transfers differences → much faster than `scp` for large sets.
- Also works locally (`rsync /src /dst`).
- Great for backups, deployments, or syncing two folders.
