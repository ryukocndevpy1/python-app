docker build -t python-app:v1 .
docker images
docker run --name python-app -p 5000 python-app:v1
# http://172.17.0.2:5000/api/v1/info
docker image tag python-app:v1 ryukocndevpy1/python-app:v1
docker images
docker push ryukocndevpy1/python-app:v1
docker rmi ryukocndevpy1/python-app:v1
docker pull ryukocndevpy1/python-app:v1