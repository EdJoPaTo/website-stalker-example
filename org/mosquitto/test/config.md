==========

test.mosquitto.org config
----------

This is mosquitto config for test.mosquitto.org.

```
per_listener_settings true

global_plugin /usr/local/lib/mosquitto_persist_sqlite.so
plugin_opt_db_file /var/lib/mosquitto/mosquitto.sqlite3

max_inflight_messages 10
max_queued_messages 1000

# MQTT, anon
listener 1883
allow_anonymous true
set_tcp_nodelay true
# Custom plugin to deny certain wildcard subs
plugin /usr/local/lib/mosquitto_wildcard_temp.so
# Custom plugin to publish message size stats
plugin /usr/local/lib/mosquitto_message_stats.so
# Custom plugin to publish client lifetime stats
plugin /usr/local/lib/mosquitto_lifetime_stats.so

# MQTT, anon, for haproxy
listener 0 /var/lib/mosquitto/mosquitto.sock
allow_anonymous true
set_tcp_nodelay true

# MQTT, password
listener 1884
password_file /etc/mosquitto/tmo.passwd
acl_file /etc/mosquitto/tmo.acl
set_tcp_nodelay true

# MQTT, password, for haproxy
listener 0 /var/lib/mosquitto/mosquitto_pw.sock
password_file /etc/mosquitto/tmo.passwd
acl_file /etc/mosquitto/tmo.acl
set_tcp_nodelay true

# Websockets, anon
listener 8080
protocol websockets
http_dir /var/lib/mosquitto/http_dir
allow_anonymous true
set_tcp_nodelay true

# Websockets, password
listener 8090
protocol websockets
http_dir /var/lib/mosquitto/http_dir
password_file /etc/mosquitto/tmo.passwd
acl_file /etc/mosquitto/tmo.acl
set_tcp_nodelay true

# Encrypted websockets - not used, replaced by haproxy
#listener 8081
#protocol websockets
#capath /etc/ssl/certs
#certfile /etc/mosquitto/certs/le-test.mosquitto.org.pem
#keyfile /etc/mosquitto/certs/le-test.mosquitto.org.key
#http_dir /var/lib/mosquitto/http_dir

websockets_log_level 0

# Encrypted MQTT - not used, replaced by haproxy
#listener 8883
#allow_anonymous true
#cafile /etc/mosquitto/ssl/mosquitto.org.crt
#certfile /etc/mosquitto/ssl/test.mosquitto.org.crt
#keyfile /etc/mosquitto/ssl/test.mosquitto.org.key

# Encrypted MQTT - not used, replaced by haproxy
#listener 8884
#allow_anonymous true
#cafile /etc/mosquitto/ssl/mosquitto.org.crt
#capath /etc/ssl/certs
#certfile /etc/mosquitto/ssl/test.mosquitto.org.crt
#keyfile /etc/mosquitto/ssl/test.mosquitto.org.key
#require_certificate true

# Encrypted MQTT - not used, replaced by haproxy
#listener 8887
#allow_anonymous true
#cafile /etc/mosquitto/ssl/mosquitto.org.crt
#certfile /etc/mosquitto/ssl/test.mosquitto.org.expired.crt
#keyfile /etc/mosquitto/ssl/test.mosquitto.org.expired.key

message_size_limit 1000000

persistence_location /var/lib/mosquitto/

log_dest none
#log_dest file /var/log/mosquitto/mosquitto.log
log_type debug
log_type error
log_type warning
log_type notice
log_type information
log_type internal

```

test.mosquitto.org ACL
----------

```
user rw
topic #

user wo
topic write #

user ro
topic read #

```
