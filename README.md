репозиторий 90 дней обучения k8s: 
1 день:
  Задача:
    Установи minikube/kind.
    Разверни nginx pod + service.
    Запушь манифесты в GitHub.
  Решение:
    - Элементарные nginx манифест и сервис доступа снаружи для nginx + коментарии.
    - Подготовил среду для дальнейшей работы. 



Работа ведется в wls oel8 kind + docker desktop + visualSC + gitHUB desktop



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

## Implementation Details

### Nginx Deployment
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80