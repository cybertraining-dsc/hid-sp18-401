## Run Raspberry Pi with Docker Swarm - Tutorial

### Docker

A docker is a world's leading software container technology. A container allows 
a developer to package the application along with dependencies associated with 
it and put all in a box which is an isolated environment so that the underlying 
host operating system is completely abstracted from the application running 
inside the box.
 
### Key benefits of Docker

* Portability
* Density
* Scalability
* Security

### Swarm

Swarm is native clustering and scheduling tool for the docker. In the context 
of swarm, a cluster is a pool of Docker hosts that acts as a bit like a single 
large docker host. You can also run swarm services and standalone containers on 
the same Docker instances. Set up and use Docker on Raspberry Pi
In this tutorial, we are going to see how to take several Raspberry Pi devices, 
cluster them using Docker Swarm and deploying containers to Swarm.

Step 1: Assembling the hardware

* We must assemble the cluster which requires the following components:
  Raspberry pi 3, standoff spacers, USB cables, USB charging hubs and SD 
  cards. With this we can build the hardware for our PI cluster.
	
Step 2: Install Raspbian Jessie on the SD cards

* Download Raspbian Jessie from <http://downloads.raspberrypi.org/raspbian/images/raspbian-2017-07-05/>
* Insert SD card into computer
* Flash the SD card with disk image of jessie

Step 3: Configure Raspbian

* Enable SSH

  * Navigate to the boot directory of SD card 
  * Create an empty file called SSH
  * Insert card onto the PI and power on

* Set up the WIFI for the PI
* When the PI is connected to the WIFI we would be able to SSH into the PI

Step 4: Figure out the IP Address of each node

* We can use nmap to scan our local network to find the devices that are connected

Step 5: Change the hostname for each node

* The default hostname is `raspberrypi`
* Though the computer can be reached with help of the IP its better to set a 
  hostname for each node for ease of use. 

Step 6: Install Docker on each node
* Run the code below to install docker on each node
  
  	for host in hostname; do 
            ssh pi@$host curl -sSL https://get.docker.com | sh; done
 
Step 7: Creating the swarm

* create swarm on a single node (this node will be a manager node) 
  * ssh into the node and run this command 

	sudo docker swarm init --advertise-addr "IP Address of the node"

* The previous command's output (token) can be used to join other nodes to the 
  swarm as a worker or manager.
* Join any more node as a managers or workers
  * SSH into the required node
  * Run 

      sudo docker swarm join --token SWMTKN-abc...manager...xyz 
      
\TODO{There seems to be some issue with indentation or incomplet documentation from here on}

`IP Address of the node` to join node as a manager
 * Run 

	sudo docker swarm join --token SWMTKN-abc...worker...xyz 

`IP Address of the node` to join node as a worker
* Finally, we can run sudo docker node ls command to check the status all the 
nodes.

