# WordPress Local Development: with Nginx + Mariadb in Docker

## Before Start 

### Proper file permissions

Setup proper file permissions of wp-content folder so that you can use your favorite editor

There is a default USER environment variable which hold the user name of current logged-in user. We will use these variables in our docker-compose.yml file and create two environment variables to be used inside wordpress container.

Find out your user name and id by 
```
id YOUR_USERNAME
```

and copy and paste the the value in .env-sample
```
LOCAL_USER_ID=sample_id
LOCAL_USER_NAME=sample_user
```

### Replace the domain name in ngin.conf file

* Out-of-the-box, nginx doesn't support environment variables inside most configuration blocks. But envsubst may be used as a workaround if you need to generate your nginx configuration dynamically before nginx starts. 
* More Links and how to use envsubst
   * [Nginx environment variables](https://www.xspdf.com/resolution/10080656.html)
   * [Substitue environment variables in NGINX config from docker-compose](https://stackoverflow.com/questions/56649582/substitute-environment-variables-in-nginx-config-from-docker-compose)
   * [Nginx docker image](https://github.com/docker-library/docs/tree/master/nginx#using-environment-variables-in-nginx-configuration)
   * [How can I use environment variables in Nginx.conf](https://serverfault.com/questions/577370/how-can-i-use-environment-variables-in-nginx-conf)


### Use mkcert if you want SSL cert on localhost

* (For ubuntu) install [homebrew](https://www.osradar.com/install-homebrew-ubuntu-20-04-debian-10/) to be able to install [mkcert] 
* install [mkcert](https://github.com/FiloSottile/mkcert) for creating the SSL cert
* Create SSL cert
```
cd cli
chmod +x create-cert.sh
./create-cert.sh
```

## Start 

 * Edit the .env-sample file with custom value, change its name to .env
 * change the server_name in nginx.conf file to your custom domain

```
docker-compose build 
docker-compose up -d
```

 * after containers up run
```
mkcert -install
```

### Useful commands for debug

```
docker-compose build --no-cache
docker-compose up -d db
docker-compose up -d wp
docker-compose up -d nginx
docker-compose up -d php-myadmin
docker container logs CONTAINER_NAME
```

### Reference Link about file permissions in host machine and docker container

* Thanks to Rajinder Deol for scripts of setting up proper file permissions 
* [Rajinder's post](https://rajislearning.com/wordpress-development-with-docker-compose/)
* More about Permission 
    * [Avoiding Permission Issues With Docker-Created Files](https://vsupalov.com/docker-shared-permissions/)
    * [Add or Remove a User from a Group](https://www.tecmint.com/add-or-remove-user-from-group-in-linux/)
    * [Add a User to Group www-data](https://www.cyberciti.biz/faq/ubuntu-add-user-to-group-www-data/)
    * [Bind mount and permissions](https://github.com/BretFisher/ama/issues/65#issuecomment-526792333)

### Reference Link about mkcert

* Thanks to [urre](https://github.com/urre/wordpress-nginx-docker-compose) for scripts to create the SSL cert
* [Local WordPress Development with Docker and Docker Compose](https://urre.me/writings/docker-for-local-wordpress-development/)
* [Mkcert valid https certificates for loclhost](https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/)