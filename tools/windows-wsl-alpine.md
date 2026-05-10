# Alpine Linux Commands

I use Windows at work and Mac at home.  I really hate cluttering up my main system by installing a bunch of tools that get out of date over time.  I prefer just to build a brand new image when anything gets out of date.

## Docker commands to build and run the docker image

### How to build the toolbox docker image

`docker build -t toolbox -f dockerfile.alpine .`

### start a new container from the image

`docker run -dit --name toolbox toolbox`

### start an existing container
`docker start toolbox`

### stop a running container
`docker stop toolbox`

### start bash in a running container
`docker exec -it toolbox /bin/bash`

## How to install Alpine Linux on WSL in Windows

### Option 1: Microsoft Store (Easiest)

This is the recommended method for most users as it handles the registration process automatically.

* Enable WSL: Open PowerShell as an administrator and run: `wsl --install`

  * If WSL is already installed, ensure it is up to date with `wsl --update`.

* Download Alpine: Open the [Microsoft Store Microsoft Store](https://apps.microsoft.com/detail/9p804crf0395?hl=en-US&gl=US) and search for Alpine WSL.

* Launch & Setup: Click Open after installation. A terminal will open to complete the setup. You will be prompted to create a UNIX username and password.

### Option 2: Manual Installation (Command Line)

If you prefer not to use the store or need a specific version, you can import it manually using a rootfs tarball.

* Download the Rootfs: Go to the [Alpine Linux Downloads page](https://alpinelinux.org/downloads/) and download the MINI ROOT FILESYSTEM for your architecture (usually x86_64).

* Import to WSL: Open PowerShell and use the following command to register the distribution: 'wsl --import <DistroName> <InstallLocation> <PathToTarFile>' 

  * Example: `wsl --import Alpine C:\WSL\Alpine C:\Users\YourName\Downloads\alpine-minirootfs.tar.gz`.

* Run Alpine: Start the distribution by typing:wsl -d Alpine.

## Switching to a non-root user in Alpine on WSL

### Install Sudo and Create a User

Alpine is a minimal distribution and does not include sudo by default.

* Install sudo: `apk update; apk add sudo`

* Create your non-root user: `addgroup tooluser; adduser -D --ingroup tooluser tooluser`

* Create a password for the new user: `echo "tooluser:changeme" | chpasswd`

* Add the new user to sudoers: `echo "tooluser ALL=(ALL) ALL" > /etc/sudoers.d/tooluser; chmod 0440 /etc/sudoers.d/tooluser`

* Switch the default user to the new user: `vi /etc/wsl.conf`

* Add these lines to the file:

```
[user]
default=tooluser
```
