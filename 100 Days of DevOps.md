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

	