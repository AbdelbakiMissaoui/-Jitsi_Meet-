# -Jitsi_Meet-
**Jitsi Meet** is an open source video conferencing service solution providing fully encrypted and secure high quality and audio without subscription or the need to create an account. The solution can either be installed natively on Ubuntu Bionic Beaver (18.04 LTS) and Debian Buster. Another way to install it, is using a containerized application running on Docker.
This tutorial explains how to install the Jitsi Meet solution on a virtual cloud instance using the [Docker Image](https://github.com/jitsi/docker-jitsi-meet)  provided by the Jitsi team, allowing you to deploy your personal Jitsi Meet video conferencing solution in a few easy steps. It is based on a Debian stable base installation and provides all additional modules availabe for Jitsi like [Etherpad](https://etherpad.org/) or [jigasi](https://github.com/jitsi/jigasi), a gateway allowing SIP connections to the Jitsi Meet instance.

# Prerequisites to run Jitsi Meet on your VPS
   * You have an account and are logged into  VPS Hosting Services
   * You have  [configured your SSH Key](https://www.cyberciti.biz/faq/how-to-set-up-ssh-keys-on-linux-unix/)
   * You have a  Instance running Ubuntu  (20.04 LTS)
   * You have a [Git](https://git-scm.com/) installed and configured
   * You have installed [Docker and Docker Compose installed](https://docs.docker.com/engine/install/) on the instance
   * For best performances of Jitsi Meet, an instance with at least 4GB RAM is recommended
   * You have a domain or subdomain pointed to your IP Address for your Instance server
# Setting Up the Solution
  1. Connect to your Scaleway Elements Instance using SSH.
  2. Update the packet cache and upgrade the software already installed on the instance using the apt packet manager:
  ``` apt update && apt upgrade -y ```
  3. Install Docker, for more detailed instructions, follow our [dedicated tutorial:](https://docs.docker.com/engine/install/ubuntu/)
  ```sh
      apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      apt update
      apt install docker-ce docker-ce-cli docker-compose containerd.io git
   ```
  4.  Clone the Docker Jitsi Meet repository using git and cd into the downloaded directory:
  ```sh
  git clone https://github.com/jitsi/docker-jitsi-meet && cd docker-jitsi-meet
  ```
 5.Copy the env.example file to create a environment (.env) configugration and create the required configuration directories:
 
  ```sh
     cp env.example .env
     mkdir -p ~/.jitsi-meet-cfg/{web/letsencrypt,transcripts,prosody,jicofo,jvb}
  ```
6.Open the .env file in a text editor and edit the basic settings as following:
