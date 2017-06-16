# Building

Install docker and docker-compose, clone this repo.

You may want to

Run:

docker-compose run luneos

After some time, you will find yourself inside the LuneOS build-environment.

If you're running in Windows, you may have to issue the command "reset" immediately, otherwise
the command prompt will be in a weird state.

Then run: MACHINE=(yourtarget) bb luneos-dev-image

