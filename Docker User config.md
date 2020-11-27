#Docker not run for user 
1. solution
```
sudo setfacl -m user:$USER:rw /var/run/docker.sock
```
2.Other solution

    sudo usermod -aG docker $USER

3.An other solution

    sudo groupadd docker
    sudo gpasswd -a $USER docker
    docker run hello-world
