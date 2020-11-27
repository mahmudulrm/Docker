Docker Host:

	docker run my web server
Docker swarm:

	docker service create --replicas=3 --name web-server my-web-server 
	docker service create --replicas=3 my-web-server  
	docker service create --replicas=3 -p 8080:80 my-web-server 
	docker service create --replicas=3 --network frontend my-web-server 
	docker service ls
	
	docker service create --mode global my-monitoring-agent
	docker service update --replicas=4 my-web-server
	
	
	docker service create nginx
	docker service update --replicas=3 80 my_web
	docker service ls
	
	docker service ps id
	
	https://docs.docker.com/engine/swarm/services/#placement-constraints