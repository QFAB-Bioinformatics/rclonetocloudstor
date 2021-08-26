# rclone to CloudStor POC
This proof of concept has been tested in Ubuntu 20.04 (Focal LTS) but it should run in any linux distribution given it's based from [rclone docker image](https://hub.docker.com/r/rclone/rclone).

# Install docker and docker compose
## Below instructions are based of the [docker documentation](https://docs.docker.com/engine/install/ubuntu/)
```
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo usermod -aG docker ubuntu
```
Log out and log back in and make sure docker can run without sudo
```
docker run hello-world

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```
# Run rclone docker container 
Copy [docker-compose.yml](docker-compose.yml) to a folder in your VM after installing docker and docker compose and run the below commands:
```
cd your_folder
```
Make sure [docker-compose.yml](docker-compose.yml) is in your folder
```
ls -la
```
Run docker compose command below
```
docker-compose up
```
# Test rclone can be run from the command line
```
docker-compose exec rclone_service rclone listremotes

docker-compose exec rclone_service rclone config
```
# Test rclone can be run using the API
```
curl http://localhost:5572

curl -X POST 'http://localhost:5572/rc/list'

curl -H "Content-Type: application/json" -X POST -d '{"potato":2,"sausage":1}' http://localhost:5572/rc/noop
```
# For more details on how to setup CloudStor remote in rclone see below document
[CloudStor Rclone Config Instructions](https://docs.google.com/document/d/1MKueROQ2NL-vvRqHqNwuMXYRlQYRrQHB/edit) 