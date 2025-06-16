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

## day 2  
Deployment Steps
Create the Secret:

```bash
kubectl apply -f mysql-secret.yaml
Create the ConfigMap:


kubectl apply -f mysql-config.yaml
Deploy the StatefulSet:


kubectl apply -f mysql-statefulset.yaml
```
💡 Note: Replace your_secure_password with a strong password before deployment. Storage size (5Gi) can be adjusted as needed.

