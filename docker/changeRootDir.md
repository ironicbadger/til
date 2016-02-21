## Getting Docker to Play Nicely with Systemd based Distros - How to Change the Root Dir for containers and images from the default.

One thing that proved to be an irritation was being able to specify an alternate Root Dir for Docker. This is where Docker stores containers and images, and defaults to `/var/lib/docker` (on Debian at least). However, if like me, this is not where I want to Root Dir. Tip: Your Root Dir can be found by running: 
```sh
$ sudo docker info
``` 

Ordinarily, this is easily fixed by editing the Docker file, which on Debian is located in `/etc/default/` to include the `-g /path/to/new/root` argument on the end of the DOCKER-OPTS line. 

This is fine for sysvinit systems, but systemd seems to ignore this completely, and instead, utilises the docker.service file, which on Debian Jessie, is located in: `/lib/systemd/system`.

The problem is, while there are docs, they could be much clearer about this; and there is evidence all over the internet that many systemd users are struggling. For many, the general solution being the messy use of a symlink from `/var/lib/docker`. I too was advised to consider this solution, but I simply refused; surely there has to be a better way... and there was! 

***Note - Solution Limitation***  
The solution here is within Debian Jessie. Things such as default paths and locations may differ with other distributions. The solutions below assume you are within the systemd/system directory on your distribution.

***Note - Existing Containers and Images***  
If you already have containers or images in `/var/lib/docker` you may wish to stop and back these up before moving them to the new root location. Moving can be done by either `rsync -a /var/lib/docker/* /path/to/new/root` or if 
permissions do not matter, you can simply use mv  or cp too.

Two solutions are presented below, one which edits the docker.service file directly; and the other which uses a systemd drop-in. The latter of which is by far the better way of doing things.

### Solution 1 (Dirty, Easy Way): Edit the docker.service file directly
1. Navigate to whereever your systemd docker.service file is located  
    ```sh
    $ cd /lib/systemd/system
    ```
2. Using your preferred application, edit the docker.service file.
    ```sh
    $ sudo nano docker.service
    ```
3. Find the line: `ExecStart=/usr/bin/docker daemon -H fd://` and ammend it to include `-g /path/to/new/root/dir` arguments (obviously make sure you specify the new root dir). So for example: `ExecStart =/usr/bin/docker daemon -g /media/docker -H fd://`

4. Save the file.

5. Restart docker.

6.  Verify the new Docker Root (see below)

### Solution 2 (Nicer, Easy Way): Create systemd drop-in to override ExecStart in docker.service
In this method, we create a drop-in snippet that effectively overrides docker’s default ExecStart arguments, which systemd will scan and execute. This is by far cleaner, given there would be no need to continually update docker.service following updates which may overwrite docker.service in the process.

1. Create docker.service.d directory:
sudo mkdir docker.service.d and move into the directory.
    ```sh
    $ sudo mkdir /etc/systemd/system/docker.service.d && cd /etc/systemd/system/docker.service.d
    ```

3. Create a `.conf` file within the new directory e.g. `docker.root.conf` (the file can be named whatever you wish as far as I know!).
    ```sh
    $ sudo nano docker.service.d/docker.root.conf
    ```
4. Add the following and save:
    ```sh 
    [Service]
    ExecStart=
    ExecStart=/usr/bin/docker daemon -g /path/to/new/root -H fd://
    ```
    ***Note*** remember, it is necessary to blank the ExecStart value before we reassign it - so the Arch Linux guys say, and they're rarely wrong right? Be sure to specify the path to your desired Docker root dir too.

5. Reload systemd, scanning for changed units
    ```sh
    $ sudo systemctl daemon-reload
    ```

6. (Re)start Docker
    ```sh
    $ sudo systemctl restart docker
    ```
    Or
    ```sh
    $ sudo systemctl start docker
    ```

7. Verify the new Docker Root (see below)

### Verify the new Docker Root
1. Confirm the change by running `sudo docker info` and pay attention to the `Root Dir` value.
Confirm any existing containers can be found and started and/or run docker’s hello-world example:
    ```sh
    $ sudo docker run -ti hello-world
    ```

2. Confirm the container(s) and/or image(s) presence within your new root dir: 
    ```sh
    $ ls -la /path/to/new/root/docker/containers
    ``` 
    ***Note*** you can check the container id(s) by running:
    ```sh
    $ sudo docker ps -a
    ```
3. If all checks out, you should be able to safely remove `/var/lib/docker` or leave it if you wish.

