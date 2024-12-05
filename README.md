# secure-jenkins

## Install Caddy
```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo apt-key add -
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

/etc/caddy/Caddyfile
```bash
{
  local_certs
}

:443 {
        # Set this path to your site's directory.
        #root * /usr/share/caddy

        # Enable the static file server.
        #file_server

        # Another common task is to set up a reverse proxy:
        tls internal
        reverse_proxy localhost:8080

        # Or serve a PHP site through php-fpm:
        # php_fastcgi localhost:9000
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
