# Proof of Concept: GitOps з ArgoCD для AsciiArtify

## 🧭 Мета

На етапі PoC команда AsciiArtify перевіряє можливість реалізації GitOps-підходу для керування розгортанням застосунків у Kubernetes. Обраний інструмент — **ArgoCD**, який забезпечує автоматичне синхронізоване розгортання з Git-репозиторію.

## ⚙️ Розгортання Kubernetes-кластеру

Кластер створено за допомогою інструменту **Kind**, рекомендованого на етапі Concept:

kind create cluster --name asciiartify

## 🚀 Встановлення ArgoCD
ArgoCD встановлено у кластер за допомогою офіційного маніфесту:

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## ⏳ Перевірка статусу
Очікуємо, поки всі поди перейдуть у статус Running:

kubectl get pods -n argocd

## 🌐 Доступ до графічного інтерфейсу ArgoCD
Портфорвардинг для доступу до веб-інтерфейсу:

kubectl port-forward svc/argocd-server -n argocd 8080:443

Інтерфейс доступний за адресою: https://localhost:8080

## 🔐 Авторизація
Ім’я користувача: admin

Пароль:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

## 🎬 Демонстрація
Запис виконано за допомогою Asciinema. У ньому показано повний процес створення кластера, встановлення ArgoCD, доступ до інтерфейсу та авторизація.

📽️ Переглянути демо на Asciinema:

https://asciinema.org/a/oYk5NDoIs2jXJnI0YQOHspfBJ

## 🧹 Завершення PoC
Після завершення демонстрації кластер було видалено:

kind delete cluster --name asciiartify

