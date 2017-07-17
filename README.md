# Docker-run-GUI-apps
Running applications with GUI on a docker container.

There are a few different options to run GUI applications inside a Docker container like using SSH with X11 forwarding,
or VNC but the simplest one is to share X11 socket with the container and use it directly.
For this example we will be running gimp on a container.

# GIMP(GNU Image Manipulation Program)

GIMP is a cross-platform image editor available for GNU/Linux, OS X, Windows and more operating systems and it's free.
# Build
First step is to get the authentication cookie from host machine. Use the command:
```xauth list```

copy the generated cookie value.
From your docker engine on the host machine, run the following command:

```docker run -i -t --net=host -e=DISPLAY --device /dev/snd -v /tmp/.X11-unix ubuntu bash```

The command will create a container with ubuntu image and share X11 socket file with the container and also share sound(optional)
> --device /dev/snd

From the container, run the following commands to install xauth and gimp.

```apt-get update && apt-get install xauth && apt-get install -y gimp```

Now we need to add the authentication cookie to the list.

```xauth add "paste here"```

Run gimp: ```gimp```

Addionally you can also mount a volume to the container by adding ```-v /path/on/host:/path/in/container``` and save your files on the following directory.
