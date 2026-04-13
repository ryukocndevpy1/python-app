docker build -t python-app:v1 .
docker images
docker run --name python-app -p 5000 python-app:v1