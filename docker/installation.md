# installation
https://docs.docker.com/install/linux/docker-ce/ubuntu/


# Install Docker CE
You can install Docker CE in different ways, depending on your needs:

  • Most users set up Docker’s repositories and install from them, for ease of installation and upgrade tasks. This is the recommended approach.

  • Some users download the DEB package and install it manually and manage upgrades completely manually. This is useful in situations such as installing Docker on air-gapped systems with no access to the internet.

  • In testing and development environments, some users choose to use automated convenience scripts to install Docker.

# Install using the repository

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

## SET UP THE REPOSITORY

  1. Update the apt package index:
```
    $ sudo apt-get update
```
  2. Install packages to allow apt to use a repository over HTTPS:
```
    $ sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common
```
  3. Add Docker’s official GPG key:
```
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.
```
    $ sudo apt-key fingerprint 0EBFCD88

    pub   rsa4096 2017-02-22 [SCEA]
          9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]
```
  4. Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.
Note: The lsb_release -cs sub-command below returns the name of your Ubuntu distribution, such as xenial. Sometimes, in a distribution like Linux Mint, you might need to change $(lsb_release -cs) to your parent Ubuntu distribution. For example, if you are using Linux Mint Tessa, you could use bionic. Docker does not offer any guarantees on untested and unsupported Ubuntu distributions.

    ○ x86_64 / amd64
		
    ○ armhf
		
    ○ arm64
		
    ○ ppc64le (IBM Power)
		
    ○ s390x (IBM Z)
```
    $ sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
```
## INSTALL DOCKER CE
  1. Update the apt package index.
```
    $ sudo apt-get update
```
  2. Install the latest version of Docker CE and containerd, or go to the next step to install a specific version:
```
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
  3. Verify that Docker CE is installed correctly by running the hello-world image.
```  
    $ sudo docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.
