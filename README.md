Minecraft Server Installer
==========================

This project will make it super easy to install a MineCraft server. You can
install it with `curl`, `wget`, running it as a script, or using `git`. It is
best to use `git` if you would like to be able to easily update this script
itself.  However, if you would prefer to do this with manual dowloading - you
can just set up your server with `curl`, `wget`, or by manually executing the
`bin/minecraft` script.

Prerequisites
-------------

It is expected that you have installed Java on your machine if it is not
already provided. The reason for this is that this script doesn't want to
make any assumptions about which Java versions you prefer, or how you want
them installed.

Super Easy Installation
-----------------------

You can install this script very easily with `curl` by using the following
command in the directory where you want your game installed. This can be any
directory.

    curl -O https://raw.github.com/monokrome/minecraft-server-installer/master/bin/minecraft && chmod +x minecraft && ./minecraft

If you don't have `curl`, you can use `wget`.

    wget https://raw.github.com/monokrome/minecraft-server-installer/master/bin/minecraft && chmod +x minecraft && ./minecraft
    

Installation With Git
---------------------

If you'd like to keep this script up to date with `git` then run the following
commands. They will create a directory called 'minecraft' where your game will
be installed.

    git clone http://github.com/monokrome/minecraft-server-installer minecraft
    cd minecraft
    bin/minecraft

You can update the script from the newly created minecraft directory with a
simple `git pull` command.

    git pull

All of your configuration files can be found in the 'etc' directory, and the
script for launching your server can be run with the command `bin/minecraft`
from inside your 'minecraft' directory.

FAQ
---

#### MineCraft is only using one gigabyte of RAM. How can I increase this?

By default, this script tells Java to run Minecraft with 1024 megabytes of RAM.

However, the amount of RAM that you want is easily configurable. You can simply
export the amount of RAM as an environment variable or you can edit the
`default_memory_size` option at the top of the script located at
`bin/minecraft`. This option is always set in Megabytes. For those who do not
know, one gigabyte is 1024 megabytes.

So, some example sizes that you could use:

- 1024 for one gigabyte
- 2048 for two gigabytes
- 4096 for four gigabytes
- 8192 for eight gigabytes

One example is that you could export MINECRAFT_MAX_MEMORY in your
profile (${HOME}/.bashrc for bash, ${HOME}/.zshrc for ZSH, etc):

    export MINECRAFT_MAX_MEMORY=4096

You could also export this variable whenever you run the script like so:

    MINECRAFT_MAX_MEMORY=4096 ./bin/minecraft

If you know how to edit a bash script, you can also change the
`default_memory_size` on line seven of `bin/minecraft`. This option is the
least recommended of options, but useful if you have no way to change your
environment (as much as I doubt that's even possible) for some reason.


#### I want to run a different version of Minecraft. Is this possible?

You can run whatever version of Minecraft you'd like by simply setting the
`MINECRAFT_VERSION` environment variable. When you set this variable, the
requested version will automatically download when you run the server.

It is important to note that the `etc` directory is created when you start
Minecraft for the first time. If you start Minecraft and then decide to
revert to an older version, it may not work as expected. You should never
downgrade Minecraft after you've started a world for this reason.


#### I want to run a Bukkit server. Is this possible?

This installer is equipped with support for Bukkit. It will automatically
provide a recommended MINECRAFT_VERSION if one hasn't been specified, and
will automatically download the current recommended Bukkit build when you
run your server.

If you prefer to run a custom version of Minecraft and/or Bukkit, you can
set the `MINECRAFT_VERSION` and `BUKKIT_URL` environment variables. It is
important that you always provide a `BUKKIT_URL` if you are specifying a
manual `MINECRAFT_VERSION` since Bukkit doesn't provide deterministic
URLs in order for us to automatically generate them for you.
