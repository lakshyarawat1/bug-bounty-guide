# Google Dorking

## Introduction

- Google Dorking is a technique used by hackers to find sensitive information on websites that are not easily available through simple searches.
- Google Dorking is also known as Google Hacking.

## Usage

- Using any keywork in "" will search for the exact phrase.
    - Any keyword inside " " will have to be there in the search results.

- site: 
    - Using this operator, the results are searched from only the site/website mentioned.
    - For example,
        - repository site:github.com
        - This will result in all the searches of repository keywork in the github.com website.

- [#]...[#] OR numrange : 
    - These operators searchers for the results in between that number range specified.
    - For example :
        - iPhone $[2000]...[4000]
        - The results will show all the iphone with prices between these two numbers.

- date : 
    - Searches for the results only within/after the specified months.
    - For example:
        - Cricket match date:3
        - This will show all the cricket matches newer than 3 months old.

- safesearch : 
    - Excludes all adult sites from the search

- link : 
    - Shows all the pages linked to the specified website.
    - For example :
        - link:www.github.com
        - This will result in all the websites or resources that are linked to github.com

- info : 
    - Shows the information about the specified website.
    
- related :
    - Shows all the pages related to the specified website.

- intitle :
    - Shows all the pages with a specified string in the title of the webpage
    
- inurl :
    - Searches for string in the url of the website

- filetype or ext:
    - Searches for files with the exact specified extension
    - For example :
        - react ext:pdf
        - This will result in showing only the pdf files for the search

- cache :
    - Displays the google cache for the specified web page.

- phonebook: OR rphonebook OR bphonebook : 
    - Displays all residential, business phone listing.

- author :
    - Searches for the author of a newsgroup

- define :
    - Only shows the definition of the specified keyword

- 