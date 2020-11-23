# how-to

## Run Zookeeper Server at localhost

### Step 1: install Zookeeper

- download [Apache ZooKeeper 3.6.2](https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.6.2/apache-zookeeper-3.6.2-bin.tar.gz)

### Step 2: create config files

- `cd ~/apache-zookeeper-3.6.2-bin`
- ``for i in `seq 3` ; do mkdir conf$i ; mkdir conf$i/data ; echo $i > conf$i/data/myid ; done``
- `vi conf1/zoo.cfg`:
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=./conf1/data
clientPort=21807
server.1=localhost:22207:22307
server.2=localhost:22217:22317
server.3=localhost:22227:22327
```
- `vi conf2/zoo.cfg`:
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=./conf2/data
clientPort=21817
server.1=localhost:22207:22307
server.2=localhost:22217:22317
server.3=localhost:22227:22327
```
- `vi conf3/zoo.cfg`:
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=./conf3/data
clientPort=21827
server.1=localhost:22207:22307
server.2=localhost:22217:22317
server.3=localhost:22227:22327
```

### Step 3: start server
- `cd ~/apache-zookeeper-3.6.2-bin`
- `bin/zkServer.sh start conf1/zoo.cfg` <br />
  `bin/zkServer.sh start conf2/zoo.cfg` <br />
  `bin/zkServer.sh start conf3/zoo.cfg`

### Step 4: connect to server
- `bin/zkCli.sh -server localhost:21807,localhost:21817,localhost:21827`

### Step 5: stop server
- `bin/zkServer.sh stop conf1/zoo.cfg` <br />
  `bin/zkServer.sh stop conf2/zoo.cfg` <br />
  `bin/zkServer.sh stop conf3/zoo.cfg`

