==========

MQTT
----------

This is test.mosquitto.org. It hosts a publicly available [Eclipse Mosquitto](https://mosquitto.org/) MQTT server/broker. MQTT is a very
lightweight protocol that uses a publish/subscribe model. This makes it
suitable for "machine to machine" messaging such as with low power sensors or
mobile devices.

For more information on MQTT, see <http://mqtt.org/> or the Mosquitto [MQTT man page](https://mosquitto.org/man/mqtt-7.html).

If you are interested in your own hosted instance of Mosquitto you should
look at the [Cedalo](https://cedalo.com/products/mosquitto/)offering. Cedalo are the company that sponsor the main development of
Mosquitto.

The server
----------

The server listens on the following ports:

* 1883 : MQTT, unencrypted, unauthenticated
* 1884 : MQTT, unencrypted, authenticated
* 8883 : MQTT, encrypted, unauthenticated
* 8884 : MQTT, encrypted, client certificate required
* 8885 : MQTT, encrypted, authenticated
* 8886 : MQTT, encrypted, unauthenticated
* 8887 : MQTT, encrypted, server certificate deliberately expired
* 8080 : MQTT over WebSockets, unencrypted, unauthenticated
* 8081 : MQTT over WebSockets, encrypted, unauthenticated
* 8090 : MQTT over WebSockets, unencrypted, authenticated
* 8091 : MQTT over WebSockets, encrypted, authenticated

The encrypted ports support TLS v1.3, v1.2 or v1.1 with x509 certificates
and require client support to connect. For ports 8883 and 8884 you should use the
certificate authority file ([mosquitto.org.crt (PEM format)](ssl/mosquitto.org.crt), or [mosquitto.org.der (DER format)](ssl/mosquitto.org.der)) to verify the server connection. Ports 8081 and 8886 have a Lets Encrypt
certificate, so you should use your system CA certificates or the appropriate
Lets Encrypt CA certificate for verification.

Port 8884 requires clients to
provide a certificate to authenticate their connection. You can[generate your own certificate](/ssl).

The [configuration](/config) is available to view.

Authentication and topic access
----------

Unauthenticated clients have access to publish all topics. Clients can also
subscribe to all topics with the exception of the literal **#** topic.

Connecting with the username **wildcard** will allow a subscription to**#** to succeed for 20 seconds before being automatically removed. This
allows discovery of topics of interest.

The authenticated listeners require a username / password:

* **rw** / **readwrite** : read/write access to the **#** topic hierarchy
* **ro** / **readonly** : read only access to the **#** topic hierarchy
* **wo** / **writeonly** : write only access to the **#** topic hierarchy

You are free to use it for any application, but please do not abuse or rely
upon it for anything of importance. It is not intended to demonstrate any
performance characteristics.

You should also build your client to cope
with the broker restarting.

If you have the mosquitto clients installed
try:

* mosquitto\_sub -h test.mosquitto.org -t "#" -u wildcard -v

Please don't publish anything sensitive, anybody could be listening.

Caveats
----------

This server is provided as a service for the community to do testing, but it
is also extremely useful for testing the server. This means that it will often
be running unreleased or experimental code and may not be as stable as you might
hope. It may also be slow - the broker often runs under [valgrind](http://valgrind.org/) or [perf](https://perf.wiki.kernel.org/index.php/Main_Page). Finally, not
all of the features may be available all of the time, depending on what testing
is being done. In particular, websockets and TLS support are the most likely to
be unavailable.

In general you can expect the server to be up and to be stable though.

Get in touch
----------

Come and discuss the Mosquitto project on [Matrix](https://matrix.to/#/#mosquitto:matrix.eclipse.org) (go to the Mosquitto channel).

If you do publish things to this server on a regular basis, please get in
touch to satisfy my curiosity - there are lots of topics that look interesting
but I know nothing about. I'm **roger** on Matrix, or see the mosquitto source for contact details.

Examples using this service
----------

* [Websockets $SYS tree for test.mosquitto.org](http://test.mosquitto.org/sys/)
* [Websockets $SYS tree for test.mosquitto.org (TLS)](https://test.mosquitto.org/sys/ssl.html)

Keep the service running
----------

Please sponsor this service so we can keep it running.

Get your own server
----------

If you have outgrown this public server and would like your own, you have a few options.

* Host your own broker - this is fairly straightforward to do and will run on any general purpose cloud instance or local server.
* Use a hosted service - [Cedalo](https://cedalo.com/) offers managed hosted Mosquitto instances.
* Use a supported on-premises broker - [Cedalo](https://cedalo.com/) will support your use of Mosquitto, offer consulting for building your system or developing features to your requirements, and have premium features available for Mosquitto.
