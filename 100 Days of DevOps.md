https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details

https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

<h1>Linux</h1>
<h3>Day 1: Linux User Setup with Non-Interactive Shell</h3>

	thor@jumphost ~$ ssh banner@stapp03
	banner@stapp03's password: 
	[banner@stapp03 ~]$ sudo useradd -s /sbin/nologin anita  -OR- sudo adduser --shell /sbin/nologin anita	

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for banner: 
	[banner@stapp03 ~]$     cat /etc/passwd | grep anita
	anita:x:1002:1002::/home/anita:/sbin/nologin
	[banner@stapp03 ~]$ 
	[banner@stapp03 ~]$ id anita
	uid=1002(anita) gid=1002(anita) groups=1002(anita)
	[banner@stapp03 ~]$ 

<h3>Day 2: Temporary User Setup with Expiry</h3>
As part of the temporary assignment to the Nautilus project, a developer named rose requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. 
	Here's what you need to do: Create a user named rose on App Server 1 in Stratos Datacenter. Set the expiry date to 2024-04-15, ensuring the user is created in lowercase as per standard protocol.
	
	 	thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:dceSnztcozLCnqnuBjm/i04vhbbNcBiXcKAVVFMqVfY.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo adduser rose
	
		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:
	
			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.
	
		[sudo] password for tony: 
		[tony@stapp01 ~]$ cat /etc/passwd
		passwd   passwd-  
		[tony@stapp01 ~]$ cat /etc/passwd
		passwd   passwd-  
		[tony@stapp01 ~]$ cat /etc/passwd | grep -i rose
		rose:x:1002:1002::/home/rose:/bin/bash
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ id rose
		uid=1002(rose) gid=1002(rose) groups=1002(rose)
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo chage -E 2024-04-15 rose
		[tony@stapp01 ~]$ 
		
<h3>Day 3: Secure Root SSH Access</h3>
Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.
	Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.
					
		thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:BcV3qL4BI7/ZuY9J9r8qfpzw6kRwbci2QXQ0/0WGRr8.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ sudo vi /etc/ssh/sshd_config

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for tony: 
		[tony@stapp01 ~]$ sudo systemctl restart sshd
		[tony@stapp01 ~]$ 


		thor@jumphost ~$ ssh steve@stapp02
		The authenticity of host 'stapp02 (172.16.238.11)' can't be established.
		ED25519 key fingerprint is SHA256:qqGg8TwKc+O6YD6VXGK4Gjb44xl+CF8HEJYbmd+5Ros.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp02' (ED25519) to the list of known hosts.
		steve@stapp02's password: 
		[steve@stapp02 ~]$ sudo vi /etc/ssh/sshd_config

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for steve: 
		[steve@stapp02 ~]$ sudo systemctl restart sshd
		[steve@stapp02 ~]$ 


		thor@jumphost ~$ ssh banner@stapp03
		The authenticity of host 'stapp03 (172.16.238.12)' can't be established.
		ED25519 key fingerprint is SHA256:5CyoCIqOzW93UqsNm7+5eMKc3Z9hFyGCBG+sIULAoww.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp03' (ED25519) to the list of known hosts.
		banner@stapp03's password: 
		[banner@stapp03 ~]$ sudo vi /etc/ssh/sshd_config

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for banner: 
		[banner@stapp03 ~]$ sudo systemctl restart sshd
		[banner@stapp03 ~]$ 


<h3>Day 4: Script Execution Permissions</h3>
In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 2 within the Stratos Datacenter.
	Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 2. Additionally, ensure that all users have the capability to execute it.

		thor@jumphost ~$ ssh banner@stapp03
		The authenticity of host 'stapp03 (172.16.238.12)' can't be established.
		ED25519 key fingerprint is SHA256:kUKMxkPhbaRr/t2RNocrjPucio6ejfTj1tdLLJPuTRU.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp03' (ED25519) to the list of known hosts.
		banner@stapp03's password: 
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ ls -la /tmp/xfusioncorp.sh
		---------- 1 root root 40 Aug 17 00:53 /tmp/xfusioncorp.sh
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ sudo chmod a+rx /tmp/xfusioncorp.sh

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for banner: 
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ ls -la /tmp/xfusioncorp.sh
		-r-xr-xr-x 1 root root 40 Aug 17 00:53 /tmp/xfusioncorp.sh
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ 


<h3>Day 5: SElinux Installation and Configuration</h3>
Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 1 in the Stratos Datacenter:
	Install the required SELinux packages.
	Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
	No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
	Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

		thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:2TVK/16bp2iB4Zocl+kxN38kGNfYJKKFdSl4xu4nEAw.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sestatus
		SELinux status:                 disabled
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ getenforce
		Disabled
		[tony@stapp01 ~]$ cat /etc/os-release
		NAME="CentOS Stream"
		VERSION="9"
		ID="centos"
		ID_LIKE="rhel fedora"
		VERSION_ID="9"
		PLATFORM_ID="platform:el9"
		PRETTY_NAME="CentOS Stream 9"
		ANSI_COLOR="0;31"
		LOGO="fedora-logo-icon"
		CPE_NAME="cpe:/o:centos:centos:9"
		HOME_URL="https://centos.org/"
		BUG_REPORT_URL="https://issues.redhat.com/"
		REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 9"
		REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
		[tony@stapp01 ~]$
		[tony@stapp01 ~]$ rpm -qa | grep selinux
		rpm -q policycoreutils
		sudo yum install -y selinux-policy  # or relevant distribution package
		sudo yum install -y policycoreutils  policycoreutils-python setools setools-console setroubleshoot # or relevant distribution packages
		libselinux-3.6-1.el9.x86_64
		libselinux-utils-3.6-1.el9.x86_64
		policycoreutils-3.6-2.1.el9.x86_64
		Last metadata expiration check: 0:01:12 ago on Sun Aug 17 01:05:04 2025.
		Dependencies resolved.
		==================================================================================
		Package                      Arch        Version               Repository   Size
		==================================================================================
		Installing:
		selinux-policy               noarch      38.1.63-1.el9         baseos       44 k
		Upgrading:
		python3-rpm                  x86_64      4.16.1.3-37.el9       baseos       65 k
		rpm                          x86_64      4.16.1.3-37.el9       baseos      536 k
		rpm-build-libs               x86_64      4.16.1.3-37.el9       baseos       89 k
		rpm-libs                     x86_64      4.16.1.3-37.el9       baseos      308 k
		rpm-sign-libs                x86_64      4.16.1.3-37.el9       baseos       21 k
		Installing dependencies:
		rpm-plugin-selinux           x86_64      4.16.1.3-37.el9       baseos       17 k
		selinux-policy-targeted      noarch      38.1.63-1.el9         baseos      6.9 M

		Transaction Summary
		==================================================================================
		Install  3 Packages
		Upgrade  5 Packages

		Total download size: 8.0 M
		Downloading Packages:
		(1/8): rpm-plugin-selinux-4.16.1.3-37.el9.x86_64.  85 kB/s |  17 kB     00:00    
		(2/8): selinux-policy-38.1.63-1.el9.noarch.rpm    182 kB/s |  44 kB     00:00    
		(3/8): python3-rpm-4.16.1.3-37.el9.x86_64.rpm     531 kB/s |  65 kB     00:00    
		(4/8): rpm-build-libs-4.16.1.3-37.el9.x86_64.rpm  709 kB/s |  89 kB     00:00    
		(5/8): rpm-4.16.1.3-37.el9.x86_64.rpm             2.1 MB/s | 536 kB     00:00    
		(6/8): rpm-sign-libs-4.16.1.3-37.el9.x86_64.rpm   305 kB/s |  21 kB     00:00    
		(7/8): rpm-libs-4.16.1.3-37.el9.x86_64.rpm        2.4 MB/s | 308 kB     00:00    
		(8/8): selinux-policy-targeted-38.1.63-1.el9.noar 8.8 MB/s | 6.9 MB     00:00    
		----------------------------------------------------------------------------------
		Total                                             7.3 MB/s | 8.0 MB     00:01     
		Running transaction check
		Transaction check succeeded.
		Running transaction test
		Transaction test succeeded.
		Running transaction
		Running scriptlet: selinux-policy-targeted-38.1.63-1.el9.noarch             1/1 
		Preparing        :                                                          1/1 
		Installing       : selinux-policy-38.1.63-1.el9.noarch                     1/13 
		Running scriptlet: selinux-policy-38.1.63-1.el9.noarch                     1/13 
		Running scriptlet: selinux-policy-targeted-38.1.63-1.el9.noarch            2/13 
		Installing       : selinux-policy-targeted-38.1.63-1.el9.noarch            2/13 
		Running scriptlet: selinux-policy-targeted-38.1.63-1.el9.noarch            2/13 
		Upgrading        : rpm-libs-4.16.1.3-37.el9.x86_64                         3/13 
		Upgrading        : rpm-4.16.1.3-37.el9.x86_64                              4/13 
		Upgrading        : rpm-build-libs-4.16.1.3-37.el9.x86_64                   5/13 
		Upgrading        : rpm-sign-libs-4.16.1.3-37.el9.x86_64                    6/13 
		Upgrading        : python3-rpm-4.16.1.3-37.el9.x86_64                      7/13 
		Installing       : rpm-plugin-selinux-4.16.1.3-37.el9.x86_64               8/13 
		Cleanup          : python3-rpm-4.16.1.3-30.el9.x86_64                      9/13 
		Cleanup          : rpm-build-libs-4.16.1.3-30.el9.x86_64                  10/13 
		Cleanup          : rpm-sign-libs-4.16.1.3-30.el9.x86_64                   11/13 
		Cleanup          : rpm-4.16.1.3-30.el9.x86_64                             12/13 
		Cleanup          : rpm-libs-4.16.1.3-30.el9.x86_64                        13/13 
		Running scriptlet: selinux-policy-targeted-38.1.63-1.el9.noarch           13/13 
		Running scriptlet: rpm-4.16.1.3-37.el9.x86_64                             13/13 
		Running scriptlet: rpm-libs-4.16.1.3-30.el9.x86_64                        13/13 
		Verifying        : rpm-plugin-selinux-4.16.1.3-37.el9.x86_64               1/13 
		Verifying        : selinux-policy-38.1.63-1.el9.noarch                     2/13 
		Verifying        : selinux-policy-targeted-38.1.63-1.el9.noarch            3/13 
		Verifying        : python3-rpm-4.16.1.3-37.el9.x86_64                      4/13 
		Verifying        : python3-rpm-4.16.1.3-30.el9.x86_64                      5/13 
		Verifying        : rpm-4.16.1.3-37.el9.x86_64                              6/13 
		Verifying        : rpm-4.16.1.3-30.el9.x86_64                              7/13 
		Verifying        : rpm-build-libs-4.16.1.3-37.el9.x86_64                   8/13 
		Verifying        : rpm-build-libs-4.16.1.3-30.el9.x86_64                   9/13 
		Verifying        : rpm-libs-4.16.1.3-37.el9.x86_64                        10/13 
		Verifying        : rpm-libs-4.16.1.3-30.el9.x86_64                        11/13 
		Verifying        : rpm-sign-libs-4.16.1.3-37.el9.x86_64                   12/13 
		Verifying        : rpm-sign-libs-4.16.1.3-30.el9.x86_64                   13/13 

		Upgraded:
		python3-rpm-4.16.1.3-37.el9.x86_64         rpm-4.16.1.3-37.el9.x86_64          
		rpm-build-libs-4.16.1.3-37.el9.x86_64      rpm-libs-4.16.1.3-37.el9.x86_64     
		rpm-sign-libs-4.16.1.3-37.el9.x86_64      
		Installed:
		rpm-plugin-selinux-4.16.1.3-37.el9.x86_64                                       
		selinux-policy-38.1.63-1.el9.noarch                                             
		selinux-policy-targeted-38.1.63-1.el9.noarch                                    

		Complete!
		Last metadata expiration check: 0:01:24 ago on Sun Aug 17 01:05:04 2025.
		Package policycoreutils-3.6-2.1.el9.x86_64 is already installed.
		No match for argument: policycoreutils-python
		Error: Unable to find a match: policycoreutils-python
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ cat /etc/selinux/config

		# This file controls the state of SELinux on the system.
		# SELINUX= can take one of these three values:
		#     enforcing - SELinux security policy is enforced.
		#     permissive - SELinux prints warnings instead of enforcing.
		#     disabled - No SELinux policy is loaded.
		# See also:
		# https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/using_selinux/changing-selinux-states-and-modes_using-selinux#changing-selinux-modes-at-boot-time_changing-selinux-states-and-modes
		#
		# NOTE: Up to RHEL 8 release included, SELINUX=disabled would also
		# fully disable SELinux during boot. If you need a system with SELinux
		# fully disabled instead of SELinux running with no policy loaded, you
		# need to pass selinux=0 to the kernel command line. You can use grubby
		# to persistently set the bootloader to boot with selinux=0:
		#
		#    grubby --update-kernel ALL --args selinux=0
		#
		# To revert back to SELinux enabled:
		#
		#    grubby --update-kernel ALL --remove-args selinux
		#
		SELINUX=enforcing
		# SELINUXTYPE= can take one of these three values:
		#     targeted - Targeted processes are protected,
		#     minimum - Modification of targeted policy. Only selected processes are protected.
		#     mls - Multi Level Security protection.
		SELINUXTYPE=targeted


		[tony@stapp01 ~]$ sudo vi /etc/selinux/config
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ cat /etc/selinux/config

		# This file controls the state of SELinux on the system.
		# SELINUX= can take one of these three values:
		#     enforcing - SELinux security policy is enforced.
		#     permissive - SELinux prints warnings instead of enforcing.
		#     disabled - No SELinux policy is loaded.
		# See also:
		# https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/using_selinux/changing-selinux-states-and-modes_using-selinux#changing-selinux-modes-at-boot-time_changing-selinux-states-and-modes
		#
		# NOTE: Up to RHEL 8 release included, SELINUX=disabled would also
		# fully disable SELinux during boot. If you need a system with SELinux
		# fully disabled instead of SELinux running with no policy loaded, you
		# need to pass selinux=0 to the kernel command line. You can use grubby
		# to persistently set the bootloader to boot with selinux=0:
		#
		#    grubby --update-kernel ALL --args selinux=0
		#
		# To revert back to SELinux enabled:
		#
		#    grubby --update-kernel ALL --remove-args selinux
		#
		SELINUX=disabled
		# SELINUXTYPE= can take one of these three values:
		#     targeted - Targeted processes are protected,
		#     minimum - Modification of targeted policy. Only selected processes are protected.
		#     mls - Multi Level Security protection.
		SELINUXTYPE=targeted

		[tony@stapp01 ~]$ 

<h3>Day 6: Create a Cron Job</h3>
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:
	a. Install cronie package on all Nautilus app servers and start crond service.
	b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.		

	thor@jumphost ~$ ssh tony@stapp01
	The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
	ED25519 key fingerprint is SHA256:ViNPiWf9piJ1kBP9vOJ/E0sMlOdJASWZFAvgZx2hwLQ.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
	tony@stapp01's password: 
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$     sudo yum install cronie -y
		sudo systemctl start crond.service
		sudo systemctl enable crond.service

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for tony: 
	CentOS Stream 9 - BaseOS                        30 kB/s | 7.3 kB     00:00    
	CentOS Stream 9 - BaseOS                        12 MB/s | 8.8 MB     00:00    
	CentOS Stream 9 - AppStream                     50 kB/s | 7.5 kB     00:00    
	CentOS Stream 9 - AppStream                     42 MB/s |  25 MB     00:00    
	CentOS Stream 9 - Extras packages               38 kB/s | 8.0 kB     00:00    
	CentOS Stream 9 - Extras packages               38 kB/s |  19 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64 152 kB/s |  36 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64 8.2 MB/s |  20 MB     00:02    
	Extra Packages for Enterprise Linux 9 openh264 5.9 kB/s | 993  B     00:00    
	Extra Packages for Enterprise Linux 9 - Next - 119 kB/s |  25 kB     00:00    
	Extra Packages for Enterprise Linux 9 - Next - 391 kB/s | 279 kB     00:00    
	Dependencies resolved.
	===============================================================================
	Package               Architecture  Version               Repository     Size
	===============================================================================
	Installing:
	cronie                x86_64        1.5.7-14.el9          baseos        118 k
	Installing dependencies:
	cronie-anacron        x86_64        1.5.7-14.el9          baseos         32 k

	Transaction Summary
	===============================================================================
	Install  2 Packages

	Total download size: 150 k
	Installed size: 346 k
	Downloading Packages:
	(1/2): cronie-anacron-1.5.7-14.el9.x86_64.rpm  451 kB/s |  32 kB     00:00    
	(2/2): cronie-1.5.7-14.el9.x86_64.rpm          452 kB/s | 118 kB     00:00    
	-------------------------------------------------------------------------------
	Total                                          345 kB/s | 150 kB     00:00     
	Running transaction check
	Transaction check succeeded.
	Running transaction test
	Transaction test succeeded.
	Running transaction
	Preparing        :                                                       1/1 
	Installing       : cronie-anacron-1.5.7-14.el9.x86_64                    1/2 
	Running scriptlet: cronie-anacron-1.5.7-14.el9.x86_64                    1/2 
	Installing       : cronie-1.5.7-14.el9.x86_64                            2/2 
	Running scriptlet: cronie-1.5.7-14.el9.x86_64                            2/2 
	Created symlink /etc/systemd/system/multi-user.target.wants/crond.service → /usr/lib/systemd/system/crond.service.

	Verifying        : cronie-1.5.7-14.el9.x86_64                            1/2 
	Verifying        : cronie-anacron-1.5.7-14.el9.x86_64                    2/2 

	Installed:
	cronie-1.5.7-14.el9.x86_64         cronie-anacron-1.5.7-14.el9.x86_64        

	Complete!
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$     sudo crontab -e
	no crontab for root - using an empty one
	crontab: installing new crontab
	[tony@stapp01 ~]$ crontab -l
	no crontab for tony
	[tony@stapp01 ~]$ sudo crontab -e
	crontab: installing new crontab
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$ crontab -l
	no crontab for tony
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$ exit
	logout
	Connection to stapp01 closed.
	thor@jumphost ~$ ssh steve@stapp02
	The authenticity of host 'stapp02 (172.16.238.11)' can't be established.
	ED25519 key fingerprint is SHA256:BnqKJr/IxK+toRm1nnhpxkKce24sNLD/ZcdBQWyzT/I.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'stapp02' (ED25519) to the list of known hosts.
	steve@stapp02's password: 
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$     sudo yum install cronie -y
		sudo systemctl start crond.service
		sudo systemctl enable crond.service

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for steve: 
	CentOS Stream 9 - BaseOS                                     39 kB/s | 7.3 kB     00:00    
	CentOS Stream 9 - BaseOS                                    8.7 MB/s | 8.8 MB     00:01    
	CentOS Stream 9 - AppStream                                  24 kB/s | 7.5 kB     00:00    
	CentOS Stream 9 - AppStream                                  42 MB/s |  25 MB     00:00    
	CentOS Stream 9 - Extras packages                            29 kB/s | 8.0 kB     00:00    
	CentOS Stream 9 - Extras packages                            43 kB/s |  19 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64              112 kB/s |  36 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64               16 MB/s |  20 MB     00:01    
	Extra Packages for Enterprise Linux 9 openh264 (From Cisco) 4.8 kB/s | 993  B     00:00    
	Extra Packages for Enterprise Linux 9 - Next - x86_64       119 kB/s |  25 kB     00:00    
	Extra Packages for Enterprise Linux 9 - Next - x86_64       278 kB/s | 279 kB     00:01    
	Dependencies resolved.
	============================================================================================
	Package                  Architecture     Version                   Repository        Size
	============================================================================================
	Installing:
	cronie                   x86_64           1.5.7-14.el9              baseos           118 k
	Installing dependencies:
	cronie-anacron           x86_64           1.5.7-14.el9              baseos            32 k

	Transaction Summary
	============================================================================================
	Install  2 Packages

	Total download size: 150 k
	Installed size: 346 k
	Downloading Packages:
	(1/2): cronie-anacron-1.5.7-14.el9.x86_64.rpm               226 kB/s |  32 kB     00:00    
	(2/2): cronie-1.5.7-14.el9.x86_64.rpm                       551 kB/s | 118 kB     00:00    
	--------------------------------------------------------------------------------------------
	Total                                                       416 kB/s | 150 kB     00:00     
	Running transaction check
	Transaction check succeeded.
	Running transaction test
	Transaction test succeeded.
	Running transaction
	Preparing        :                                                                    1/1 
	Installing       : cronie-anacron-1.5.7-14.el9.x86_64                                 1/2 
	Running scriptlet: cronie-anacron-1.5.7-14.el9.x86_64                                 1/2 
	Installing       : cronie-1.5.7-14.el9.x86_64                                         2/2 
	Running scriptlet: cronie-1.5.7-14.el9.x86_64                                         2/2 
	Created symlink /etc/systemd/system/multi-user.target.wants/crond.service → /usr/lib/systemd/system/crond.service.

	Verifying        : cronie-1.5.7-14.el9.x86_64                                         1/2 
	Verifying        : cronie-anacron-1.5.7-14.el9.x86_64                                 2/2 

	Installed:
	cronie-1.5.7-14.el9.x86_64               cronie-anacron-1.5.7-14.el9.x86_64              

	Complete!
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$ sudo crontab -e
	no crontab for root - using an empty one
	crontab: installing new crontab
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$ exit
	logout
	Connection to stapp02 closed.
	thor@jumphost ~$ ssh banner@stapp03
	The authenticity of host 'stapp03 (172.16.238.12)' can't be established.
	ED25519 key fingerprint is SHA256:Lt79Neq98wjijCbWlgHtf8yj8/eFv2LynLdDKB+6gmY.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'stapp03' (ED25519) to the list of known hosts.
	banner@stapp03's password: 
	[banner@stapp03 ~]$     sudo yum install cronie -y
		sudo systemctl start crond.service
		sudo systemctl enable crond.service

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for banner: 
	CentOS Stream 9 - BaseOS                                    5.4 kB/s | 7.3 kB     00:01    
	CentOS Stream 9 - BaseOS                                     20 MB/s | 8.8 MB     00:00    
	CentOS Stream 9 - AppStream                                  33 kB/s | 7.5 kB     00:00    
	CentOS Stream 9 - AppStream                                  41 MB/s |  25 MB     00:00    
	CentOS Stream 9 - Extras packages                            79 kB/s | 8.0 kB     00:00    
	CentOS Stream 9 - Extras packages                            42 kB/s |  19 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64              227 kB/s |  36 kB     00:00    
	Extra Packages for Enterprise Linux 9 - x86_64               21 MB/s |  20 MB     00:00    
	Extra Packages for Enterprise Linux 9 openh264 (From Cisco) 5.6 kB/s | 993  B     00:00    
	Extra Packages for Enterprise Linux 9 - Next - x86_64       114 kB/s |  25 kB     00:00    
	Extra Packages for Enterprise Linux 9 - Next - x86_64       400 kB/s | 279 kB     00:00    
	Dependencies resolved.
	============================================================================================
	Package                  Architecture     Version                   Repository        Size
	============================================================================================
	Installing:
	cronie                   x86_64           1.5.7-14.el9              baseos           118 k
	Installing dependencies:
	cronie-anacron           x86_64           1.5.7-14.el9              baseos            32 k

	Transaction Summary
	============================================================================================
	Install  2 Packages

	Total download size: 150 k
	Installed size: 346 k
	Downloading Packages:
	(1/2): cronie-anacron-1.5.7-14.el9.x86_64.rpm               237 kB/s |  32 kB     00:00    
	(2/2): cronie-1.5.7-14.el9.x86_64.rpm                       556 kB/s | 118 kB     00:00    
	--------------------------------------------------------------------------------------------
	Total                                                       297 kB/s | 150 kB     00:00     
	Running transaction check
	Transaction check succeeded.
	Running transaction test
	Transaction test succeeded.
	Running transaction
	Preparing        :                                                                    1/1 
	Installing       : cronie-anacron-1.5.7-14.el9.x86_64                                 1/2 
	Running scriptlet: cronie-anacron-1.5.7-14.el9.x86_64                                 1/2 
	Installing       : cronie-1.5.7-14.el9.x86_64                                         2/2 
	Running scriptlet: cronie-1.5.7-14.el9.x86_64                                         2/2 
	Created symlink /etc/systemd/system/multi-user.target.wants/crond.service → /usr/lib/systemd/system/crond.service.

	Verifying        : cronie-1.5.7-14.el9.x86_64                                         1/2 
	Verifying        : cronie-anacron-1.5.7-14.el9.x86_64                                 2/2 

	Installed:
	cronie-1.5.7-14.el9.x86_64               cronie-anacron-1.5.7-14.el9.x86_64              

	Complete!
	[banner@stapp03 ~]$ 
	[banner@stapp03 ~]$ sudo crontab -e
	no crontab for root - using an empty one
	crontab: installing new crontab
	[banner@stapp03 ~]$ 
	[banner@stapp03 ~]$ exi
	-bash: exi: command not found
	[banner@stapp03 ~]$ exit
	logout
	Connection to stapp03 closed.
	thor@jumphost ~$ 


<h3>Day 7: Linux SSH Authentication</h3>
The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:
	Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

	thor@jumphost ~$ id
	uid=1000(thor) gid=1000(thor) groups=1000(thor),10(wheel)
	thor@jumphost ~$ 
	thor@jumphost ~$ whoami
	thor
	thor@jumphost ~$ 
	thor@jumphost ~$ ssh-keygen
	Generating public/private rsa key pair.
	Enter file in which to save the key (/home/thor/.ssh/id_rsa): 
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /home/thor/.ssh/id_rsa
	Your public key has been saved in /home/thor/.ssh/id_rsa.pub
	The key fingerprint is:
	SHA256:WS30ltyO6OEJWQcC9NQG0wfMHWO0lJuN8u3m5+GI9ho thor@jumphost.stratos.xfusioncorp.com
	The key's randomart image is:
	+---[RSA 3072]----+
	|     .o.=*++*o   |
	|       o +*B+=   |
	|        ..+.O=.  |
	|         =.=+o.  |
	|        S oo...  |
	|         + o. .  |
	|          +E . . |
	|           .o = o|
	|          .oo=.+.|
	+----[SHA256]-----+
	thor@jumphost ~$ 
	thor@jumphost ~$ cat /home/thor/.ssh/id_rsa.pub
	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDJtWZ5krYt8Fca5mulq3vn86Sp5kojzX5sQTkgNCFqTlu2gH85sM366jQocO4mMPAT9Lo/L0/Jk+PwJQ1RbvYSUJLgJ2Ez2jEY0SoeY/8Qa+AOshc2uelJ7G10vYeKGJqBdPe+64hbRdnTDCWrrc8IqIpVpyPCWf5D2/vjK4YK3M2aNOB5SkJSGIawT/qW27z5ssVm5CJsoz1Dy5H5ngli4TGqh/yjOznQBkR/0EwYLKu91MZsA9ufVPmLAMrLRnYeW792Wm3aMJH/kb2F0bXB3jyPVVaKVK3DaUx5Y9GvxD+e9HkcpLyMjCO9KS3Z5tSLfuB6rUX/QITTYyIxBChPO0XkfZDppBL32cTetv7Whzp8bEzIkLqAMM1qiWLmu483AaZ4odPva7bXdP43GdV4FoXL6+pf3K3TwEgu+8WVcxFxowl45IFn58xyc6Kwc/N8pexBetebHQGjYaw+BsH0jGXPhIj88ul8PIxO8fUeJtBSL6zSYWuk7rpYAMP02Cs= thor@jumphost.stratos.xfusioncorp.com
	thor@jumphost ~$ 
	thor@jumphost ~$ ssh-copy-id tony@stapp01
	/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/thor/.ssh/id_rsa.pub"
	The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
	ED25519 key fingerprint is SHA256:BP3NKf/pDWl3aKjAO0PYiJwZSW+a5CoeLFWx4t79q4A.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
	/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
	tony@stapp01's password: 

	Number of key(s) added: 1

	Now try logging into the machine, with:   "ssh 'tony@stapp01'"
	and check to make sure that only the key(s) you wanted were added.
	
	thor@jumphost ~$ ssh tony@stapp01
	Last login: Sun Aug 17 01:26:23 2025 from 172.16.238.3
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$ 
	[tony@stapp01 ~]$ exit
	logout
	Connection to stapp01 closed.


	thor@jumphost ~$ ssh-copy-id steve@stapp02
	/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/thor/.ssh/id_rsa.pub"
	The authenticity of host 'stapp02 (172.16.238.11)' can't be established.
	ED25519 key fingerprint is SHA256:XXdlG+cewuQcTWsBFj+Ye8jRGTPJYt6s1YfHWpksOms.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
	/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
	steve@stapp02's password: 

	Number of key(s) added: 1

	Now try logging into the machine, with:   "ssh 'steve@stapp02'"
	and check to make sure that only the key(s) you wanted were added.

	thor@jumphost ~$ ssh steve@stapp02
	[steve@stapp02 ~]$ exit
	logout
	Connection to stapp02 closed.
	thor@jumphost ~$ 


	thor@jumphost ~$ ssh-copy-id banner@stapp03
	/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/thor/.ssh/id_rsa.pub"
	The authenticity of host 'stapp03 (172.16.238.12)' can't be established.
	ED25519 key fingerprint is SHA256:puP8NtFnMDT3cN+E4DLEmv1L2ZIZjxz6LqyWcdhpZRw.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
	/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
	banner@stapp03's password: 

	Number of key(s) added: 1

	Now try logging into the machine, with:   "ssh 'banner@stapp03'"
	and check to make sure that only the key(s) you wanted were added.

	thor@jumphost ~$ ssh 'banner@stapp03'
	[banner@stapp03 ~]$ 
	[banner@stapp03 ~]$ exit
	logout
	Connection to stapp03 closed.
	thor@jumphost ~$ 


<h3>Day 8: Install Ansible</h3>	
During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.
	Install ansible version 4.9.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

	thor@jumphost ~$ cat /etc/os-release
	NAME="CentOS Stream"
	VERSION="9"
	ID="centos"
	ID_LIKE="rhel fedora"
	VERSION_ID="9"
	PLATFORM_ID="platform:el9"
	PRETTY_NAME="CentOS Stream 9"
	ANSI_COLOR="0;31"
	LOGO="fedora-logo-icon"
	CPE_NAME="cpe:/o:centos:centos:9"
	HOME_URL="https://centos.org/"
	BUG_REPORT_URL="https://issues.redhat.com/"
	REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 9"
	REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
	thor@jumphost ~$ 
	thor@jumphost ~$ uname -r
	5.15.0-1083-gcp
	thor@jumphost ~$ 
	thor@jumphost ~$ sudo pip3 install ansible==4.9.0

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for thor: 
	Sorry, try again.
	[sudo] password for thor: 
	Collecting ansible==4.9.0
	Downloading ansible-4.9.0.tar.gz (36.6 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 36.6/36.6 MB 67.9 MB/s eta 0:00:00
	Installing build dependencies ... done
	Getting requirements to build wheel ... done
	Preparing metadata (pyproject.toml) ... done
	Collecting ansible-core<2.12,>=2.11.6 (from ansible==4.9.0)
	Downloading ansible-core-2.11.12.tar.gz (7.1 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.1/7.1 MB 121.2 MB/s eta 0:00:00
	Installing build dependencies ... done
	Getting requirements to build wheel ... done
	Preparing metadata (pyproject.toml) ... done
	Collecting jinja2 (from ansible-core<2.12,>=2.11.6->ansible==4.9.0)
	Downloading jinja2-3.1.6-py3-none-any.whl.metadata (2.9 kB)
	Requirement already satisfied: PyYAML in /usr/lib64/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (5.4.1)
	Requirement already satisfied: cryptography in /usr/lib64/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (36.0.1)
	Collecting packaging (from ansible-core<2.12,>=2.11.6->ansible==4.9.0)
	Downloading packaging-25.0-py3-none-any.whl.metadata (3.3 kB)
	Collecting resolvelib<0.6.0,>=0.5.3 (from ansible-core<2.12,>=2.11.6->ansible==4.9.0)
	Downloading resolvelib-0.5.4-py2.py3-none-any.whl.metadata (3.7 kB)
	Requirement already satisfied: cffi>=1.12 in /usr/lib64/python3.9/site-packages (from cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (1.14.5)
	Collecting MarkupSafe>=2.0 (from jinja2->ansible-core<2.12,>=2.11.6->ansible==4.9.0)
	Downloading MarkupSafe-3.0.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.0 kB)
	Requirement already satisfied: pycparser in /usr/lib/python3.9/site-packages (from cffi>=1.12->cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (2.20)
	Requirement already satisfied: ply==3.11 in /usr/lib/python3.9/site-packages (from pycparser->cffi>=1.12->cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (3.11)
	Downloading resolvelib-0.5.4-py2.py3-none-any.whl (12 kB)
	Downloading jinja2-3.1.6-py3-none-any.whl (134 kB)
	━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 134.9/134.9 kB 34.8 MB/s eta 0:00:00
	Downloading packaging-25.0-py3-none-any.whl (66 kB)
	━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 66.5/66.5 kB 19.0 MB/s eta 0:00:00
	Downloading MarkupSafe-3.0.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (20 kB)
	Building wheels for collected packages: ansible, ansible-core
	Building wheel for ansible (pyproject.toml) ... done
	Created wheel for ansible: filename=ansible-4.9.0-py3-none-any.whl size=60168827 sha256=2a73757fb41b93c431ba5dd07c7e0455a7b910713636a3139e43b2e410accd4d
	Stored in directory: /root/.cache/pip/wheels/33/b7/3a/a0419b4a74d0493a7a17adb9b944b045ed8e81c6e5ec5f81d6
	Building wheel for ansible-core (pyproject.toml) ... done
	Created wheel for ansible-core: filename=ansible_core-2.11.12-py3-none-any.whl size=1961046 sha256=76c08f07f95f9b8b94ddfa1b7d6525290d00cf1d1dd06d7e96e66c7ee9b54eb2
	Stored in directory: /root/.cache/pip/wheels/06/b5/3d/4a4a1b494bb61ba26534ba172b81d1972467ee6c792d737b78
	Successfully built ansible ansible-core
	Installing collected packages: resolvelib, packaging, MarkupSafe, jinja2, ansible-core, ansible
	Successfully installed MarkupSafe-3.0.2 ansible-4.9.0 ansible-core-2.11.12 jinja2-3.1.6 packaging-25.0 resolvelib-0.5.4
	WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

	[notice] A new release of pip is available: 24.0 -> 25.2
	[notice] To update, run: pip install --upgrade pip
	thor@jumphost ~$ 
	thor@jumphost ~$ 
	thor@jumphost ~$ ansible --version
	ansible [core 2.11.12] 
	config file = None
	configured module search path = ['/home/thor/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
	ansible python module location = /usr/local/lib/python3.9/site-packages/ansible
	ansible collection location = /home/thor/.ansible/collections:/usr/share/ansible/collections
	executable location = /usr/local/bin/ansible
	python version = 3.9.18 (main, Jan 24 2024, 00:00:00) [GCC 11.4.1 20231218 (Red Hat 11.4.1-3)]
	jinja version = 3.1.6
	libyaml = True
	thor@jumphost ~$ pip install --upgrade pip
	Defaulting to user installation because normal site-packages is not writeable
	Requirement already satisfied: pip in /usr/local/lib/python3.9/site-packages (24.0)
	Collecting pip
	Downloading pip-25.2-py3-none-any.whl.metadata (4.7 kB)
	Downloading pip-25.2-py3-none-any.whl (1.8 MB)
	━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.8/1.8 MB 26.4 MB/s eta 0:00:00
	Installing collected packages: pip
	Successfully installed pip-25.2

	[notice] A new release of pip is available: 24.0 -> 25.2
	[notice] To update, run: python3 -m pip install --upgrade pip
	thor@jumphost ~$ 
	thor@jumphost ~$ sudo pip3 install ansible==4.9.0
	Requirement already satisfied: ansible==4.9.0 in /usr/local/lib/python3.9/site-packages (4.9.0)
	Requirement already satisfied: ansible-core<2.12,>=2.11.6 in /usr/local/lib/python3.9/site-packages (from ansible==4.9.0) (2.11.12)
	Requirement already satisfied: jinja2 in /usr/local/lib/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (3.1.6)
	Requirement already satisfied: PyYAML in /usr/lib64/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (5.4.1)
	Requirement already satisfied: cryptography in /usr/lib64/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (36.0.1)
	Requirement already satisfied: packaging in /usr/local/lib/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (25.0)
	Requirement already satisfied: resolvelib<0.6.0,>=0.5.3 in /usr/local/lib/python3.9/site-packages (from ansible-core<2.12,>=2.11.6->ansible==4.9.0) (0.5.4)
	Requirement already satisfied: cffi>=1.12 in /usr/lib64/python3.9/site-packages (from cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (1.14.5)
	Requirement already satisfied: MarkupSafe>=2.0 in /usr/local/lib64/python3.9/site-packages (from jinja2->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (3.0.2)
	Requirement already satisfied: pycparser in /usr/lib/python3.9/site-packages (from cffi>=1.12->cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (2.20)
	Requirement already satisfied: ply==3.11 in /usr/lib/python3.9/site-packages (from pycparser->cffi>=1.12->cryptography->ansible-core<2.12,>=2.11.6->ansible==4.9.0) (3.11)
	WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

	[notice] A new release of pip is available: 24.0 -> 25.2
	[notice] To update, run: pip install --upgrade pip
	thor@jumphost ~$ 
	thor@jumphost ~$ 


<h3>Day 9: MariaDB Troubleshooting</h3>
There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
	Look into the issue and fix the same.

	thor@jumphost ~$ ssh peter@stdb01
	The authenticity of host 'stdb01 (172.16.239.10)' can't be established.
	ED25519 key fingerprint is SHA256:uWERjaPRUsiIrmnk8m6dT3mb8nAuTQ80zy0hUEt1Aq0.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'stdb01' (ED25519) to the list of known hosts.
	peter@stdb01's password: 
	[peter@stdb01 ~]$ 
	[peter@stdb01 ~]$ sudo systemctl status mariadb

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for peter: 
	○ mariadb.service - MariaDB 10.5 database server
		Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
		Active: inactive (dead) since Sun 2025-08-17 02:19:33 UTC; 58s ago
	Duration: 5.873s
		Docs: man:mariadbd(8)
				https://mariadb.com/kb/en/library/systemd/
		Process: 896 ExecStartPre=/usr/libexec/mariadb-check-socket (code=exited, status=0/SUCCESS)
		Process: 1105 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)
		Process: 1472 ExecStart=/usr/libexec/mariadbd --basedir=/usr $MYSQLD_OPTS $_WSREP_NEW_CLUSTER (code=exited, status=0/SUCCESS)
		Process: 1521 ExecStartPost=/usr/libexec/mariadb-check-upgrade (code=exited, status=0/SUCCESS)
	Main PID: 1472 (code=exited, status=0/SUCCESS)
		Status: "MariaDB server is down"

	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Got notification message from PID 1472 (STATUS=Free innodb buffer pool, EXTEND_TIMEOUT_USEC=30000000)
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Got notification message from PID 1472 (STATUS=MariaDB server is down)
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Got notification message from PID 1472 (STATUS=MariaDB server is down)
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Child 1472 belongs to mariadb.service.
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Main process exited, code=exited, status=0/SUCCESS (success)
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Deactivated successfully.
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Service restart not allowed.
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Changed stop-sigterm -> dead
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Job 114 mariadb.service/stop finished, result=done
	Aug 17 02:19:33 stdb01.stratos.xfusioncorp.com systemd[1]: Stopped MariaDB 10.5 database server.
	[peter@stdb01 ~]$ 
	[peter@stdb01 ~]$ 
	[peter@stdb01 ~]$ 
	[peter@stdb01 ~]$  cd /var/lib/
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ ls -l
	total 52
	drwxr-xr-x 1 root root  4096 Jun  5  2024 alternatives
	drwxr-xr-x 1 root root  4096 Jun  5  2024 dnf
	drwxr-xr-x 2 root root  4096 Aug  9  2021 games
	drwxr-xr-x 2 root root  4096 Aug  9  2021 misc
	drwxr-xr-x 1 root mysql 4096 Aug 17 02:19 mysql
	drwx------ 2 root root  4096 Jun  5  2024 private
	drwxr-xr-x 1 root root  4096 Dec 13  2023 rpm
	drwxr-xr-x 2 root root  4096 Aug  9  2021 rpm-state
	drwxr-xr-x 3 root root  4096 May 27  2024 selinux
	drwxr-xr-x 1 root root  4096 Aug 17 02:19 systemd
	drwxr-xr-x 1 root root  4096 Jun  5  2024 tpm2-tss
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ chown mysql:mysql mysql
	chown: changing ownership of 'mysql': Operation not permitted
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ sudo chown mysql:mysql mysql
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ ls -l
	total 52
	drwxr-xr-x 1 root  root  4096 Jun  5  2024 alternatives
	drwxr-xr-x 1 root  root  4096 Jun  5  2024 dnf
	drwxr-xr-x 2 root  root  4096 Aug  9  2021 games
	drwxr-xr-x 2 root  root  4096 Aug  9  2021 misc
	drwxr-xr-x 1 mysql mysql 4096 Aug 17 02:19 mysql
	drwx------ 2 root  root  4096 Jun  5  2024 private
	drwxr-xr-x 1 root  root  4096 Dec 13  2023 rpm
	drwxr-xr-x 2 root  root  4096 Aug  9  2021 rpm-state
	drwxr-xr-x 3 root  root  4096 May 27  2024 selinux
	drwxr-xr-x 1 root  root  4096 Aug 17 02:19 systemd
	drwxr-xr-x 1 root  root  4096 Jun  5  2024 tpm2-tss
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ sudo systemctl start mariadb
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ sudo systemctl status mariadb
	● mariadb.service - MariaDB 10.5 database server
		Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
		Active: active (running) since Sun 2025-08-17 02:22:37 UTC; 6s ago
		Docs: man:mariadbd(8)
				https://mariadb.com/kb/en/library/systemd/
		Process: 2251 ExecStartPre=/usr/libexec/mariadb-check-socket (code=exited, status=0/SUCCESS)
		Process: 2285 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)
		Process: 2414 ExecStartPost=/usr/libexec/mariadb-check-upgrade (code=exited, status=0/SUCCESS)
	Main PID: 2380 (mariadbd)
		Status: "Taking your SQL requests now..."
		Tasks: 15 (limit: 411434)
		Memory: 77.0M
		CGroup: /docker/8b925690bc15bb7fc38200d589201a87b05672942a519c74018fc126f6a79c57/system.slice/mariadb.service
				└─2380 /usr/libexec/mariadbd --basedir=/usr

	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[2414]: Remounted /run/systemd/unit-root/run/systemd/incoming.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[2414]: Remounted /run/systemd/unit-root/run/credentials.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[2414]: mariadb.service: Executing: /usr/libexec/mariadb-check-upgrade
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Child 2414 belongs to mariadb.service.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Control process exited, code=exited, status=0/SUCCESS (success)
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Got final SIGCHLD for state start-post.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Changed start-post -> running
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Job 243 mariadb.service/start finished, result=done
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: Started MariaDB 10.5 database server.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Failed to send unit change signal for mariadb.service: Connection reset by peer
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ sudo systemctl enable mariadb
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ 
	[peter@stdb01 lib]$ sudo systemctl status mariadb
	● mariadb.service - MariaDB 10.5 database server
		Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
		Active: active (running) since Sun 2025-08-17 02:22:37 UTC; 18s ago
		Docs: man:mariadbd(8)
				https://mariadb.com/kb/en/library/systemd/
	Main PID: 2380 (mariadbd)
		Status: "Taking your SQL requests now..."
		Tasks: 15 (limit: 411434)
		Memory: 76.9M
		CGroup: /docker/8b925690bc15bb7fc38200d589201a87b05672942a519c74018fc126f6a79c57/system.slice/mariadb.service
				└─2380 /usr/libexec/mariadbd --basedir=/usr

	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Control process exited, code=exited, status=0/SUCCESS (success)
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Got final SIGCHLD for state start-post.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Changed start-post -> running
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Job 243 mariadb.service/start finished, result=done
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: Started MariaDB 10.5 database server.
	Aug 17 02:22:37 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Failed to send unit change signal for mariadb.service: Connection reset by peer
	Aug 17 02:22:53 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Changed dead -> running
	Aug 17 02:22:53 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Failed to reset devices.allow/devices.deny: Operation not permitted
	Aug 17 02:22:53 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Failed to set 'trusted.invocation_id' xattr on control group /docker/8b925690bc15bb7fc38200d589201a87b05672942a519c74018fc126f6a79c57/system.slice/mariadb.service, ignoring: Operation not permitted
	Aug 17 02:22:53 stdb01.stratos.xfusioncorp.com systemd[1]: mariadb.service: Failed to remove 'trusted.delegate' xattr flag on control group /docker/8b925690bc15bb7fc38200d589201a87b05672942a519c74018fc126f6a79c57/system.slice/mariadb.service, ignoring: Operation not permitted
	[peter@stdb01 lib]$ 


<h3>Day 10: Linux Bash Scripts</h3>
The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 1 in Stratos Datacenter, and they need to create a bash script named ecommerce_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 1).
	a. Create a zip archive named xfusioncorp_ecommerce.zip of /var/www/html/ecommerce directory.
	b. Save the archive in /backup/ on App Server 1. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.
	c. Copy the created archive to Nautilus Backup Server server in /backup/ location.
	d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.
	Note:
	The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. You can install it either manually or through the bash script as needed.

		thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:W+S9RUpM8FowOLdu6tpEMi6EpqyAqO/XnFG5NtcB5Zk.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		Permission denied, please try again.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ vi /scripts/ecommerce_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ cat /scripts/ecommerce_backup.sh
		#! /bin/bash

		zip -r /backup/xfusioncorp_ecommerce.zip /var/www/html/ecommerce
		scp /backup/xfusioncorp_ecommerce.zip clint@stbkp01:/backup/

		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /scripts/ecommerce_backup.sh
		-rw-r--r-- 1 tony tony 141 Aug 20 22:37 /scripts/ecommerce_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ chmod +x /scripts/ecommerce_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /scripts/ecommerce_backup.sh
		-rwxr-xr-x 1 tony tony 141 Aug 20 22:37 /scripts/ecommerce_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh-keygen
		Generating public/private rsa key pair.
		Enter file in which to save the key (/home/tony/.ssh/id_rsa): 
		Created directory '/home/tony/.ssh'.
		Enter passphrase (empty for no passphrase): 
		Enter same passphrase again: 
		Your identification has been saved in /home/tony/.ssh/id_rsa
		Your public key has been saved in /home/tony/.ssh/id_rsa.pub
		The key fingerprint is:
		SHA256:JRJg2o4hCjrb7GXAecDqJhoujXZEhr12VMUiV2vsObM tony@stapp01.stratos.xfusioncorp.com
		The key's randomart image is:
		+---[RSA 3072]----+
		|    o.. +o       |
		| . + . =...      |
		|o B . = o+.      |
		|+= X . .oo.      |
		|= B =   S=       |
		|.= * .    +      |
		|+== +    E       |
		|B+.+             |
		|+.o              |
		+----[SHA256]-----+
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh-copy-id clint@stbkp01
		/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/tony/.ssh/id_rsa.pub"
		The authenticity of host 'stbkp01 (172.16.238.16)' can't be established.
		ED25519 key fingerprint is SHA256:/fOVlvrbwARkWMsd23v7zdQ04Z4wKE4pnKnV8N/ddug.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
		/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
		clint@stbkp01's password: 
		Permission denied, please try again.
		clint@stbkp01's password: 

		Number of key(s) added: 1

		Now try logging into the machine, with:   "ssh 'clint@stbkp01'"
		and check to make sure that only the key(s) you wanted were added.

		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh client@stbkp01
		client@stbkp01's password: 
		Permission denied, please try again.
		client@stbkp01's password: 

		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh 'clint@stbkp01'
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ logout
		Connection to stbkp01 closed.
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /backup
		total 24
		drwxrwxrwx 2 root root  4096 Aug 20 22:26 .
		drwxr-xr-x 1 root root 20480 Aug 20 22:42 ..
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh 'clint@stbkp01'
		Last login: Wed Aug 20 22:42:11 2025 from 172.16.238.10
		[clint@stbkp01 ~]$ ls -la /backup/
		total 24
		drwxrwxrwx 2 root root  4096 Aug 20 22:26 .
		drwxr-xr-x 1 root root 20480 Aug 20 22:42 ..
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ logout
		Connection to stbkp01 closed.
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ /scripts/ecommerce_backup.sh 
		/scripts/ecommerce_backup.sh: line 3: zip: command not found
		stat local "/backup/xfusioncorp_ecommerce.zip": No such file or directory
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo apt install zip

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for tony: 
		sudo: apt: command not found
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ cat /etc/os-release 
		NAME="CentOS Stream"
		VERSION="9"
		ID="centos"
		ID_LIKE="rhel fedora"
		VERSION_ID="9"
		PLATFORM_ID="platform:el9"
		PRETTY_NAME="CentOS Stream 9"
		ANSI_COLOR="0;31"
		LOGO="fedora-logo-icon"
		CPE_NAME="cpe:/o:centos:centos:9"
		HOME_URL="https://centos.org/"
		BUG_REPORT_URL="https://issues.redhat.com/"
		REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 9"
		REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo yum install zip
		CentOS Stream 9 - BaseOS                        44 kB/s | 7.3 kB     00:00    
		CentOS Stream 9 - BaseOS                       9.3 MB/s | 8.8 MB     00:00    
		CentOS Stream 9 - AppStream                     40 kB/s | 7.5 kB     00:00    
		CentOS Stream 9 - AppStream                     18 MB/s |  25 MB     00:01    
		CentOS Stream 9 - Extras packages               36 kB/s | 8.0 kB     00:00    
		CentOS Stream 9 - Extras packages               30 kB/s |  19 kB     00:00    
		Docker CE Stable - x86_64                       43 kB/s | 3.5 kB     00:00    
		Docker CE Stable - x86_64                      347 kB/s |  78 kB     00:00    
		Extra Packages for Enterprise Linux 9 - x86_64 136 kB/s |  36 kB     00:00    
		Extra Packages for Enterprise Linux 9 - x86_64  21 MB/s |  20 MB     00:00    
		Extra Packages for Enterprise Linux 9 openh264 3.1 kB/s | 993  B     00:00    
		Extra Packages for Enterprise Linux 9 - Next - 133 kB/s |  25 kB     00:00    
		Extra Packages for Enterprise Linux 9 - Next - 353 kB/s | 279 kB     00:00    
		Dependencies resolved.
		===============================================================================
		Package         Architecture     Version               Repository        Size
		===============================================================================
		Installing:
		zip             x86_64           3.0-35.el9            baseos           266 k
		Installing dependencies:
		unzip           x86_64           6.0-59.el9            baseos           182 k

		Transaction Summary
		===============================================================================
		Install  2 Packages

		Total download size: 447 k
		Installed size: 1.1 M
		Is this ok [y/N]: y
		Downloading Packages:
		(1/2): unzip-6.0-59.el9.x86_64.rpm             723 kB/s | 182 kB     00:00    
		(2/2): zip-3.0-35.el9.x86_64.rpm               1.0 MB/s | 266 kB     00:00    
		-------------------------------------------------------------------------------
		Total                                          990 kB/s | 447 kB     00:00     
		Running transaction check
		Transaction check succeeded.
		Running transaction test
		Transaction test succeeded.
		Running transaction
		Preparing        :                                                       1/1 
		Installing       : unzip-6.0-59.el9.x86_64                               1/2 
		Installing       : zip-3.0-35.el9.x86_64                                 2/2 
		Running scriptlet: zip-3.0-35.el9.x86_64                                 2/2 
		Verifying        : unzip-6.0-59.el9.x86_64                               1/2 
		Verifying        : zip-3.0-35.el9.x86_64                                 2/2 

		Installed:
		unzip-6.0-59.el9.x86_64                 zip-3.0-35.el9.x86_64                

		Complete!
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ /scripts/ecommerce_backup.sh 
		adding: var/www/html/ecommerce/ (stored 0%)
		adding: var/www/html/ecommerce/.gitkeep (stored 0%)
		adding: var/www/html/ecommerce/index.html (stored 0%)
		xfusioncorp_ecommerce.zip                    100%  623     2.6MB/s   00:00    
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /backup/
		total 28
		drwxrwxrwx 2 root root  4096 Aug 20 22:46 .
		drwxr-xr-x 1 root root 20480 Aug 20 22:46 ..
		-rw-r--r-- 1 tony tony   623 Aug 20 22:46 xfusioncorp_ecommerce.zip
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh 'clint@stbkp01'
		Last login: Wed Aug 20 22:42:46 2025 from 172.16.238.10
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ ls -la /backup/
		total 36
		drwxrwxrwx 2 root  root   4096 Aug 20 22:46 .
		drwxr-xr-x 1 root  root  28672 Aug 20 22:48 ..
		-rw-r--r-- 1 clint clint   623 Aug 20 22:46 xfusioncorp_ecommerce.zip
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ 


<h3>Day 11: Install and Configure Tomcat Server</h3>
The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:
	a. Install tomcat server on App Server 3.
	b. Configure it to run on port 8083.
	c. There is a ROOT.war file on Jump host at location /tmp.

	Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e curl http://stapp03:8083


		thor@jumphost ~$ ansible --version
		bash: ansible: command not found
		thor@jumphost ~$ sudo pip3 install ansible

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for thor: 
		Collecting ansible
		Downloading ansible-8.7.0-py3-none-any.whl.metadata (7.9 kB)
		Collecting ansible-core~=2.15.7 (from ansible)
		Downloading ansible_core-2.15.13-py3-none-any.whl.metadata (7.0 kB)
		Collecting jinja2>=3.0.0 (from ansible-core~=2.15.7->ansible)
		Downloading jinja2-3.1.6-py3-none-any.whl.metadata (2.9 kB)
		Requirement already satisfied: PyYAML>=5.1 in /usr/lib64/python3.9/site-packages (from ansible-core~=2.15.7->ansible) (5.4.1)
		Requirement already satisfied: cryptography in /usr/lib64/python3.9/site-packages (from ansible-core~=2.15.7->ansible) (36.0.1)
		Collecting packaging (from ansible-core~=2.15.7->ansible)
		Downloading packaging-25.0-py3-none-any.whl.metadata (3.3 kB)
		Collecting resolvelib<1.1.0,>=0.5.3 (from ansible-core~=2.15.7->ansible)
		Downloading resolvelib-1.0.1-py2.py3-none-any.whl.metadata (4.0 kB)
		Collecting importlib-resources<5.1,>=5.0 (from ansible-core~=2.15.7->ansible)
		Downloading importlib_resources-5.0.7-py3-none-any.whl.metadata (2.8 kB)
		Collecting MarkupSafe>=2.0 (from jinja2>=3.0.0->ansible-core~=2.15.7->ansible)
		Downloading MarkupSafe-3.0.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.0 kB)
		Requirement already satisfied: cffi>=1.12 in /usr/lib64/python3.9/site-packages (from cryptography->ansible-core~=2.15.7->ansible) (1.14.5)
		Requirement already satisfied: pycparser in /usr/lib/python3.9/site-packages (from cffi>=1.12->cryptography->ansible-core~=2.15.7->ansible) (2.20)
		Requirement already satisfied: ply==3.11 in /usr/lib/python3.9/site-packages (from pycparser->cffi>=1.12->cryptography->ansible-core~=2.15.7->ansible) (3.11)
		Downloading ansible-8.7.0-py3-none-any.whl (48.4 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 48.4/48.4 MB 48.5 MB/s eta 0:00:00
		Downloading ansible_core-2.15.13-py3-none-any.whl (2.3 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 91.8 MB/s eta 0:00:00
		Downloading importlib_resources-5.0.7-py3-none-any.whl (24 kB)
		Downloading jinja2-3.1.6-py3-none-any.whl (134 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 134.9/134.9 kB 15.0 MB/s eta 0:00:00
		Downloading resolvelib-1.0.1-py2.py3-none-any.whl (17 kB)
		Downloading packaging-25.0-py3-none-any.whl (66 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 66.5/66.5 kB 16.7 MB/s eta 0:00:00
		Downloading MarkupSafe-3.0.2-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (20 kB)
		Installing collected packages: resolvelib, packaging, MarkupSafe, importlib-resources, jinja2, ansible-core, ansible
		WARNING: The scripts ansible, ansible-config, ansible-connection, ansible-console, ansible-doc, ansible-galaxy, ansible-inventory, ansible-playbook, ansible-pull and ansible-vault are installed in '/usr/local/bin' which is not on PATH.
		Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
		WARNING: The script ansible-community is installed in '/usr/local/bin' which is not on PATH.
		Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
		Successfully installed MarkupSafe-3.0.2 ansible-8.7.0 ansible-core-2.15.13 importlib-resources-5.0.7 jinja2-3.1.6 packaging-25.0 resolvelib-1.0.1
		WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

		[notice] A new release of pip is available: 24.0 -> 25.2
		[notice] To update, run: pip install --upgrade pip
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ ansible --version
		ansible [core 2.15.13]
		config file = None
		configured module search path = ['/home/thor/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
		ansible python module location = /usr/local/lib/python3.9/site-packages/ansible
		ansible collection location = /home/thor/.ansible/collections:/usr/share/ansible/collections
		executable location = /usr/local/bin/ansible
		python version = 3.9.18 (main, Jan 24 2024, 00:00:00) [GCC 11.4.1 20231218 (Red Hat 11.4.1-3)] (/usr/bin/python3)
		jinja version = 3.1.6
		libyaml = True
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ vi inventory.ini
		thor@jumphost ~$ 
		thor@jumphost ~$ cat inventory.ini 
		stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n ansible_become_pass=BigGr33n
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ vi playbook.yaml
		thor@jumphost ~$ 
		thor@jumphost ~$ cat playbook.yaml 
		---
		- name: Deploy Nautilus beta Java app on Tomcat
		hosts: stapp03
		become: yes
		tasks:
			- name: Install Tomcat and required packages
			  dnf:
				name:
				- tomcat
				- tomcat-webapps
				- tomcat-admin-webapps
				state: present

			- name: Change tomcat port in server.xml
			  ansible.builtin.replace:
				path: /etc/tomcat/server.xml
				regexp: 'port="8080"'
				replace: 'port="8083"'

			- name: Remove old extracted ROOT app folder
			  ansible.builtin.file:
				path: /var/lib/tomcat/webapps/ROOT
				state: absent

			- name: Copy ROOT.war from jump host to App Server 3
			  ansible.builtin.copy:
				src: /tmp/ROOT.war
				dest: /var/lib/tomcat/webapps/ROOT.war
				mode: '0644'

			- name: Enable and start Tomcat service
			  ansible.builtin.systemd:
				name: tomcat
				enabled: yes
				state: restarted
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory.ini playbook.yaml
		ERROR! We were unable to read either as JSON nor YAML, these are the errors we got from each:
		JSON: Expecting value: line 1 column 1 (char 0)

		Syntax Error while loading YAML.
		could not find expected ':'

		The error appears to be in '/home/thor/playbook.yaml': line 27, column 12, but may
		be elsewhere in the file depending on the exact syntax problem.

		The offending line appears to be:

			ansible.builtin.copy
				src: /tmp/ROOT.war
				^ here		
		
		
		thor@jumphost ~$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory.ini playbook.yaml
		ERROR! We were unable to read either as JSON nor YAML, these are the errors we got from each:
		JSON: Expecting value: line 1 column 1 (char 0)

		Syntax Error while loading YAML.
		found character that cannot start any token

		The error appears to be in '/home/thor/playbook.yaml': line 26, column 1, but may
		be elsewhere in the file depending on the exact syntax problem.

		The offending line appears to be:

			ansible.builtin.copy:
				src: /tmp/ROOT.war
		^ here
		There appears to be a tab character at the start of the line.

		YAML does not use tabs for formatting. Tabs should be replaced with spaces.

		For example:
			- name: update tooling
			vars:
				version: 1.2.3
		#    ^--- there is a tab there.

		Should be written as:
			- name: update tooling
			vars:
				version: 1.2.3
		# ^--- all spaces here.
		thor@jumphost ~$ ansible-lint playbook.yaml 
		bash: ansible-lint: command not found
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ pip3 install ansible-lint
		Defaulting to user installation because normal site-packages is not writeable
		Collecting ansible-lint
		Downloading ansible_lint-6.22.2-py3-none-any.whl.metadata (7.4 kB)
		Requirement already satisfied: ansible-core>=2.12.0 in /usr/local/lib/python3.9/site-packages (from ansible-lint) (2.15.13)
		Collecting ansible-compat>=4.1.11 (from ansible-lint)
		Downloading ansible_compat-24.10.0-py3-none-any.whl.metadata (4.0 kB)
		Collecting black>=22.8.0 (from ansible-lint)
		Downloading black-25.1.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_28_x86_64.whl.metadata (81 kB)
			━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 81.3/81.3 kB 3.9 MB/s eta 0:00:00
		Collecting filelock>=3.3.0 (from ansible-lint)
		Downloading filelock-3.19.1-py3-none-any.whl.metadata (2.1 kB)
		Collecting jsonschema>=4.10.0 (from ansible-lint)
		Downloading jsonschema-4.25.1-py3-none-any.whl.metadata (7.6 kB)
		Requirement already satisfied: packaging>=21.3 in /usr/local/lib/python3.9/site-packages (from ansible-lint) (25.0)
		Collecting pathspec>=0.10.3 (from ansible-lint)
		Downloading pathspec-0.12.1-py3-none-any.whl.metadata (21 kB)
		Requirement already satisfied: pyyaml>=5.4.1 in /usr/lib64/python3.9/site-packages (from ansible-lint) (5.4.1)
		Collecting rich>=12.0.0 (from ansible-lint)
		Downloading rich-14.1.0-py3-none-any.whl.metadata (18 kB)
		Collecting ruamel.yaml>=0.18.5 (from ansible-lint)
		Downloading ruamel.yaml-0.18.15-py3-none-any.whl.metadata (25 kB)
		Collecting subprocess-tee>=0.4.1 (from ansible-lint)
		Downloading subprocess_tee-0.4.2-py3-none-any.whl.metadata (3.3 kB)
		Collecting yamllint>=1.30.0 (from ansible-lint)
		Downloading yamllint-1.37.1-py3-none-any.whl.metadata (4.3 kB)
		Collecting wcmatch>=8.1.2 (from ansible-lint)
		Downloading wcmatch-10.1-py3-none-any.whl.metadata (5.1 kB)
		Collecting typing-extensions>=4.5.0 (from ansible-compat>=4.1.11->ansible-lint)
		Downloading typing_extensions-4.14.1-py3-none-any.whl.metadata (3.0 kB)
		Requirement already satisfied: jinja2>=3.0.0 in /usr/local/lib/python3.9/site-packages (from ansible-core>=2.12.0->ansible-lint) (3.1.6)
		Requirement already satisfied: cryptography in /usr/lib64/python3.9/site-packages (from ansible-core>=2.12.0->ansible-lint) (36.0.1)
		Requirement already satisfied: resolvelib<1.1.0,>=0.5.3 in /usr/local/lib/python3.9/site-packages (from ansible-core>=2.12.0->ansible-lint) (1.0.1)
		Requirement already satisfied: importlib-resources<5.1,>=5.0 in /usr/local/lib/python3.9/site-packages (from ansible-core>=2.12.0->ansible-lint) (5.0.7)
		Collecting click>=8.0.0 (from black>=22.8.0->ansible-lint)
		Downloading click-8.1.8-py3-none-any.whl.metadata (2.3 kB)
		Collecting mypy-extensions>=0.4.3 (from black>=22.8.0->ansible-lint)
		Downloading mypy_extensions-1.1.0-py3-none-any.whl.metadata (1.1 kB)
		Collecting platformdirs>=2 (from black>=22.8.0->ansible-lint)
		Downloading platformdirs-4.3.8-py3-none-any.whl.metadata (12 kB)
		Requirement already satisfied: tomli>=1.1.0 in /usr/local/lib/python3.9/site-packages (from black>=22.8.0->ansible-lint) (2.0.1)
		Collecting attrs>=22.2.0 (from jsonschema>=4.10.0->ansible-lint)
		Downloading attrs-25.3.0-py3-none-any.whl.metadata (10 kB)
		Collecting jsonschema-specifications>=2023.03.6 (from jsonschema>=4.10.0->ansible-lint)
		Downloading jsonschema_specifications-2025.4.1-py3-none-any.whl.metadata (2.9 kB)
		Collecting referencing>=0.28.4 (from jsonschema>=4.10.0->ansible-lint)
		Downloading referencing-0.36.2-py3-none-any.whl.metadata (2.8 kB)
		Collecting rpds-py>=0.7.1 (from jsonschema>=4.10.0->ansible-lint)
		Downloading rpds_py-0.27.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.2 kB)
		Collecting markdown-it-py>=2.2.0 (from rich>=12.0.0->ansible-lint)
		Downloading markdown_it_py-3.0.0-py3-none-any.whl.metadata (6.9 kB)
		Collecting pygments<3.0.0,>=2.13.0 (from rich>=12.0.0->ansible-lint)
		Downloading pygments-2.19.2-py3-none-any.whl.metadata (2.5 kB)
		Collecting ruamel.yaml.clib>=0.2.7 (from ruamel.yaml>=0.18.5->ansible-lint)
		Downloading ruamel.yaml.clib-0.2.12-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.7 kB)
		Collecting bracex>=2.1.1 (from wcmatch>=8.1.2->ansible-lint)
		Downloading bracex-2.6-py3-none-any.whl.metadata (3.6 kB)
		Requirement already satisfied: MarkupSafe>=2.0 in /usr/local/lib64/python3.9/site-packages (from jinja2>=3.0.0->ansible-core>=2.12.0->ansible-lint) (3.0.2)
		Collecting mdurl~=0.1 (from markdown-it-py>=2.2.0->rich>=12.0.0->ansible-lint)
		Downloading mdurl-0.1.2-py3-none-any.whl.metadata (1.6 kB)
		Requirement already satisfied: cffi>=1.12 in /usr/lib64/python3.9/site-packages (from cryptography->ansible-core>=2.12.0->ansible-lint) (1.14.5)
		Requirement already satisfied: pycparser in /usr/lib/python3.9/site-packages (from cffi>=1.12->cryptography->ansible-core>=2.12.0->ansible-lint) (2.20)
		Requirement already satisfied: ply==3.11 in /usr/lib/python3.9/site-packages (from pycparser->cffi>=1.12->cryptography->ansible-core>=2.12.0->ansible-lint) (3.11)
		Downloading ansible_lint-6.22.2-py3-none-any.whl (297 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 298.0/298.0 kB 17.7 MB/s eta 0:00:00
		Downloading ansible_compat-24.10.0-py3-none-any.whl (24 kB)
		Downloading black-25.1.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_28_x86_64.whl (1.8 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.8/1.8 MB 62.5 MB/s eta 0:00:00
		Downloading filelock-3.19.1-py3-none-any.whl (15 kB)
		Downloading jsonschema-4.25.1-py3-none-any.whl (90 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 90.0/90.0 kB 17.3 MB/s eta 0:00:00
		Downloading pathspec-0.12.1-py3-none-any.whl (31 kB)
		Downloading rich-14.1.0-py3-none-any.whl (243 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 243.4/243.4 kB 53.5 MB/s eta 0:00:00
		Downloading ruamel.yaml-0.18.15-py3-none-any.whl (119 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 119.7/119.7 kB 32.6 MB/s eta 0:00:00
		Downloading subprocess_tee-0.4.2-py3-none-any.whl (5.2 kB)
		Downloading wcmatch-10.1-py3-none-any.whl (39 kB)
		Downloading yamllint-1.37.1-py3-none-any.whl (68 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 68.8/68.8 kB 17.8 MB/s eta 0:00:00
		Downloading attrs-25.3.0-py3-none-any.whl (63 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.8/63.8 kB 15.2 MB/s eta 0:00:00
		Downloading bracex-2.6-py3-none-any.whl (11 kB)
		Downloading click-8.1.8-py3-none-any.whl (98 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.2/98.2 kB 26.2 MB/s eta 0:00:00
		Downloading jsonschema_specifications-2025.4.1-py3-none-any.whl (18 kB)
		Downloading markdown_it_py-3.0.0-py3-none-any.whl (87 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 87.5/87.5 kB 24.4 MB/s eta 0:00:00
		Downloading mypy_extensions-1.1.0-py3-none-any.whl (5.0 kB)
		Downloading platformdirs-4.3.8-py3-none-any.whl (18 kB)
		Downloading pygments-2.19.2-py3-none-any.whl (1.2 MB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 106.3 MB/s eta 0:00:00
		Downloading referencing-0.36.2-py3-none-any.whl (26 kB)
		Downloading rpds_py-0.27.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (383 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 383.6/383.6 kB 65.8 MB/s eta 0:00:00
		Downloading ruamel.yaml.clib-0.2.12-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (724 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 724.9/724.9 kB 89.0 MB/s eta 0:00:00
		Downloading typing_extensions-4.14.1-py3-none-any.whl (43 kB)
		━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.9/43.9 kB 11.9 MB/s eta 0:00:00
		Downloading mdurl-0.1.2-py3-none-any.whl (10.0 kB)
		Installing collected packages: typing-extensions, subprocess-tee, ruamel.yaml.clib, rpds-py, pygments, platformdirs, pathspec, mypy-extensions, mdurl, filelock, click, bracex, attrs, yamllint, wcmatch, ruamel.yaml, referencing, markdown-it-py, black, rich, jsonschema-specifications, jsonschema, ansible-compat, ansible-lint
		Successfully installed ansible-compat-24.10.0 ansible-lint-6.22.2 attrs-25.3.0 black-25.1.0 bracex-2.6 click-8.1.8 filelock-3.19.1 jsonschema-4.25.1 jsonschema-specifications-2025.4.1 markdown-it-py-3.0.0 mdurl-0.1.2 mypy-extensions-1.1.0 pathspec-0.12.1 platformdirs-4.3.8 pygments-2.19.2 referencing-0.36.2 rich-14.1.0 rpds-py-0.27.0 ruamel.yaml-0.18.15 ruamel.yaml.clib-0.2.12 subprocess-tee-0.4.2 typing-extensions-4.14.1 wcmatch-10.1 yamllint-1.37.1

		[notice] A new release of pip is available: 24.0 -> 25.2
		[notice] To update, run: python3 -m pip install --upgrade pip
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ ansible-lint playbook.yaml 
		WARNING  Listing 1 violation(s) that are fatal
		load-failure[runtimeerror]: Failed to load YAML file: playbook.yaml
		playbook.yaml:1 while scanning for the next token
		found character that cannot start any token
		in "<unicode string>", line 26, column 1


							Rule Violation Summary                     
		count tag                        profile rule associated tags 
			1 load-failure[runtimeerror] min     core, unskippable    

		Failed: 1 failure(s), 0 warning(s) on 1 files.
		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ vi playbook.yaml 
		thor@jumphost ~$ 
		thor@jumphost ~$ ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory.ini playbook.yaml

		PLAY [Deploy Nautilus beta Java app on Tomcat] *******************************************************

		TASK [Gathering Facts] *******************************************************************************
		ok: [stapp03]

		TASK [Install Tomcat and required packages] **********************************************************
		changed: [stapp03]

		TASK [Change tomcat port in server.xml] **************************************************************
		changed: [stapp03]

		TASK [Remove old extracted ROOT app folder] **********************************************************
		changed: [stapp03]

		TASK [Copy ROOT.war from jump host to App Server 3] **************************************************
		changed: [stapp03]

		TASK [Enable and start Tomcat service] ***************************************************************
		changed: [stapp03]

		PLAY RECAP *******************************************************************************************
		stapp03                    : ok=6    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

		thor@jumphost ~$ 
		thor@jumphost ~$ 
		thor@jumphost ~$ ssh banner@stapp03
		banner@stapp03's password: 
		Last login: Fri Aug 22 13:19:45 2025 from 172.16.238.3
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ curl http://stapp03:8083
		<!DOCTYPE html>
		<!--
		To change this license header, choose License Headers in Project Properties.
		To change this template file, choose Tools | Templates
		and open the template in the editor.
		-->
		<html>
			<head>
				<title>SampleWebApp</title>
				<meta charset="UTF-8">
				<meta name="viewport" content="width=device-width, initial-scale=1.0">
			</head>
			<body>
				<h2>Welcome to xFusionCorp Industries!</h2>
				<br>
			
			</body>
		</html>
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ 
		[banner@stapp03 ~]$ 


<h3>Day 12: Linux Network Services</h3>
Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue, as its Apache service is not reachable on port 5001 (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp01:5001 command from jump host.

		thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:kzpLpYXmJg1Szy9ZICvev0UOkNwZuGQvgYOUbiSuoYM.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ 

		[tony@stapp01 ~]$ netstat -ntlup
		(No info could be read for "-p": geteuid()=1001 but you should be root.)
		Active Internet connections (only servers)
		Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
		tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
		tcp        0      0 127.0.0.1:3004          0.0.0.0:*               LISTEN      -                   
		tcp        0      0 127.0.0.11:40085        0.0.0.0:*               LISTEN      -                   
		tcp6       0      0 :::22                   :::*                    LISTEN      -                   
		udp        0      0 127.0.0.11:40382        0.0.0.0:*                           -                   
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo systemctl status httpd

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for tony: 
		● httpd.service - The Apache HTTP Server
		Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
		Active: failed (Result: exit-code) since Fri 2025-08-22 13:50:36 UTC; 4min 17s ago
			Docs: man:httpd.service(8)
		Process: 489 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=1/FAILURE)

		Main PID: 489 (code=exited, status=1/FAILURE)
		Status: "Reading configuration..."

		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: (98)Address already in use: AH00072: make_
		sock: could not bind to address 0.0.0.0:3004
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: no listening sockets available, shutting d
		own
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: AH00015: Unable to open logs
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Chi
		ld 489 belongs to httpd.service.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Mai
		n process exited, code=exited, status=1/FAILURE
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Fai
		led with result 'exit-code'.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Cha
		nged start -> failed
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Job
		httpd.service/start finished, result=failed
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Failed to start Th
		e Apache HTTP Server.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Uni
		t entered failed state.
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ sudo journalctl -xe | grep httpd
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd-init.service: Failed to load configuration: No such file or directory
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Trying to enqueue job httpd.service/restart/replace
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd-init.service: Cannot add dependency job, ignoring: Unit httpd-init.service not found.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Installed new job httpd.service/restart as 54
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Enqueued job httpd.service/restart as 54
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Job httpd.service/restart finished, result=done
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Converting job httpd.service/restart -> httpd.service/start
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Failed to reset devices.list: Operation not permitted
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Failed to set invocation ID on control group /docker/9f9a3980c27e7d725cab825d9202fa12b4de79802e068b0bee621b2b887136fd/system.slice/httpd.service, ignoring: Operation not permitted
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Passing 0 fds to service
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: About to execute: /usr/sbin/httpd $OPTIONS -DFOREGROUND
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Forked /usr/sbin/httpd as 489
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Changed dead -> start
		-- Subject: Unit httpd.service has begun start-up
		-- Unit httpd.service has begun starting up.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=13 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=14 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Got message type=method_call sender=n/a destination=org.freedesktop.systemd1 path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=Get cookie=3 reply_cookie=0 signature=ss error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[489]: Successfully mounted /tmp/systemd-private-3de91ca9d8294e25a7fcf63a75afa7a9-httpd.service-GC5pQb/tmp to /run/systemd/unit-root/tmp
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[489]: Successfully mounted /var/tmp/systemd-private-3de91ca9d8294e25a7fcf63a75afa7a9-httpd.service-5QvWjm/tmp to /run/systemd/unit-root/var/tmp
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[489]: httpd.service: Executing: /usr/sbin/httpd -DFOREGROUND
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Got notification message from PID 489 (RELOADING=1, STATUS=Reading configuration...)
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=17 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=18 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using stapp01.stratos.xfusioncorp.com. Set the 'ServerName' directive globally to suppress this message
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: (98)Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:3004
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: no listening sockets available, shutting down
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com httpd[489]: AH00015: Unable to open logs
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Received SIGCHLD from PID 489 (httpd).
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Child 489 (httpd) died (code=exited, status=1/FAILURE)
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Child 489 belongs to httpd.service.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Main process exited, code=exited, status=1/FAILURE
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Failed with result 'exit-code'.
		-- The unit httpd.service has entered the 'failed' state with result 'exit-code'.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Changed start -> failed
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Job httpd.service/start finished, result=failed
		-- Subject: Unit httpd.service has failed
		-- Unit httpd.service has failed.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: Unit entered failed state.
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Spawning thread to nuke /tmp/systemd-private-3de91ca9d8294e25a7fcf63a75afa7a9-httpd.service-GC5pQb
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Spawning thread to nuke /var/tmp/systemd-private-3de91ca9d8294e25a7fcf63a75afa7a9-httpd.service-5QvWjm
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=21 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Sent message type=signal sender=org.freedesktop.systemd1 destination=n/a path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=PropertiesChanged cookie=22 reply_cookie=0 signature=sa{sv}as error-name=n/a error-message=n/a
		Aug 22 13:50:36 stapp01.stratos.xfusioncorp.com systemd[1]: Got message type=method_call sender=n/a destination=org.freedesktop.systemd1 path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=Get cookie=4 reply_cookie=0 signature=ss error-name=n/a error-message=n/a
		Aug 22 13:54:53 stapp01.stratos.xfusioncorp.com sudo[606]:     tony : TTY=pts/0 ; PWD=/home/tony ; USER=root ; COMMAND=/bin/systemctl status httpd
		Aug 22 13:54:53 stapp01.stratos.xfusioncorp.com dbus-daemon[570]: [system] Activating via systemd: service name='org.freedesktop.login1' unit='dbus-org.freedesktop.login1.service' requested by ':1.4' (uid=0 pid=606 comm="sudo systemctl status httpd " label="unconfined")
		Aug 22 13:54:53 stapp01.stratos.xfusioncorp.com systemd[1]: Got message type=method_call sender=n/a destination=org.freedesktop.systemd1 path=/org/freedesktop/systemd1/unit/httpd_2eservice interface=org.freedesktop.DBus.Properties member=GetAll cookie=1 reply_cookie=0 signature=s error-name=n/a error-message=n/a
		Aug 22 13:54:53 stapp01.stratos.xfusioncorp.com systemd[1]: Preset files say disable httpd.service.

		[tony@stapp01 ~]$ sudo journalctl -xe | grep httpd
		[tony@stapp01 ~]$ sudo netstat -tulpn | grep :3004
		[tony@stapp01 ~]$ sudo systemctl stop sendmail
		[tony@stapp01 ~]$ sudo netstat -tulpn | grep :3004
		[tony@stapp01 ~]$ sudo systemctl start httpd
		[tony@stapp01 ~]$ sudo netstat -tulpn
		[tony@stapp01 ~]$ sudo iptables -L -n
		[tony@stapp01 ~]$ sudo iptables -I INPUT 4 -p tcp --dport 3004 -j ACCEPT
		[tony@stapp01 ~]$ sudo service iptables save
		[tony@stapp01 ~]$ logout

		thor@jumphost ~$ curl http://stapp01:3004


<h3></h3>
