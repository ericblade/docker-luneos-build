# Building

Install docker and docker-compose, clone this repo.

If using Windows, then un-comment the "volumes" section in docker-compose.yml.

Then:

````
cd docker-luneos-build
mkdir sstate-cache
mkdir tmp-glibc
sudo chown 999:999 sstate-cache
sudo chown 999:999 tmp-glibc

docker-compose build
docker-compose run luneos
````

After some time, you will find yourself inside the LuneOS build-environment.

If you're running in Windows, you may have to issue the command "reset" immediately, otherwise
the command prompt will be in a weird state.

Then run:

````MACHINE=(yourtarget) bb luneos-dev-image````

# TODO

Figure out how to get the volumes to work in such a way that doesn't require chowning? not sure if that's possible.  Figure out if it's possible to put the Windows volumes also in the normal Windows filesystems, instead of wherever it is that Docker for Windows stores named volumes currently.

Document what to do after a system is built.
