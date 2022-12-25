# Docker Composer Yaml File









version: '2'
services:
  db:
    image: mysql:5.7
    ports:
      - "6603:3306"
    environment:
      - MYSQL_ALLOW_EMPTY_PASSWORD=true
      - MYSQL_DATABASE=laravelProject
      - LANG=C.UTF-8
    volumes:
      - db:/var/lib/mysql
    command: mysqld --sql-mode=NO_ENGINE_SUBSTITUTION --character-set-server=utf8 --collation-server=utf8_unicode_ci

  web:
    image: arbiedev/php-nginx:7.1.8
    ports:
      - "8080:80"
    volumes:
      - ./www:/var/www
      - ./nginx.conf:/etc/nginx/sites-enabled/default

volumes:
  db:






2.

    web:
      build: path/to/your/Dockerfile/directory
      image: your-image-tag
      ports:
        - "8080:80"
      volumes:
        - ./www:/var/www
        - ./nginx.conf:/etc/nginx/sites-enabled/default


3.




















