# theHarvestor

## Introduction

- theHarvester is a tool for gathering e-mail accounts, subdomain names, virtual hosts, open ports/ banners, and employee names from different public sources (search engines, pgp key servers).
- It is a really simple tool, but very effective for the early stages of a penetration test or just to know the visibility of your company on the Internet.


## Usage 

- All flags are optional, but the minimum you should use is:
  - `-d`: Domain name
  - `-l`: Limit the number of results to work with search engines results (default=500, max=500)
  - `-b`: Data source (google, googleCSE, bing, bingapi, pgp, linkedin, google-profiles, people123, jigsaw, twitter, googleplus, all)
  - `-h`: Use SHODAN database to query discovered hosts for open ports.
  - `-s`: Start in result number X (default=0)
  - `-v`: Verify host name via DNS resolution and search for virtual hosts.
  - `-f`: Save the results into an HTML and XML file format.
  - `-n`: Perform a DNS reverse query on all ranges discovered 

- Note : Wayback tool is also an alternative to it.