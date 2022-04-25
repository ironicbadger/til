### grep for multiple files in subdirs

Use grep to find and delete multiple files at once, in subfolders too.

```
tree -fi | grep '.*-2.MP4'

tree -fi | grep '.*-2.MP4'
./2021-08-19/7F8A1487-2.MP4
./2021-08-19/7F8A1517-2.MP4
./2021-08-20/7F8A1757-2.MP4
./2021-08-20/7F8A1758-2.MP4

# pipe to xargs to delete
tree -fi | grep '.*-2.MP4' | xargs rm
```

Tree is useful as it prints a relative path into the subdirs for use by `xargs rm`. `ls -R` lists recursive files but without relative paths from your current working dir.

Or if just in the current directory a simple `ls` will suffice:

```
ls | grep '.*-2.CR3'
```