# note.vim
`note.vim` is a syntax highlighting file for general plain text notes, which
means it works with all the files with a `.note` extension just like `cpp.vim`
for `.cpp` files.
## 1. Installation
### Step 1
**Linux**: put the file into the `~/.vim/syntax/` directory.

**Windows**: put the file into the `...\Vim\vimfiles\syntax\` directory. For
example mine is `E:\ProgramFiles\Vim\vimfiles\syntax\`.
### Step 2
Put the following line into your `vimrc` file
```vim
au BufRead,BufNewFile *.note setf note
```
### Step 3 (optional)
By default, all `.note` files are set to read-only since this syntax uses the
`conceal` feature in Vim. Relevant configurations can be seen below or in the
file:
```vim
setlocal ro

if has("conceal")
    setlocal cole=2 cocu=n
endif
```
Also I have the following key-mapping function in my `vimrc`:
```vim
function ToggleReadOnly()
    if &ro == 1
        setl noro
        if has("conceal")
            setl cole=2 cocu=i
        endif
    else
        setl ro
        if has("conceal")
            setl cole=2 cocu=cn
        endif
    endif
endfunction
nnoremap <C-F1> :call ToggleReadOnly()<CR>
```
This is for the convenience of reading and editing, since it will be annoying
that the concealed contents keep appearing and disappearing. **So just feel
free to play around with them to understand what they mean and find your
favourite setup.**
## 2. Usage
First of all, create a `.note` file, for example `test.note`. Then set it to
not read-only by `:setl noro` or call the `ToggleReadOnly()` function provided
above before typing in any content. Currently there are **2** highlighting
styles - **foreground** and **background**, and **5** colors for each -
**blue**, **green**, **orange**, **purple** and **red**. Additionally,
**black** is available for foreground highlight as it was just for fun. What's
more, `#` (hash) is used for commenting just like in that in Python and `*`
(asterisk) will be in a different color if it is the start of a line so that
you can make a block with it. The following screenshots will show examples of
the usage.

|Inputs         |Results        |More Examples  |
|:-------------:|:-------------:|:-------------:|
|![Inputs](https://github.com/Neur1n/note.vim/blob/master/screenshots/note_usage.PNG)|![Results](https://github.com/Neur1n/note.vim/blob/master/screenshots/note_result.PNG)|![More Examples](https://github.com/Neur1n/note.vim/blob/master/screenshots/note_examples.PNG)|
## 3. Known Bugs
(1) Conflicts with [luochen1990/rainbow](https://github.com/luochen1990/rainbow),
and I have not tested with the other rainbow parentheses plugins yet. If you
don't need this plugin in your `.note` file, you can disable it on Vim startup
by putting the following in the `_vimrc` file:
```vim
let g:rainbow_active = 0
```
Then syntax highlightings in `.note` file will be fine until rainbow
parentheses is turned on manually.
