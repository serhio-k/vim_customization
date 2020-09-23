# VIM customization

[Original info can be found on linode](https://www.linode.com/docs/tools-reference/tools/introduction-to-vim-customization/)

## Customize the Global vimrc File

Place the following data to `/etc/vimrc` or `/etc/vim/vimrc` file
> **Note!**  
*Prefixing the sudo command is necessary when editing files where read and/or write permissions are not granted to your user account*

```vim
set showcmd› › " Show (partial) command in status line.
set showmatch› › " Show matching brackets.
set ignorecase›› " Do case insensitive matching
set smartcase› › " Do smart case matching
set incsearch› › " Incremental search
set autowrite› › " Automatically save before commands like :next and :make
set hidden›› " Hide buffers when they are abandoned
set mouse=a› › " Enable mouse usage (all modes)
```

Create `~/.vimrc` file for current user

```vim
" Set compatibility to Vim only.
set nocompatible

" Helps force plug-ins to load correctly when it is turned back on below.
filetype off

" Turn on syntax highlighting.
syntax on

" For plug-ins to load correctly.
filetype plugin indent on

" Turn off modelines
set modelines=0

" Automatically wrap text that extends beyond the screen length.
set wrap
" Vim's auto indentation feature does not work properly with text copied from outside of Vim. Press the <F2> key to toggle paste mode on/off.
nnoremap <F2> :set invpaste paste?<CR>
imap <F2> <C-O>:set invpaste paste?<CR>
set pastetoggle=<F2>

" Uncomment below to set the max textwidth. Use a value corresponding to the width of your screen.
" set textwidth=79
set formatoptions=tcqrn1
set tabstop=2
set shiftwidth=2
set softtabstop=2
set expandtab
set noshiftround

" Display 5 lines above/below the cursor when scrolling with a mouse.
set scrolloff=5
" Fixes common backspace problems
set backspace=indent,eol,start

" Speed up scrolling in Vim
set ttyfast

" Status bar
set laststatus=2

" Display options
set showmode
set showcmd

" Highlight matching pairs of brackets. Use the '%' character to jump between them.
set matchpairs+=<:>

" Display different types of white spaces.
set list
set listchars=tab:›\ ,trail:•,extends:#,nbsp:.

" Show line numbers
set number

" Set status line display
set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ [BUFFER=%n]\ %{strftime('%c')}

" Encoding
set encoding=utf-8

" Highlight matching search patterns
set hlsearch
" Enable incremental search
set incsearch
" Include matching uppercase words with lowercase search term
set ignorecase
" Include only uppercase words with uppercase search term
set smartcase

" Store info from no more than 100 files at a time, 9999 lines of text, 100kb of data. Useful for copying large amounts of data between files.
set viminfo='100,<9999,s100

" Map the <Space> key to toggle a selected fold opened/closed.
nnoremap <silent> <Space> @=(foldlevel('.')?'za':"\<Space>")<CR>
vnoremap <Space> zf

" Automatically save and load folds
autocmd BufWinLeave *.* mkview
autocmd BufWinEnter *.* silent loadview"
```

## Install the Vim-Plug Plug-In Manager

```sh
sudo curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## Install Your First Plug-In With Vim-Plug

1. Create a separate file to manage your plug-ins, and a new directory to store them.

```sh
touch ~/.vimrc.plug
mkdir ~/vimplug-plugins
```

2. Open `~/.vimrc` in the Vim editor and add the following text at the bottom to call the .vimrc.plug file.

```vim
 " Call the .vimrc.plug file
 if filereadable(expand("~/.vimrc.plug"))
     source ~/.vimrc.plug
 endif
 ```

3. Now, open the `~/.vimrc.plug` file in Vim. Populate the file with the contents below to add the Fugitive Vim plug-in, a Github wrapper. With this plug-in installed, you can now run a Git terminal from within Vim!

> **Note!**  
*Any additional plug-ins to be installed need to be added between the “plug#begin” and “plug#end” lines.*

```vim
call plug#begin('~/.vim/plugged')

"Fugitive Vim Github Wrapper
Plug 'tpope/vim-fugitive'

call plug#end()
```

> **Note!**  
*If after this step you receive an error similar to "E117 Unknown Function: plug#end" check the user permissions over `~/.vim/` you may need to `chmod -R 0755`*

4. After saving and closing the *.vimrc.plug file*, exit and restart Vim. The final installation procedure is to issue the PlugInstall command in command mode. This will open the plug-in manager within Vim and proceed to install all plug-ins listed in the **vimrc.plug file*. Installed plug-ins will automatically load the next time Vim is started.

```vim
:PlugInstall
```

5. Additional commands for managing plug-ins via Vim-Plug are listed below.

|Command|Description|
|---|:---|
|PlugInstall|Install plugins|
|PlugUpdate|Install or update plugins|
|PlugClean[!]|Delete removed plugins|
|PlugUpgrade|Upgrade Vim-Plug|
|PlugStatus|List plugins and current status|
|PlugDiff|Display changes made during updates|
|PlugSnapshot[1] [/output/path]|Generate script for restoring current plugins|

## Addition materials

[Useful plugins on vimawesome.com](https://vimawesome.com/)

[Generate your own config with vimconfig.com](https://vimconfig.com/)
