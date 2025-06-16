# 90 Days of Kubernetes Learning

## Day 1: Getting Started

### Task
1. Install minikube/kind
2. Deploy an Nginx pod + service
3. Push manifests to GitHub

### Solution
- Created basic Nginx manifests with external access service (includes detailed comments)
- Set up working environment for future tasks

### Environment Setup
- **WSL**: Oracle Enterprise Linux 8 (OEL8)
- **Kubernetes**: Kind cluster
- **Tools**:
  - Docker Desktop
  - Visual Studio Code
  - GitHub Desktop  

---   
## Day 2:   
### Task  
Task: Deploy a StatefulSet for MySQL with PersistentVolume
Requirements:

Database password must be stored in a Secret.

Configuration (username, database name) must be stored in a ConfigMap.

Implement Liveness and Readiness probes.

### Exampl to connect from another pod whith mysql-client
Вот как можно запустить тестовый под:

```bash

kubectl run mysql-client --rm -it --image=mysql:5.7 -- bash
После запуска внутри bash:

mysql -h mysql-0.mysql -u myuser -p
# Введи пароль: 
```

