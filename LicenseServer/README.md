<h1>Running License Server on AWS</h1>

Lots of this refers to details in: 
https://ai-solutions.com/_help_Files/network_licensing.htm

This is just to try and streamline that process, but if you have issues then refer there.

Steps:

## Downloading FreeFlyer Files

1. Log in to FreeFlyer
2. Download the Network Licensing Tools
3. Download the License Information Utility


## Setting Up AWS Instance

1. Start an RHEL 7 instance (ideally without SQL since that  often breaks)
2. In **Security Groups** open ports 8090, 27000, and 27011
3. In **Elastic IPs** allocate a permanent IP address and associate it with your instance


## Running AWS Instance

1. Set up SSH keys*
2. Log in to the instance

*Example SSH config:

```bash
Host aws
    HostName ec2-192-168-0-1.eu-west-2.compute.amazonaws.com
    AddKeysToAgent yes
    User ec2-user
    IdentityFile /Users/[username]/Downloads/[nameOfKey].pem
```

## Adding Relevant Riles to Instance

1. Copy everything we downloaded to the instance
   1. `scp -r ./NetworkLicensing aws:~/`
   2. `scp -r ./License_Information_Utility aws:~/`


## Getting Required Details for License Request

1. Log in to the instance
2. `cd ~/License_Information_Utility/Linux`
3. `sudo chmod u+x ./freeflyer_license_information`
4. `./freeflyer_license_information`
5. Send this to `fflicense@ai-solutions.com`
6. Proceed once you have your network license file


## Installing the License Server

1. `cd ~/NetworkLicensing/lmadmin`
2. `sudo yum -y install lsb`
3. `sudo yum -y install java`
4. `sudo chmod u+x ./lmadmin-x64_lsb-11_16_2_0.bin` 
   - *Note version may vary*
5. `sudo chmod 777 /opt/` 
   - *Note this is required for default install location* 
6. `./lmadmin-x64_lsb-11_16_2_0.bin`
7. Accept the default settings until `License Server Port Number`, which you should set to `27000`
8. `cp ./freeflyr /opt/FNPLicenseServerManager/`
9. `chmod u+x /opt/FNPLicenseServerManager/freeflyr`



## Running the License Server

1. `cd /opt/FNPLicenseServerManager/`
2. `./lmadmin`
3. On your own machine connect to [instance ip]:8090 in a web browser
4. Go to *Administration*, and login with `admin` and `admin`
5. Change the password to something better when prompted.
6. Go to *Vendor Daemon Configuration*
7. Click *Import License* and add the license sent by AI Solutions
8. Click on the *freeflyr* daemon, change the default port to `27011`
9. Click *Save* and then *Start*


## Connecting to the License Server

1. Install FreeFlyer (see other README)
2. `ff -de -rls [instance ip] 27000`