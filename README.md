# demo-tkg-efk
## What's this?
Sample kubernetes manifests of elasticsearch, fluent bit, and kibana for TKG (Tanzu Kubernetes Grid) clusters.
This repo covers only elasticsearch and kibana. To deploy Fluent bit please read the official TKG document below.
https://docs.vmware.com/en/VMware-Tanzu-Kubernetes-Grid/1.0/vmware-tanzu-kubernetes-grid-10/GUID-manage-instance-logging-elasticsearch.html

## How to use
- es-kb-deployment.yaml  
You can deploy elasticsearch and kibana via "kubectl apply -f es-kb-deployment.yaml"  
After that you access to the worker node where elasticsearch and kibana Pods are running, with nodePort 30201 or 30202.  
http://$YOUR_WORKER_NODE_IP:30201 (elasticsearch)  
http://$YOUR_WORKER_NODE_IP:30202 (kibana)  

If you want to deploy fluent bit on a workload cluster, and elasticsearch and kibana on your management cluster, fluent bit fails to name resolutions of elasticsearch because they use diffefent kube-dns.  
To solve this problem, nodePort services are used, and Host and Port settings of the configMap of fluent bit have to be pointed to nodePort as follows:  
- 04-fluent-bit-configmap.yaml  
Host     $YOUR_WORKER_NODE_IP  
Port     30201  
