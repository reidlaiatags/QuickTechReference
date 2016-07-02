# Install Docker in Ubuntu 14.04 LTS and above

1. Log into your machine as a user with sudo or root privileges.
2. Open a terminal window.
3. Update package information, ensure that APT works with the https method, and that CA certificates are installed.

  ```
  $ sudo apt-get update
  $ sudo apt-get install apt-transport-https ca-certificates
  $ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
  ```
  
4. Open the /etc/apt/sources.list.d/docker.list file in your favorite editor.
5. Add an entry for your Ubuntu operating system.
The possible entries are:

  Ubuntu Trusty 14.04 (LTS)

  ```
  deb https://apt.dockerproject.org/repo ubuntu-trusty main
   ```

  Ubuntu Xenial 16.04 (LTS)

  ```
  deb https://apt.dockerproject.org/repo ubuntu-xenial main
  ```

6. Save and close the /etc/apt/sources.list.d/docker.list file.

7. Update the APT package index.

  ```
  $ sudo apt-get update
  ```

8. Purge the old repo if it exists.

  ```
  $ sudo apt-get purge lxc-docker
  ```

9. Verify that APT is pulling from the right repository.

  ```
  $ sudo apt-cache policy docker-engine
  ```
  
10. Update apt-get repository

  ```
  $ sudo apt-get update
  ```

11. Install docker-engine

  ```
  $ sudo apt-get install docker-engine
  ```
  
12. Add user into docker group and restart docker service

  ```
  $ sudo usermod -aG docker $USER
  $ sudo service docker restart
  ```
  
13. Logout and login user again to make new group effective