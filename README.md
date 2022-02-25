# Getting started with K3S
The primary goal here is to setup a functional highly available K3S cluster. This will include 4 necessary steps:
1. Setup a NGINX loadbalancer
2. Setup a mysql database.
3. Configure Kubernetes
4. Setup Rancher
5. (Optional) Setup management from dev machine (Outside of cluster)

I go into further detail with each step within the steps respective folder.

## Useful Docker Commands
- The load balancer and database are setup using Docker-compose
	- Useful Docker compose commands:
	```bash
		# Sping up a docker based on docker-compose.yml file
		docker-compose -f
		# Find list of running docker processes
		docker ps
		# Get into shell of a running docker
		docker exec -it [option] bash
		# Update running docker with new configuration changes
		docker-compose up -d --force-recreate
	```
## Useful Kubectl Commands
- Kubernetes commands (Mostly pulled from [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/))
	- Finding ressources
	 ```bash
	# Get commands with basic output
	kubectl config view 						  # Show Merged kubeconfig settings.
	kubeclt get nodes							  # Show all nodes in the cluster
	kubectl get services                          # List all services in the namespace
	kubectl get pods --all-namespaces             # List all pods in all namespaces
	kubectl get pods -o wide                      # List all pods in the current namespace, with more details
	kubectl get deployment my-dep                 # List a particular deployment
	kubectl get pods                              # List all pods in the namespace
	kubectl get pod my-pod -o yaml                # Get a pod's YAML```

	# Describe commands with verbose output
	kubectl describe nodes my-node
	kubectl describe pods my-pod

	# List Services Sorted by Name
	kubectl get services --sort-by=.metadata.name
	```
	- Updating resources
	```bash
	kubectl set image deployment/frontend www=image:v2               # Rolling update "www" containers of "frontend" deployment, 	updating the image
	kubectl rollout history deployment/frontend                      # Check the history of deployments including the revision 
	kubectl rollout undo deployment/frontend                         # Rollback to the previous deployment
	kubectl rollout undo deployment/frontend --to-revision=2         # Rollback to a specific revision
	kubectl rollout status -w deployment/frontend                    # Watch rolling update status of "frontend" deployment until 	completion
	kubectl rollout restart deployment/frontend                      # Rolling restart of the "frontend" deployment
	```

## Resources
- Shout out to [TheQuib](https://github.com/TheQuib/k3s) I thank him for his collaboration on this
- Rancher [Documentation](https://rancher.com/docs/k3s/latest/en/)
- Docker Compose [Documentation](https://docs.docker.com/compose/)

