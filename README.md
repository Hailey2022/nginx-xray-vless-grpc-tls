# nginx-xray-vless-grpc-tls

```
apt install nginx socat -y

# run nginx -V and make sure nginx version > 1.13.10
systemctl stop nginx

# install xray
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install -u root

# https://github.com/acmesh-official/acme.sh/wiki/How-to-issue-a-cert
curl https://get.acme.sh | sh

# make sure tcp port 80 is opened or use zerossl
~/.acme.sh/acme.sh --register-account -m whatever@gmail.com

# replace yourdomain.com and you can add --server letsencrypt if you don't like zerossl
~/.acme.sh/acme.sh --issue --standalone -d yourdomain.com
~/.acme.sh/acme.sh --installcert --key-file /root/private.key --fullchain-file /root/cert.crt -d yourdomain.com

# copy xray.json to /usr/local/etc/xray/config.json and replace the domain serviceName and uuid
vim /usr/local/etc/xray/config.json
systemctl restart xray

# copy nginx.conf to /etc/nginx/sites-enabled/default
vim /etc/nginx/sites-enabled/default

# add grpc.conf to /etc/nginx/nginx.conf
vim /etc/nginx/nginx.conf

systemctl restart nginx

# make a fake website /usr/share/nginx/html
```
