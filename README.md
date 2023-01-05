# nginx-xray-vless-grpc-tls

#### replace the domain serviceName and uuid
```
apt install nginx socat -y
systemctl stop nginx

# install xray
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install -u root

# https://github.com/acmesh-official/acme.sh/wiki/How-to-issue-a-cert
curl https://get.acme.sh | sh

# make sure tcp port 80 is opened or use zerossl
~/.acme.sh/acme.sh --register-account -m whatever@gmail.com
~/.acme.sh/acme.sh --issue -d yourdomain.com --standalone
~/.acme.sh/acme.sh --installcert -d yourdomain.com --key-file /root/private.key --fullchain-file /root/cert.crt

# copy nginx.conf to /etc/nginx/sites-enabled/default
vim /etc/nginx/sites-enabled/default
systemctl restart nginx

# copy xray.json to /usr/local/etc/xray/config.json
vim /usr/local/etc/xray/config.json
systemctl restart xray

# make a fake website /usr/share/nginx/html
```
