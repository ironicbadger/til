### elevate privileges in vim

You forgot to `sudo` before opening a file again didn't you. Here's how to get the required permissions on that file without leaving vim.

`:w !sudo tee %`

Or, add this to your `.vimrc` and simply `w!!` for the same effect.

`cmap w!! w !sudo tee > /dev/null %`
