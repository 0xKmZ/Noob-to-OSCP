# Nmap Cheat Sheet

```
Basic Scanning Techniques
    • Scan a single target nmap [target]
    • Scan multiple targets nmap [target1,target2,etc]
    • Scan a list of targets nmap -iL [list.txt]
    • Scan a range of hosts nmap [range of IP addresses]
    • Scan an entire subnet nmap [IP address/cdir]
    • Scan random hosts nmap -iR [number]
    • Excluding targets from a scan nmap [targets] –exclude [targets]
    • Excluding targets using a list nmap [targets] –excludefile [list.txt]
    • Perform an aggressive scan nmap -A [target]
    • Scan an IPv6 target nmap -6 [target]
Discovery Options
    • Perform a ping scan only nmap -sP [target]
    • Don’t ping nmap -PN [target]
    • TCP SYN Ping nmap -PS [target]
    • TCP ACK ping nmap -PA [target]
    • UDP ping nmap -PU [target]
    • SCTP Init Ping nmap -PY [target]
    • ICMP echo ping nmap -PE [target]
    • ICMP Timestamp ping nmap -PP [target]
    • ICMP address mask ping nmap -PM [target]
    • IP protocol ping nmap -PO [target]
    • ARP ping nmap -PR [target]
    • Traceroute nmap –traceroute [target]
    • Force reverse DNS resolution nmap -R [target]
    • Disable reverse DNS resolution nmap -n [target]
    • Alternative DNS lookup nmap –system-dns [target]
    • Manually specify DNS servers nmap –dns-servers [servers] [target]
    • Create a host list nmap -sL [targets]
Firewall Evasion Techniques
    • Fragment packets nmap -f [target]
    • Specify a specific MTU nmap –mtu [MTU] [target]
    • Use a decoy nmap -D RND: [number] [target]
    • Idle zombie scan nmap -sI [zombie] [target]
    • Manually specify a source port nmap –source-port [port] [target]
    • Append random data nmap –data-length [size] [target]
    • Randomize target scan order nmap –randomize-hosts [target]
    • Spoof MAC Address nmap –spoof-mac [MAC|0|vendor] [target]
    • Send bad checksums nmap –badsum [target]
Version Detection
    • Operating system detection nmap -O [target]
    • Attempt to guess an unknown nmap -O –osscan-guess [target]
    • Service version detection nmap -sV [target]
    • Troubleshooting version scans nmap -sV –version-trace [target]
    • Perform a RPC scan nmap -sR [target]
Output Options
    • Save output to a text file nmap -oN [scan.txt] [target]
    • Save output to a xml file nmap -oX [scan.xml] [target]
    • Grepable output nmap -oG [scan.txt] [target]
    • Output all supported file types nmap -oA [path/filename] [target]
    • Periodically display statistics nmap –stats-every [time] [target]
    • 133t output nmap -oS [scan.txt] [target]
Ndiff
    • Comparison using Ndiff ndiff [scan1.xml] [scan2.xml]
    • Ndiff verbose mode ndiff -v [scan1.xml] [scan2.xml]
    • XML output mode ndiff –xml [scan1.xm] [scan2.xml]
Nmap Scripting Engine
    • Execute individual scripts nmap –script [script.nse] [target]
    • Execute multiple scripts nmap –script [expression] [target]
    • Execute scripts by category nmap –script [cat] [target]
    • Execute multiple scripts categories nmap –script [cat1,cat2, etc]
    • Troubleshoot scripts nmap –script [script] –script-trace [target]
    • Update the script database nmap –script-updatedb
    • Script categories
    ◦ all
    ◦ auth
    ◦ default
    ◦ discovery
    ◦ external
    ◦ intrusive
    ◦ malware
    ◦ safe
    ◦ vuln

```

---

### Types of Ports States

Open
Filtered (NMAP does not know if open or closed)
Closed

### **MODS**

- sS - TCP SYN scan
- sT - TCP scan
- sU - UDP scan
- sY - SCTP INIT scan
- sN - (TCP NULL/NO FLASG [Empty Packets])
- sX (xmas scan as the flags that it sets (PSH, URG and FIN))
- sF (a request is sent with the FIN flag (usually used to gracefully close an active connection)).

---

To run a ping scan, run the following command:

- nmap -sp 192.100.1.1/24 (This command then returns a list of hosts on your network)

To run a host scan, use the following command:

- nmap -sp <target IP range>

To run a OS scan, use the following command:

- nmap -O <target IP>

Scan The Most Popular Ports:

- nmap --top-ports 20 192.168.1.106

To your command to output the results to a text file:

- oN output.txt

Disable DNS Name Resolution (for large networks):

- nmap -sp -n <IP>/24

MTU Scan (change the byte size packets that sent to the server ,important step for avoiding IDS, must be multiple of 8 [8,16,24,32])

- nmap --mtu 8 <target IP>

Decoy Addresses (for spoofing IP address):

- nmap -D RND:10 [target] (Generates a random number of decoys)
- nmap -D decoy1,decoy2,decoy3 etc. (Manually specify the IP addresses of the decoys)

Source port number specification (A common error that many administrators are doing when configuring firewalls is to set up a rule to allow all incoming traffic that comes from a specific port number.)

- nmap --source-port 53 <target-ip>

Append Random Data (chancing the packet data, again to avoid IDS):

- nmap --data-length 25 <target-ip>

Scan with Random Order (scans the hosts on the server in none order to prevent detection)

- nmap --randomize-hosts <target-ip-range>

---

Firewall Evasion

- Pn: force nmap to check for open ports even if we can't ping the target, because sometimes windows block ICMP protocol by default.
- f :- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
- An alternative to -f, but providing more control over the size of the packets: --mtu <number>, accepts a maximum transmission unit size to use for the packets sent. This must be a multiple of 8.
- -scan-delay <time>ms:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
- -badsum:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.
