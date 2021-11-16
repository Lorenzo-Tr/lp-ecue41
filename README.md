# TD 1 : Vendre des livres numériques avec WooCommerce

## S'assurer d'avoir docker compose

```shell
echo 'export PATH=~/bin:$PATH' >> ~/.bashrc
mkdir -p ~/bin
cd ~/bin
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o ~/bin/docker-compose
chmod +x ~/bin/docker-compose
```

## Démarrer un wordpress

```shell
mkdir -p wordpress/{data,database}
chmod -R a+rwx wordpress
```

```yaml
version: '3.6'

services:
    db:
        image: mysql:5.7
        volumes:
            - ./wordpress/database:/var/lib/mysql
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: mypassword
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpress
            MYSQL_PASSWORD: wordpress

    wordpress:
        image: wordpress:latest
        depends_on:
            - db
        ports:
            - 8080:80
        restart: always
        environment:
            WORDPRESS_DB_HOST: db:3306
            WORDPRESS_DB_USER: wordpress
            WORDPRESS_DB_PASSWORD: wordpress
        volumes:
            - ./wordpress/data:/var/www/html/wp-content
```

## Installer l'extension Woocommerce

http://localhost:8080/wp-admin
Extension ⇒ Ajouter ⇒ chercher “woocommerce” ⇒ Installer.

