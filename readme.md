Install helm on the machine
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# list to variable input 
helm show values ingress-nginx/ingress-nginx
# helm install--
  helm install ingress-nginx ingress-nginx/ingress-nginx \
    --namespace ingress-basic \
    --set controller.replicaCount=2 \
    --set controller.nodeSelector."kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
    --set controller.service.externalTrafficPolicy=Local \
    --set controller.service.loadBalancerIP="52.154.156.139"     # put LB IP
# verifiy the ingress resources pod, svc etc
kubectl get service -l app.kubernetes.io/name=ingress-nginx --namespace ingress-basic
# List Pods
kubectl get pods -n ingress-basic
kubectl get all -n ingress-basic
# Access Public IP
http://<Public-IP-created-for-Ingress>
