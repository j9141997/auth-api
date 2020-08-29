# Rails6 on Docker

# Requirement

- Ruby 2.6.6
- Rails 6.0.3.2

# Usage

1. docker-compose run を実行し、アプリケーションを生成

```
$ docker-compose run web rails new . --force --no-deps --database=postgresql
```

2. アプリケーション生成後、build

```
$ docker-compose build
```

3. database.yml を変更

```yml
# 設定箇所のみ抜粋
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password # docker-compose.ymlのPOSTGRES_PASSWORDで指定した値
  pool: 5
:
:
development:
  <<: *default
  database: myapp_development
:
:
test:
  <<: *default
  database: myapp_test
```

4. DB を作成する

```
$ docker-compose run web rails db:create
```

5. docker を起動

```
docker-compose up -d
```

6. http://localhost:3001 にアクセスし、確認

```
http://localhost:3001
// ポートは3001に設定しているため、変更したければdocker-compose, dockerfileの変更が必要
```
