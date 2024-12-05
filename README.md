# secure-jenkins

## Install Jenkins
```bash
sudo apt update -y

# Install OpenJDK 17 JRE Headless
sudo apt install openjdk-17-jre-headless -y

# Download Jenkins GPG key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Add Jenkins repository to package manager sources
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package manager repositories
sudo apt update

# Install Jenkins
sudo apt install jenkins -y

sudo systemctl enable --now jenkins
```

## Install Caddy
```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo apt-key add -
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update -y
sudo apt install caddy

sudo systemctl enable --now caddy
```
### nip.io is a free DNS service that generates IP-based domains with HTTPS support for development and testing purposes.
/etc/caddy/Caddyfile
```bash
54.224.96.252.nip.io {
        reverse_proxy localhost:8080
}
```

CA Certificate
```bash
sudo cp /var/lib/caddy/.local/share/caddy/pki/authorities/local/root.crt /usr/local/share/ca-certificates/
sudo update-ca-certificates
```
```bash
sudo systemctl restart caddy
```
