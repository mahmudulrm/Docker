git clone:   git clone https://github.com/dockersamples/example-voting-app.git

docker run -d --name=redis redis
docker run -d -e POSTGRES_PASSWORD="postgres" --name=db postgres:9.4
docker run -d --link redis:redis --link db:db worker-app

cd example-voting-app/vote/
docker build . -t voting-app
docker run -d -p 5000:80 --link redis:redis voting-app


cd example-voting-app/result
docker build . -t result-app
docker run -d -p 5001:80 --link db:db -t result-a