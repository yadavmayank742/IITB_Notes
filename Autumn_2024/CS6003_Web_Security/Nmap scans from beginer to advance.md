> **Note:** This doc is prepared for `Nmap 7.94SVN` (*latest version as of August 2024*).

**Basic Command :** `nmap [Scan Type(s)] [Options] {target specification}`

Example: 
	
1. `nmap -v -A scanme.nmap.org` : **Verbos** (provides detailed and extensive output or information) and **Aggressive** scan of target *scanme.nmap.org*. 
	
2. `nmap -v -sn 192.168.0.0/16 10.0.0.0/8` : **Verbos** **Ping Scan** (used to be `-sP` in older `nmap` versions, called ***Ping Sweep***, it means, do not scan the ports, just check if a host is alive or not) of *subnet 192.168.0.0/16* and *subnet 10.0.0.0/8* .
	
3. `nmap -v -iR 10000 -Pn -p 80` : **Verbos** scan **port 80** of **10000 Randomly generated IP Addresses** **without checking if the host is alive or not**
`
## Scan Type(s):

### HOST DISCOVERY:

```

  -sL: List Scan - simply list targets to scan
  -sn: Ping Scan - disable port scan
  -Pn: Treat all hosts as online -- skip host discovery
  -PS/PA/PU/PY[portlist]: TCP SYN/ACK, UDP or SCTP discovery to given ports
  -PE/PP/PM: ICMP echo, timestamp, and netmask request discovery probes
  -PO[protocol list]: IP Protocol Ping
  -n/-R: Never do DNS resolution/Always resolve [default: sometimes]
  --dns-servers <serv1[,serv2],...>: Specify custom DNS servers
  --system-dns: Use OS's DNS resolver
  --traceroute: Trace hop path to each host
```
### SCAN TECHNIQUES:
```
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sN/sF/sX: TCP Null, FIN, and Xmas scans
  --scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
```

### PORT SPECIFICATIONS AND SCAN ORDER:
```
  -p <port ranges>: Only scan specified ports
    Ex: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
  --exclude-ports <port ranges>: Exclude the specified ports from scanning
  -F: Fast mode - Scan fewer ports than the default scan
  -r: Scan ports sequentially - don't randomize
  --top-ports <number>: Scan <number> most common ports
  --port-ratio <ratio>: Scan ports more common than <ratio>
```

### SERVICE/VERSION DETECTION:
```
  -sV: Probe open ports to determine service/version info
  --version-intensity <level>: Set from 0 (light) to 9 (try all probes)
  --version-light: Limit to most likely probes (intensity 2)
  --version-all: Try every single probe (intensity 9)
  --version-trace: Show detailed version scan activity (for debugging)
```

### SCRIPT SCANS:
```
  -sC: equivalent to --script=default
  --script=<Lua scripts>: <Lua scripts> is a comma separated list of
           directories, script-files or script-categories
  --script-args=<n1=v1,[n2=v2,...]>: provide arguments to scripts
  --script-args-file=filename: provide NSE script args in a file
  --script-trace: Show all data sent and received
  --script-updatedb: Update the script database.
  --script-help=<Lua scripts>: Show help about scripts.
           <Lua scripts> is a comma-separated list of script-files or
           script-categories.
```

### OS DETECTION:
```
  -O: Enable OS detection
  --osscan-limit: Limit OS detection to promising targets
  --osscan-guess: Guess OS more aggressively
```



## Target Specification(s) :
You are not restricted to just provide the IP Address of a target to be scanned, there're variety of options available to specify the target(**s**) i.e. Can pass ***hostnames***, ***IP addresses***, ***networks***, etc.:
```
  -iL <inputfilename>: Input from list of hosts/networks
  -iR <num hosts>: Choose random targets
  --exclude <host1[,host2][,host3],...>: Exclude hosts/networks
  --excludefile <exclude_file>: Exclude list from file
```


## Saving the `nmap` output :
based on your workflow you may need to scan results to be formatted specifically in certain industry standards, they can be specified using the switches:
```
  -oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3,
     and Grepable format, respectively, to the given filename.
  -oA <basename>: Output in the three major formats at once
  -v: Increase verbosity level (use -vv or more for greater effect)
  -d: Increase debugging level (use -dd or more for greater effect)
  --reason: Display the reason a port is in a particular state
  --open: Only show open (or possibly open) ports
  --packet-trace: Show all packets sent and received
  --iflist: Print host interfaces and routes (for debugging)
  --append-output: Append to rather than clobber specified output files
  --resume <filename>: Resume an aborted scan
  --noninteractive: Disable runtime interactions via keyboard
  --stylesheet <path/URL>: XSL stylesheet to transform XML output to HTML
  --webxml: Reference stylesheet from Nmap.Org for more portable XML
  --no-stylesheet: Prevent associating of XSL stylesheet w/XML output
```


## Other Options:
### TIMING AND PERFORMANCE:
Options which take `<time>` are in seconds, or append 'ms' (milliseconds), 's' (seconds), 'm' (minutes), or 'h' (hours) to the value (e.g. 30m).
  
```
  -T<0-5>: Set timing template (higher is faster)
  --min-hostgroup/max-hostgroup <size>: Parallel host scan group sizes
  --min-parallelism/max-parallelism <numprobes>: Probe parallelization
  --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>: Specifies
      probe round trip time.
  --max-retries <tries>: Caps number of port scan probe retransmissions.
  --host-timeout <time>: Give up on target after this long
  --scan-delay/--max-scan-delay <time>: Adjust delay between probes
  --min-rate <number>: Send packets no slower than <number> per second
  --max-rate <number>: Send packets no faster than <number> per second
```
### FIREWALL/IDS EVASION AND SPOOFING:
```
  -f; --mtu <val>: fragment packets (optionally w/given MTU)
  -D <decoy1,decoy2[,ME],...>: Cloak a scan with decoys
  -S <IP_Address>: Spoof source address
  -e <iface>: Use specified interface
  -g/--source-port <portnum>: Use given port number
  --proxies <url1,[url2],...>: Relay connections through HTTP/SOCKS4 proxies
  --data <hex string>: Append a custom payload to sent packets
  --data-string <string>: Append a custom ASCII string to sent packets
  --data-length <num>: Append random data to sent packets
  --ip-options <options>: Send packets with specified ip options
  --ttl <val>: Set IP time-to-live field
  --spoof-mac <mac address/prefix/vendor name>: Spoof your MAC address
  --badsum: Send packets with a bogus TCP/UDP/SCTP checksum
```


## Miscellaneous Options:
```
  -6: Enable IPv6 scanning
  -A: Enable OS detection, version detection, script scanning, and traceroute
  --datadir <dirname>: Specify custom Nmap data file location
  --send-eth/--send-ip: Send using raw ethernet frames or IP packets
  --privileged: Assume that the user is fully privileged
  --unprivileged: Assume the user lacks raw socket privileges
  -V: Print version number
  -h: Print this help summary page.
```
# Beginner Labs :

## Warm-up:
1. Check your `nmap` version
2. update using `sudo apt install nmap -y` (*NOTE: command specific to Debian*.)
3. Open the help menu of `nmap`
4. Which `nmap` scan is based on *[TCP Split Handshake](https://nmap.org/misc/split-handshake.pdf)* ?
5. How many ports are scanned by 
	1. default ?
	2. `-F` option ?
6. what is the switch (or flag) to scan all ports on a target?

## Challenge 1:
Scan your local machine and report 
1. **How many** ports are open?
2. What are the **services** running on those ports?
3. What is the default **scan type** ? *Hint: it's not XMAS Scan*.

## Challenge 2:
Scan `scanme.nmap.org` and report 
1. **How many** ports are open?
2. What are the **services** running on those ports?
3. What are **versions** of those services?
4. What is the **most probable OS** running the target ? *Think: why are root privileges required in this scan?*
5. Perform the following scans with `-T` options and observer the time it takes to report the results:
	1. TCP SYN scan
	2. TCP Connect scan
	3. UDP scan
	4. XMAS scan

# Intermediate Labs:
Target : `scanme.nmap.org`, 

*save all the scan results in Grepable and XML Format*
## Challenge 1:
> NSE
1. Scan using default NSE Scripts
2. Scan with wildcard script
## Challenge 2:
> Custom TCP Flags

Target:`scanme.nmap.org`
1. Which protocol(s) is/are supported by the target ?
2. Scan by resetting all the TCP Flags. *Hint: `--scanflags`*
3. Scan by setting all the TCP Flags. *Hint: `--scanflags`*
4. Scan only by setting `SYN` and `ACK` TCP Flags. *Hint: `--scanflags`*
5. How many flags are set in TCP Window Scan ?

## Challenge 3:
> MAC Spoofing

## Challenge 4:
> Fragmented Packets


# Advanced Labs:
> Zombie Scan

> Spoofed IP

> Firewall detection

> Firewall Evasion


# References :
1. [Cheat Sheet](https://hackertarget.com/nmap-cheatsheet-a-quick-reference-guide/).
2. 