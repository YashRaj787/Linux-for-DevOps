## ## Linux Networking Commands   
These are the Linux Networking Commands commonly used in DevOps.
| #  | Command             | #  | Command       |
|----|---------------------|----|---------------|
| 1  | ping                | 13 | dig           |
| 2  | netstat             | 14 | nc (netcat)   |
| 3  | ifconfig            | 15 | whois         |
| 4  | traceroute / tracepath | 16 | ifplugstatus |
| 5  | mtr                 | 17 | route         |
| 6  | nslookup            | 18 | nmap          |
| 7  | telnet              | 19 | wget          |
| 8  | hostname            | 20 | watch         |
| 9  | ip                  | 21 | iptables      |
| 10 | iwconfig            | 22 | traceroute    |
| 11 | ss                  | 23 | curl vs wget  |
| 12 | arp                 |    |               |

## 1. `ping`
**What it does:**
- Checks connectivity between your system and another host by sending ICMP echo requests.

**Syntax:**
```
ping [options] host
```
**Examples:**
```
ping google.com        # test connection to google
ping -c 5 8.8.8.8      # send only 5 packets to IP
```
**Notes:**
- Useful for testing if a host is reachable and measuring latency (time in ms).
- `Ctrl + C` stops continuous pings and shows a summary.
- Some systems need `sudo` for ping (due to raw socket permissions).

## 2. `netstat`
**What it does:**
- Displays network connections, routing tables, interface statistics, and listening ports.

**Syntax:**
```
netstat [options]
```
**Examples:**
```
netstat -tuln        # show listening TCP/UDP ports (numeric)
netstat -anp         # show all connections with PID/program
netstat -rn          # show routing table
```
**Notes:**
- Deprecated on many systems → replaced by `ss`.
- Requires `sudo` for some info (like processes).

## 3. `ifconfig`
**What it does:**
- Displays or configures network interface settings.

**Syntax:**
```
ifconfig [interface] [options]
```
**Examples:**
```
ifconfig              # view all network interfaces
ifconfig eth0         # details of eth0 interface
sudo ifconfig eth0 down    # disable interface
sudo ifconfig eth0 up      # enable interface
```
**Notes:**
- Legacy tool; modern alternative is `ip` (e.g., `ip addr`, `ip link`).
- Still widely available on older systems.

## 4. `traceroute` vs `tracepath`
`traceroute`

**What it does:**
- Shows the route packets take from your system to a destination, listing every hop (router) along the way.

**Syntax:**
```
traceroute [host/IP]
```
**Example:**
```
traceroute google.com
```
**Notes:**
- Requires installation on some systems (`sudo apt install traceroute`).
- Uses UDP or ICMP packets.
- Good for diagnosing where latency or packet loss occurs.

`tracepath`

**What it does:**
- Similar to `traceroute`, but:
   - Usually installed by default on Linux.
   - Runs without root privileges.
   - Simpler output.

**Syntax:**
```
tracepath [host/IP]
```
**Example:**
```
tracepath google.com
```
**Notes:**
- Great for quick route checks.
- If you need more control/options, use `traceroute`.

## 5. `mtr` — My Traceroute
**What it does:**
- Combines `ping` and `traceroute` into an interactive tool that shows live stats (latency, packet loss) for every hop.

**Syntax:**
```
mtr [options] host
```
**Examples:**
```
mtr google.com        # run in interactive mode
mtr -r -c 10 google.com   # run 10 cycles and output report
```
**Notes:**
- Provides real-time view of where network issues occur.
- May need installation (`sudo apt install mtr`).

## 6. `nslookup`
**What it does:**
- Queries DNS servers to find IP addresses of domains (or vice versa).

**Syntax:**
```
nslookup [domain] [server]
```
**Examples:**
```
nslookup google.com        # get IP for google.com
nslookup 8.8.8.8           # reverse lookup (IP → domain)
nslookup example.com 8.8.8.8   # use specific DNS server
```
**Notes:**
- Good for testing DNS resolution.
- For scripting, `dig` is often preferred (more modern).

## 7. `telnet`
**What it does:**
- Connects to a remote host on a specified port using the Telnet protocol (plain text).

**Syntax:**
```
telnet [host] [port]
```
**Example:**
```
telnet mail.example.com 25     # test SMTP service on port 25
```
**Notes:**
- Used for testing if a TCP port is open/reachable.
- Not secure (no encryption) → avoid for sensitive work.
- Often replaced by `ssh`, `nc (netcat)`, or `curl`.

## 8. `hostname`
**What it does:**
- Displays or sets the system’s hostname.

**Syntax:**
```
hostname            # show current hostname
sudo hostname newname   # temporarily change hostname
```
**Notes:**
- To make changes permanent, edit `/etc/hostname` & `/etc/hosts`.
- Useful for identifying a machine on a network.

## 9. `ip`
**What it does:**
- Modern tool for managing and displaying IP addresses, routes, and interfaces (replaces `ifconfig`).
**Common forms:**
```
ip a              # show all interfaces & IPs
ip link show      # list network interfaces
ip addr add 192.168.1.10/24 dev eth0   # add IP to interface
ip route show     # display routing table
```
**Notes:**
- Preferred over `ifconfig` (more features, actively maintained).
- Works with IPv4 & IPv6.

## 10. `iwconfig`
**What it does:**
- Shows or configures wireless network interfaces.
**Syntax:**
```
iwconfig                 # view wireless info
sudo iwconfig wlan0 essid "MyWiFi" key s:password
```
**Notes:**
- For managing Wi-Fi (signal strength, ESSID, frequency, etc.).
- Comes from the `wireless-tools` package.
- For newer systems, `iw` or NetworkManager tools are preferred.

## 11. `ss` — Socket Statistics
**What it does:**
- Displays detailed info about network sockets (connections, ports, listening services).
- It’s a modern replacement for `netstat` (faster and more features).
**Common usage:**
```
ss               # show all sockets
ss -t            # show TCP connections
ss -u            # show UDP connections
ss -ltn          # list listening TCP ports (numeric)
ss -s            # summary of socket stats
```
**Notes:**
- Preferred over `netstat` for performance.
- Great for debugging open ports or active connections.

## 12. `arp` — Address Resolution Protocol
**What it does:**
- Shows and manipulates the ARP table (maps IP → MAC addresses on the local network).

**Example:**
```
arp -a            # list current ARP cache
sudo arp -d 192.168.1.5   # delete entry
sudo arp -s 192.168.1.5 00:1C:42:2B:60:4A   # add static entry
```
**Notes:**
- Useful for diagnosing LAN connectivity issues.
- On modern Linux, `ip neigh` is often used instead.

## 13. `dig` — Domain Information Groper
**What it does:**
- Performs DNS lookups (query DNS servers for records).

**Syntax:**
```
dig [domain] [record-type]
```
**Examples:**
```
dig example.com             # default A record
dig example.com MX          # mail servers
dig @8.8.8.8 example.com    # use specific DNS server
dig +trace example.com      # full DNS resolution path
```
**Notes:**
- More advanced than `nslookup` (better formatting and options).
- Good for troubleshooting DNS records and propagation.

## 14. `nc` — Netcat
**What it does:**
- A powerful utility for reading/writing data across network connections using TCP or UDP.
Often called the Swiss Army knife of networking.
**Common usage:**
```
nc host port                 # connect to host:port
nc -l -p 1234                # listen on port 1234
echo "hello" | nc host 80    # send data to port 80
nc -zv host 1-100            # scan ports 1–100
```
**Notes:**
- Can test connectivity, send files, create simple chat servers, or scan open ports.
- Variants: `ncat` (Nmap) or `socat` (advanced).

## 15. `whois`
**What it does:**
- Looks up domain registration details (owner info, registrar, creation/expiry date).

**Syntax:**
```
whois domain-name
```
**Example:**
```
whois google.com
```
**Notes:**
- Useful for checking domain availability or registration data.
- Output depends on the registry and may hide some details (GDPR privacy).

## 16. `ifplugstatus`
**What it does:**
- Shows whether a network interface has a cable plugged in (link detected or not).

**Syntax:**
```
ifplugstatus
```
**Notes:**
- Handy for troubleshooting wired connections (Ethernet).
- Part of `ifplugd` package (may need install).
- For Wi-Fi, use `iwconfig` or `nmcli`.

## 17. `route`
**What it does:**
- Displays or modifies the kernel’s IP routing table (how packets choose their path).

**Syntax:**
```
route -n          # show routing table (numeric)
sudo route add default gw 192.168.1.1
sudo route del default gw 192.168.1.1
```
**Notes:**
- Mostly replaced by `ip route show` / `ip route add`.
- Still useful on older systems or scripts.

## 18. `nmap` — Network Mapper
**What it does:**
- Scans hosts and networks to discover open ports, services, and OS info.

**Syntax / examples:**
```
nmap 192.168.1.1              # basic host scan  
nmap -sV example.com          # detect service versions  
nmap -p 20-100 host           # scan port range  
nmap -A host                  # aggressive scan (OS + scripts)
```
**Notes:**
- Powerful security & troubleshooting tool.
- Needs installation (`sudo apt install nmap`).
- Use responsibly (scanning other people’s networks without permission may be illegal).

## 19. `wget`
**What it does:**
- Downloads files from the web via HTTP, HTTPS, or FTP.

**Syntax / examples:**
```
wget http://example.com/file.zip
wget -c http://example.com/file.zip       # resume download
wget -r http://example.com/dir/           # recursive download
```
**Notes:**
- Great for scripting bulk downloads.
- Works even on slow or unstable connections (resumes).

## 20. `watch`
**What it does:**
- Runs a command repeatedly at fixed intervals and shows output in real time.

**Syntax / examples:**
```
watch ls -l                     # refresh file list
watch -n 2 free -h              # run every 2 seconds
watch -d netstat -tuln          # highlight differences
```
**Notes:**
- Perfect for monitoring changes (CPU, memory, logs, etc.).
- Default interval is 2 s (`-n` changes it).

## 21. `iptables`
**What it does:**
- Manages firewall rules in Linux (packet filtering, NAT).

**Syntax / examples:**
```
sudo iptables -L               # list rules
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT   # allow SSH
sudo iptables -A INPUT -j DROP # block all others
```
**Notes:**
- Requires root.
- For modern systems, `nftables` or `firewalld` is replacing it.
- Always back up rules before big changes.

## 22. `traceroute` (recap)
**What it does:**
- Shows every hop packets take to a destination.
*Example:**
```
traceroute google.com
```
**Notes:**
- Use `tracepath` if you don’t have root / want simpler output.

## 23. `curl` vs `wget`
| Tool   | What it does                                                                             | When to use                                                     |
| ------ | ---------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| `curl` | Transfers data from/to a server, supports many protocols (HTTP, HTTPS, FTP, SFTP, etc.). | For APIs, POST/PUT requests, testing endpoints, custom headers. |
| `wget` | Downloads files or whole sites (HTTP/HTTPS/FTP).                                         | For downloading large or recursive files reliably.              |

**Examples:**
```
curl https://api.github.com/users/octocat        # fetch API JSON
curl -O https://example.com/file.zip             # save file
wget https://example.com/file.zip                # simple download
```

**Notes:**
- `curl` is more versatile for scripting and APIs.
- `wget` shines for unattended, robust file downloads.
