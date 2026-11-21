# Л09: Kubernetes basics

## Цель
Изучить базовые объекты Kubernetes (Pod, Deployment, Service). Научиться применять манифесты, выполнять rolling update и rollback приложений.

## Файлы проекта
- `deployment.yaml` — манифест для развертывания 3 реплик Nginx.
- `service.yaml` — манифест для создания сервиса типа NodePort.

## Ход выполнения

### 1. Развертывание приложения
Применены манифесты с помощью `kubectl apply`. Кластер (Minikube) успешно создал 3 пода (реплики) и сервис для доступа к ним.
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
<img width="861" height="258" alt="Снимок экрана 2026-11-21 154329" src="https://github.com/user-attachments/assets/5fc1238e-8796-44b3-8996-de700a0a9d59" />

### 2. Проверка доступности
С помощью minikube service получен URL и выполнен curl к приложению. Сервер Nginx отвечает.
<img width="876" height="722" alt="Снимок экрана 2026-11-21 154609" src="https://github.com/user-attachments/assets/b91644c5-948e-469f-be20-8852625084a7" />

### 3.Rolling Update (Обновление)
Выполнено обновление версии образа Nginx (с 1.14.2 на 1.16.1). Kubernetes плавно, без простоя, заменил старые поды на новые.
```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```
<img width="853" height="232" alt="Снимок экрана 2026-11-21 154836" src="https://github.com/user-attachments/assets/f26cf3de-5657-4a4c-a5b6-d5ce55fd9b62" />

### 4. Rollback (Откат)
Выполнен откат на предыдущую версию с помощью команды kubectl rollout undo.
<img width="873" height="113" alt="Снимок экрана 2026-11-21 154941" src="https://github.com/user-attachments/assets/7c0082ab-f65f-45d7-ac21-bb86ad6ea380" />

## Итог
Отработаны команды kubectl apply, get, set image, rollout. Изучен принцип декларативного управления кластером и жизненный цикл деплоймента.
