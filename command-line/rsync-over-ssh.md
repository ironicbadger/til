## Sync a folder over SSH using rsync

### Update the contents of a folder

In order to save bandwidth and time, we can avoid copying the files that we already have in the destination folder that have not been modified in the source folder. To do this, we can add the parameter -u to rsync, this will synchronize the destination folder with the source folder, this is where the delta-transfer algorithm enters. To synchronize two folders like this we use:

  rsync -rtvu source_folder/ destination_folder/
By default, rsync will take into consideration the date of modification of the file and the size of the file to decide whether the file or part of it needs to be transferred or if the file can be left alone, but we can instead use a hash to decide whether the file is different or not. To do this we need to use the -c parameter, which will perform a checksum in the files to be transferred. This will skip any file where the checksum coincides.

  rsync -rtvuc source_folder/ destination_folder/

### Synchronizing two folders with rsync

To keep two folders in synchrony, not only do we need to add the new files in the source folder to the destination folder, as in the past topics, we also need to remove the files that are deleted in the source folder from the destination folder. rsync allow us to do this with the parameter --delete, this used in conjunction with the previously explained parameter -u that updates modified files allow us to keep two directories in synchrony while saving bandwidth.

  rsync -rtvu --delete source_folder/ destination_folder/
  
The deletion process can take place in different moments of the transfer by adding some additional parameters:

rsync can look for missing files and delete them before it does the transfer process, this is the default behavior and can be set with `--delete-before`
rsync can look for missing files after the transfer is completed, with the parameter --delete-after
rsync can delete the files done during the transfer, when a file is found to be missing, it is deleted at that moment, we enable this behavior with `--delete-during`
rsync can do the transfer and find the missing files during this process, but instead of delete the files during this process, waits until it is finished and delete the files it found afterwards, this can be accomplished with `--delete-delay`
e.g.:

  rsync -rtvu --delete-delay source_folder/ destination_folder/

- Source(s)
  - [1](http://www.jveweb.net/en/archives/2010/11/synchronizing-folders-with-rsync.html)
