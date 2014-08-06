ansible-prj-lxc-deploy
=====

This Ansible project is an example on how to use the roles:
* ansible-role-tor-basic
* ansible-role-ferm-basic
* ansible-role-ferm-tor
* ansible-role-ferm-route-lxc-through-host-tor
* ansible-role-lxc-deploy

It will install and configure [tor](https://www.torproject.org/), [ferm](http://ferm.foo-projects.org/) and [LXC](https://linuxcontainers.org/) to route containers traffic to the Internet through Tor.

Requirements
------------

Ansible 1.6 or higher.

Project variables
-----------------

All these variables are defined in ansible-role-lxc-deploy/vars/main.yml and will be used by default.   
                                                                                
    # for lxc-install                                                           
    host_user: "user"                                                           
    host_user_home: "/home/{{host_user}}"                                       
    lxclib_path: "{{host_user_home}}/lxclib"                                    
    lxccache_path: "{{host_user_home}}/lxccache"                                
                                                                                
    ## set to true if the host where the role is running is configured to block 
    ## all outbound traffic except tor                                          
    usetor: true                                                                
                                                                                
                                                                                
    ## for lxc-create-container                                                 
    bridge_name: "lxcbr0"                                                       
    bridge_network: 172.16.0.0                                                  
    bridge_cidr: 24                                                             
    bridge_address: 172.16.0.1                                                  
    bridge_netmask: 255.255.255.0                                               
                                                                                
    ## by default network is 172.16.0.0/24, if different change                 
    ## bridge_address and  bridge_netmask                                       
    container_address: 172.16.0.2                                               
    container_name: "debianwheezy"                                              
    distribution: "wheezy"                                                      
    start: true                                                                 
    ## set to true to add the container ip and name to /etc/hosts               
    addtoetchosts: true                                                         
                                                                                
The two main variables needed to create new containers (to modify in your       
playbook) are:                                                                  
                                                                                
    container_address: 172.16.0.2                                               
    container_name: "debianwheezy" 

Dependencies
------------

The following roles are needed:
* ansible-role-tor-basic
* ansible-role-ferm-basic
* ansible-role-ferm-tor
* ansible-role-ferm-route-lxc-through-host-tor

Install
--------

    git clone --recursive  https://github.com/leewoboo/ansible-prj-lxc-deploy

License
-------

GPLv3

Author Information
------------------

Lee Woboo
