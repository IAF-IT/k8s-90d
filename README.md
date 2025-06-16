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

### Backup and Restore
Backup MySQL Database
Create a dump file from the running MySQL pod:

```bash
kubectl exec mysql-0 -- mysqldump -u root -p$(kubectl get secret mysql-secret -o jsonpath='{.data.password}' | base64 -d) app_db > backup.sql
Copy the backup locally:


kubectl cp mysql-0:backup.sql ./backup.sql
Restore MySQL Database
Copy the backup file to a new pod:


kubectl cp ./backup.sql mysql-0:/tmp/backup.sql
Restore the database:


kubectl exec mysql-0 -- mysql -u root -p$(kubectl get secret mysql-secret -o jsonpath='{.data.password}' | base64 -d) app_db < /tmp/backup.sql
``` 

# Automated Deployment  
kubectl delete namespace mysql-ns  # Удалит ВСЕ ресурсы в namespace

### Requirements  
- Ansible 2.14+  
- kubectl configured with cluster access  

### Usage  
```bash  
cd automation  
ansible-playbook deploy_mysql_stack.yml
```
```
TASK [Show connection string] ***********************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "mysql -h mysql-0.mysql.mysql-ns.svc.cluster.local -u"
}
```
playbook deployed to 1,5 min. 

✅ Success Criteria:

MySQL pod becomes Ready within 3 minutes

You can connect using generated credentials

Data persists after pod restart

## ✅ Критерии успешной установки

- [x] MySQL Pod успешно создаётся в `default` namespace
- [x] Проверка подключения к MySQL выполняется через `mysqladmin`/`mysql`
- [x] Данные в БД сохраняются после удаления Pod (тест персистентности)
- [x] Плейбук завершает установку за ~50 секунд

### 💾 Требования

- Kubernetes кластер с настроенным `default` StorageClass
- Доступный `kubectl` с контекстом, указывающим на нужный кластер
- Установлен `ansible` и `kubernetes.core`:
  ```bash
  ansible-galaxy collection install kubernetes.core
