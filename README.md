
Quick setup:
------------

Create a compute engine with at least 15GB of RAM and 15 GB of disk.  
Then run the following commands:


1. install git

        sudo apt install git

2. install Docker

        sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common 
    
        curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

        sudo apt-get update

        sudo apt-get install docker-ce docker-ce-cli containerd.io

        sudo docker run hello-world   

3. install docker-compose   
   
        sudo curl -L "https://github.com/docker/compose/releases/download/1.26.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   	
        sudo chmod +x /usr/local/bin/docker-compose
   	
   
4. clone git GCP Pilot project from GitHub

        git clone https://github.com/jplaroche2000/gcp_pilot.git

        Note:
        Product ODS table def file needs to be built with the Striim image,
	
5. create directory where to put trail files

        sudo mkdir /export/trailfiles
	
        sudo chmod a+rwx /export/trailfiles
	
	
5. Run Striim/Confluent on Docker

        cd ./gcp_pilot/docker
	
        sudo docker-compose -f docker-compose-striim-confluent.yml build
	
        sudo docker swarm init

        sudo docker-compose -f docker-compose-striim-confluent.yml up -d

        sudo docker container ls
	
        sudo docker container logs docker_striim_1 -f &
	

Done!


Configure tunneling on your laptop for:

- port 9092 for Kafka
- port 9021 for Control Center
