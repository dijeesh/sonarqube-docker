# sonarqube-docker

Setup and run Sonarqube with Postgres backend and Nginx reverse proxy using docker and docker-compose

### Steps

1. Provision EC2 (Ubuntu 18.04) instance

2. Install system updates 

```
sudo apt-get update && apt-get upgrade -y
```

3. Setup DNS Record for sonarqube.yourdomain.com to point to the Instance.

3. Install certbot, Docker and Docker-compose

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update && sudo apt install docker-ce docker-compose certbot -y

sudo systemctl start docker && sudo systemctl enable docker
```

4. Provision Letsencrypt Certficate 

```
sudo certbot certonly --agree-tos --email mail@yourdomain.com -d sonarqube.yourdomain.com
```

5. Clone repository

```
git clone https://github.com/dijeesh/sonarqube-docker.git
```

6. Update domain, credentials 

```
Edit sonarqube-docker/nginx/default.conf and update yourdomain.com details

Edit sonarqube-docker/docker-compose.yaml and update Postgres user credentials
```

7. Run docker-compose 

```
cd sonarqube-docker ; docker-compose up -d
```

8. Login with default credentials `admin/admin` and set a secure password for admin user.