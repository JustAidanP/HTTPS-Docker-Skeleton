# HTTPS-Docker-Skeleton
This is a skeleton setup for https in docker. All traffic will get upgraded to https.

## Initial Setup
First, change `acme.com` and `development@acme.com` to your website and certificate email respectively, these are only referenced in `nginx/nginx.conf`

To setup ssl for the first time on a server, run `docker-compose up certbot-initial dhparam`. This will setup the initial certificates and Diffie Helman parameters, 
these are stored in the volumes `ssl_letsencrypt` and `ssl_dhparam`, these shouldn't be deleted.

### Note
When changes are made to nginx.conf, you need to make sure that `ssl_dhparam` points to `/etc/ssl/certs/dhparam.pem`

## Certificate renewal
Certificate renewal expects the nginx webserver to be running. Run `certbot-renew`, this will perform a webroot certificate challenge using the volume
`ssl_renew_www`, the nginx webserver routes the acme-challenge to that route.

### Cron
This will attempt a renewal every day at 00:30 in the morning
```
30 0 */1 * * docker-compose -f <PATH_TO_COMPOSE_FILE> -d cerbot-renew
```
