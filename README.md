# EFK on Kubernetes 

Start with PV settings after mapping the appropriate files. Make sure you have the nfs utils on the host.

## Commands

```bash
kubectl apply -f pv.yaml
kubectl create -f kube-logging.yaml
kubectl create -f elasticsearch_svc.yaml

kubectl get services --namespace=kube-logging
kubectl create -f elasticsearch_statefulset.yaml
kubectl rollout status sts/es-cluster --namespace=kube-logging

kubectl port-forward es-cluster-0 9200:9200 --namespace=kube-logging
curl http://localhost:9200/_cluster/state?pretty

kubectl create -f kibana.yaml
kubectl get pods --namespace=kube-logging

kubectl port-forward kibana-6c9fb4b5b7-plbg2 5601:5601 --namespace=kube-logging
```
