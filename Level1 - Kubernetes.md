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

	thor@jumphost ~$ k create job countdown-devops --image debian:latest --dry-run=client -o yaml -- sleep 5 > job.yaml

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
		  name: countdown-devops	-- add
		spec:
		  containers:
		  - command:
			- sleep
			- "5"
			image: debian:latest
			name: container-countdown-devops -- change
			resources: {}
		  restartPolicy: Never
	status: {}


<h3>10 Set Up Time Check Pod in Kubernetes</h3>
The Nautilus DevOps team needs a time check pod created in a specific Kubernetes namespace for logging purposes. Initially, it's for testing, but it may be integrated into an existing cluster later. Here's what's required:

Create a pod called time-check in the datacenter namespace. The pod should contain a container named time-check, utilizing the busybox image with the latest tag (specify as busybox:latest).

Create a config map named time-config with the data TIME_FREQ=10 in the same namespace.

Configure the time-check container to execute the command: while true; do date; sleep $TIME_FREQ;done. Ensure the result is written /opt/devops/time/time-check.log. Also, add an environmental variable TIME_FREQ in the container, fetching its value from the config map TIME_FREQ key.

Create a volume log-volume and mount it at /opt/devops/time within the container.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

	thor@jumphost ~$ k get ns
	NAME                 STATUS   AGE
	default              Active   19m
	kube-node-lease      Active   19m
	kube-public          Active   19m
	kube-system          Active   19m
	local-path-storage   Active   18m
	thor@jumphost ~$ 
	thor@jumphost ~$ k create ns datacenter
	namespace/datacenter created
	thor@jumphost ~$
	thor@jumphost ~$ k -n datacenter create cm time-config --from-literal TIME_FREQ=10
	configmap/time-config created
	thor@jumphost ~$ 
	thor@jumphost ~$ k -n datacenter get cm
	NAME               DATA   AGE
	kube-root-ca.crt   1      103s
	time-config        1      7s
	thor@jumphost ~$ k -n datacenter run time-check --image busybox:latest --command -- sh -c "while true; do date; sleep $TIME_FREQ;done" --dry-run=client -o yaml > pod.yaml
	thor@jumphost ~$ 
	thor@jumphost ~$ k -n datacenter run time-check --image busybox:latest --dry-run=client -o yaml --command -- sh -c "while true; do date; sleep $TIME_FREQ;done" > pod.yaml
	thor@jumphost ~$ cat pod.yaml 
	thor@jumphost ~$ cat pod.yaml 
	apiVersion: v1
	kind: Pod
	metadata:
	creationTimestamp: null
	labels:
		run: time-check
	name: time-check
	namespace: datacenter
	spec:
	containers:
	- command:
		- sh
		- -c
		- while true; do date; sleep ;done > /opt/devops/time/time-check.log
		env:
		- name: TIME_FREQ
		valueFrom:
			configMapKeyRef:
			name: time-config
			key: TIME_FREQ
		volumeMounts:
		- name: log-volume
		mountPath: /opt/devops/time
		image: busybox:latest
		name: time-check
		resources: {}
	volumes:
		- name: log-volume
		emptyDir: {}
	dnsPolicy: ClusterFirst
	restartPolicy: Always
	status: {}
	thor@jumphost ~$ k -n datacenter get po,cm
	NAME             READY   STATUS    RESTARTS   AGE
	pod/time-check   1/1     Running   0          57s

	NAME                         DATA   AGE
	configmap/kube-root-ca.crt   1      18m
	configmap/time-config        1      17m


<h3>11 Resolve Pod Deployment Issue</h3>
A junior DevOps team member encountered difficulties deploying a stack on the Kubernetes cluster. The pod fails to start, presenting errors. Let's troubleshoot and rectify the issue promptly.

There is a pod named webserver, and the container within it is named httpd-container, its utilizing the httpd:latest image.

Additionally, there's a sidecar container named sidecar-container using the ubuntu:latest image.

Identify and address the issue to ensure the pod is in the running state and the application is accessible.

Note: The kubectl utility on jump_host is configured to interact with the Kubernetes cluster.

	thor@jumphost ~$ k get po
	NAME        READY   STATUS             RESTARTS   AGE
	webserver   1/2     ImagePullBackOff   0          78s
	thor@jumphost ~$ 
	thor@jumphost ~$ k logs webserver 
	Defaulted container "httpd-container" out of: httpd-container, sidecar-container
	Error from server (BadRequest): container "httpd-container" in pod "webserver" is waiting to start: trying and failing to pull image
	thor@jumphost ~$ 
	thor@jumphost ~$ k edit po webserver  -- change the 'httpd:latests' to 'httpd:latest'
	pod/webserver edited
	thor@jumphost ~$ 
	thor@jumphost ~$ k get po -w
	NAME        READY   STATUS             RESTARTS   AGE
	webserver   1/2     ImagePullBackOff   0          3m40s
	webserver   2/2     Running            0          3m41s
	^Cthor@jumphost ~$ 
	thor@jumphost ~$ 
	thor@jumphost ~$ 


<h3>12 Update Deployment and Service in Kubernetes</h3>

<h3>13 Deploy Highly Available Pods with ReplicationController</h3>

<h3>14 Resolve VolumeMounts Issue in Kubernetes</h3>