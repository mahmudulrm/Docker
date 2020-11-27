docker rm $(docker ps -a -q)
docker rm $(docker ps -f "status=exited" -q)
docker system df 
docker system info
docker system pruned


docker inspect -f "{{ .NetworkSettings.IPAddress }}" 66f

Voting app
===========

docker run -d -e POSTGRES_PASSWORD="postgres" --name=db postgres:9.4
docker run -d --name=redis redis

docker build . -t voting-app
docker run -d  -p 5000:80 voting-app

docker build . -t result-app
docker run -d -p 5001:80 --link db:db -t result-app

docker build . -t worker-app
docker run -d --link redis:redis --link db:db worker-app