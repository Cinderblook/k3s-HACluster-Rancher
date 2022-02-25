# Deploying Rancher on Workers
This deployment will be using the self-generated Rancher Certificate. <br>
Hop on a Server Node, or client connected to kubectl cluster and do the following:
1. Adding Helm Chart Repository
    - Use Stable release: `helm repo add rancher-stable https://releases.rancher.com/server-charts/stable`
2. Create Namespace within K3s for Rancher
    - `kubectl create namespace cattle-system`
3. Install Cert Manager (Required for self-hosted cert)
    - `kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.5.1/cert-manager.crds.yaml`
    - `helm repo add jetstack https://charts.jetstack.io`
    -  `helm repo update`
    - ```
       helm install cert-manager jetstack/cert-manager \
        --namespace cert-manager \
        --create-namespace \
        --version v1.5.1```
    - Verify it is working w/ `kubectl get pods --namespace cert-manager`
4. Install Rancher using Helm
    - ```
        helm install rancher rancher-stable/rancher \
        --namespace cattle-system \
        --set hostname=rancher.my.org \
        --set replicas=3
    - Check on deployment w/ `kubectl -n cattle-system rollout status deploy/rancher`
    - Once finished, obtain info on deployment w/ `kubectl -n cattle-system get deploy rancher`
5. 