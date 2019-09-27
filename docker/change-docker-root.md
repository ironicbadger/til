### Change Docker root dir using systemd

The Docker root dir is usually something like `/var/lib/docker` by default. Here's how to change it using a systemd `.service` file.

Find your current root directory using `docker info`.

    $ docker info
        Root Dir: /var/lib/docker/aufs

Since we're using systemd modifying the `DOCKER-OPTS` tag within `/etc/default/docker` to include `-g /new/root/dir` isn't going to work. There are two options, both require you to edit your `docker.service` file.

> Pro tip: `systemctl status docker.service` will print the location of this file at the top of the output

##### Option 1 - Direct edit to `docker.service`

* Edit `ExecStart` line to look like this `ExecStart =/usr/bin/dockerd -g /new/docker/root/dir -H fd://`
* `systemctl daemon-reload`
* `systemctl restart docker`
* `docker info` - verify the root dir has updated

##### Option 2 - Create a systemd drop-in service file (better way)

This option is preferred as directly editing `.service` files should be avoided. They may be overwritten during an update for example.

* `vi /etc/systemd/system/docker.service.d/docker.root.conf` and populate with:

```sh
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -g /new/docker/root -H fd://
```

* `systemctl daemon-reload`
* `systemctl restart docker`
* `docker info` - verify the root dir has updated

##### Option 3 - Create/Modify a json config file (even better way)

This option is preferred over Option 2 because it only changes the docker root directory and nothing else.
Open or create `/etc/docker/daemon.json` and populate it with:

```json
{
    "data-root": "/new/docker/root"
}
```

* `systemctl daemon-reload`
* `systemctl restart docker`
* `docker info` - verify the root dir has updated

***Note - Existing Containers and Images***  
If you already have containers or images in `/var/lib/docker` you may wish to stop and back these up before moving them to the new root location. Moving can be done by either `rsync -a /var/lib/docker/* /path/to/new/root` or if permissions do not matter, you can simply use mv  or cp too.
