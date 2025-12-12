# Flux + Minikube + .NET – Lunch & Learn Demo

```bash
git clone https://github.com/Kathyw4123/flux-minikube-dotnet-demo.git
cd flux-minikube-dotnet-demo

minikube start --cpus=4 --memory=8g
minikube addons enable registry

# Build the image Flux expects
eval $(minikube docker-env)
docker build -t dotnet-app-demo:v1 .

# Bootstrap Flux (100% safe to run again if needed)
export GITHUB_USER=<your username>
export GITHUB_TOKEN=<token>
export REPO_NAME="flux-minikube-dotnet-demo" (or your repo name)
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=$REPO_NAME \
  --branch=main \
  --path=clusters/minikube \
  --personal \
  --token-auth

# Open the app
minikube service dotnet-app -n dotnet-app --url
