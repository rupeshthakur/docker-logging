#### Test POC

### Run elasticsearch

docker run -p 9200:9200 -p 9300:9300 \
-e "discovery.type=single-node" \
-e ES_JAVA_OPTS="-Xms256m -Xmx256m" \
elasticsearch:7.3.1

### Build & Run fluentd  

docker build -t fluentd:1.0.0 ./ # cd to fluentd directory and execute.

docker run -it --rm \
-p 24224:24224 \
## replace <> dir path
-v <absolute path to dir, ex. example/fluentd>:/fluentd/etc \  ## mount your dir as container dir.
fluentd:1.0.0 \
-c /fluentd/etc/fluent.conf  ## pass configuration

### Pull & Run httpd

docker pull httpd
docker run -d -p 8080:80 \
--log-driver=fluentd \
--log-opt tag="docker.{{.ID}}" \
## replace hostname
--log-opt fluentd-address=<docker hostname>:24224 \
httpd

### Pull & run kibana

## replace name / container-id
docker run --link <name or container-id ex. cfa93039db6d>:elasticsearch -p 5601:5601 kibana:7.3.1

[https://github.com/rupeshthakur/docker-logging/blob/master/example/kibana/Screen%20Shot%202019-08-25%20at%2011.12.04%20PM.png] 
