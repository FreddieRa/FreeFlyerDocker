# FreeFlyerDocker
 A basic guide for running FreeFlyer in a Docker container. There are two options:
 - RedHat Enterprise Linux 
   - Pros
     - Recommended by FreeFlyer
     - Correct versions of required packages are easy to install
   - Cons
     - Requires a RHEL license to use, and account to login
- Fedora
   - Pros
     - No license required
     - Simpler to install
   - Cons
     - Have to keep better track of versions
     - Requires some slightly hacky symlinks
     - Not guaranteed to be supported if FreeFlyer changes something


# RedHat Setup

### Step 1: Install Docker

Before doing anything, you will need Docker. This can be installed at:
https://www.docker.com/get-started


### Step 2: Download FreeFlyer

You will also need the Linux release for FreeFlyer. Once you have an account and have logged in, this can be downloaded at:
https://ai-solutions.com/restricted/freeflyer-downloads/

Once you've got it, put it in the top level of this directory.

### Step 3: Create a RedHat Enterprise account

FreeFlyer is configured to run on RedHat Enterprise Linux (RHEL). You will need to create an account on RedHat Enterprise Linux. You may use a free trial license, or you can purchase a license. This can all be done at:
https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux


### Step 4: Update environment variables

Once you have your RHEL account, you will need to update the your environment variables. This can be done with:
```bash
export FFUSER=<your username>
export FFPASS=<your password>
```

### Step 5: Check Versions

All of this was built for FreeFlyer 7.6.1. If that changes, you will need to update the `redHat` dockerfile accordingly.


### Step 6: Build the Docker Image

Actually building the image should be very straightforward. You can do this by running the following command:
```bash
docker build \
--build-arg FFUSER \
--build-arg FFPASS \
-t freeflyer \
-f redHat .
```

This will use the `redHat` dockerfile to build the image, and tag the resulting build with the name `freeflyer`.

**Note**: The line beginning `Importing GPG key 0xFD431D51:` may be in red. This is not an issue, and should be fine.



# Fedora Setup


### Step 1: Install Docker

Before doing anything, you will need Docker. This can be installed at:
https://www.docker.com/get-started


### Step 2: Download FreeFlyer

You will also need the Linux release for FreeFlyer. Once you have an account and have logged in, this can be downloaded at:
https://ai-solutions.com/restricted/freeflyer-downloads/

Once you've got it, put it in the top level of this directory.

### Step 3: Build the Docker Image

Actually building the image should be very straightforward. You can do this by running the following command:

```bash
docker build \
-t freeflyer \
-f fedora .
```

This will use the `fedora` dockerfile to build the image, and tag the resulting build with the name `freeflyer`.

# Running FreeFlyer

## Running the Container

To run the container simply type:

```bash
docker run -it --name runningff freeflyer /bin/bash
```
This will run the container `freeflyer` interactively (`-it`), call the running container `runningff`, and run the `/bin/bash` shell.

You can leave again with `exit` to exit and **stop** the container, or with `CTRL+p CTRL+q` to exit and leave it running in the background.

To rejoin, you can use `docker attach runningff`.


## Connecting to the License Server
TODO

## Running a Mission
TODO

