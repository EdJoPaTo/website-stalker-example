## Troubleshooting

If you encountered any problems with the installation of BigBlueButton, this section covers how to resolve many of the common issues.

If you have not already done so, read through the
[getting help section](https://docs.bigbluebutton.org/support/getting-help)
.

## Introduction

**Start here:**
run
sudo bbb-conf --check

We’ve built in a BigBlueButton configuration utility, called
bbb-conf
, to help you configure your BigBlueButton server and troubleshoot your setup if something doesn’t work right.

If you think something isn’t working correctly, the first step is enter the following command.

$
sudo
bbb-conf
--check

This will check your setup to ensure the correct processes are running, the BigBlueButton components have correctly started, and look for common configuration problems that might prevent BigBlueButton from working properly.

If you see text after the line
** Potential problems described below **
, then it may be warnings (which you can ignore if you’ve change settings) or errors with the setup.

## Recording

### Recording not processing after upgrading

If after updating from BigBlueButton 2.0 to BigBlueButton 2.2 your recordings are not processing, and if you are seeing
Permission denied
errors in
/var/log/bigbluebutton/bbb-rap-worker.log

I, [2019-06-07T14:26:09.034878 #14808]  INFO -- : /usr/lib/ruby/2.5.0/logger.rb:754:in `initialize': Permission denied @ rb_sysopen - /var/log/bigbluebutton/presentation/process-02feca80700b3e95b877af85db972904397857a1-1559909318977.log (Errno::EACCES)

You can resolve the errors with the following command

$
sudo chown
-hR
bigbluebutton:bigbluebutton /var/log/bigbluebutton/presentation /var/log/bigbluebutton/screenshare

and then rebuild the recordings that had not yet processed. You can see the list of recordings with

$
bbb-record
--list

and then to rebuild a recording, use
sudo bbb-record --rebuild &lt;internal_meeting_id&gt;
, as in

$
sudo
bbb-record
--rebuild
298b06603719217df51c5d030b6e9417cc036476-1559314745219

## Kurento

### WebRTC video not working with Kurento

Check the value for
/proc/sys/net/ipv4/tcp_syncookies
that it contains the value
1
.

$
cat
/proc/sys/net/ipv4/tcp_syncookies
1

If not, edit
/etc/sysctl.conf
and set the value for
net.ipv4.tcp_syncookies
to
1
.

net.ipv4.tcp_syncookies
=
1

Save the file and restart.

### Unit kurento-media-server.service is masked

If
sudo bbb-conf --check
returns the warning

Restarting BigBlueButton 2.0.0-RC9
(
and cleaning out all log files
)
...
Stopping BigBlueButton
 ... cleaning log files
Starting BigBlueButton
Failed to start kurento-media-server.service: Unit kurento-media-server.service is masked.

You can unmask Kurento using the command

$
systemctl unmask kurento-media-server.service

### Unable to share webcam

The default installation of BigBlueButton should work in most netowrk configurations; however, if your users ae behind a restrictive network that blocks outgoing UDP connections, they may encounter 1020 errors (media unable to reach server).

If you get reports of these errors, setup TURN server to help their browsers send WebRTC audio and video streams via TCP over port 443 to the TURN server. The TURN server will then relay the media to your BigBlueButton server.

See
[Configure TURN](https://docs.bigbluebutton.org/2.2/setup-turn-server.html)
.

## FreeSWITCH

### Configure BigBluebutton/FreeSWITCH to support IPV6

The HTML5 client now enables users on mobile devices to connect to a BigBlueButton server. However, on some cellular networks iOS devices only receive an IPV6 address.

To enable BigBlueButton (FreeSWITCH) to accept incoming web socket connections on IPV6, the BigBlueButton server must have an IPV6 address. You also need to make the following changes to the server.

First, create the file
/etc/nginx/conf.d/bigbluebutton_sip_addr_map.conf
with this content:

map
$remote_addr
$freeswitch_addr
{
"~:"
[2001:db8::1]
;
default
192
.0.2.1
;
}

replacing the ip addresses
192.0.2.1
with the system’s external IPV4 addresses, and replace
2001:db8::1
with the system’s external IPV6 address. Next, edit the file
/etc/bigbluebutton/nginx/sip.nginx
to have the following:

proxy_pass
https://
$freeswitch_addr
:
7443
;

Next, ensure all of the following params are present in freeswitch’s
sip_profiles/external-ipv6.xml
:

- ws-binding
- wss-binding
- rtcp-audio-interval-msec
- rtcp-video-interval-msec
- dtmf-type
- liberal-dtmf
- enable-3pcc

If any are missing, copy them from
sip_profiles/external.xml
, then restart BigBlueButton (
sudo bbb-conf --restart
).

### FreeSWITCH fails to bind to IPV4

In rare occasions after shutdown/restart, the FreeSWITCH database can get corrupted. This will cause FreeSWITCH to have problems binding to IPV4 address (you may see error 1006 when users try to connect).

To check, look in
/opt/freeswitch/var/log/freeswitch/freeswitch.log
for errors related to loading the database.

2018-10-25 11:05:11.444727 [ERR] switch_core_db.c:108 SQL ERR [unsupported file format]
2018-10-25 11:05:11.444737 [ERR] switch_core_db.c:223 SQL ERR [unsupported file format]
2018-10-25 11:05:11.444759 [NOTICE] sofia.c:5949 Started Profile internal-ipv6 [sofia_reg_internal-ipv6]
2018-10-25 11:05:11.444767 [CRIT] switch_core_sqldb.c:508 Failure to connect to CORE_DB sofia_reg_external!
2018-10-25 11:05:11.444772 [CRIT] sofia.c:3049 Cannot Open SQL Database [external]!

If you see these errors, clear the FreeSWITCH database (BigBlueButton doesn’t use the database and FreeSWITCH will recreate it on startup).

$
sudo
systemctl stop freeswitch
$
rm
-rf
/opt/freeswitch/var/lib/freeswitch/db/
*
$
sudo
systemctl start freeswitch

### Forward calls from an Asterisk server to FreeSWITCH

Let’s assume the following:

asterisk server ip:          192.168.1.100
bigbluebutton/freeswitch ip: 192.168.1.200

#### Changes to your Asterisk server

Setup your gateway to BigBlueButton/FreeSWITCH. in
/etc/asterisk/sip.conf
add

[fs-gw]
type
=
peer
username
=
fs-gw
insecure
=
very
contactpermit
=
192.168.1.200/255.255.255.255
qualify
=
no
nat
=
yes
host
=
192.168.1.200
canreinvite
=
no
disallow
=
all
allow
=
ulaw

Route the calls to the gateway. In
/etc/asterisk/extensions.conf
context where your calls are being handled, forward the calls to the gateway. Here, when someone dials 85001, the call is sent to the
fs-gw
defined above.

exten
=&gt;
85001
,
1
,
Dial
(
SIP
/
fs
-
gw
/${
EXTEN
})
exten
=&gt;
85001
,
2
,
Hangup

#### Changes to your BigBlueButton/FreeSWITCH server

In BigBlueButton/FreeSWITCH, make the following changes:

Lock down so that only Asterisk can forward calls to FreeSWITCH. In
/opt/freeswitch/conf/autoload_configs/acl.conf.xml
, add the following ACL. We also need to allow BigBlueButton to call into FreeSWITCH, that’s why we add the IP of BigBlueButton/FreeSWITCH into the ACL.

&lt;list
name=
"asterisk-gw"
default=
"deny"
&gt;
&lt;node
type=
"allow"
cidr=
"192.168.1.200/32"
/&gt;
&lt;node
type=
"allow"
cidr=
"192.168.1.100/32"
/&gt;
&lt;node
type=
"allow"
cidr=
"127.0.0.1/32"
/&gt;
&lt;/list&gt;

Then we apply the ACL into the profile that receives the calls from external gateways. In
/opt/freeswitch/conf/sip_profiles/external.xml
, add the ACL under
&lt;settings&gt;

&lt;settings&gt;
&lt;!-- Apply ACL from asterisk-gw --&gt;
&lt;param
name=
"apply-inbound-acl"
value=
"asterisk-gw"
/&gt;
...
&lt;/settings&gt;

To debug, try connecting to FS CLI and increase logging level. Once connected, make your call and see what the logs say.

$
/opt/freeswitch/bin/fs_cli
-p
$(
xmlstarlet sel
-t
-m
'configuration/settings/param[@name="password"]'
-v
@value /opt/freeswitch/etc/freeswitch/autoload_configs/event_socket.conf.xml
)
Once connected:
help
--
shows the available commands
  console loglevel &lt;level&gt;
--
change log level

  Ctrl-D to
exit

### FreeSWITCH fails to bind to port 8021

FreeSWITCH supports both IPV4 and IPV6. However, if your server does not support IPV6, FreeSWITCH will be unable to bind to port 8021. If you run
sudo bbb-conf --check
and see the following error

# Error: Found text in freeswitch.log:
#
#    Thread ended for mod_event_socket
#
# FreeSWITCH may not be responding to requests on port 8021 (event socket layer)
# and users may have errors joining audio.
#

it might be that your server has IPV6 disabled (or does not support it). You can check this by running the following command

$
sudo
ip addr |
grep
inet6
inet6 ::1/128 scope host
...

If you do not see the line
inet6 ::1/128 scope host
, then your server has IPV6 disabled. In this case, we need to disable FreeSWITCH’s support for IPV6. First, edit
/opt/freeswitch/etc/freeswitch/autoload_configs/event_socket.conf.xml
and change the line

&lt;param
name=
"listen-ip"
value=
"::"
/&gt;

to

&lt;param
name=
"listen-ip"
value=
"127.0.0.1"
/&gt;

This tells FreeSWITCH that instead of binding port 8021 to the local IPV6 address, bind to the IPV4 address 127.0.0.1. Next, execute the following two commands

$
sudo mv
/opt/freeswitch/etc/freeswitch/sip_profiles/internal-ipv6.xml /opt/freeswitch/etc/freeswitch/sip_profiles/internal-ipv6.xml_
$
sudo mv
/opt/freeswitch/etc/freeswitch/sip_profiles/external-ipv6.xml /opt/freeswitch/etc/freeswitch/sip_profiles/external-ipv6.xml_

and then restart BigBlueButton with the commands

$
sudo
bbb-conf
--clean
$
sudo
bbb-conf
--check

### FreeSWITCH fails to start with a SETSCHEDULER error

When running in a container (like a chroot, OpenVZ or LXC), it might not be possible for FreeSWITCH to set its CPU priority to
[real-time round robin](https://man7.org/linux/man-pages/man2/sched_setscheduler.2.html)
. If not, it will result in lower performance compared to a non-virtualized installation.

If you running BigBlueButton in a container and an error starting FreeSWITCH, try running
systemctl status freeswitch.service
and see if you see the error related to SETSCHEDULER

$
systemctl status freeswitch.service
● freeswitch.service - freeswitch
   Loaded: loaded
(
/lib/systemd/system/freeswitch.service
;
enabled
;
vendor preset: enabled
)
Active: inactive
(
dead
)
(
Result: exit-code
)
since Mon 2017-10-02 16:17:29 UTC
;
18s ago
  Process: 10967
ExecStart
=
/opt/freeswitch/bin/freeswitch
-u
freeswitch
-g
daemon
-ncwait
$DAEMON_OPTS
(
code
=
exited,
status
=
214/SETSCHEDULER
)
Main PID: 3327
(
code
=
exited,
status
=
0/SUCCESS
)
Oct 02 16:17:29 scw-9e2305 systemd[1]: Failed to start freeswitch.
Oct 02 16:17:29 scw-9e2305 systemd[1]: freeswitch.service: Unit entered failed state.
Oct 02 16:17:29 scw-9e2305 systemd[1]: freeswitch.service: Failed with result
'exit-code'
.
Oct 02 16:17:29 scw-9e2305 systemd[1]: freeswitch.service: Service hold-off
time
over, scheduling restart.
Oct 02 16:17:29 scw-9e2305 systemd[1]: Stopped freeswitch.
Oct 02 16:17:29 scw-9e2305 systemd[1]: freeswitch.service: Start request repeated too quickly.
Oct 02 16:17:29 scw-9e2305 systemd[1]: Failed to start freeswitch.

If you see
SETSCHEDULER
in the error message, edit
/lib/systemd/system/freeswitch.service
and comment out the line containing
CPUSchedulingPolicy=rr
(round robin)

IOSchedulingPriority
=
2
#CPUSchedulingPolicy=rr
CPUSchedulingPriority
=
89

Save the file, run
systemctl daemon-reload
, and then restart BigBlueButton. FreeSWITCH should now startup without error.

### Users not able to join Listen Only mode

When doing
sudo bbb-conf --check
, you may see the warning

voice Application failed to register with sip server

This error occurs when
bbb-apps-sip
isn’t able to make a SIP call to FreeSWITCH. You’ll see this in BigBlueButton when users click the headset icon and don’t join the voice conference.

One possible cause for this is you have just installed BigBlueButton, but not restarted it. The packages do not start up the BigBlueButton components in the right order. To restart BigBlueButton, do the following:

$
sudo
bbb-conf
--restart
$
sudo
bbb-conf
--check

If you don’t want FreeSWITCH to bind to 127.0.0.1, you need to figure out which IP address its using. First, determine the IP address FreeSWITCH is monitoring for incoming SIP calls with the following command:

$
netstat
-ant
|
grep
5060

You should see an output such as

tcp        0      0 234.147.116.3:5060    0.0.0.0:
*
LISTEN

In this example, FreeSWITCH is listening on IP address 234.147.116.3. The IP address on your server will be different.

Next, edit
/usr/share/red5/webapps/sip/WEB-INF/bigbluebutton-sip.properties
and set the value for
sip.server.host
to the IP address returned from the above command. Save the changes (you’ll need to edit the file as root to save changes).

Restart BigBlueButton using the commands and run the built-in diagnostics checks.

$
sudo
bbb-conf
--clean
$
sudo
bbb-conf
--check

### Unable to connect using fs_cli

As of BigBlueButton 2.2.18, the packaging now replaces the default
ClueCon
password for connecting to the FreeSWITCH command line interface (
fs_cli
) with a random password.

(By default, FreeSWITCH only allowed unauthenticated connections from 127.0.0.1, but it’s still good security practice to not use default passwords).

To connect to
fs_cli
, use the following command which supplies the password for authenticating.

/opt/freeswitch/bin/fs_cli -p $(xmlstarlet sel -t -m 'configuration/settings/param[@name="password"]' -v @value /opt/freeswitch/etc/freeswitch/autoload_configs/event_socket.conf.xml)

We also added
/usr/local/bin/fs_clibbb
with the contents

#!/bin/bash
/opt/freeswitch/bin/fs_cli
-p
$(
xmlstarlet sel
-t
-m
'configuration/settings/param[@name="password"]'
-v
@value /opt/freeswitch/etc/freeswitch/autoload_configs/event_socket.conf.xml
)

that will let you type
fs_clibbb
at the command prompt to get into FreeSWITCH console.

### Echo test hangs upgrading BigBlueButton 2.2

The install scripts now change the default CLI password for FreeSWITCH and the other parts of BigBlueButton need to use this new password. For a new installation, the install scripts will automatically set this new password.

If you upgrade using
[bbb-install.sh](https://github.com/bigbluebutton/bbb-install)
, the script will update the FreeSWITCH password using
sudo bbb-conf --setip &lt;hostname&gt;
.

If you upgraded using
[manual steps](https://docs.bigbluebutton.org/2.2/install.html#upgrading-from-bigbluebutton-22)
, be sure to do ao
sudo bbb-conf --setip &lt;hostname&gt;
to sync all the FreeSWITCH passwords.

### FreeSWITCH using default stun server

For many years, in BigBlueButton’s FreeSWITCH configuration file
/opt/freeswitch/etc/freeswitch/vars.xml
, the default value for
external_rtp_ip
was
stun.freeswitch.org

&lt;X-PRE-PROCESS
cmd=
"set"
data=
"external_rtp_ip=stun:stun.freeswitch.org"
/&gt;

However, this is not a reliable choice for stun server. Recommend either changing it to your servers external IP address or setup your own
[stun/turn server](https://docs.bigbluebutton.org/admin/setup-turn-server.html)
. For example, if your server has an external IP at 234.32.3.3

&lt;X-PRE-PROCESS
cmd=
"set"
data=
"external_rtp_ip=234.32.3.3"
/&gt;

You can add a line in
/etc/bigbluebutton/bbb-conf/apply-conf.sh
to always apply this value even if the FreeSWITCH package upgrades.

xmlstarlet edit
--inplace
--update
'//X-PRE-PROCESS[@cmd="set" and starts-with(@data, "external_rtp_ip=")]/@data'
--value
"external_rtp_ip=234.32.3.3"
/opt/freeswitch/conf/vars.xml

Note: If your server has an internal/exteral IP address, such as on AWS EC2 server, be sure to set it to the external IP address configure a dummy network interface card (see
[Update FreeSWITCH](https://docs.bigbluebutton.org/admin/configure-firewall.html#update-freeswitch)
).

## HTML5 Server

### bbb-html5 fails to start with a SETSCHEDULER error

As of 2.2.31, the systemd unit file for
bbb-html5.service
now contains the following lines

CPUSchedulingPolicy
=
fifo
Nice
=
19

You can override this with creating the following directory

mkdir /etc/systemd/system/bbb-html5.service.d

and creating
/etc/systemd/system/bbb-html5.service.d/override.conf
with the following contents

[Service]
CPUSchedulingPolicy=other
Nice=-10

Then do
systemctl daemon-reload
and restart BigBlueButton.

## Installation and packages

### The following packages have unmet dependencies

When installing the latest build of BigBlueButton, the package
bbb-conf
now uses
yq
to manage YAML files.

You need to add the repository
ppa:rmescandon/yq
to your server. For steps on how to do this, see
[Update your server](http://docs.bigbluebutton.org/2.2/install.html#1-update-your-server)
in the BigBlueButton 2.2 install guide.

Alternatively, if you have not made any customizations to BigBlueButton (outside of using
bbb-conf
), you can use
[bbb-install.sh](https://github.com/bigbluebutton/bbb-install)
to install/upgrade to the latest version (the
bbb-install.sh
script will automatically install the repository for
yq
).

### No Symbolic Link

If you’ve installed/uninstalled BigBlueButton packages, you may get a
No Symbolic Link
warning from
bbb-conf --check
:

**
Potential Problems
**
nginx
(
conf
)
: no symbolic
link
in
/etc/nginx/sites-enabled
for
bigbluebutton

To solve this, add a symbolic link to nginx for the BigBlueButton site:

$
sudo ln
-s
/etc/nginx/sites-available/bigbluebutton /etc/nginx/sites-enabled/bigbluebutton
$
sudo
/etc/init.d/nginx restart

### Package install fails with sed error

Some of the BigBlueButton packages use
sed
scripts to extract contents from configuration files. If the file does not exist at the time of the script’s execution, or the sed script matches multiple entries in a file (such as when a configuration line is commented out), you can see an error such as

Setting up bbb-client
(
1:2.0.0-374
)
...
sed
:
-e
expression
#1, char 42: unterminated `s' command
dpkg: error processing package bbb-client
(
--configure
)
:
 subprocess installed post-installation script returned error
exit
status 1
dpkg: dependency problems prevent configuration of bbb-config:
 bbb-config depends on bbb-client
;
however:
  Package bbb-client is not configured yet.

dpkg: error processing package bbb-config
(
--configure
)
:
 dependency problems - leaving unconfigured
Errors were encountered
while
processing:
 bbb-client
 bbb-config
E: Sub-process /usr/bin/dpkg returned an error code
(
1
)

In the above example, the
/var/lib/dpkg/info/bbb-client.postinst
failed to finish. To debug, edit this file and change the first line to read

#!/bin/bash -ex

and run

$
sudo
apt-get
install
-f

You should now see each command in
bbb-conf.postinst
as it executes upto the line in which the error occurs. Post this output to
https://groups.google.com/forum/#!forum/bigbluebutton-setup
for help in resolving the issue.

### Errors with packages

Some hosting providers do not provide a complete
/etc/apt/source.list
. If you are finding your are unable to install a package, try replacing your
/etc/apt/sources.list
with the following

deb http://archive.ubuntu.com/ubuntu xenial main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu xenial-updates main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu xenial-security main restricted universe multiverse

then do

$
sudo
apt-get update

and try installing BigBlueButton again from the beginning.

## WebRTC errors (1001, 1002,…)

WebRTC offers very high-quality audio. However, the user’s network settings (or firewall) may not allow WebRTC to connect (or keep connected).

Here are the following lists the possible WebRTC error messages that a user may encounter:

- **1001: WebSocket disconnected**
- The WebSocket had connected successfully and has now disconnected. Possible Causes:
	- Loss of internet connection
	- Nginx restarting can cause this
- **1002: Could not make a WebSocket connection**
- The initial WebSocket connection was unsuccessful. Possible Causes:
	- Firewall blocking ws protocol
	- Server is down or improperly configured
	- See potential solution
[here](https://github.com/bigbluebutton/bigbluebutton/issues/2628)
.
- **1003: Browser version not supported**
- Browser doesn’t implement the necessary WebRTC API methods. Possible Causes:
	- Out of date browser
- **1004: Failure on call**
- The call was attempted, but failed. Possible Causes:
	- For a full list of causes refer
[here](http://sipjs.com/api/0.6.0/causes/)
	- There are 24 different causes so I don’t really want to list all of them
	- Solution for this issue
[outlined here](https://groups.google.com/forum/#!msg/bigbluebutton-setup/F2MlW6Voj-0/ZXDq5_-uEQAJ)
.
- **1005: Call ended unexpectedly**
- The call was successful, but ended without user requesting to end the session. Possible Causes:
	- Unknown
- **1006: Call timed out**
- The library took too long to try and connect the call. Possible Causes:
	- Previously caused by Firefox 33-beta on Mac. We’ve been unable to reproduce since release of FireFox 34
- **1007: ICE negotiation failed**
- The browser and FreeSWITCH try to negotiate ports to use to stream the media and that negotiation failed. Possible Causes:
	- NAT is blocking the connection
	- Firewall is blocking the UDP connection/ports
- **1008: Call transfer failed**
- A timeout while waiting for FreeSWITCH to transfer from the echo test to the real conference. This might be caused by a misconfiguration in FreeSWITCH, or there might be a media error and the DTMF command to transfer didn’t go through (In this case, the voice in the echo test probably didn’t work either.)
- **1009: Could not fetch STUN/TURN server information**
- This indicates either a BigBlueButton bug (or you’re using an unsupported new client/old server combination), but could also happen due to a network interruption.
- **1010: ICE negotiation timeout**
- After the call is accepted the client’s browser and the server try and negotiate a path for the audio data. In some network setups this negotiation takes an abnormally long time to fail and this timeout is set to avoid the client getting stuck.
- **1020: Media cloud could not reach the server**
- See how to solve this
[here](https://github.com/bigbluebutton/bigbluebutton/issues/6797#issuecomment-607866043)
.

## Networking

### Server running behind NAT

The
[following issue](https://github.com/bigbluebutton/bigbluebutton/issues/8792)
might be helpful in debugging if you run into errors and your server is behind NAT.

### Could not get your microphone for a WebRTC call

Chrome requires (As of Chrome 47) that to access the user’s microphone for WebRTC your site must be serving pages via HTTPS (that is, nginx is configured with a SSL certificate).

If the user attempts to share their microphone and your BigBlueButton sever is not configured for SSL, Chrome will block access and BigBlueButton will report the following error

*WebRTC Audio Failure: Detected the following WebRTC issue: Could not get your microphone for a WebRTC call. Do you want to try flash instead?*

To enable Chrome to access the user’s microphone, see
[Configure HTTPS on BigBlueButton](https://docs.bigbluebutton.org/2.2/install.html#configure-ssl-on-your-bigbluebutton-server)
.

### The browser is not supported

When you attempt to join a BigBlueButton session, the client looks for supported browsers before fully loading. The client gets its list of supported browsers from
/usr/share/meteor/bundle/programs/server/assets/app/config/settings.yml
. You can see the list of supported browsers at the bottom. For example,

-
browser
:
mobileSafari
version
:
-
11
-
1

states that
Mobile Safari
version 11.1 or later is supported (notice the first letter is lower case and concatenated with the remainder of the browser name).

To add a browser to the list, first open the following page
[https://test.bigbluebutton.org/html5client/useragent](https://demo.bigbluebutton.org/html5client/useragent)
with the browser, which will print its useragent string. For example, with the Vivaldi browser you might see

Vivaldi 2.8.1664 / Linux 0.0.0

Next, to add this as a supported browser, append to
settings.yml

-
browser
:
vivaldi
version
:
-
2
-
8

save the updated
settings.yml
file, and then restart your BigBlueButton server with
sudo bbb-conf --restart
. Note any browser you add must support WebRTC libraries (not all do), so be sure to check it first with
[https://test.webrtc.org/](https://test.webrtc.org/)
.

### Tomcat shows “Cannot assign requested address on startup”

If your server has multiple IP addresses, Tomcat might not pick the right address to bind. This could throw an error on installation when tomcat is attempting to install.

Check
/var/log/tomcat7/catalina.out
for the following error

Jan 30, 2018 9:17:37 AM org.apache.catalina.core.StandardServer await
SEVERE: StandardServer.await: create[localhost:8005]:
java.net.BindException: Cannot assign requested address (Bind failed)
 at java.net.PlainSocketImpl.socketBind(Native Method)

If you see this, first ensure that there isn’t another copy of tomcat running by doing
ps -aef | grep tomcat7
. If you do see another copy running, try killing it and then restarting tomcat.

If you still see the same error in
catalina.out
, then
/etc/tomcat7/server.xml
and change

&lt;Server
port=
"8005"
shutdown=
"SHUTDOWN"
&gt;
&lt;Server
address=
"0.0.0.0"
port=
"8005"
shutdown=
"SHUTDOWN"
&gt;

Restart tomcat7 again and it should start normally.

### nginx not running

The common reasons for nginx not running are inability to bind to port 80 and configuration errors. To check if port 80 is already in use, use

$
sudo
netstat
-ant

to see if any process is currently bound to port 80. If so, check to see if another web server is installed. If so, then stop the web server and try to restart nginx. One of the server requirements before you install BigBlueButton is that port 80 is not in use by another application (such as Apache). For details on why this is a requirements, see
[We recommend running BigBlueButton on port 80](http://docs.bigbluebutton.org/support/faq.html#we-recommend-running-bigbluebutton-on-port-80443)
.

If port 80 is free, check if your nginx configuration file has errors. Try a restart of nginx

$
sudo
systemctl restart nginx

and look for the output of

[ OK ]

If you see
[ Fail ]
, then your nginx configuration files might have a syntax error. Check the syntax of the nginx configuration files using the command

$
sudo
nginx
-t

and see if it reports any errors. You can also check the error.log file for nginx to see what errors it gives on startup

$
sudo cat
/var/log/nginx/error.log

### “Welcome to nginx”

During installation of BigBlueButton the packaging scripts attempt to assign the correct IP address during setup. However, if the IP address changes (such as when rebooting a VM), or the first IP address was not the correct IP address for the server, you may see a “Welcome to nginx” page.

To reconfigure the BigBlueButton to use the correct IP address or hostname, see
[BigBlueButton does not load](https://docs.bigbluebutton.org/support/troubleshooting.html#bigbluebutton-does-not-load)
.

## bbb-web

### 404 Error when loading the client

BigBlueButton 2.2 requires Java 8 as the default Java. Recently, some Ubuntu 16.04 distributions have switched the default version of Java to Java 9 (or later).

Use
java -version
to check that the default version of
1.8.0
.

~/dev
$
java
-version
openjdk version
"1.8.0_242"
OpenJDK Runtime Environment
(
build 1.8.0_242-8u242-b08-0ubuntu3~16.04-b08
)
OpenJDK 64-Bit Server VM
(
build 25.242-b08, mixed mode
)

If not, do the following

sudo
apt-get
install
openjdk-8-jre
update-alternatives
--config
java
# Choose java-8 as default

Run
java -version
and confirm it now shows the default as
1.8.0
, and then restart BigBlueButton with
sudo bbb-conf --restart

### Blank presentation area on create or upload

If you join a meeting and the default presentation is not visible or your uploaded presentation doesn’t display, then this is most likely due to a permissions error. To solve this, ensure that
/var/bigbluebutton/
is owned by
bigbluebutton
rather than
root
or any other account. See
[this issue](https://github.com/bigbluebutton/bigbluebutton/issues/9867)
for more explanation.

### Unable to create presentation

If you see the following error in
/var/log/bigbluebutton/bbb-web.log

failed to map segment from shared object: Operation not permitted

use the command
mount
to check that the
/tmp
director does not have
noexec
permissions (which would prevent executables from running in the /tmp directory). If you see
noexec
for
/tmp
, you need to remount the directory with permissions that enable processes (such as the slide conversion) to execute in the
/tmp
directory.

### Too many open files

On servers with greater than 8 CPU cores,
bbb-web
log (
/var/log/bigbluebutton/bbb-web.log
) may throw an error of
Too many open files

Caused by: java.io.IOException: Too many open files

To resolve, create an override file that increases the number of open files for
bbb-web

$
sudo mkdir
-p
/etc/systemd/system/bbb-web.service.d/
$
sudo cat
&gt;
/etc/systemd/system/bbb-web.service.d/override.conf
&lt;&lt;
HERE
[Service]
LimitNOFILE=
LimitNOFILE=8192
HERE
$
sudo
systemctl daemon-reload

### bbb-web takes a long time to startup

bbb-web
relies on the SecureRandom class (which uses available entropy) to provide random values for its session IDs. On a virtualized server, however, the available entropy can run low and cause bbb-web to block for a long period before it finishes it’s startup sequence (see
[Slow startup of tomcat](https://stackoverflow.com/questions/28201794/slow-startup-on-tomcat-7-0-57-because-of-securerandom)
).

To provide
bbb-web
with more entropy, you can install haveged

$
sudo
apt-get
install
haveged

For more information see
[How to Setup Additional Entropy for Cloud Servers Using Haveged](https://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)
.

### Error installing bbb-web

If you get the following error during upgrade to BigBlueButton

Unpacking bbb-web
(
1:2.2.0-67
)
over
(
1:2.2.0-66
)
...
dpkg: error processing archive /var/cache/apt/archives/bbb-web_1%3a2.2.0-67_amd64.deb
(
--unpack
)
:
 trying to overwrite
'/etc/bigbluebutton/nginx/web'
, which is also
in
package bbb-client 1:2.2.0-28
dpkg-deb: error: subprocess
paste
was killed by signal
(
Broken pipe
)
Errors were encountered
while
processing:
 /var/cache/apt/archives/bbb-web_1%3a2.2.0-67_amd64.deb
E: Sub-process /usr/bin/dpkg returned an error code
(
1
)
```

Then first uninstall
bbb-client

$
sudo
apt-get purge bbb-client

and try installing BigBlueButton again.

## Other errors

### Root partition too small

If the root partition on your BigBlueButton server is too small (for disk space requirements see
[Before you install](https://docs.bigbluebutton.org/2.2/install.html#before-you-install)
), we recommend moving the following directories to an external partition with sufficient disk space.

BigBlueButton processing and storage of recordings:

Location of all media directories on disk
[available here](https://docs.bigbluebutton.org/dev/recording.html#media-storage)
.

To make the move, we’ll first stop BigBlueButton, then move the above directories to a new location on the external partition, create symbolic links from the original locations to the new locations, and restart BigBlueButton.

In the following example, the external partition is mounted on
/mnt
.

$
sudo
bbb-conf
--stop
$
sudo mv
/var/freeswitch/meetings /mnt
$
sudo ln
-s
/mnt/recordings /var/freeswitch/meetings
$
sudo mv
/usr/share/red5/webapps/video/streams /mnt
$
sudo ln
-s
/mnt/streams /usr/share/red5/webapps/video/streams
$
sudo
/var/bigbluebutton /mnt
$
sudo ln
-s
/mnt/bigbluebutton /var/bigbluebutton
$
sudo
bbb-conf
--start

### BigBlueButton does not load

If your has changed it’s network connection (such as on reboot), you can clean most of BigBlueButton’s configuration files with the following steps.

$
sudo
bbb-conf
--setip
&lt;ip_address_or_hostname&gt;
$
sudo
bbb-conf
--clean
$
sudo
bbb-conf
--check

For more information see
[bbb-conf options](https://docs.bigbluebutton.org/install/bbb-conf.html)
.

### Running within an LXD Container

[LXD](https://www.ubuntu.com/containers/lxd)
is a very powerful container system for Ubuntu lets you run full Ubuntu 16.04 servers within a container. Because you can easily clone and snapshot LXD containers, they are ideal for development and testing of BigBlueButton.

However, if you install BigBlueButton within an LXD container, you will get the following error from
sudo bbb-conf --check

**
Potential problems described below
**
#
# Error: Unable to connect to the FreeSWITCH Event Socket Layer on port 8021

You’ll also get an error from starting FreeSWITCH with
bbb-conf --restart
. When you try
systemctl status freeswitch.service
, you’ll see an error with SETSCHEDULER.

$
sudo
systemctl status freeswitch.service
● freeswitch.service - freeswitch
   Loaded: loaded
(
/lib/systemd/system/freeswitch.service
;
enabled
;
vendor preset: enabled
)
Active: inactive
(
dead
)
(
Result: exit-code
)
since Wed 2017-04-26 16:34:24 UTC
;
23h ago
  Process: 7038
ExecStart
=
/opt/freeswitch/bin/freeswitch
-u
freeswitch
-g
daemon
-ncwait
$DAEMON_OPTS
(
code
=
exited,
status
=
214/SETSCHEDULER
)
Apr 26 16:34:24 big systemd[1]: Failed to start freeswitch.
Apr 26 16:34:24 big systemd[1]: freeswitch.service: Unit entered failed state.
Apr 26 16:34:24 big systemd[1]: freeswitch.service: Failed with result
'exit-code'
.
Apr 26 16:34:24 big systemd[1]: freeswitch.service: Service hold-off
time
over, scheduling restart.
Apr 26 16:34:24 big systemd[1]: Stopped freeswitch.
Apr 26 16:34:24 big systemd[1]: freeswitch.service: Start request repeated too quickly.
Apr 26 16:34:24 big systemd[1]: Failed to start freeswitch.

This error occurs because the default systemd unit script for FreeSWITCH tries to run with permissions not available to the LXD container. To run FreeSWITCH within an LXD container, edit
/lib/systemd/system/freeswitch.service
and replace with the following

[Unit]
Description
=
freeswitch
After
=
syslog.target network.target local-fs.target
[Service]
Type
=
forking
PIDFile
=
/opt/freeswitch/var/run/freeswitch/freeswitch.pid
Environment
=
"DAEMON_OPTS=-nonat"
EnvironmentFile
=
-/etc/default/freeswitch
ExecStart
=
/opt/freeswitch/bin/freeswitch -u freeswitch -g daemon -ncwait $DAEMON_OPTS
TimeoutSec
=
45s
Restart
=
always
WorkingDirectory
=
/opt/freeswitch
User
=
freeswitch
Group
=
daemon
[Install]
WantedBy
=
multi-user.target

Then enter the following commands to load the new unit file and restart BigBlueButton.

$
sudo
systemctl daemon-reload
$
sudo
bbb-conf
--restart

You can run BigBlueButton within a LXD container.

### Unable to connect to redis

The packages
bbb-apps-akka
,
bbb-fsesl-akka
, and
bbb-transcode-akka
are packaged by sbt, but they need to have redis-server running before they startup. If
sudo bbb-conf --debug
shows redis connection errors

Sep 22 15:32:12 sv21 bbb-apps-akka[7804]: Exception in thread "main" io.lettuce.core.RedisConnectionException: Unable to connect to 127.0.0.1:6379
Sep 22 15:32:12 sv21 bbb-apps-akka[7804]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:78)
Sep 22 15:32:12 sv21 bbb-apps-akka[7804]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:56)
Sep 22 15:32:12 sv21 bbb-apps-akka[7804]: Caused by: io.netty.channel.AbstractChannel$AnnotatedConnectException: Connection refused: /127.0.0.1:6379
Sep 22 15:32:12 sv21 bbb-apps-akka[7804]: Caused by: java.net.ConnectException: Connection refused
Sep 22 15:32:12 sv21 bbb-fsesl-akka[7893]: Exception in thread "main" io.lettuce.core.RedisConnectionException: Unable to connect to 127.0.0.1:6379
Sep 22 15:32:12 sv21 bbb-fsesl-akka[7893]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:78)
Sep 22 15:32:12 sv21 bbb-fsesl-akka[7893]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:56)
Sep 22 15:32:12 sv21 bbb-fsesl-akka[7893]: Caused by: io.netty.channel.AbstractChannel$AnnotatedConnectException: Connection refused: /127.0.0.1:6379
Sep 22 15:32:12 sv21 bbb-fsesl-akka[7893]: Caused by: java.net.ConnectException: Connection refused
Sep 22 15:32:13 sv21 bbb-transcode-akka[8001]: Exception in thread "main" io.lettuce.core.RedisConnectionException: Unable to connect to 127.0.0.1:6379
Sep 22 15:32:13 sv21 bbb-transcode-akka[8001]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:78)
Sep 22 15:32:13 sv21 bbb-transcode-akka[8001]: #011at io.lettuce.core.RedisConnectionException.create(RedisConnectionException.java:56)
Sep 22 15:32:13 sv21 bbb-transcode-akka[8001]: Caused by: io.netty.channel.AbstractChannel$AnnotatedConnectException: Connection refused: /127.0.0.1:6379
Sep 22 15:32:13 sv21 bbb-transcode-akka[8001]: Caused by: java.net.ConnectException: Connection refused

you can add overrides for these three packages to ensure they start after redis.server. Run the following script.

#!/bin/bash

mkdir -p /etc/systemd/system/bbb-apps-akka.service.d
cat &gt; /etc/systemd/system/bbb-apps-akka.service.d/override.conf &lt;&lt;HERE
[Unit]
Requires=redis-server.service
After=redis-server.service
HERE

mkdir -p /etc/systemd/system/bbb-fsesl-akka.service.d
cat &gt; /etc/systemd/system/bbb-fsesl-akka.service.d/override.conf &lt;&lt;HERE
[Unit]
Requires=redis-server.service
After=redis-server.service
HERE

mkdir -p /etc/systemd/system/bbb-transcode-akka.service.d
cat &gt; /etc/systemd/system/bbb-transcode-akka.service.d/override.conf &lt;&lt;HERE
[Unit]
Requires=redis-server.service
After=redis-server.service
HERE

The script
bbb-install
now creates these overrides by default.

### 500 Internal Server Error

It is most likely an error on GreenLight. Check the log file according to
[Troubleshooting Greenlight](https://docs.bigbluebutton.org/greenlight/gl-install.html#troubleshooting-greenlight)
.

If this error occurrs on just a small number of PCs accessing a BigBlueButton server within a LAN through a proxy server and you find the description “Error::Unsafe Host Error (x.x.x.x is not a safe host)” (where x.x.x.x is an IP address) in the log file, check if the “Don’t use the proxy server for local (intranet) addresses” (in the Windows proxy setting) is ticked.

## Legacy errors

### Conference not found errors

The command
sudo bbb-conf --debug
searches through the red5, tomcat7, and nginx logs looking for errors and exceptions. However, the messages such as

-- ERRORS found in /usr/share/red5/log/* --
/usr/share/red5/log/bigbluebutton.log:2015-05-02 13:50:37,681-04:00 [pool-17-thread-1] ERROR o.b.w.v.f.a.PopulateRoomCommand - Not XML: [Conference 78505 not found]

are innocuous and can be ignored.
