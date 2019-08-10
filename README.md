Quick tmp README

1. Clone repo: `git clone https://github.com/dzoladz/coral.git`
2. Copy example environment into .env and edit: `cp .env-example .env`
3. Bring up Coral: `docker-compose up --build`
4. Remove write access of conf files `docker exec -t coral_app_1 chmod 755 -R /var/www/html/` 
5. Complete via web installer at <http://localhost:8080/coral/>
