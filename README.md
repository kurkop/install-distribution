# install-distribution
Distribution (or Registry) with local nginx and certs SSL. Basic configuration.

## Create certs with let's encrypt

Exists a image for create interactively the ssl certs. Only is necessary run the next command:

```
sudo docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" quay.io/letsencrypt/letsencrypt:latest certonly
```

And run as webserver and define a subdomain: "registry.mydomain.co" (for this example).

## Install nginx in local server

* Install with apt or yum (apt-get install -y nginx)
* Add distribution.conf to /etc/nginx/config.d or /etc/nginx/sites-enable (In redhat or debian distros)
* Restart service

## Create user and password

Use the next command for create a user/password encrypted

```
htpasswd -Bbn user password
```

## Run Distribution
```
sudo docker run -d -p 5000:5000 -v registry-data:/var/lib/registry -e "REGISTRY_HTTP_SECRET=user:passwordEncrypted" --restart=always --name registry registry:2
```

#### This is all.
