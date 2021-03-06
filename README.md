# use Singer tap-mysql migrate data to postgresql

## how to running

> use python3 venv

* pg venv

```code
mkdir pg
python3 -m venv .
```

* gitbase mysql venv

```code
mkdir gitbase
python3 -m venv
```

* install tap && target

```code
pg target

cd pg  && source bin/activate && pip install target-postgres

mysql tap: use my change code

cd gitbase && git clone https://github.com/rongfengliang/tap-mysql.git

&& source bin/activate && pip install -e tap-mysql

```

* start demo server

> gitbase && postgresql  use docker-compose

```code
docker-compose up -d
```

* simple blobs table migrate

```code
./gitbase/bin/tap-mysql -c mysql-tap.json --catalog p.json | ./pg/bin/target-postgres -c pg-target.json
```

* for all gitbase table migrate 2 pg 

```code
./gitbase/bin/tap-mysql -c mysql-tap.json -p gitbase.json | ./pg/bin/target-postgres -c pg-target.json
```

## some notes

for better data stora you can create new schema in pg database with below

```code
create schema gitbase
```

and change pg target with below

```code
{
    "host": "localhost",
    "port": 5432,
    "dbname": "postgres",
    "user": "postgres",
    "password": "dalong",
    "schema": "gitbase"
}
```
