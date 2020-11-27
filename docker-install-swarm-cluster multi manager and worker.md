========swarm Command===========
```
yum install -y yum-utils   device-mapper-persistent-data   lvm2 
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y -q docker-ce
systemctl enable docker
systemctl start docker

usermod -aG docker ansadmin

{
sed -i '/swap/d' /etc/fstab
swapoff -a


systemctl disable firewalld

systemctl stop firewalld
#systemctl enable firewalld
#systemctl start firewalld

cat >> /etc/sysctl.conf<<EOF
net.ipv4.ip_forward=1
net.bridge.bridge-nf-call-iptables=1
net.ipv4.neigh.default.gc_thresh1=4096
net.ipv4.neigh.default.gc_thresh2=6144
net.ipv4.neigh.default.gc_thresh3=8192
EOF

modprobe br_netfilter
sysctl -p


cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
vm.swappiness=0
EOF

sysctl --system 
}

docker swarm init --advertise-addr 192.168.0.188
add-worker
docker swarm join --token SWMTKN-1-5kdgzuy9zkqv5sr17dmzmawsdnkfo09nv1x01miupz500zir7o-2mmz2n3u4276fagz6ec4o0xzp 192.168.0.188:2377

docker swarm join-token manager
docker swarm join-token worker

docker swarm join --token SWMTKN-1-5kdgzuy9zkqv5sr17dmzmawsdnkfo09nv1x01miupz500zir7o-e3wkxl0uitkumx7ob34044pqw 192.168.0.188:2377

=======
only for manager node not assignt contener:
docker node update --availability drain <Node>

docker node promote decker_sww02

All manager down:
docker swarm init --force-new-cluster

Node02 Remove:

Node02$:	docker swarm leave
Remove node form cluster: 
	docker node demote <NODE>
	docker node rm <NODE>
	
Leave:
docker swarm leave --force


# From the node to recover
docker swarm init --force-new-cluster --advertise-addr node01:2377