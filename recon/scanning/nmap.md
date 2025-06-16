# Scanning using nmap

- `nmap -A -F -T1 [IP Address] -v`

    - -A : aggressive scan
    - -F : scans first 100 ports
    - -T1 : slows down the scan (T3 is default)
    - -v : increases verbosity

## States

- open : port is open and accepting connections
- closed : port is closed but responding to probes
- filtered : port is not responding to probes (firewall or filter in place)

## Scan Phases

### Script Pre-scan

- Nmap Scripting Engine uses a collection of scripts to gain more info. about remote systems.
- We have to request a pre-scan usiing --script or -sC option.
- Pre-scan only happens if the we use scripts that runs only once per scan.

### Target Enumeration

- Nmap researches host specifiers.
- -sL -n option lists the scans without scanning the target.

### Host Discovery

- Network scans usually start with host discovery to find live hosts.
- Techniques include ARP ping, ICMP echo request, TCP SYN, and TCP ACK.
- We can use -Pn option to skip host discovery.
- To quit after host discovery, use -sn option.

### Reverse DNS Resolution

- After host discovery, Nmap performs reverse DNS resolution to find hostnames.
- This can be skipped using -n option.
- Flag -R can be used to force reverse DNS resolution.

### Port Scanning

- Nmap core operation
- You can specify the ports to scan using -p option.

### Version Detection

- Determines the version of services running on open ports.
- Use -sV option to enable version detection.

### OS Detection

- Determines the operating system of the target host.
- Use -O option to enable OS detection.

### Traceroute

- Enabled by --traceroute option.
- Find network routes to many hosts in parallel.

### Script Scanning

### Output

## Agressive Scan

- `nmap -A -p- [IP Address]`

    - -p- : scans all ports (1-65535)
    - -A : aggressive scan (OS detection, version detection, script scanning, and traceroute)

## Super Stealth scan

- ```bash
nmap -sS -sV -O --script=safe -f --data-length 30 --ttl 64 -T1 --max-retries 1 --max-rate 20 -Pn -oA vdp_ultraquiet_scan target.com
```
    - -sS : TCP SYN scan (stealth scan)
    - -sV : service version detection
    - -O : OS detection
    - --script=safe : run only safe scripts
    - -f : fragment packets to evade detection
    - --data-length 30 : add 30 bytes of random data to each packet
    - --ttl 64 : set Time to Live (TTL) value to 64
    - -T1 : slow scan (stealthy)
    - --max-retries 1 : set maximum retries to 1
    - --max-rate 20 : limit the scan rate to 20 packets per second
    - -Pn : treat all hosts as online (skip host discovery)
    - -oA vdp_ultraquiet_scan : output in all formats (XML, grepable, and normal) to the specified file name
    - target.com : target domain or IP address

