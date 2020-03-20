## We have used ubuntu as the instance OS, all installations and scripts are tailored for ubuntu

### STEP 1: Ansible installation on host - Ubuntu
citing https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04#step-1-%E2%80%94-installing-ansible for ansible installation guidelines

1) sudo apt-add-repository ppa:ansible/ansible

2) sudo apt update

3) sudo apt install ansible

4) sudo nano /etc/ansible/hosts
Paste:    
[servers]  
<master_alias> ansible_host=<master_ip>  
<slave1_alias> ansible_host=<slave_ip>  
<slave2_alias>ansible_host=<slave_ip>  

[servers:vars]  
ansible_python_interpreter=/usr/bin/python3

### STEP 2: Create Jetstream instances for 1 Kubernetes master and 2 workers and 1 Jenkins master 
#### Citing: https://iujetstream.atlassian.net/wiki/spaces/JWT/overview for commands and information
#### Create instances using the scripts in the folder Jetstream_create_instance  
1) Go to https://iu.jetstream-cloud.org/ and sign-in with your credentials
2) Download the v3 RC file for project allocation TG-CCR180043
3) Open a terminal in Linux and naviagte to the directory where TG-CCR180043 RC file is present
4) install openstack client - pip install python-openstackclient
5) source <RC_FILE>

### If you dont have your keys installed and copied in ~/.ssh already do this:
1) openstack security group create --description "ssh & icmp enabled" ${OS_USERNAME}-global-ssh
2) openstack security group rule create --protocol tcp --dst-port 1:65535 --remote-ip 0.0.0.0/0 ${OS_USERNAME}-global-ssh
3) openstack security group rule create --protocol udp --dst-port 1:65535 --remote-ip 0.0.0.0/0 ${OS_USERNAME}-global-ssh
4) openstack security group rule create --protocol icmp ${OS_USERNAME}-global-ssh
5) ssh-keygen -b 2048 -t rsa -f ${OS_USERNAME}-api-key -P ""
6) openstack keypair create --public-key ${OS_USERNAME}-api-key ${OS_USERNAME}-api-key
7) Navigate to cd ~/.ssh in a terminal
8) Replace the id_rsa & id_rsa.pub files with the keys generated in the above steps.

### If you dont have a network configured:
1) openstack network create ${OS_USERNAME}-api-net

2) Verify that the private network was created	
   openstack network list

3) Create a subnet within the private network space	
   openstack subnet create --network ${OS_USERNAME}-api-net --subnet-range 10.0.0.0/24 ${OS_USERNAME}-api-subnet1

4) Verify that subnet was created	
   openstack subnet list
   
   Create a router	
   openstack router create ${OS_USERNAME}-api-router

   Connect the newly created subnet to the router
   openstack router add subnet ${OS_USERNAME}-api-router ${OS_USERNAME}-api-subnet1

   Connect the router to the gateway named "public"	
   openstack router set --external-gateway public ${OS_USERNAME}-api-router

   Verify that the router has been connected to the gateway	
   openstack router show ${OS_USERNAME}-api-router

### Creating instances:
#### Open create_instances.sh file and replace the <master_alias>, <slave_alias_1>, <slave_alias_2> and <Jenkins_alias> with a name of your choice to identify your intsances uniquely.  
1) source <RC_FILE>
2) run create_instances.sh and enter the floating ip when prompted(Dont make a mistake in this otherwise an ip will not be assigned to the instance)
If you enter the ip incorrectly run this in a terminal after sourcing .RC file: openstack server add floating ip <alias> <FLOATING_IP>
