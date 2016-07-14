# Start CoreOS using PXE

This example is based on Ubuntu 16.04.

## Set up DHCP

1. Install DHCP server

	```
	sudo apt install isc-dhcp-server
	```
2. Edit /etc/default/isc-dhcp-server
3. add network interfaces in INTERFACES variables, separated by space for multiple interfaces.
4. Save /etc/default/isc-dhcp-server
5. Edit /etc/dhcp/dhcpd.conf

	```
	allow booting;
	allow bootp;
	
	subnet xxx.xxx.xxx.0 netmask 255.255.255.0 {
	  range <min_dynamic_ip> <max_dynamic_ip>;
	  option broadcast-address xxx.xxx.xxx.255;
	  filename "/pxelinux.0";
	}
	
	host pxe_client {
	  hardware ethernet 08:00:27:10:41:9c;
	  fixed-address <pxe_server_ip>;
	}
	```

6. Save /etc/dhcp/dhcpd.conf
7. Restart isc-dhcp-server service

	```
	sudo service isc-dhcp-server restart
	```
	
## Set up TFTP Server

1. Install tftpd-hpa and pxelinux package

	```
	sudo apt install tftpd-hpa pxelinux
	```
	
2. Copy /usr/lib/PXELINUX/pxelinux.0 to /var/lib/tftpboot
3. Make directory /var/lib/tftpboot/pxelinux.cfg
4. Create file /var/lib/tftpboot/pxelinux.cfg/default and add the following content

	```
	default coreos
	prompt 1
	
	display boot.msg
	
	label coreos
	  rootfstype btrfs
	  console tty0
	  console ttyS0
	  menu default
	  kernel coreos_production_pxe.vmlinuz
	  append initrd=coreos_production_pxe_image.cpio.gz rootfstype=btrfs console=tty0 console=ttyS0 coreos.autologin
	```
5. Go to /var/lib/tftpboot
6. Download CoreOS PXE images as follow

	```
	sudo wget http://stable.release.core-os.net/amd64-usr/current/coreos_production_pxe.vmlinuz
	sudo wget http://stable.release.core-os.net/amd64-usr/current/coreos_production_pxe_image.cpio.gz
	```
7. Go to /var/lib and change directory mode as following:

	```
	sudo chmod -R 777 tftpboot
	```
	
8. Restart tftpd-hpa service
