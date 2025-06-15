kubectl apply -f nginx-pod.yaml  
kubectl apply -f nginx-service.yaml
kubectl port-forward svc/nginx-service 8080:80 # пробрасывает порт 8080 на вашей локальной машине к порту 80 Service'а в кластере. http://localhost:8080