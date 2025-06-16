# Amass for Bug Bounty Hunting

## Overview

Amass is a powerful tool used for subdomain enumeration. It's particularly useful in bug bounty hunting as it can help identify potential targets within a given domain.

## Installation

Provide instructions on how to install Amass.

## Usage

Describe how to use Amass for bug bounty hunting. Include common commands and their descriptions.

### Basic Command

```bash
amass enum -d example.com
```

### Good command for bug bounty hunting

```bash
amass enum -passive -d example.com -oA example_com_passive_enum -timeout 30 -max-dns-queries 10
```

### Explanation of Flags

- `-passive`: Use passive mode to avoid detection.
- `-d`: Specify the domain to enumerate subdomains for.
- `-oA`: Output all formats (JSON, CSV, etc.) to a specified file.
- `-timeout`: Set a timeout for DNS queries.
- `-max-dns-queries`: Limit the number of DNS queries to avoid rate limiting.
