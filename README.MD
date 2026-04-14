1. Installation of docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh


2. Build docker images
docker build -t python-app:v1 .
docker images
docker run --name python-app -p 5000 python-app:v1
# http://172.17.0.2:5000/api/v1/info
docker image tag python-app:v1 ryukocndevpy1/python-app:v1
docker images
docker push ryukocndevpy1/python-app:v1
docker rmi ryukocndevpy1/python-app:v1
docker pull ryukocndevpy1/python-app:v1

3. Create k8n cluster
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# Install kubectl
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.35/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
sudo apt-get update
sudo apt-get install -y kubectl

# Create cluster
kind create cluster --config kind-config.yaml

kubectl cluster-info --context kind-kind

