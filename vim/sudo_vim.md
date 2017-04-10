### elevate privileges in vim

You forgot to `sudo` before opening a file again didn't you. Here's how to get the required permissions on that file without leaving vim.

`:w !sudo tee %`
