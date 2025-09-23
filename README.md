# Blue/Green Helm Demo

## Build Docker Images
# From the 'app' directory
docker build -t tinyapp:blue .
docker build -t tinyapp:green .

## Start local Kubernetes (k3s, Minikube, or kind)
# Example: Minikube
minikube start

## Deploy with Blue Active
helm upgrade --install app ./chart -n demo --create-namespace --set activeColor=blue

## Port-forward to test
kubectl port-forward svc/app -n demo 8080:80 &
curl http://localhost:8080/version
# Expected Output: {"color": "blue", "version": "1.0.0"}

## Switch to Green
helm upgrade app ./chart -n demo --set activeColor=green
curl http://localhost:8080/version
# Expected Output: {"color": "green", "version": "1.0.0"}

## Switch back to Blue
helm upgrade app ./chart -n demo --set activeColor=blue
curl http://localhost:8080/version
# Expected Output: {"color": "blue", "version": "1.0.0"}

## Optional: Enable NetworkPolicy
# In values.yaml: networkPolicy.enabled: true
