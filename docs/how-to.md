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

- sample directory structure after setup:
```
~/apache-zookeeper-3.6.2-bin % tree .

...
├── conf1
│   └── data
│   │   └── myid
│   │   └── version-2
│   └── zoo.cfg
├── conf2
│   └── data
│   │   └── myid
│   │   └── version-2
│   └── zoo.cfg
├── conf3
│   └── data
│   │   └── myid
│   │   └── version-2
│   └── zoo.cfg
...
```

### Step 3: start server
- `cd ~/apache-zookeeper-3.6.2-bin`
- `bin/zkServer.sh start conf1/zoo.cfg` <br />
  `bin/zkServer.sh start conf2/zoo.cfg` <br />
  `bin/zkServer.sh start conf3/zoo.cfg`
- sample output for start servers
```
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: conf1/zoo.cfg
Starting zookeeper ... STARTED
```

### Step 4: connect to server
- `bin/zkCli.sh -server localhost:21807,localhost:21817,localhost:21827`
- sample output message after connection
```
/usr/bin/java
Connecting to localhost:21807,localhost:21817,localhost:21827
2020-11-23 16:38:18,440 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.6.2--803c7f1a12f85978cb049af5e4ef23bd8b688715, built on 09/04/2020 12:44 GMT
2020-11-23 16:38:18,442 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=mandys-mbp.lan
2020-11-23 16:38:18,442 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=14.0.1
2020-11-23 16:38:18,443 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2020-11-23 16:38:18,443 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/Library/Java/JavaVirtualMachines/jdk-14.0.1.jdk/Contents/Home
2020-11-23 16:38:18,443 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../zookeeper-server/target/classes:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../build/classes:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../zookeeper-server/target/lib/*.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../build/lib/*.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/zookeeper-prometheus-metrics-3.6.2.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/zookeeper-jute-3.6.2.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/zookeeper-3.6.2.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/snappy-java-1.1.7.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/slf4j-log4j12-1.7.25.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/slf4j-api-1.7.25.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/simpleclient_servlet-0.6.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/simpleclient_hotspot-0.6.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/simpleclient_common-0.6.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/simpleclient-0.6.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-transport-native-unix-common-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-transport-native-epoll-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-transport-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-resolver-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-handler-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-common-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-codec-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/netty-buffer-4.1.50.Final.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/metrics-core-3.2.5.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/log4j-1.2.17.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/json-simple-1.1.1.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jline-2.14.6.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-util-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-servlet-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-server-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-security-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-io-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jetty-http-9.4.24.v20191120.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jackson-databind-2.10.3.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jackson-core-2.10.3.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/jackson-annotations-2.10.3.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/commons-lang-2.6.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/commons-cli-1.2.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../lib/audience-annotations-0.5.0.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../zookeeper-*.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/Users/mandyxu/apache-zookeeper-3.6.2-bin/bin/../conf:
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/Users/mandyxu/Library/Java/Extensions:/Library/Java/Extensions:/Network/Library/Java/Extensions:/System/Library/Java/Extensions:/usr/lib/java:.
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/var/folders/jn/06zl_01x3hs03p44_x9js7440000gn/T/
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Mac OS X
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=x86_64
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=10.16
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=mandyxu
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/Users/mandyxu
2020-11-23 16:38:18,444 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/Users/mandyxu/apache-zookeeper-3.6.2-bin
2020-11-23 16:38:18,445 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=248MB
2020-11-23 16:38:18,446 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=256MB
2020-11-23 16:38:18,446 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=256MB
2020-11-23 16:38:18,448 [myid:] - INFO  [main:ZooKeeper@1006] - Initiating client connection, connectString=localhost:21807,localhost:21817,localhost:21827 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@77b52d12
2020-11-23 16:38:18,450 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2020-11-23 16:38:18,458 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2020-11-23 16:38:18,462 [myid:] - INFO  [main:ClientCnxn@1716] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
2020-11-23 16:38:18,471 [myid:localhost:21807] - INFO  [main-SendThread(localhost:21807):ClientCnxn$SendThread@1167] - Opening socket connection to server localhost/127.0.0.1:21807.
2020-11-23 16:38:18,472 [myid:localhost:21807] - INFO  [main-SendThread(localhost:21807):ClientCnxn$SendThread@1169] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
JLine support is enabled
2020-11-23 16:38:18,491 [myid:localhost:21807] - INFO  [main-SendThread(localhost:21807):ClientCnxn$SendThread@999] - Socket connection established, initiating session, client: /127.0.0.1:59395, server: localhost/127.0.0.1:21807
2020-11-23 16:38:18,545 [myid:localhost:21807] - INFO  [main-SendThread(localhost:21807):ClientCnxn$SendThread@1433] - Session establishment complete on server localhost/127.0.0.1:21807, session id = 0x10000a40b820000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: localhost:21807,localhost:21817,localhost:21827(CONNECTING) 0] 

```

### Step 5: stop server
- `bin/zkServer.sh stop conf1/zoo.cfg` <br />
  `bin/zkServer.sh stop conf2/zoo.cfg` <br />
  `bin/zkServer.sh stop conf3/zoo.cfg`
- sample output after stop servers
```
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: conf1/zoo.cfg
Stopping zookeeper ... STOPPED
```

