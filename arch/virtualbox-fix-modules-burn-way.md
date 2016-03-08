# Virtualbox - Fix after Kernel Update
So, there I was left with a broken Virtualbox following an Arch kernel update. Ok, should be simple, need to reload the host kernel modules for virtualbox... well if only!, and dkms let me down too.

Despite nothing really working and virtualbox constantly spitting out a kernel driver error message, I resorted to google and found this last "burn it all" solution to work:

1. Refresh the system:
    ```sh
    sudo pacman -Syyu
    ```
    This should iron out any package conflicts and such. 

2. Then, (re)install virtualbox and the virtualbox-host-modules package:
    ```sh
    sudo pacman -S virtualbox virtualbox-host-modules
    ```

3. Add your user to the virtualbox group:
    ```sh
    sudo gpasswd -a yourusername vboxusers
    ```
    
4. run /sbin/rcvboxdrv setup
    ```sh
    sudo /sbin/rcvbox setup
    ```
    This should now successfully fix the modules and allow virtualbox to play nice again. Although I did install the new kernel headers too.
    
Credit: https://bbs.archlinux.org/viewtopic.php?id=150349
