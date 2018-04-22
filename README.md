# Docker Rails

## Usage

1. Create new rails project
```
$ docker-compose run --rm web rails new . --force --database=mysql --skip-bundle --skip-git
```

2. Modify Gemfile to uncomment
```
gem 'mini_racer', platforms: :ruby
```

3. Copy environment variables file
```
$ cp env-example .env
```

4. Modify `config/database.yml` as following
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= ENV.fetch("MYSQL_ROOT_PASSWORD") %>
  host: db
```
5. Run `docker-compose build`

6. Create database `$ docker-compose run --rm web rake db:create`

7. Scaffold
```
$ docker-compose run --rm web rails g scaffold Post title:string body:text
$ docker-compose run --rm web rake db:migrate
```

8. RUN `$ docker-compose up -d`

9. Open http://localhost:3000/posts
