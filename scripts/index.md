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
