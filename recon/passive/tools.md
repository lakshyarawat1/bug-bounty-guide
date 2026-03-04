# Passive Reconnaisance Tools

## Email Address Enumeration

- Hunter.io

## Subdomains

- crt.sh
- Sublist3r
- amass
- subfinder - Best command `subfinder -d example.com -o subdomains.txt -v -t 100 -all -r 8.8.8.8,8.8.4.4 -s dnsdumpster,crtsh,virustotal,securitytrails,robtex`

## Technology

- BuiltWith
- Wappalyzer
- Whatweb (Kali) - Best command - `whatweb -a 4 --max-threads=12 --no-errors -v --log-verbose=whatweb-full.log --log-xml=whatweb.xml https://target.com`
- cdncheck - tech for each IP

## DNS resolution

- dnsx