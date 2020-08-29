# Rails6 on Docker

# Requirement

- Ruby 2.6.6
- Rails 6.0.3.2

# Usage

1. git clone

```bash
git clone https://github.com/j9141997/rails_on_docker_base.git { new project name }
```

2. push 先リポジトリを変更

```bash
 $ git remote set-url origin { new url }
```

3. docker-compose run を実行し、アプリケーションを生成

```bash
$ docker-compose run web rails new . --force --no-deps --database=postgresql
```

4. アプリケーション生成後、build

```bash
$ docker-compose build
```

5. .env を作成し、環境変数を設定する

```bash
$ vim .env
```

```
DB_PASSWORD=hogehoge
```

6. database.yml を変更

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

7. DB を作成する

```bash
$ docker-compose run web rails db:create
```

8. docker を起動

```bash
$ docker-compose up -d
```

9. http://localhost:3001 にアクセスし、確認

```
$ open http://localhost:3001
// ポートは3001に設定しているため、変更したければdocker-compose, dockerfileの変更が必要
```
