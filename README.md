Crear certificado la primera vez:

Paso 1
docker-compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run --expand -d verenzuela.com,www.verenzuela.com,dunamis.verenzuela.com,demo-selector.verenzuela.com

Paso 2
docker-compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ --expand -d verenzuela.com,www.verenzuela.com,dunamis.verenzuela.com,demo-selector.verenzuela.com
