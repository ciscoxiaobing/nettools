# nettools
Advanced Network Technology Center -University of Oregon

http://azurespeedtest.azurewebsites.net/

http://www.azurespeed.com/

http://packetlife.net/captures/

http://ipv6-test.com/pingtest/

#MTU
[root@localhost ~]# cat /sys/class/net/eth0/mtu        
1500
[root@localhost ~]# echo "1460" > /sys/class/net/eth0/mtu
[root@localhost ~]# cat /sys/class/net/eth0/mtu          
1460

#Net Tools
apt install -y tcptraceroute
tcptraceroute 20.0.0.9 80

wget http://pingpros.com/pub/tcpping
chmod 755 tcpping

mv tcpping /usr/bin/
tcpping 20.0.0.9:80
apt install hping3
