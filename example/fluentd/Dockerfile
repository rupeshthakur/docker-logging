FROM fluent/fluentd:v1.4-1
MAINTAINER <Your Name> <email@address>

USER root

RUN apk add --no-cache --update --virtual .build-deps \
        sudo build-base ruby-dev \
 # cutomize following instruction as you wish
 && sudo gem install fluent-plugin-elasticsearch \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /home/fluent/.gem/ruby/2.5.0/cache/*.gem

# COPY fluent.conf /fluentd/etc/
# COPY entrypoint.sh /bin/

USER fluent

# To build
#docker build -t fluentd:1.0.0 ./

# To run as docker container with custom configuraiton.
# docker run -it --rm \
# -p 24224:24224
# -v <absolute path to dir, ex. example/fluentd>:/fluentd/etc \  ## mount your dir as container dir.
# fluentd:1.0.0 \
# -c /fluentd/etc/fluent.conf  ## pass configuration 

