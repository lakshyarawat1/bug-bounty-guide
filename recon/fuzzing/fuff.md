# Introduction

- Ffuf is a fast web fuzzer written in Go. It is a replacement of dirbuster and dirb.

## What is fuzzing?

- Fuzzing is the method of sending malformed and abnormal data to applications to find bugs and vulnerabilities.
- It helps us to see the behavior of the application when it receives unexpected data.
- Fuzzing is also known as fuzz testing, robustness testing, and negative testing.

## Usage

- `ffuf -w /usr/share/wordlists/dirb/common.txt -u http://tenet.htb/FUZZ -fc 403 -p 2`

    - Explaining the above command:

        - `-w` is used to specify the wordlist.
        - `-u` is used to specify the URL.
        - `-fc` is used to filter out the status code.
        - `-p` is used to delay the request.

- Ffuf is fast enough to be rate-limited by the server. To avoid this, we can use the `-p` flag to delay the request.

- You can use dirb to fuzz slow.
