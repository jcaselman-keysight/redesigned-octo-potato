# Container Images for Eggplant Functional

This repository contains Dockerfiles which will build container images
containing Eggplant Functional, as well as an example set of GitHub Actions demonstrating how the container can be build and then used to run an Eggplant Functional script.

The Dockerfiles allow you to create images for both Linux flavors of Eggplant
Functional: RedHat (using CentOS 7 as the base image) and Ubuntu (using Ubuntu 16.04
as the base image).

The images are configured to run Eggplant Functional with the headless GNUstep backend,
allowing it to run in a container without a GUI.  Bonjour discovery is disabled, as
that makes little sense in a container environment (and is known to cause a crash!).

The EULA and the privace policy have been pre-accepted, but you will still need to
provide a license key. Using this container image and providing a license key implies your
acceptance of the EULA and the privacy agreement.

To provide a license key, run the following command:

```
runscript -CommandLineOutput yes -LicenseKey 0123-4567-89ab-cdef-012
```

To run a Eggplant Functional script, run the following command:
You will need to map a volume if you want to use a local suite

```
runscript  -CommandLineOutput yes ./{your-suite}.suite/Scripts/{your-script}.script
```

To start Eggdrive, run the following command, be sure you expose the driveport you are choosing:

```
runscript  -driveport 5400 -CommandLineOutput yes
```
