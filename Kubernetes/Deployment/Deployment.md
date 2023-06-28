# 1️⃣Steps
- Build image
- Push image to Docker hub
- minikube start --driver=docker
- kubectl create deployment NAME --image=DOCKER_HUB_IMAGE
- kubectl expose NAME --type=LoadBalancer/ClusterIP/NodePort --port PORT
- minikube service NAME
- minikube dashboard
- kubectl scale deployment/NAME --replicas=NUMBER_OF_REPLICAS