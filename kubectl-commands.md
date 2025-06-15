# Kubernetes Quick Commands

## Deploy
```bash
# Create Nginx pod
kubectl apply -f nginx-pod.yaml

# Expose as Service
kubectl apply -f nginx-service.yaml
```
## Access
```bash
# Forward port 8080 → Service 80
kubectl port-forward svc/nginx-service 8080:80
```
Access at: http://localhost:8080  
Ctrl+C to stop

## Verify
```bash
kubectl get pods
kubectl get svc
```
## Tips
```bash
# Apply both at once
kubectl apply -f nginx-pod.yaml -f nginx-service.yaml

# Background forwarding
kubectl port-forward svc/nginx-service 8080:80 &
```
💡 Service type defaults to ClusterIP (internal access). Use NodePort for external access