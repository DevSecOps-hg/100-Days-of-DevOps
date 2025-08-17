<h3>1 Deploy Pods in Kubernetes Cluster</h3>

<h3>2 Deploy Applications with Kubernetes Deployments</h3>

<h3>3 Setup Kubernetes Namespaces and PODs</h3>

<h3>4 Set Resource Limits in Kubernetes Pods</h3>
	
<h3>5 Execute Rolling Updates in Kubernetes</h3>

<h3>6 Revert Deployment to Previous Version in Kubernetes</h3>

<h3>7 Deploy ReplicaSet in Kubernetes Cluster</h3>
The Nautilus DevOps team is gearing up to deploy applications on a Kubernetes cluster for migration purposes. A team member has been tasked with creating a ReplicaSet outlined below:

Create a ReplicaSet using httpd image with latest tag (ensure to specify as httpd:latest) and name it httpd-replicaset.
Apply labels: app as httpd_app, type as front-end.
Name the container httpd-container. Ensure the replica count is 4.
Note: The kubectl utility on jump_host is set up to interact with the Kubernetes cluster.	
	
	thor@jumphost ~$ k create deployment httpd-replicaset --image httpd:latest --replicas 4 --dry-run=client -o yaml > rs.yaml
			
	thor@jumphost ~$ cat rs.yaml 
	apiVersion: apps/v1
	kind: ReplicaSet				-- change
	metadata:
	  creationTimestamp: null
	  labels:
		app: httpd-replicaset
		app: httpd_app				-- add
		type: front-end				-- add
	  name: httpd-replicaset
	spec:
	  replicas: 4
	  selector:
		matchLabels:
		  app: httpd-replicaset
		  app: httpd_app			-- add
		  type: front-end			-- add
	  template:
		metadata:
		  creationTimestamp: null
		  labels:
			app: httpd-replicaset
			app: httpd_app			-- add
			type: front-end			-- add
		spec:
		  containers:
		  - image: httpd:latest
			name: httpd-container	-- change
			resources: {}
	status: {}


<h3>8 Schedule Cronjobs in Kubernetes</h3>
The Nautilus DevOps team is setting up recurring tasks on different schedules. Currently, they're developing scripts to be executed periodically. To kickstart the process, they're creating cron jobs in the Kubernetes cluster with placeholder commands. Follow the instructions below:

Create a cronjob named datacenter.
Set Its schedule to something like */4 * * * *. You can set any schedule for now.
Name the container cron-datacenter.
Utilize the nginx image with latest tag (specify as nginx:latest).
Execute the dummy command echo Welcome to xfusioncorp!.
Ensure the restart policy is OnFailure.
Note: The kubectl utility on jump_host is configured to work with the kubernetes cluster.

	thor@jumphost ~$ k create cj nautilus --schedule "*/3 * * * *" --image nginx:latest --dry-run=client -o yaml -- echo "Welcome to xfusioncorp!" > cj.yaml

	thor@jumphost ~$ cat cj.yaml
	apiVersion: batch/v1
	kind: CronJob
	metadata:
	  creationTimestamp: null
	  name: nautilus
	spec:
	  jobTemplate:
		metadata:
		  creationTimestamp: null
		  name: nautilus
		spec:
		  template:
			metadata:
			  creationTimestamp: null
			spec:
			  containers:
			  - command:
				- echo
				- Welcome to xfusioncorp!
				image: nginx:latest
				name: cron-nautilus
				resources: {}
			  restartPolicy: OnFailure
	  schedule: '*/3 * * * *'
	status: {}


<h3>9 Create Countdown Job in Kubernetes</h3>
The Nautilus DevOps team is crafting jobs in the Kubernetes cluster. While they're developing actual scripts/commands, they're currently setting up templates and testing jobs with dummy commands. Please create a job template as per details given below:

Create a job named countdown-devops.
The spec template should be named countdown-devops (under metadata), and the container should be named container-countdown-devops
Utilize image debian with latest tag (ensure to specify as debian:latest), and set the restart policy to Never.
Execute the command sleep 5

Note: The kubectl utility on jump_host is set up to operate with the Kubernetes cluster.

	thor@jumphost ~$ cat job.yaml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  creationTimestamp: null
	  name: countdown-devops
	spec:
	  template:
		metadata:
		  creationTimestamp: null
		  name: countdown-devops
		spec:
		  containers:
		  - command:
			- sleep
			- "5"
			image: debian:latest
			name: container-countdown-devops
			resources: {}
		  restartPolicy: Never
	status: {}
