cat > Dockerfile
FROM ubuntu:16.04
RUN apt-get update && apt-get install -y python python-pip
RUN pip install flask
COPY app.py /opt/
ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0 --port=8080

======================
cat > app.py
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
	
==================

docker build .

docker build . -f Dockerfile2 -t mywebapp

added tag and name:

docker build . -t simple-webapp  

docker history simple-webapp 
cd /var/lib/docker
cd aufs
check size
du -sh *

docker system df   / total all images and contenars
docker system df -v  // share size show 

=================

DOCKER COMPOSE

docker run mmumshad /simple webapp
docker run mongodb
docker run redis:alpine
docker run ansible

docker-compose.yml
services:
	web:
		image: "mmumshad /simple-webapp"
	database:
		image: "mongodb"
	messaging:
		image: "redis:alpine"
	orchestration:
		image: "ansible"
		
docker compose up
======================

docker service create mmumshad /simple webapp
docker service create mongodb
docker service create redis
docker service create ansible
---------------------
docker-compose.yml
services:
	web:
		image: "mmumshad /simple webapp"
	database:
		image: "mongodb"
	messaging:
		image: "redis:alpine"
	orchestration:
		image: "ansible"


docker stack deploy


============volume==================

docker run v data_volume var / mysql mysql
/
var / mysql
docker
run v data_volume2:/ var / mysql mysql
docker
run v /data/ mysql var / mysql mysql
/data
mysql
container layer
Read Write
mysql
/
var / mysql
docker
run
–
mount type= bind,source =/ mysql,target var / mysql mysql



=======networks===========
docker-compose.yml

version: 2
	services: 
	redis
		image: redis
		
		networks:
			- back-end
			
	db:
		image: postgres:9.4
		
		networks:
			- back-end		
	vote:
		image: voting-app
		ports:
			- 5000:80
		networks:
			- front-end	
			- back-end
	
	result:
		image: result
		networks:
			- front-end	
			- back-end

networks:
	front-end:
	back-end:

