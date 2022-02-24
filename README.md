# AUVSI SUAS Interoperability

For the original repo, please visit https://github.com/auvsi-suas/interop

The Interoperability System is released to teams as Docker images and Docker Compose YAML configurations. These can be used to run the server and client tools with minimal setup.

## First Time Setup


Gitclone the current Git repo.

```bash
git clone https://github.com/asd65241/HKU-UAS-SUAS-Server.git && cd HKUUAS-SUAS-Server
```

Create the interop server's database.

```bash
sudo ./interop-server.sh create_db
```

If you want to run the image locally, run interop-server-dev.sh instead:

```bash
sudo ./interop-server-dev.sh create_db
```

Load initial test data into the server. This provides access to a default admin
account (u: `testadmin`, p: `testpass`) and a default team account (u:
`testuser`, p: `testpass`). This will also load a sample mission into the server.

```bash
sudo ./interop-server.sh load_test_data
```

### Run the Server

Run the server on port 8000, so it can be accessed in a local web browser at
`localhost:8000`. Other machines on the same network can replace `localhost`
with the host computer's IP address.

```bash
sudo ./interop-server.sh up
```

The server will run until stopped using `Ctrl-C`.

```bash
sudo ./interop-server.sh up_d
```

The server will run in detech mode, and stop on 'down'.


```bash
sudo ./interop-server.sh down
```

For deteched mode, stop the server using the above command.


### View Server Log

Logs are also available via volumes on the host computer under
`volumes/var/log/uwsgi/interop.log`.

### Upgrade the Server

Upgrade the Server by downloading new images, deleting the old containers, and
starting the server again.

```bash
sudo ./interop-server.sh upgrade
```

Note server data is persisted due to volumes. If the existing data causes an
issue, you can delete it (see next section).

### Delete Server Data

While the server isn't running, you can delete the server data by deleting the
volumes and containers. Note this action is permanent.

```bash
sudo ./interop-server.sh rm_data
```

After deleting the data, you will need to follow First Time Setup instructions.
