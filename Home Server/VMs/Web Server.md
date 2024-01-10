l#### Resources

[# Nginx Proxy Manager - How-To Installation and Configuration](https://www.youtube.com/watch?v=P3imFC7GSr0)

##### Setup VM
1) Set up new VM from template
2) Install Docker
```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update

# Install Docker Packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Check if Successful
sudo docker run hello-world

# Add john to a new docker group
sudo usermod -aG docker john
```

3) copy docker-compose yaml file from docs

```bash

version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP
    environment:
      # Mysql/Maria connection parameters:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "john"
      DB_MYSQL_PASSWORD: "JHDs8dwqbIdw8^&Dwnb"
      DB_MYSQL_NAME: "nginx_proxy_db"
      # Uncomment this if IPv6 is not enabled on your host
      # DISABLE_IPV6: 'true'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
    depends_on:
      - db

  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'JHDs8dwqbIdw8^&Dwnb'
      MYSQL_DATABASE: 'nginx_proxy_db'
      MYSQL_USER: 'john'
      MYSQL_PASSWORD: 'JHDs8dwqbIdw8^&Dwnb'
    volumes:
      - ./mysql:/var/lib/mysql
```

4) Run docker compose
```bash
docker compose up -d
```

5) Go to IP port 81 in web browser

`email` admin@example.com
`password` changeme

6) Change email and password
##### Setup Router
3) Open ports 80 and 443 on router

