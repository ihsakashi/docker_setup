# Home lab

My setup is Gitea and Drone behind Nginx-proxy.
Traefik is very accomodating but jwilder/nginx-proxy proves more flexible and faster.

## To-do

* Reverse proxy caching
* Monit and health
* Gitea mounted to external HDD
* Pterodactyl panel

## Instructions

This is setup worked for me. Hopefully, it works the same for you.

1. Replace docker-compose.yaml variables. Worry about gitea and postgresql for now.
1. Run `docker network create nginx-proxy`
3. In containerd: `docker-compose up -d`
4. In gitd: `docker-compose up -d gitea postgres-db`
    1. Install Gitea and create user
    2. User settings > Applications. Type following
        * Application Name: Drone
        * Redirect URI: ${DRONE_SRV_URL}/login
    3. Copy and paste Oauth2 info into gitd docker-compose.yaml
5. In gitd: `docker-compose down`
6. Remove # placeholders in docker-compose.yaml
7. Repeat 4