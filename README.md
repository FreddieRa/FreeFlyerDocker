# FreeFlyerDocker
 A basic guide for running FreeFlyer in a RedHat Enterprise Docker container

# Installation

## Install Docker

Before doing anything, you will need Docker. This can be installed at:
https://www.docker.com/get-started


## Download FreeFlyer

You will also need the Linux release for FreeFlyer. Once you have an account and have logged in, this can be downloaded at:
https://ai-solutions.com/restricted/freeflyer-downloads/

Once you've got it, put it in the top level of this directory.

## Create a RedHat Enterprise account

FreeFlyer is configured to run on RedHat Enterprise Linux (RHEL). You will need to create an account on RedHat Enterprise Linux. You may use a free trial license, or you can purchase a license. This can all be done at:
https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux


## Update `env.list`

Once you have your RHEL account, you will need to update the `env.list` file. This file is located in the top level of this directory, and simply replace the `username` and `password` with your account information.


## Check Versions

All of this was built for FreeFlyer 7.6.1. If that changes, you will need to update the `redHat` dockerfile accordingly.


## Build the Docker Image

Actually building the image should be very straightforward. You can do this by running the following command:
```bash
docker build -t freeflyer -f redHat .
```

This will save it as a Docker image called `freeflyer`.

### Notes

- The line beginning `Importing GPG key 0xFD431D51:` may be in red. This is not an issue, and should be fine.
- If all goes well, it should print out the current FreeFlyer version at the end.