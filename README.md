# Docker Rails

## Usage
copy environment variables file
```
$ cp env-example .env
```

create rails project
```
$ docker-compose run --rm web rails new . --force --database=mysql --skip-bundle
```

edit .gitignore
```
# add .env
.env
```

edit config/database.yml
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= ENV.fetch("MYSQL_ROOT_PASSWORD") %>
  host: db
```

create database
```
$ docker-compose run --rm web rake db:create
```

scaffold
```
$ docker-compose run --rm web rails g scaffold Post title:string body:text
$ docker-compose run --rm web rake db:migrate
$ docker-compose up -d
```

open 'http://localhost:3000/posts'