![LittleBrother-Logo](doc/icon-baby-panda-128x128.png)
![Snapcraft-Logo](doc/snapcraft-logo-128x128.png)

# Snapcraft Support for `LittleBrother`

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/little-brother-slave)

## Overview

There is a snap available to run a LittleBrother slave process. Note that you still need an active master process
which is currently not available as snap but only as Debian package. 
See [here](https://github.com/marcus67/little_brother).

Follow these steps to install and configure the slave process snap:
 
* Install the [snap daemon](https://snapcraft.io/docs/installing-snapd).    

* Install the LittleBrother snap:

      sudo snap install little-brother-slave

* Configure the snap

      sudo snap little-brother-slave set master.host.url=MASTER_HOST_URL access.token=ACCESS_TOKEN
 
  where `MASTER_HOST_URL` points to your master installation and `ACCESS_TOKEN` is the configured credential of
  the master.

* There are more options which have a reasonable default:
  * `port`: Port address to reach the health check of the slave. Defaults to 5555. 
  * `log.level`: Verbosity of the logging. Valid values are: `ERROR`, `WARNING`, `INFO` (default), `DEBUG`
  * `app.secret`: A random secret that will be used to secure the web access. This is automatically initialized 
     as a random UUID.
  * `host.name`: The name that will be used as label for the slave on the master. This value is automatically
     derived from the variable `${HOSTNAME}` using the suffix `.snap`.


* Manually connect the required plugs:

      sudo snap connect little-brother-slave:process-control :process-control
      sudo snap connect little-brother-slave:system-observe :system-observe

* Restart the snap

      sudo snap little-brother-slave restart

and you are all set!

## Versioning

The version number of the snap consists of two parts:

    N.N.N.M

The `N.N.N` part refers to the semantic versioning of the `LittleBrother`. 
See [here](https://github.com/marcus67/little_brother/blob/master/CHANGES.md) for a full descriptions of all changes.
The `M` part refers to the snap itself. Each release of `LittleBrother` should trigger a new version of the snap using
`M=0`. If there is trouble with the snap itself the `M` will denote subsequent fixes to the snap.

## Change History 

See [here](CHANGES.md)

## Security Details

In order for `LittleBrother` to be able to observe and kill processes, the snap has to be allowed to use the 
following plugs:

* `system-observe`: Obtain permission to monitor the running processes.
* `process-control`: Obtain permission to kill the required processes. Note that the snap will only kill processes that 
  belong to monitored users.
* `network-bind`: Obtain permission to bind to the port `PORT` to provide a health check.

These plugs are pre-configured for the snap. However, only the `network-bind` plug is automatically connected. The
other two plugs have to be connected manually. See Above.
