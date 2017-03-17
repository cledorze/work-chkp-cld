# work-chkp-cld

Requirements:
•	fedora-23.x86_64 image loaded in glance / no metadata needed
•	Check-Point-R77.30-image loaded in glance / no metadata needed
•	Heat template contained in the work-cld-XXX.yaml.

How to start the stack :
•	From the shell on the control node or from Horizon :
openstack stack create -t work-cld-111.yaml --parameter key_name=dorz-MBP --parameter image=fedora-23.x86_64 --parameter flavor=demo-cld-cp --parameter external_net_cidr=10.0.0.0/24 --parameter external_net_gateway=10.0.0.1 --parameter external_net_pool_end=10.0.0.100 --parameter external_net_pool_start=10.0.0.20 --parameter external_net_name=external --parameter public_net=floating --parameter internal_net_cidr=10.1.0.0/24 --parameter internal_net_gateway=10.1.0.10 --parameter internal_net_pool_end=10.1.0.100 --parameter internal_net_pool_start=10.1.0.80 --parameter internal_net_name=internal --parameter flavorR77=2048MiB-50GiB-1CPU --parameter imageR77=Check-Point-R77.30-image --parameter password=linux teststack124

•	Then associate Floating IP to the R77.30 instance
•	Then log with SSH and the key defined to the R77.30's IP.
•	Initialize the configuration : 
chkvsec> set user admin password-hash $1$lICtM9Cs$x4w0ZcqmObnXBl2Q3OkG61
chkvsec> config_system -s 'install_security_gw=true&install_ppak=true&install_security_managment=true&install_mgmt_primary=true&install_mds_primary=false&mgmt_admin_name=admin&mgmt_admin_passwd=linux&mgmt_gui_clients_radio=any'

•	Connect to the WebUI on the Floating IP 
•	Set network interfaces if needed.
•	Download SmartConsole from the WebUI (only works on Windows ?!?)
	Need to load Security Policy / Fail obtaining a Windows Box, try with an export/import of the config …

Issues :
[Expert@chkvsec:0]# fw stat
HOST      POLICY     DATE
 Unable to open '/dev/fw0': No such file or directory
 Failed to get interface list: No such file or directory
 Cannot get interface list: No such file or directory
 Failed to get status from localhost
[Expert@chkvsec:0]# timed out waiting for input: auto-logout

fw unloadlocal
Uninstalling Security Policy from all.all@chkvsec
 Unable to open '/dev/fw0': No such file or directory
 Failed to Uninstall Security Policy: No such file or directory
[Expert@chkvsec:0]# cpstart
cpstart: Power-Up self tests passed successfully




