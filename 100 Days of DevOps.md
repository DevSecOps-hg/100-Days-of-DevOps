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

	thor@jumphost ~$ ssh steve@stapp02
	The authenticity of host 'stapp02 (172.16.238.11)' can't be established.
	ED25519 key fingerprint is SHA256:Gp9F345hUHCwu2muzQigkuHnfwDdyrkDURMs7f9ucaI.
	This key is not known by any other names
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'stapp02' (ED25519) to the list of known hosts.
	steve@stapp02's password: 
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$ ls -la /tmp/xfusioncorp.sh
	---------- 1 root root 40 Aug  9 00:12 /tmp/xfusioncorp.sh
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$ chmod 111 /tmp/xfusioncorp.sh
	chmod: changing permissions of '/tmp/xfusioncorp.sh': Operation not permitted
	[steve@stapp02 ~]$ sudo chmod 111 /tmp/xfusioncorp.sh

	We trust you have received the usual lecture from the local System
	Administrator. It usually boils down to these three things:

		#1) Respect the privacy of others.
		#2) Think before you type.
		#3) With great power comes great responsibility.

	[sudo] password for steve: 
	[steve@stapp02 ~]$ 
	[steve@stapp02 ~]$ ls -la /tmp/xfusioncorp.sh
	---x------ 1 root root 40 Aug  9 00:12 /tmp/xfusioncorp.sh
	[steve@stapp02 ~]$ 

	[steve@stapp02 ~]$ sudo chmod a+x /tmp/xfusioncorp.sh
	[steve@stapp02 ~]$ ls -la /tmp/xfusioncorp.sh
	---x--x--x 1 root root 40 Aug  9 00:12 /tmp/xfusioncorp.sh
	[steve@stapp02 ~]$ 


