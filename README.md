# **Deploy Starbucks Clone Application local**
```
git clone https://github.com/gurpreetsingh-5/starbucks-app.git
open package.json or package-lock.json file.
find engines in .json file and check node version
install node and visit
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm install v20.18.0
node -v
npm -v
npm install
npm run start
ipaddress/localhost:3000
```
 
# **Deploy Starbucks Clone Application using nginx:**
```
sudo apt install nginx -y
sudo systemctl start nginx.service
sudo systemctl status nginx.service
npm run build ( in starbucks folder )
and creted build folder
all file copy in build folder
cp -r * /  /var/www/html
```


# **Deploy Starbucks Clone Application using Docker:**
```
sudo apt update
git clone https://github.com/gurpreetsingh-5/starbucks-app.git
sudo apt install docker.io -y
touch Dockerfile
  - FROM node:alpine
    WORKDIR /app
    COPY package.json package-lock.json ./
    RUN npm ci --only=production
    COPY . .
    EXPOSE 3000
    CMD ["npm", "start"]

** multistage Docker file
FROM node:alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build  # If using a build step (e.g., React)

FROM node:alpine
WORKDIR /app
COPY --from=builder /app .
EXPOSE 3000
CMD ["npm", "start"]



 - FROM node:alpine
   WORKDIR /app
   COPY package.json package-lock.json ./
   RUN npm install
   COPY . .
   EXPOSE 3000
   CMD ["npm","start"]
docker build -t star .
docker images
docker run -d -p 80:3000 star (run port 80)
docker run -d -p 3000:3000 star (run port 3000)
docker ps -a (check container)
docker exec -it <container-id>  /bin/bash
```

# Deploy Starbucks Clone Application AWS using DevSecOps Approach
https://app.eraser.io/workspace/59NJfCay26dUMl5YAlFl?origin=share

# **Install AWS CLI**
```
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
 
# **Install Jenkins on Ubuntu:**

```
#!/bin/bash
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
sudo systemctl status jenkins
```


# **Install Docker on Ubuntu:**
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker ubuntu
sudo chmod 777 /var/run/docker.sock
newgrp docker
sudo systemctl status docker
```

# **Install Trivy on Ubuntu:**

Reference Doc: https://aquasecurity.github.io/trivy/v0.55/getting-started/installation/
```
sudo apt-get install wget apt-transport-https gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```
