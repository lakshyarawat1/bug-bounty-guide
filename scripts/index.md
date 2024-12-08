# Some scripting basics

## Vim Editor

### Introduction

- Open source

- Improved clone of Vi editor.

- Vim offers six fundamental modes that makes our work easier :

  - Normal : All inputs are considered as editor commands. So there is no insertion of entered characters into the editor buffer. Normal mode is default.

  - Insert : With a few exceptions, all entered characters are inserted into the buffer.

  - Visual : It is used to mark a contiguous part of the text, which will be visually highlighted. By positioning the cursor, we change the selected user. The highlighted area can then be edited in various ways, such as deleting, replacing.

  - Command : It allows us to enter single line commands at the bottom of the editor. This is used for sorting, replacing text sections or deleting them.

  - Replace : The newly entered text will override existing text characters unless there as no more old characters.

- We can close vim by first going to command mode using ":" then typing q for exiting the editor.

- Vim offers vimtutor to excel in vim editor.

### Basic Commands

- To enter the vim editor the command is `vim <filename>`

- To enter insert mode press `i`

- To save the file press `:w`

- To save and exit press `:wq`

- To exit without saving press `:q!`

- To move the cursor use `h` for left, `j` for down, `k` for up and `l` for right.

- To delete a character press `x`

### Other commands

- `: set number` : It sets line numbers for the code.

- `: set nonumber` : It removes line numbers from the code.

- `: set autoindent` : It automatically indents the code.

- `: set noautoindent` : It removes autoindent from the code.

- `: set ignorecase` : It ignores the case of the text.

- To save all the options we have to configure the .vimrc file for the vim directory.

- To open this file type `vim ~/.vimrc`

- A good example is :

```vim
" ------------------------------
" Basic Settings
" ------------------------------
set nocompatible             " Disable compatibility with old-time vi
filetype off                 " Required for vim-plug

" ------------------------------
" Vim-Plug Plugin Manager
" ------------------------------
" Specify a directory for plugins
call plug#begin('~/.vim/plugged')

" List of plugins
Plug 'tpope/vim-sensible'    " Sensible default settings for Vim
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }  " Fuzzy file finder
Plug 'junegunn/fzf.vim'      " Fzf integration
Plug 'tpope/vim-fugitive'    " Git commands in Vim
Plug 'airblade/vim-gitgutter' " Git diff in the gutter
Plug 'preservim/nerdtree'    " File system explorer
Plug 'vim-airline/vim-airline' " Status/tabline
Plug 'vim-airline/vim-airline-themes' " Themes for vim-airline
Plug 'scrooloose/nerdcommenter' " Easy commenting
Plug 'sheerun/vim-polyglot'  " Language pack
Plug 'dense-analysis/ale'    " Asynchronous linting
Plug 'dracula/vim', { 'as': 'dracula' } " Dracula theme

call plug#end()

" ------------------------------
" Interface Enhancements
" ------------------------------
syntax on                    " Enable syntax highlighting
set number                   " Show line numbers
set relativenumber           " Show relative line numbers
set showcmd                  " Show (partial) command in status line
set cursorline               " Highlight the current line
set wildmenu                 " Enhanced command line completion
set wildmode=longest:full,full
set lazyredraw               " Don't redraw while executing macros
set showmatch                " Show matching brackets
set scrolloff=8              " Minimum lines to keep above and below the cursor
set sidescrolloff=8          " Minimum columns to keep to the left and right of the cursor
set termguicolors            " Enable true color support

" ------------------------------
" File Handling
" ------------------------------
set encoding=utf-8           " Set encoding to UTF-8
set fileencoding=utf-8       " File encoding to UTF-8
set autoread                 " Automatically reload files changed outside of Vim
set hidden                   " Allow changing buffers without saving
set backup                   " Keep a backup file
set writebackup              " Keep a backup before overwriting a file
set undodir=~/.vim/undodir   " Directory for undo files
set undofile                 " Enable persistent undo
set swapfile                 " Enable swap file
set backupdir=~/.vim/backup// " Directory for backup files

" ------------------------------
" Search Settings
" ------------------------------
set incsearch                " Incremental search
set hlsearch                 " Highlight search results
set ignorecase               " Ignore case in search
set smartcase                " Case-sensitive if search contains uppercase

" ------------------------------
" Indentation Settings
" ------------------------------
set tabstop=4                " Number of spaces that a <Tab> in the file counts for
set softtabstop=4            " Number of spaces that a <Tab> counts for while editing
set shiftwidth=4             " Number of spaces to use for each step of (auto)indent
set expandtab                " Use spaces instead of tabs
set autoindent               " Copy indent from current line when starting a new line
set smartindent              " Automatically inserts one extra level of indentation in some cases

" ------------------------------
" Key Mappings
" ------------------------------
nnoremap <C-n> :NERDTreeToggle<CR> " Toggle NERDTree with Ctrl+n
nnoremap <C-p> :Files<CR>          " Trigger FZF with Ctrl+p
vnoremap <C-c> :Commentary<CR>     " Toggle comments in visual mode with Ctrl+c

" ------------------------------
" Airline Configuration
" ------------------------------
let g:airline#extensions#tabline#enabled = 1
let g:airline_theme='dracula'

" ------------------------------
" ALE Configuration
" ------------------------------
let g:ale_linters = {
\   'python': ['flake8'],
\   'javascript': ['eslint'],
\}
let g:ale_fixers = {
\   '*': ['remove_trailing_lines', 'trim_whitespace'],
\   'javascript': ['eslint'],
\}
let g:ale_fix_on_save = 1

" ------------------------------
" Colorscheme
" ------------------------------
colorscheme dracula

" ------------------------------
" Miscellaneous
" ------------------------------
set clipboard=unnamedplus    " Use system clipboard
set mouse=a                  " Enable mouse support in all modes

```

### Visual Mode

- Press v to enter the visual mode

- Use the arrow keys to select the text

- Press d to delete the selected text

- Press y to copy the selected text

- Press p to paste the copied text

- Press c to change the selected text

- Press > to indent the selected text

- Press < to unindent the selected text

- Press U to convert the selected text to uppercase

- Press u to convert the selected text to lowercase

- Press ~ to toggle the case of the selected text

- Press r to replace the selected text with the entered character

- Press : to enter the command mode

## Powershell

### Introduction

- Powershell is a task automation and configuration management framework from Microsoft.

- It is a command line shell and scripting language.

- It is built on the .NET framework.

### Basic Commands

- `$PSVersionTable.PSVersion` : Gives the powershell version installed.

- `ExecutionPolicy Bypass`: This parameter sets the execution policy for the new PowerShell session to Bypass i.e. nothing is blocked.

- Comments can be added using #.

- Use | to pipe multiple commands.

- Variables can be set in CLI using $ symbol.

### Scripting

- `Write-Host` : Used to write the text in console.

- `Read-Host` : Used to read the user input from the console.

  - We can use the -Prompt option to display any question or info before asking for inputs.

- `set-location` : Enter any particular folder or location

- `get-location` : Get the current location

- `get-childitem` : Get the list of files and folders in the current location

- `gal ` : Command is used for searching commandlets of similar name

  - For example : `gal *sm` gives all commands ending from sm

- `Export-csv` : exports the output to a csv file

- `Import-csv` : imports the csv file

- `Get-Process` : Get the list of processes running

- `Get-Service` : Get the list of services running

- `Export-clixml` : Exports the content to xml

- `ConvertTo-csv` : Converts the data to csv but not make a new file.

- `-Confirm` : Parameter asks for conformation before executing the command.

### Arrays

- Arrays in powershell can be declared using @(``) syntax

- We can append the array using += symbol.

### Hashmaps

- Hashmaps can be declared using @{} syntax.

- We can access the hashmap using the key.

- We can use the .Add function to add the elements to the hashmap.

## Bash scripting

### Introduction

- Bash is a Unix shell and command language.

- It is a default shell on most Linux distributions.

### Basics

- `echo` : Used to print the text on the console.

- `read` : Used to read the user input from the console.

- Variables can be declared using the syntax `var_name=value`

- Variables can be accessed using $ symbol.

- We can use the `export` command to make the variable global.

- Quoting :

  - Single quotes : Used to print the text as it is.

  - Double quotes : Used to print the text with variable values.

### Handling named arguments

- We can handle named arguments using the switch case and do case loops.

- One example is,

- ```sh
  deploy=false
  uglify=false

  while (( $# > 1 )); do case $1 in
      --deploy) deploy="$2";;
      --uglify) uglify="$2";;
      *) break;
      esac; shift 2
  done

  $deploy && echo "will deploy... deploy = $deploy"
  $uglify && echo "will uglify... deploy = $uglify"
  ```

### Basic operations

- **Env Shebang** : The first line of the script must include the absolute path to the env executable with the argument bash.

  - Example is : `#!/usr/bin/env bash`

- **Direct Shebang** : the shebang is ignored when the bash command is used in the cli.

- **Navigating directories** : The keyword `cd` can be used to navigate directories. Use $ sign to go to specific directory

  - For example : ```sh
    cd $(dirname "$(readlink -f "$0")")"

    ```
    - Explanation : `readlink -f $0"` determines the path to current script, dirname gives the name of current directory

    ```

  - **Listing Files** : Use the ls to list directories and files.

    - - Regular file
        b - Block special file
        c - Character special file
        C - High performance ("contiguous data") file
        d - Directory
        D - Door (special IPC file in Solaris 2.5+ only)
        l - Symbolic link
        M - Off-line ("migrated") file (Cray DMF)
        n - Network special file (HP-UX)
        p - FIFO (named pipe)
        P - Port (special system file in Solaris 10+ only)
        s - Socket
        ? - Some other file type

  - Listing all recently modified files : `ls -lt | head`

### Cat Keyword

- __Options__ : 

  - __-n__ : Print line numbers
  - __-v__ : Show non printing characters using ^ and M- notation except LFD and TAB
  - __-T__ : Show tabs
  - __-E__ : Show linefeed(LF) characters as $

- Concatenate files : 

  - ` cat file1 file2 > file_all `

- Printing the contents of the file :

  - `cat file.txt`
  - To display the contents of the file in completely unambiguous byte to byte form, a hexdump is the standard solution.

- Write to a file :

  - `cat > file.txt`

  - Use `>>` to append to a file.

- We can read from a special input using <.

### Grep 

- Searching patterns in a file.

  - `grep foo ~/Desktop/bar`

### Aliases

- Using a keyword alias to create and unalias to delete the alias.

### Redirection

- Use the arrow braces to redirect the input and output of a command.

### If statements syntax

- `if [[ $1 -eq ]]; then `

### Looping over an array

- ```sh
    arr=(a b c d)
    for i in "${arr[@]}"; do
      echo "$i"
    done
  ```

