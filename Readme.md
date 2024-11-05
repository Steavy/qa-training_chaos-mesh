# Chaos Testing with Mesh and Kubernetes on Windows
https://github.com/Steavy/qa-training_chaos-mesh

## installation
install choco for windows (https://chocolatey.org/install)

install helm (choco install kubernetes-helm)

(Mocht je geen kubernetes onder Docker voor Windows hebben draaien voer dan onderstaande 2 stappen -- eerst uit)
--install minikube (https://minikube.sigs.k8s.io/docs/start)
--minikube start

install chaos mesh (https://chaos-mesh.org/docs/production-installation-using-helm)

## run first experiment
git clone this repo

cmd into this git repo path

kubectl apply -f network-delay.yaml

kubectl describe networkchaos network-delay

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
