![LittleBrother-Logo](doc/icon-baby-panda-128x128.png)
![Snapcraft-Logo](doc/snapcraft-logo-128x128.png)

# Snapcraft Support for `LittleBrother`

## Overview

There is a snap available to run a LittleBrother slave process. The easiest way to use it start as follows:
 
* Install the [snap daemon](https://snapcraft.io/docs/installing-snapd).    

* Install the LittleBrother snap:

      sudo snap install little-brother-slave

* Configure the snap

      sudo snap little-brother-slave set master.host.url=MASTER_HOST_URL access.token=ACCESS_TOKEN
 
  where `MASTER_HOST_URL` points to your master installation and `ACCESS_TOKEN` is the configured credential of
  the master.

* Restart the snap

      sudo snap little-brother-slave restart

and you are all set!

## Security Details

* In order for `LittleBrother` to be able to kill processes, the snap has to be allowed to use the 
  `process-control` plug. This is pre-configured for the snap. Note that the snap will only kill processes that 
  belong to monitored users.
