# Gatling Real-time Monitoring

docker compose file already clone on 10.200.18.129

## active gatling graphite
remove comment on
```
vim /home/${user}/krug-gatling/src/test/resources/gatling.conf
```

```
data {
  writers = [file, graphite]      
  .....
  graphite {
      light = false              
      host = "localhost"         
      port = 2003                
      protocol = "tcp"           
      #rootPathPrefix = "gatling" 
      bufferSize = 8192          
      writePeriod = 1            
    }
  .....
}
```

## active grafana-influx-gatling docker compose
docker compose file location
```
cd /home/tpedev/grafana-influx-gatling/grafana-influx-gatling
```
start
```
docker-compose up -d
```
stop
```
docker-compose down
```

## grafana ui
http://10.200.18.129:3000/
account:admin
pass:admin

## reminder
datas in influx was not clean up auto
should remove by manual or clear docker container

## detail config info
Gatling can provide live metrics via the Graphite protocol which can be persisted and visualised.
This project shows how to use InfluxDB, Graphite, and Grafana to monitor Gatling tests in real-time.

Use `docker-compose up` to launch Grafana and Influx DB infrastructure. Go to [localhost:3000](http://localhost:3000) to see Grafana dashboard.

Configure your Gatling instance to use graphite protocol to send data to InfluxDB. 
Update following config in data section of your gatling.conf file:
```
data {
  writers = [file, graphite]      # The list of DataWriters to which Gatling write simulation data (currently supported : console, file, graphite, jdbc)
  .....
  graphite {
      light = false              # only send the all* stats
      host = "localhost"         # The host where the Carbon server is located
      port = 2003                # The port to which the Carbon server listens to (2003 is default for plaintext, 2004 is default for pickle)
      protocol = "tcp"           # The protocol used to send data to Carbon (currently supported : "tcp", "udp")
      #rootPathPrefix = "gatling" # The common prefix of all metrics sent to Graphite
      bufferSize = 8192          # Internal data buffer size, in bytes
      writePeriod = 1            # Write period, in seconds
    }
  .....
}
```
Fore more details see Gatling docs [here.](https://gatling.io/docs/2.3/realtime_monitoring/#id3)
