# iot-demo
## Install Pravega and flink
Execute 
```vagrant up``` 
to create a virtualbox VM with a docker host and containers for Pravega and Flink.

Then enter the image with
```vagrant ssh```

Once you're in, to start Flink, do:
```docker-compose up```

to start 1 taskmanager or
```docker-compose up -scale taskmanager <N>```

to start <N> taskmanagers.
### Network
The VM has the IP address 192.168.50.14 assigned.
The Flink jobmanager listens to port 8081 (HTTP), 6123 (RPC) and 6124 (to upoad blobs). Pravega controller listens to 9090.
Communication to Flink, using a local installation and the according command line interface doesn't work (at least in my case), 
based on IP adress. It only worked after I've added 
```192.168.50.14  jobmanager``` 
to my hosts file.

To test, type:
```flink list -m tcp://jobmanager:6123``` 
