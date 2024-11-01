### [Stop and remove all containers](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes#stop-and-remove-all-containers)

**List:**
```
docker ps -a
```
**Remove:**
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
## [Removing Volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes#removing-volumes)

**List:**
```
docker volume ls
```
**Remove:**
```
docker volume rm volume_name volume_name
```
## [Removing Docker Images](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes#removing-docker-images)

**List:**
```
docker images -a
```
**Remove:**
```
docker rmi Image1 Image2
```
**Remove all:**
```
docker rmi -f $(docker images -aq)
```
### [Remove Dangling Docker Images](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes#remove-dangling-docker-images)

**List:**
```
docker images -f dangling=true
```
**Remove:**
```
docker image prune
```
