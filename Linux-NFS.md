
# Setting up a Linux Network File System (NFS) Server 



##  Install Required Packages:

```bash
sudo yum install nfs-utils libnfsidmap -y
```
## Enable and Start the NFS Server:

```bash
systemctl enable rpcbind nfs-server
systemctl start rpcbind nfs-server rpc-statd nfs-idmap
```
## Check Status:
```bash
systemctl status rpcbind nfs-server rpc-statd nfs-idmap
```

## Server Side Configuration: 

- Create a directory for NFS and give all the permission:
```bash 
mkdir /server/apps
```
```bash
chmod 777 /server/
chmod 777 /server/apps/
```

- Modify the /etc/exports file and add new shared filesystem:
```bash
/server/apps <IP_allow>(rw, sync, no_root_squash) 
```
```bash
exportfs -rv
```
## Client Side Configuration:

- To install NFS Packages:
```bash
yum install nfs-utils rpcbind -y
```
- Enable and start the rpcbind service:
```bash
systemctl enable rpcbind
systemctl start rpcbind
systemctl status rpcbind
```
- To stop the firewall:
```bash
systemctl stop firewall /iptable
```
- Show mount from NFS Server:
```bash
showmount -e <IP of server side>
```
- Create a mount point (a directory):
```bash
mkdir /mnt/apps
```
- Mount the NFS file systemctl
```bash
mount <IP_Server>:/server/apps /mnt/apps 
```
- To Check if its attached or Not:
```bash
df -h
```
