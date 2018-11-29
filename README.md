# Linux_1
Portfolio 2 - evaluated

Raspberry pi when it is connected to SDU Edurom it's ip adress is 10.126.81.220. It is possible to connect to it with ssh or with a serial port (if it is connected to your computer).

Containers were made with a use of LXC. On containers Alpine Linux is working.
*********************************************************************************************************************
Usefull commands for containers:
lxc-start -n C1 && lxc-start -n C2
lxc-stop -n C2 && lxc-stop -n C2
lxc-ls -f //Display status of containers (if working or not) and its ip adresses (IPv4 and IPv6) and additional info. 
lxc-console -n NAME //Log into the container, user=root;
systemctl status lxc-net
systemctl restart lxc-net //restarting the lxc network service
ipatables //see routing and nat configuration

Mandatory commands to execute on PI:
sysctl -w net.ipv4.ip_forward=1 //enabling ipforwarding
iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 80 -j DNAT --to-destination 10.0.42.10:80 //NAT configuration for container, configuring iptables

--------------------------------------------------------------------------------------------------------------------

Usefull commands inside container:
rc-status //display working services
apk add PACKAGE_NAME //install new packages (recommended to get nano file editor)
Mandatory: apk add socat 
*********************************************************************************************************************

Important files on pi
/etc/default/lxc-net // Bridge additional configuration
/etc/lxc/default.conf //Bridge basic configuration
/etc/lxc/dhcp.conf //DHCP configuration - Containers have static ip adresses (C1 - 10.0.42.10 && C2 - 10.0.42.15)
