## Setup WSL Ubuntu
- install WSL 2 by using this command in Terminal (admin)
    ```
    wsl --install
    ```
- (optional) adjust wsl configuration like cpu core, ram, storage.
-  restart the machine
-  install wsl distro, here I use Ubuntu-22.04
    ```
    wsl --install -d Ubuntu-22.04
    ```
- set your ubuntu wsl user and login
- login as root (admin)
    ```
    sudo su -
    ```
- getting latest ubuntu update
    ```
    sudo apt-get update
    ````

## Setup Docker Engine (as root)
-  uninstall all conflicting packages
    ```
    for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
    ```

-  Set up Docker's apt repository.
    ```
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

-  Install the Docker packages.
    ```
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```


- try to docker service, and see if this return Hello From Docker! then its good.
    ```
    docker run hello-world
    ```

## IMPORTANT!
file permission hack between Linux system and windows system
- try to add this under file /etc/wsl.conf in wsl
    ```
    open up wsl config as root
    ---
    sudo vi /etc/wsl.conf

    then paste this config at the bottom.
    ---
    [automount]
    options="metadata"
    ```