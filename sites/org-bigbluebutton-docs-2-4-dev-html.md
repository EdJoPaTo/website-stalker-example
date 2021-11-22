## Development

Welcome to the BigBlueButton Developer’s Guide for BigBlueButton 2.4.

This document gives you an overview of how to set up a development environment for BigBlueButton 2.4.

# Before you begin

You first need to set up a BigBlueButton 2.4 server. See the instructions at
[Install BigBlueButton 2.4](https://docs.bigbluebutton.org/2.4/install.html)
.

# Overview

A BigBlueButton server is built from a number of components that correspond to Ubuntu packages. Some of these components are

- bbb-web – Implements the BigBlueButton API and conversion of documents for presentation
- akka-bbb-apps – Server side application that handles the state of meetings on the server
- bbb-html5 – HTML5 client that loads in the browser. The client server-side Meteor application that leverages MongoDB and React.js
- bbb-learning-dashboard – a live dashboard available to moderators, which displays user activity information that can be useful for instructors
- bbb-fsesl-akka – Component to send commands to FreeSWITCH
- bbb-playback-presentation – Record and playback script to create presentation layout
- bbb-webrtc-sfu – Server that bridges incoming requests from client to Kurento
- kurento-media-server – WebRTC media server for sending/receiving/recording video (webcam and screen share)
- bbb-freeswitch-core – WebRTC media server for sending/receiving/recording audio

This document describes how to set up a development environment using an existing BigBlueButton 2.4 server. Once the environment is set up, you will be able to make custom changes to BigBlueButton source, compile the source, and replace the corresponding components on the server (such as updating the BigBlueButton client).

The instructions in this guide are step-by-step so you can understand each step needed to modify a component. If you encounter problems or errors at any section, don’t ignore the errors. Stop and double-check that you have done the step correctly. If you are unable to determine the cause of the error, do the following

- First, use Google to search for the error. There is a wealth of information in
[bigbluebutton-dev](https://groups.google.com/forum/?fromgroups=#!forum/bigbluebutton-dev)
that has been indexed by Google.
- Try doing the same steps on a different BigBlueButton server.
- Post a question to bigbluebutton-dev with a description of the problem and the steps to reproduce. Post logs and error messages to
[Pastebin](http://pastebin.com/)
link them in your post.

### You Have a Working BigBlueButton Server

Before you can start developing on BigBlueButton, you must install BigBlueButton 2.4 (see
[installation steps](https://docs.bigbluebutton.org/2.4/install.html)
) and ensure it’s working correctly. Make sure there were no errors during the installation and that you can join a session successfully.

We emphasize that your BigBlueButton server must be working
**before**
you start setting up the development environment. Be sure that you can log in, start sessions, join the audio bridge, share your webcam, and record and play back sessions – all using the built-in API demos.

By starting with a working BigBlueButton server, you have the ability to switch back-and-forth between the default-packaged components and any modifications you make.

For example, suppose you modify the BigBlueButton client and something isn’t working (such as the client is not fully loading), you can easily switch back to the default-packaged client and check that it’s working correctly (thus ruling out any environment issues that may also be preventing your modified client from loading).

**Another Note:**
These instructions assume you have the
bbb-demo
package installed so you can run any of the API demos to test your setup.

### Developing on Windows

To develop BigBlueButton from within Windows, you have two options:

- use Windows Subsystem for Linux
- use VMWare Player or VirtualBox to create a virtual machine (VM).

Choose the OS to be Ubuntu 18.04 64-bit. The associated documentation for VMWare Player and VirtualBox or WSL will guide you on setting up a new 18.04 64-bit VM.

**Note:**
When setting up the VM, it does not matter to BigBlueButton if you set up Ubuntu 18.04 server or desktop. If you install desktop, you’ll have the option of using a graphical interface to edit files. When running the VM, you will need a host operating system capable of running a
[64-bit virtual machine](http://stackoverflow.com/questions/56124/can-i-run-a-64-bit-vmware-image-on-a-32-bit-machine)
.

### Developing on Linux host via container

Consider using a Docker setup for a development environment - https://github.com/bigbluebutton/docker-dev

### Root Privileges

**Important:**
Make sure you create another user such as “ubuntu” to avoid running into permission errors such as Nginx 403 Forbidden error or
[error-null-while-compiling-resource-bundles-under-linux-with-hudson](http://stackoverflow.com/questions/3863066/error-null-while-compiling-resource-bundles-under-linux-with-hudson)
.

Do not run commands as the root user and only use sudo when instructed to.

These instructions are written for an account called “ubuntu”, but they will apply to any account that has the permissions to execute commands as root, such as

sudo ls

### wget

You’ll need to download some files throughout these instructions using wget. If it’s not installed on your server, you can install the package using the following command

sudo
apt-get
install
wget

### Have a GitHub Account

The BigBlueButton
[source is hosted on GitHub](https://github.com/bigbluebutton/bigbluebutton)
. You need a GitHub account. In addition, you need to be very familiar with how git works. Specifically, you need to know how to

- clone a repository
- create a branch
- push changes back to a repository

If you have not used git before, or if the terms
***clone***
,
***branch***
, and
***commit***
are unfamiliar to you, stop now. These are fundamental concepts to git that you need to become competent with before trying to develop on BigBlueButton. To become competent, a good place to start is this
[free book](http://git-scm.com/book)
and
[GitHub Help pages](http://help.github.com/)
.

Using GitHub makes it easy for you to work on your own copy of the BigBlueButton source, store your updates to the source to your GitHub account, and make it easy for you to
[contribute to BigBlueButton](https://docs.bigbluebutton.org/support/faq.html#contributing-to-bigbluebutton)
.

### Subscribe to bigbluebutton-dev

We recommend you subscribe to the
[bigbluebutton-dev](http://groups.google.com/group/bigbluebutton-dev/topics?gvc=2)
mailing list to follow updates to the development of BigBlueButton and to collaborate with other developers.

# Set up a Development Environment

First, you need to install the core development tools.

sudo
apt-get
install
git-core ant ant-contrib openjdk-8-jdk-headless

With the JDK installed, you need to set the JAVA_HOME variable. Edit
~/.profile
(here we are using vim to edit the file)

vi ~/.profile

Add the following line at the end of the file

export
JAVA_HOME
=
/usr/lib/jvm/java-8-openjdk-amd64

Reload your profile (this will happen automatically when you next login, but we’ll do it explicitly here to load the new environment variable).

source
~/.profile

Do a quick test to ensure JAVA_HOME is set.

$
echo
$JAVA_HOME
/usr/lib/jvm/java-8-openjdk-amd64

In the next step, you need to install a number of tools using sdkman.

curl
-s
"https://get.sdkman.io"
| bash
source
"
$HOME
/.sdkman/bin/sdkman-init.sh"
sdk
install
gradle 5.5.1
sdk
install
grails 3.3.9
sdk
install
sbt 1.2.8
sdk
install
maven 3.5.0

## Checking out the Source

With the development tools installed, we’ll next clone the source in the following directory:

/home/ubuntu/dev

Using your GitHub account, do the following

[Fork](http://help.github.com/fork-a-repo/)
the BigBlueButton repository into your GitHub account
Clone your repository into your
~/dev
folder

After cloning, you’ll have the following directory (make sure the
bigbluebutton
directory is within your
dev
directory).

/home/ubuntu/dev/bigbluebutton

Confirm that you are working on the
v2.4.x-release
branch.

cd
/home/ubuntu/dev/bigbluebutton
git status

BigBlueButton 2.4 source code lives on branch
v2.4.x-release
. This is where any patches to 2.4 will be merged. If you are looking to customize your BigBlueButton 2.4 clone to fit your needs, this is the branch to use.

Alternatively if you are looking to try out or contribute to the very latest source code of BigBlueButton, you should see branch
develop
. This is where new features are developed and introduced. If you are planning on sending a pull request to contribute to BigBlueButton, please use branch
develop
.

For the purpose of these instructions we’ll assume you are only tweaking your clone of BigBlueButton. Thus we recommend you checkout branch
v2.4.x-release
.

On branch v2.4.x-release
Your branch is up-to-date with 'origin/v2.4.x-release'.
nothing to commit, working directory clean

The first thing we need to do is to add the remote repository to our local clone.

git remote add upstream https://github.com/bigbluebutton/bigbluebutton.git

You can now check your local list of tracked repositories to verify that the addition worked. You should see at least two results (origin and upstream). The one named “origin” should link to your personal fork and is the repository that you cloned. The second result “upstream” should link to the main BigBlueButton repository.

git remote
-v

After, we need to fetch the most up to date version of the remote repository.

git fetch upstream

You are now ready to create a new branch to start your work and base the
v2.4.x-release
release branch

git checkout
-b
my-changes-branch upstream/v2.4.x-release

“checkout” switches branches

“-b” is an option to create a new branch before switching

“my-changes-branch” will be the name of the new branch

“upstream/v2.4.x-release” is where you want to start your new branch

You should now confirm that you are in the correct branch.

git status
# On branch my-changes-branch
nothing to commit
(
working directory clean
)

## (Optional) Install bbb-demo

Note that at this point we recommend installing and using
[GreenLight](https://docs.bigbluebutton.org/greenlight/install.html)
or using API-MATE (link can be found when you run
$ bbb-conf --salt
).

If you want to test the installation or to easily start/join meetings while you are developing, you can alternatively install
bbb-demos
:

sudo
apt-get
install
bbb-demo

You can access https://BBB_DOMAIN , and you will be able to join meetings.

# Developing the HTML5 client

## Background

A bit of context is needed to fully explain what the HTML5 client is, why it has server component, what the architecture is, and only then how to make a change and re-deploy.

The HTML5 client in BigBlueButton is build using the framework
[Meteor](https://meteor.com/)
. Meteor wraps around a NodeJS server component, MongoDB server database, React frontend user interface library and MiniMongo frontend instance of MongoDB storing a subset of MongoDB’s data. When deployed, these same components are split into independently running pieces - NodeJS instance, MongoDB database and a browser optimized client files served by NginX. There is no “Meteor” in a production deployment, but rather separate components.

Make sure to check the HTML5 portion of the
[Architecture page](https://docs.bigbluebutton.org/2.3/architecture.html#html5-client)
.

Install Meteor.js.

$
curl https://install.meteor.com/ | sh

The HTML5 client in BigBlueButton 2.4 depends on Meteor version 2.3.6. Navigate to
bigbluebutton-html5/
and set the appropriate version of Meteor.

meteor update --allow-superuser --release 2.3.6

There is one change required to settings.yml to get webcam and screenshare working in the client (assuming you’re using HTTPS already). The first step is to find the value for
kurento.wsUrl
packaged settings.yml.

grep
"wsUrl"
/usr/share/meteor/bundle/programs/server/assets/app/config/settings.yml

Next, edit the development settings.yml and change
wsUrl
to match what was retrieved before.

$
vi private/config/settings.yml

You’re now ready to run the HTML5 code. First shut down the packaged version of the HTML5 client so you are not running two copies in parallel.

$ sudo systemctl stop bbb-html5

Install the npm dependencies.

$
meteor npm
install

Finally, run the HTML5 code.

$
npm start

By default, the client will run in
development
mode with only one instance of
NodeJS
handling both “backend” and “frontend” roles.

$ NODE_ENV
=
production npm start

In certain cases when making changes that span multiple BigBlueButton components you would want to ensure that the changes work well with the multiple different
NodeJS
processes.

You can deploy locally your modified version of the HTML5 client source using the script
[bigbluebutton-html5/deploy_to_usr_share.sh](https://github.com/bigbluebutton/bigbluebutton/blob/v2.4.x-release/bigbluebutton-html5/deploy_to_usr_share.sh)
- which deploys your [customized] bigbluebutton-html5/* code as locally running
bbb-html5
package (production mode, requiring the
poolhtml5servers
NginX rule). Make sure to read through the script to understand what it does prior to using it.

## Switch NginX to redirect requests to Meteor

When you are running bbb-html5 from package (i.e. in production mode) NginX needs to be able to point client sessions to a bbb-html5-frontend instance from the pool. However, in development mode (i.e. running Meteor via
npm start
), we only have one process, rather than a pool. We need to tweak the NginX configuration so that client sessions are only pointed to port
4100
where Meteor is running.

You would want to make a change in
/etc/bigbluebutton/nginx/bbb-html5.nginx
to use 4100 port rather than the pool.

The default - used for production mode:

location ~ ^/html5client/ {
  # proxy_pass http://127.0.0.1:4100; # use for development
  proxy_pass http://poolhtml5servers; # use for production
  ...

Development mode, only port 4100 is used.

location ~ ^/html5client/ {
  proxy_pass http://127.0.0.1:4100; # use for development
  # proxy_pass http://poolhtml5servers; # use for production
  ...

After this change, reload NginX’s configuration with
sudo systemctl reload nginx

A symptom of running
npm start
with the incompatible
poolhtml5servers
NginX configuration is seeing
It looks like you are trying to access MongoDB over HTTP on the native driver port.
and
Uncaught SyntaxError: Unexpected Identifier

When you switch back to running the
bbb-html5
packaged version you would want to revert your change so the
poolhtml5servers
are used for spreading the load of the client sessions.

## Audio configuration for development environment

You may see the error “Call timeout (Error 1006)” during the microphone echo test after starting the developing HTML5 client by “npm start”. A misconfiguration of Freeswitch may account for it, especially when BigBlueButton is set up with bbb-install.sh script. Try changing “sipjsHackViaWs” true in bigbluebutton-html5/private/config/settings.yml.

## Production

Using NODE_ENV=production is not meant to be actually used in production, see
[here](https://guide.meteor.com/deployment.html#never-use-production-flag)
for more information. Instead, you should build the meteor app so that the
bbb-html5
service can work with it.

First, ensure that you’re in the
bigbluebutton-html5
directory. If you follow the instructions above and have
ubuntu
as your user, you can run the following:

meteor build
--server-only
/home/ubuntu/dev/bigbluebutton/bigbluebutton-html5/meteorbundle

Meteor will build your customized version into a
.tar.gz
so we need to unpack it and place it in the right directory for
bbb-html5
to use it. Run:

sudo tar
-xzvf
/home/ubuntu/dev/bigbluebutton/bigbluebutton-html5/meteorbundle/
*
.tar.gz
-C
/usr/share/meteor

Finally, start the HTML5 client with
sudo systemctl start bbb-html5
.

There we go! Remember that this will be overwritten every time you upgrade, so you may want to have some mechanism put in place to replace it, or if your changes add new functionality/solve a bug, consider upstreaming them. To avoid having to uninstall and reinstall the
bbb-html5
package to restore a working version, you may want to make a copy of the original
bundle
folder.

## /private/config

All configurations are located in
**/private/config/settings.yml**
. If you make any changes to the YAML configuration you will need to restart the meteor process.

During Meteor.startup() the configuration file is loaded and can be accessed through the Meteor.settings.public object.
Note that individual configuration settings are overridden with their values (if defined) from file
/etc/bigbluebutton/bbb-html5.yml
(if the file exists).

# Build bbb-common-message

The bbb-common-message is required by a few components of BigBlueButton. So it is required to build this
first. Otherwise, you will run into compile errors.

cd
~/dev/bigbluebutton/bbb-common-message
./deploy.sh

# Developing BBB-Web

First, we need to update the latest bigbluebutton.properties file according to your setup. Basically, you will have to change the URL and security salt. If you don’t know your salt, run
sudo bbb-conf --salt

cd
~/dev/bigbluebutton/
# Edit the file and change the values of bigbluebutton.web.serverURL and securitySalt.
vi bigbluebutton-web/grails-app/conf/bigbluebutton.properties

Now you need to give your user account access to upload slides to the presentation directory and also access to write log files.

sudo chmod
-R
ugo+rwx /var/bigbluebutton
sudo chmod
-R
ugo+rwx /var/log/bigbluebutton

Open the file
~/.sbt/1.0/global.sbt
using your editor

mkdir
-p
~/.sbt/1.0
vi ~/.sbt/1.0/global.sbt

Add the following into it

resolvers
+=
"Artima Maven Repository"
at
"https://repo.artima.com/releases"
updateOptions
:=
updateOptions
.
value
.
withCachedResolution
(
true
)

Build bbb-common-web

cd
~/dev/bigbluebutton/bbb-common-web
./deploy.sh

Now let’s start building bbb-web

cd
~/dev/bigbluebutton/bigbluebutton-web/

We need to stop the bbb-web service

sudo
service bbb-web stop

Download the necessary libraries.

./build.sh

Start grails and tell to listen on port 8090

./run.sh

or

grails
-reloading
-Dserver
.port
=
8090 run-app

If you get an error
Could not resolve placeholder 'apiVersion'
, just run
grails -Dserver.port=8090 run-war
again. The error is grails not picking up the “bigbluebutton.properties” the first time.

Now test again if you can join the demo meeting.

The command above will run a development version of bbb-web, but if you want to deploy your custom-built bbb-web you need to package a war file.

**Instructions for deploying bbb-web**

First we need to compile all the project in a single war file.

grails assemble

The
war
application is generated under
build/libs/bigbluebutton-0.10.0.war
.

Create a new directory and open it.

mkdir
exploded
&amp;&amp;
cd
exploded

Extract the war content in the newly create directory

jar
-xvf
../build/libs/bigbluebutton-0.10.0.war

Then copy the
run-prod.sh
after checking all the jar dependencies are listed in

cp
../run-prod.sh
.

In the next step we will make a copy of the current production directory for
bbb-web

sudo cp
-R
/usr/share/bbb-web /usr/share/bbb-web-old

Then we will delete all the files we need to be copied for production

sudo rm
-rf
/usr/share/bbb-web/assets/ /usr/share/bbb-web/META-INF/ /usr/share/bbb-web/org/ /usr/share/bbb-web/run-prod.sh  /usr/share/bbb-web/WEB-INF/

Next, let’s copy the complied files into the production directory

sudo cp
-R
.
/usr/share/bbb-web/

Make sure the copied files have the right user ownership.

$
sudo chown
bigbluebutton:bigbluebutton /usr/share/bbb-web
$
sudo chown
-R
bigbluebutton:bigbluebutton /usr/share/bbb-web/assets/ /usr/share/bbb-web/META-INF/ /usr/share/bbb-web/org/ /usr/share/bbb-web/run-prod.sh /usr/share/bbb-web/WEB-INF/

And finally we run the service.

sudo
service bbb-web start

If you need to revert back your original production
bbb-web
just run the following command. (Don’t forget to stop bbb-web service before doing it)

sudo mv
/usr/share/bbb-web /usr/share/bbb-web-dev
&amp;&amp;
/usr/share/bbb-web-old /usr/share/bbb-web

Your compiled code will be under the
/usr/share/bbb-web-dev
directory and you can safely run the original production ``bbb-web`.

# Developing Akka-Apps

You can manually run the application.

cd
~/dev/bigbluebutton/akka-bbb-apps
./run.sh

Don’t forget to modify service-bbbWebAPI, service-sharedSecret in ~/dev/bigbluebutton/akka-bbb-apps/src/universal/conf/application.conf, to get it work properly. For instance, these are necessary for starting the breakout rooms.

You can deploy locally akka-apps by building a simple .deb package using
sbt
and deploying it right away:

sbt debian:packageBin
dpkg -i ./target/bbb-apps-akka_&lt;tab&gt;.deb

# Developing Akka-FSESL

You need to build the FS ESL library

cd
~/dev/bigbluebutton/bbb-fsesl-client
./deploy.sh

Then you can run the application.

cd
~/dev/bigbluebutton/akka-bbb-fsesl
./run.sh

You can deploy locally akka-fsesl by building a simple .deb package using
sbt
and deploying it right away:

sbt debian:packageBin
dpkg -i ./target/bbb-fsesl-akka_&lt;tab&gt;.deb

# Troubleshooting

## Welcome to Nginx page

If you get the “Welcome to Nginx” page. Check if bigbluebutton is enabled in nginx. You should see
**bigbluebutton**
in
/etc/nginx/sites-enabled
.

If not, enable it.

sudo ln
-s
/etc/nginx/sites-available/bigbluebutton /etc/nginx/sites-enabled/bigbluebutton
sudo
/etc/init.d/nginx restart

## Pausing/Restarting VM gives wrong date in commit

If you are developing using a VM and you’ve paused the VM and later restart it, the time on the VM will be incorrect. The incorrect time will affect any commits you do in GitHub.

To ensure your VM has the correct time, you can install ntp with

sudo
apt-get
install
ntp
sudo
/etc/init.d/ntp restart

and then do the following after starting the VM from a paused state

sudo
/etc/init.d/ntp restart

The above will re-sync your clock.

# Set up HTTPS

Follow
[Configure SSL on your BigBlueButton server](https://docs.bigbluebutton.org/2.4/install.html#configure-ssl-on-your-bigbluebutton-server)
