# Docker TiDB playground

`docker-tidb-playground` provides a simple docker file for application developers, that you can use to build your local development environment using [TiDB](https://docs.pingcap.com/tidb/dev/overview) (or test environment for CI).

Building a local development environment using the tidb-playground docker image is as easy as using mysql docker.

## Usage

### Version
`docker-tidb-playground` installs the latest TiDB version by default.
If you need to specify the TiDB version, update the `.env` file as follows.

- edit .env
```
TIDB_VERSION=v6.5.0
```
Here are the available [TiDB Versions](https://docs.pingcap.com/tidb/dev/release-notes) .

### Build & Recreate

```
docker compose up -d --build
```

```
docker compose logs tidb
...
...
docker-tidb-playground-tidb-1  |
172.20.0.2:3930 ... Done
CLUSTER START SUCCESSFULLY, Enjoy it ^-^
docker-tidb-playground-tidb-1  | To connect TiDB: mysql --comments --host 172.20.0.2 --port 4000 -u root -p (no password)
docker-tidb-playground-tidb-1  | To view the dashboard: http://172.20.0.2:2379/dashboard
docker-tidb-playground-tidb-1  | PD client endpoints: [172.20.0.2:2379]
docker-tidb-playground-tidb-1  | To view the Prometheus: http://172.20.0.2:9090
docker-tidb-playground-tidb-1  | To view the Grafana: http://172.20.0.2:3000
```

### Use

```
mysql -u root -h 127.0.0.1 -P 4000 -D test -p # password is empty

mysql > create table t0 ( id bigint primary key);

mysql > insert into t0 values (1),(2),(3);
```

confirm

```
mysql -u root -h 127.0.0.1 -P 4000 -D test -e "select * from t0"
+----+
| id |
+----+
|  1 |
|  2 |
|  3 |
+----+
```

#### WEB GUI
* Grafana : http://127.0.0.1:3000
  * user: `admin`
  * password: `admin`
* TiDB Dashboard : http://127.0.0.1:2379/dashboard
  * user: `root`
  * password : `` (empty)

### Stop

```
docker compose stop tidb
```

### Start

```
docker compose start tidb
```

```
mysql -u root -h 127.0.0.1 -P 4000 -D test -e "select * from t0"
+----+
| id |
+----+
|  1 |
|  2 |
|  3 |
+----+
```

### Remove
```
docker compose down
```
