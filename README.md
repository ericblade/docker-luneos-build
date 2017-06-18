# What is it?

A docker image with an environment to build LuneOS (a fork of the open sourced webOS)

# Building the environment

Install docker and docker-compose, clone this repo.

If using Windows, then un-comment the "volumes" section in docker-compose.yml.  You may also need to expand the size of your Hyper-V volume inside Hyper-V Manager.

Then:

````
cd docker-luneos-build
mkdir sstate-cache
mkdir tmp-glibc
sudo chown 999:999 sstate-cache
sudo chown 999:999 tmp-glibc

docker-compose build
````

# Building LuneOS
To build the LuneOS system, use:

````
docker-compose run luneos
````

You should find yourself inside the LuneOS build-environment.

If you're running in Windows, you may have to issue the command "reset" immediately, otherwise
the command prompt will be in a weird state.

Then run:

````
MACHINE=(yourtarget) bb luneos-dev-image
````
MACHINE is a valid LuneOS target, as of this writing, valid targets are:
mako, tuna, grouper, tenderloin, raspberrypi3, hammerhead, ... ?

Note that Windows users may receive a bunch of warnings about cross-device links, during the build. These probably? don't affect the resulting image.
Windows users may also receive a whole host of "file is owned by uid 999, which is the same as the user running bitbake" warnings.
I do not know at the time of this writing how Windows permissions on the file system will affect things. Or for that matter, why there are windows
file system permissions involved, since it should be storing it on linux filesystems inside the Docker VM

# What to do after building?

Your output files should be in tmp-glibc/deploy/images/(MACHINE)/

If you're using Linux, you can probably just manipulate these files directly from the disk,
if you're in Windows, you may have to use 'docker cp' to copy the output files back to the host
machine.

If you're using one of the supported MACHINEs, you should be able to find directions to install
the image onto your device here: http://webos-ports.org/index.php?search=install+luneos&title=Special%3ASearch&go=Go

For example, the following will get you a copy of the qemux86 build image in your local filesystem:
````
docker cp -L dockerluneosbuild_luneos_1:/home/luneos/luneos-build/webos-ports-env/webos-ports/tmp-glibc/deploy/images/qemux86/luneos-dev-image-qemux86.tar.gz .
````

# TODO

Figure out how to get the volumes to work in such a way that doesn't require chowning? not sure if that's possible.  Figure out if it's possible to put the Windows volumes also in the normal Windows filesystems, instead of wherever it is that Docker for Windows stores named volumes currently.
