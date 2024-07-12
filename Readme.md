# Chaos Testing with Mesh and Cubernetes
https://github.com/dhomi/qa-training_chaos-mesh

## installation
install docker
install kubernetes (voor mac os de minicube op https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fhomebrew)
install helm https://helm.sh/docs/intro/install/
install chaos mesh https://chaos-mesh.org/docs/simulate-pod-chaos-on-kubernetes/

## run in mac os
minikube start

### to enable the dashboard
helm upgrade chaos-mesh chaos-mesh/chaos-mesh -n=chaos-mesh --version 2.6.3 --set dashboard.securityMode=false

kubectl port-forward -n chaos-mesh svc/chaos-dashboard 2333:2333

dashboard is dus hier te zien: http://127.0.0.1:2333/


## create a helm pod with ngnix
(read: https://scribe.rip/@muppedaanvesh/deploying-nginx-on-kubernetes-a-quick-guide-04d533414967?)

met de hand:
kubectl apply -f nginx-pod.yaml -n chaos-mesh
kubectl get pods -n chaos-mesh
kubectl apply -f nginx-service.yaml -n chaos-mesh
kubectl get svc -n chaos-mesh
minikube service nginx-svc --url http://127.0.0.1:80 -n chaos-mesh

nu een pod-kill experiment uitveren
TODO: time in sec. in de pod-kill experiment invoeren

kubectl get svc -n chaos-mesh
kubectl get pods -n chaos-mesh 
