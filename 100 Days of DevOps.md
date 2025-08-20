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
	The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named media_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).
	a. Create a zip archive named xfusioncorp_media.zip of /var/www/html/media directory.
	b. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.
	c. Copy the created archive to Nautilus Backup Server server in /backup/ location.
	d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

		thor@jumphost ~$ ssh tony@stapp01
		The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
		ED25519 key fingerprint is SHA256:yHfHGhqXCBD4DoZFPnUf9hRwq0W6xDOIQFAWdsrsnEI.
		This key is not known by any other names
		Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
		Warning: Permanently added 'stapp01' (ED25519) to the list of known hosts.
		tony@stapp01's password: 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ vi /scripts/official_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ping stbkp01
		ping: socket: Operation not permitted
		[tony@stapp01 ~]$ ping 172.16.238.16
		ping: socket: Operation not permitted
		[tony@stapp01 ~]$ sudo ping 172.16.238.16

		We trust you have received the usual lecture from the local System
		Administrator. It usually boils down to these three things:

			#1) Respect the privacy of others.
			#2) Think before you type.
			#3) With great power comes great responsibility.

		[sudo] password for tony: 
		.PING 172.16.238.16 (172.16.238.16) 56(84) bytes of data.
		64 bytes from 172.16.238.16: icmp_seq=1 ttl=64 time=0.127 ms
		64 bytes from 172.16.238.16: icmp_seq=2 ttl=64 time=0.070 ms
		64 bytes from 172.16.238.16: icmp_seq=3 ttl=64 time=0.052 ms
		64 bytes from 172.16.238.16: icmp_seq=4 ttl=64 time=0.064 ms
		^C
		--- 172.16.238.16 ping statistics ---
		4 packets transmitted, 4 received, 0% packet loss, time 3049ms
		rtt min/avg/max/mdev = 0.052/0.078/0.127/0.029 ms
		[tony@stapp01 ~]$ cat /scripts/official_backup.sh
		#! /bin/bash
		tar cvzf xfusioncorp_official.zip /var/www/html/official
		mv xfusioncorp_official.zip /backup/
		scp /backup/xfusioncorp_official.zip clint@stbkp01:/backup/
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ chmod +x /scripts/official_backup.sh
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh-keygen
		Generating public/private rsa key pair.
		Enter file in which to save the key (/home/tony/.ssh/id_rsa): 
		Created directory '/home/tony/.ssh'.
		Enter passphrase (empty for no passphrase): 
		Enter same passphrase again: 
		Your identification has been saved in /home/tony/.ssh/id_rsa.
		Your public key has been saved in /home/tony/.ssh/id_rsa.pub.
		The key fingerprint is:
		SHA256:bV7vq3N7s9TAN1FALGwtpDhav10aMauNpiE6RPHSnqA tony@stapp01.stratos.xfusioncorp.com
		The key's randomart image is:
		+---[RSA 2048]----+
		|           o.+o..|
		|    .    . .= o .|
		|     +  + ..oo . |
		|    + oo +   =  .|
		|   o +..S + + +..|
		|  E . o  o B = oo|
		|   .  . . * + ...|
		|    .. . +  ..o..|
		|    ..  .   .++=o|
		+----[SHA256]-----+
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh-copy-id clint@stbkp01
		/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/tony/.ssh/id_rsa.pub"
		The authenticity of host 'stbkp01 (172.16.238.16)' can't be established.
		ECDSA key fingerprint is SHA256:rZFSbspebX+RHY8dKacYCNxFEcP0kQwPjh+G54CwXOY.
		ECDSA key fingerprint is MD5:49:e3:31:8f:b9:e8:30:13:17:80:03:40:64:df:fd:44.
		Are you sure you want to continue connecting (yes/no)? yes
		/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
		/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
		clint@stbkp01's password: 

		Number of key(s) added: 1

		Now try logging into the machine, with:   "ssh 'clint@stbkp01'"
		and check to make sure that only the key(s) you wanted were added.

		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /var/www/html/official
		total 12
		drwxr-xr-x 2 root   root   4096 Aug 17 03:02 .
		drwxr-xr-x 1 apache apache 4096 Aug 17 03:10 ..
		-rw-r--r-- 1 root   root      0 Aug 17 03:02 .gitkeep
		-rw-r--r-- 1 root   root     42 Aug 17 03:10 index.html
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /backup/
		total 8
		drwxrwxrwx 2 root root 4096 Aug 17 03:10 .
		drwxr-xr-x 1 root root 4096 Aug 17 03:18 ..
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ pwd
		/home/tony
		[tony@stapp01 ~]$ /scripts/official_backup.sh 
		tar: Removing leading `/' from member names
		/var/www/html/official/
		/var/www/html/official/.gitkeep
		/var/www/html/official/index.html
		xfusioncorp_official.zip                     100%  224   788.3KB/s   00:00    
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /var/www/html/official
		total 12
		drwxr-xr-x 2 root   root   4096 Aug 17 03:02 .
		drwxr-xr-x 1 apache apache 4096 Aug 17 03:10 ..
		-rw-r--r-- 1 root   root      0 Aug 17 03:02 .gitkeep
		-rw-r--r-- 1 root   root     42 Aug 17 03:10 index.html
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ls -la /backup/
		total 12
		drwxrwxrwx 2 root root 4096 Aug 17 03:23 .
		drwxr-xr-x 1 root root 4096 Aug 17 03:18 ..
		-rw-rw-r-- 1 tony tony  224 Aug 17 03:23 xfusioncorp_official.zip
		[tony@stapp01 ~]$ 
		[tony@stapp01 ~]$ ssh 'clint@stbkp01'
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ ls -la /backup/
		total 28
		drwxrwxrwx 2 root  root   4096 Aug 17 03:23 .
		drwxr-xr-x 1 root  root  20480 Aug 17 03:24 ..
		-rw-r--r-- 1 clint clint   224 Aug 17 03:23 xfusioncorp_official.zip
		[clint@stbkp01 ~]$ 
		[clint@stbkp01 ~]$ 	


<h3></h3>


<h3></h3>
<h3></h3>
