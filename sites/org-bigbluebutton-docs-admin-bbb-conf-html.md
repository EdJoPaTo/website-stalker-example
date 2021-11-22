## bbb-conf

# Introduction

bbb-conf
is BigBlueButton’s configuration tool.  It makes it easily for you to modify parts of BigBlueButton’s configuration, manage the BigBlueButton system (start/stop/reset), and troubleshooting potential problems with your setup.

As a historical note, this tool was created early in the development of BigBlueButton.  Early on in its development as BigBlueButton grew, the core developers wrote this tool to quickly update BigBlueButton’s configuration files for setup and testing.

bbb-conf
is located in
/usr/bin/bbb-conf
.  If you are a developer, we recommend taking look through the source for
bbb-conf
(it’s a shell script) as it help you understand the various components of BigBlueButton and how they work together (see also
[Architecture Overview](https://docs.bigbluebutton.org/overview/architecture.html)
).

# Options

If you type
bbb-conf
with no parameters it will print out the list of available options.

$
bbb-conf
BigBlueButton Configuration Utility - Version 1.0.N

   bbb-conf
[
options]

Configuration:
--version
Display BigBlueButton version
(
packages
)
--setip
&lt;host&gt;                   Set IP/hostname
for
BigBlueButton
--setsecret
&lt;secret&gt;             Change the shared secret
in
bigbluebutton.properties

Monitoring:
--check
Check configuration files and processes
for
problems
--debug
Scan the log files
for
error messages
--watch
Scan the log files
for
error messages every 2 seconds
--secret
View the URL and shared secret
for
the server
--lti
View the URL and secret
for
LTI
(
if
installed
)
Administration:
--restart
Restart BigBlueButton
--stop
Stop BigBlueButton
--start
Start BigBlueButton
--clean
Restart and clean all log files
--zip
Zip up log files
for
reporting an error

Testing:
--disablewebrtc
Disables WebRTC audio
in
the server

You run
bbb-conf
as a normal user.  If a particular command requires you to run BigBlueButton as root, it will output a message saying
you need to run this command as root
.  Below is an outline of the various commands.

### --setip &lt;hostname_or_ip&gt;

Sets the IP/Hostname for BigBlueButton’s configuration.  For example, if your BigBlueButton server has the IP address of 192.168.0.211, you can change BigBlueButton’s configuration files to use this IP address with the command

$
sudo
bbb-conf
--setip
192.168.0.211

or, if you want to use the hostname bbb.mybbbserver.com, then use the command

$
sudo
bbb-conf
--setip
bbb.mybbbserver.com

### --clean

Restart BigBlueButton and clear all the log files during the restart.  This is good for debugging as it clears away previous errors in the log files.

### --check

Run a series of check on your current setup and report any potential problems.  Not all reported problems are actual issues.  For example, if you uses
--setip &lt;hostname_or_IP&gt;
, then
bbb-conf
will complain that the hostname does not match the server’s IP, but that’s fine as you configured the BigBlueButton server to listen on a hostname instead of IP address.

### --debug

Greps through the various log files for errors (such as exceptions in the Java log files for tomcat7 and red5).

### --network

This command shows you the number of active connections for port 80 (HTTP), 1935 (RTMP), and 9123 (Desktop sharing) for each remote IP address.

The main purpose of this command is to check for users that are tunnelling to the BigBlueButton server.  If you see a connected users that has no entries in 1935 or 9123, then that users is tunnelling (all their connections are going through port 80).

### --secret

Display the current security salt for the BigBlueButton API.  For example:

$
bbb-conf
--secret
URL: http://192.168.0.35/bigbluebutton/
      Salt: f6c72afaaae95faa28c3fd90e39e7e6e

### --setup-samba

Recommend only running this command if your developing BigBlueButton on a local VM and want to mount the development directory using Windows file sharing.

### --setsecret &lt;new_secret&gt;

Assign a new security secret for the BigBlueButton API.  This does not change the security secret for the API demos, so if you run this command and still want to use the API demos, you’ll need to update the shared secret in
/var/lib/tomcat7/webapps/demo/bbb_api_conf.jsp
.

### --start

Start all the BigBlueButton processes.

### --stop

Stop all the BigBlueButton processes.

### --watch

Watch log files for error messages every 2 seconds.  Use this command after
sudo bbb-conf --clean
to clean out all the log files.

### --zip

Zip up log files for reporting an error.  This option is rarely used as it’s often easier to use pastebin to share the log of the error message if you are, for example, posting to the bigbluebutton-dev mailing list.
