![LittleBrother-Logo](doc/icon-baby-panda-128x128.png)
![Snapcraft-Logo](doc/snapcraft-logo-128x128.png)

# Snapcraft Support for `LittleBrother`

## Overview

There is a snap available to run a LittleBrother slave process. The easiest way to use it start as follows:
 
* Install the [snap daemon](https://snapcraft.io/docs/installing-snapd).    

* Install the LittleBrother snap:

      sudo snap install little-brother-slave

* Configure the snap

      sudo snap little-brother-slave set master.host.url=MASTER_HOST_URL access.token=ACCESS_TOKEN port=PORT
 
  where `MASTER_HOST_URL` points to your master installation, `ACCESS_TOKEN` is the configured credential of
  the master, and `PORT` is the port number allocated for the health check.

* Manually connect the required plugs:

      sudo snap connect little-brother-slave:process-control :process-control
      sudo snap connect little-brother-slave:system-observe :system-observe

* Restart the snap

      sudo snap little-brother-slave restart

and you are all set!

## Security Details

In order for `LittleBrother` to be able to observe and kill processes, the snap has to be allowed to use the 
following plugs:

* `system-observe`: Obtain permission to monitor the running processes.
* `process-control`: Obtain permission to kill the required processes. Note that the snap will only kill processes that 
  belong to monitored users.
* `network-bind`: Obtain permission to bind to the port `PORT` to provide a health check.

These plugs are pre-configured for the snap. However, only the `network-bind` plug is automatically connected. The
other two plugs have to be connected manually. See Above.
