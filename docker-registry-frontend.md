https://hub.docker.com/_/registry

docker run -d -p 5000:5000 --restart always --name registry registry:2

docker pull hello-world
docker tag hello-world localhost:5000/hello-world-my
docker push localhost:5000/hello-world-my
check:
docker exec -it 8807 /bin/sh
cd /var/lib/registry/docker/registry/v2/repositories

docker pull localhost:5000/hello-world-my
docker run localhost:5000/hello-world-my

https://hub.docker.com/r/konradkleine/docker-registry-frontend

sudo docker run \
  -d \
  -e ENV_DOCKER_REGISTRY_HOST=registry \
  -e ENV_DOCKER_REGISTRY_PORT=5000 \
  -p 8080:80 \
  --link registry:registry \
  konradkleine/docker-registry-frontend:v2



sudo vi /etc/docker/daemon.json
 
{
"insecure-registries": ["192.168.0.182:5000"]
}

sudo systemctl restart docker