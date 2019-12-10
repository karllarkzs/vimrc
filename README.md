# vimrc


" Load runtime path
set runtimepath^=~/.vim runtimepath+=~/.vim/after runtimepath+=/usr/local/opt/fzf
let &packpath = &runtimepath

" Neovim General settings
syntax on

if has("autocmd")
    filetype plugin indent on
    "           │     │    └──── Enable file type detection.
    "           │     └───────── Enable loading of indent file.
    "           └─────────────── Enable loading of plugin files.
endif

filetype on
" Make Vim more useful
set nocompatible

set tabstop=2                  " ┐
set softtabstop=2              " │ Set global <TAB> settings.
set shiftwidth=2							 " │
set expandtab                  " ┘
set smartindent
set autoindent

set visualbell                 " ┐
set noerrorbells               " │ Disable beeping and window flashing
set t_vb=                      " ┘ https://vim.wikia.com/wiki/Disable_beeping

set smartcase                  " Override `ignorecase` option
                               " if the search pattern contains
                               " uppercase characters.

set report=0                   " Report the number of lines changed.
set ruler                      " Show cursor position<Paste>

set nostartofline              " Kept the cursor on the same column.

set hlsearch                   " Enable search highlighting.
set ignorecase                 " Ignore case in search patterns.

set incsearch                  " Highlight search pattern
                               " as it is being typed.

set listchars=tab:»·             " ┐
set listchars+=trail:·           " │ Use custom symbols to
set listchars+=eol:↴           " │ represent invisible characters.
set listchars+=nbsp:_          " ┘

" disable showmode, since we are using lightline
set noshowmode

" Use the OS clipboard by default (on versions compiled with `+clipboard`)
set clipboard=unnamed

" Enhance command-line completion
set wildmenu

" Allow cursor keys in insert mode
" set esckeys
" Allow backspace in insert mode
set backspace=indent,eol,start

" Optimize for fast terminal connections
set ttyfast

" Optimal terminal color
set termguicolors

" Use <Space> to search
map <space> /

" Add the g flag to search/replace by default
set gdefault

" tabline enable
set hidden

" Use UTF-8 without BOM
set encoding=utf-8 nobomb

" Set wildmode
set wildmode=list:longest,full

" Don’t add empty newlines at the end of files
set binary
set noeol

" Set line numbers
set number

set backupdir=~/.vim/backups   " Set directory for backup files.
set directory=~/.vim/swaps     " Set directory for .swp files.

" Prevent arrow keys on normal mode
noremap <Up> <Nop>
noremap <Down> <Nop>
noremap <Left> <Nop>
noremap <Right> <Nop>

" move up/down consider wrapped lines
nnoremap j gj
nnoremap k gk

nnoremap <C-D> :bnext<CR>
nnoremap <C-S> :bprev<CR>

" End General settings


" ---------------------------------------------------------
let NERDTreeShowHidden=1

" Language specific settings

" Go
let g:go_highlight_functions = 1
let g:go_highlight_methods = 1
let g:go_highlight_structs = 1
let g:go_highlight_interfaces = 1
let g:go_highlight_operators = 1
let g:go_highlight_build_constraints = 1
let g:go_highlight_types = 1
let g:go_highlight_fields = 1
let g:go_highlight_function_calls = 1
let g:go_fmt_command = "goimports"
let g:go_list_type = "quickfix"
let g:go_auto_sameids = 1
let g:go_auto_type_info = 1
let g:go_snippet_engine = "neosnippet"
let g:go_def_mode='gopls'
let g:go_info_mode='gopls'

let g:javascript_plugin_flow = 1

" Rust
let g:rustfmt_autosave = 1


" Ale
let g:ale_linters = {
\   'go': ['gopls', 'golint', 'go vet'],
\}

let g:ale_sign_error = '⤫'
let g:ale_sign_warning = '⚠'

" silver_searcher
let g:ackprg = 'ag --nogroup --nocolor --column'


" End language specific settings


" ----------------------------------------------------------------------
" | Helper Functions                                                   |
" ----------------------------------------------------------------------
function! StripTrailingWhitespaces()

    " Save last search and cursor position.

    let searchHistory = @/
    let cursorLine = line(".")
    let cursorColumn = col(".")

    " - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

    " Strip trailing whitespaces.

    %s/\s\+$//e

    " - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

    " Restore previous search history and cursor position.

    let @/ = searchHistory
    call cursor(cursorLine, cursorColumn)


endfunction

function! ToggleRelativeLineNumbers()

    if ( &relativenumber == 1 )
        set number
    else
        set relativenumber
    endif

endfunction

function! CocCurrentFunction()
    return get(b:, 'coc_current_function', '')
endfunction

" End Helper Functions
" ----------------------------------------------------------------------

" Shortcuts/Map Leader
" - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

