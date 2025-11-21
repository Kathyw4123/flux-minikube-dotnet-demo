# Flux + Minikube + .NET – Lunch & Learn Demo

Just run these 6 commands → fully working GitOps demo in <5 minutes!

```bash
git clone https://github.com/Kathyw4123/flux-minikube-dotnet-demo.git
cd flux-minikube-dotnet-demo

minikube start --cpus=4 --memory=8g
minikube addons enable registry

# Build the exact image Flux expects
eval $(minikube docker-env)
docker build -t dotnet-app-demo:v1 .

# Bootstrap Flux (100% safe to run again if needed)
flux bootstrap github \
  --owner=Kathyw4123 \
  --repository=flux-minikube-dotnet-demo \
  --branch=main \
  --path=clusters/minikube \
  --personal

# Open the app
minikube service dotnet-app -n dotnet-app --url
