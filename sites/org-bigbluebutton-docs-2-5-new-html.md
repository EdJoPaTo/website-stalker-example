What's New
----------

![](https://docs.bigbluebutton.org/images/25-header.png)

Overview
==========

This document gives you an overview of BigBlueButton 2.5, the latest version of BigBlueButton now in development.

*Note:* This document is DRAFT and will be expanded upon as 2.5 development goes through alpha, beta, and release.

BigBlueButton 2.5 offers users improved usability, increased engagement, and more performance.

* **Usability** - making common functions (such as raise hand) easier
* **Engagement** - giving the instructor more ways to engage students
* **Performance** - increasing overall performance and scalability

Here’s a breakdown of what’s new in 2.5.

Usability
----------

### Screenshot of current slide with annotations ###

To capture the current slide with annotations, you can now have BigBlueButton give you a PNG image of the current slide.

![Download Annotations](https://docs.bigbluebutton.org/images/25-download-annotations.png)

### Easier setup of breakout rooms ###

Breakout rooms remember your previous rooms assignments within the current session. This lets you re-use the existing breakout rooms.

### Change time of breakout rooms ###

You can now easily change the duration of a breakout rooms to a new time.

![Change time](https://docs.bigbluebutton.org/images/25-change-time.gif)

When you change the duration of breakout rooms, BigBlueButton will notify each breakout room in the public chat of the new duration.

![New duration](https://docs.bigbluebutton.org/images/25-new-duration.png)

### Webcam pinning ###

You can now pin a webcam so it always stays visible. This is useful if one on of the webcams is showing sign language, for example, and you always want it to be visible.

![Pin webcam](https://docs.bigbluebutton.org/images/25-pin-webcam.png)

### Improvements to Guest Lobby ###

Private guest lobby message, display position in waiting line

Engagement
----------

### Text message broadcasting to breakout rooms ###

You can now broadcast a text message to all breakout rooms. This message will appear in the public chat of each breakout room.

![Message breakout rooms](https://docs.bigbluebutton.org/images/25-message.gif)

### Polling support for multiple answers per question ###

Analytics
----------

### Learning Analytics Dashboard improvements ###

Newly introduced Timeline with slide thumbnails and improved display of user emoji timing.

Performance
----------

### Improved scaling of webcams and screenshare ###

BigBlueButton now uses [mediasoup](https://mediasoup.org/) (instead of Kurento) as its default WebRTC media server. You’ll find mediasoup able to handle more media streams (including screenshare) using less memory and CPU.

For analysis on mediasoup vs. Kurento, see [BigBlueButton World - BigBlueButton’s Media Stack and the Road Ahead](https://youtu.be/SBO5iWLs0KE). Note that Kurento is still installed on the system and still plays a role in the recording of media.

Experimental
----------

### Two-way microphone connections using Mediasoup ###

FreeSWITCH is awesome, but it doesn’t support dual-stack IPV4 and IPV6 (we bridge this with nginx). It does not support trickle ICE for quick connections.

The experimental microphone bridge introduced in 2.4 is moving towards feature complete in 2.5. Support for the following features are now in 2.5:

* mediasoup now proxies audio connections for FreeSWITCH
* Echo test
* Input and output device switching
* Audio filters

For a list of pending issues for the experimental audio bridge to be considered production-grade, check this [Depends on](https://github.com/bigbluebutton/bigbluebutton/issues/14021#fullaudio-depends-on) section in GitHub.

Moreover, the steps for enabling this have changed slightly since 2.4. If you want to try this (keep in mind it is still experimental), you need to add the `fullAudioEnabled: true` flag in bbb-webrtc-sfu’s configuration (`/etc/bigbluebutton/bbb-webrtc-sfu/production.yml`).

```
mkdir -p /etc/bigbluebutton/bbb-webrtc-sfu
if ! grep -q "fullAudioEnabled: true" /etc/bigbluebutton/bbb-webrtc-sfu/production.yml; then echo "fullAudioEnabled: true" >> /etc/bigbluebutton/bbb-webrtc-sfu/production.yml; fi

```

Once that flag is enabled in bbb-webrtc-sfu, there are two ways of opting in:

1. Using API parameters you can have specific meetings use the experimental bridge by passing: CREATE parameter `meta_fullaudio-bridge=fullaudio` to override the default `sipjs` value

2. You can change the defaults in the settings for bbb-html5 by adding the following to `/etc/bigbluebutton/bbb-html5.yml` (you will likely want to merge it carefully with your existing file):

```
  public:
    media:
      audio:
        defaultFullAudioBridge: fullaudio

```

After a restart of BigBlueButton (`sudo bbb-conf --restart`), it should be ready to test. Reverting to the default options can be achieved by removing the override sections (and passed API parameters) and restart of BigBlueButton.

Upgraded components
----------

### Ubuntu 20.04 ###

Under the hood, BigBlueButton 2.5 installs on Ubuntu 20.04 64-bit, and the following key components have been upgraded

* Tomcat 9
* Java 11
* Meteor 2.7.1
* NodeJS 14.19.1 (for bbb-html5-\*)
* SBT 1.6.2
* Grails 5.0.1
* Gradle 7.3.1
* Note that BigBlueButton 2.5 is the first iteration running on Ubuntu 20.04

For full details on what is new in BigBlueButton 2.5, see the release notes. Recent releases:

* [beta.2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5.0-beta.2)
* [beta.1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5.0-beta.1)
* [alpha.6](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5.0-alpha.6)
* [alpha.5](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5.0-alpha.5)
* [alpha-4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5-alpha-4)
* [alpha-3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5-alpha-3)
* [alpha-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5-alpha-2)
* [alpha-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5-alpha-1)

Installation
==========

For server requirements, BigBlueButton 2.5 needs similar [minimum server requirements](https://docs.bigbluebutton.org/2.5/install.html#minimum-server-requirements) as 2.4.

To install 2.5, use [bbb-install-2.5.sh](https://github.com/bigbluebutton/bbb-install/blob/master/bbb-install-2.5.sh). For example, the following command installs BigBlueButton 2.5-dev using `bbb.example.com` as the hostname and `notice@example.com` as the email for Let’s Encrypt (you would substitute these values for your own hostname and email address). Notice the version is `-v focal-250`, which will install the latest officially published release (alpha/beta/etc) of BigBlueButton 2.5. If you instead use `-v focal-25-dev`, you will be installing/updating to the very latest build tracking the source code from branch `v2.5.x-release`.

```
wget -qO- https://ubuntu.bigbluebutton.org/bbb-install-2.5.sh | bash -s -- -v focal-250 -s bbb.example.com -e notice@example.com  -a -w

```

After installation finishes, you should see the following installed packages (your version numbers may be slightly different).

```
# dpkg -l | grep bbb-

ii  bbb-apps-akka              2.5           all          BigBlueButton Apps (Akka)
ii  bbb-config                 1:2.5-9       amd64        BigBlueButton configuration utilities
ii  bbb-demo                   1:2.5-2       amd64        BigBlueButton API demos
ii  bbb-etherpad               1:2.5-3       amd64        The EtherPad Lite components for BigBlueButton
ii  bbb-freeswitch-core        2:2.5-4       amd64        BigBlueButton build of FreeSWITCH
ii  bbb-freeswitch-sounds      1:2.5-2       amd64        FreeSWITCH Sounds
ii  bbb-fsesl-akka             2.5           all          BigBlueButton FS-ESL (Akka)
ii  bbb-html5                  1:2.5-12      amd64        The HTML5 components for BigBlueButton
ii  bbb-learning-dashboard     1:2.5-2       amd64        BigBlueButton bbb-learning-dashboard
ii  bbb-libreoffice-docker     1:2.5-2       amd64        BigBlueButton setup for LibreOffice running in docker
ii  bbb-mkclean                1:0.8.7-1     amd64        Clean and optimize Matroska and WebM files
ii  bbb-pads                   1:2.5-2       amd64        BigBlueButton Pads
ii  bbb-playback               1:2.5-2       amd64        BigBlueButton playback
ii  bbb-playback-presentation  1:2.5-2       amd64        BigBluebutton playback of presentation
ii  bbb-record-core            1:2.5-3       amd64        BigBlueButton record and playback
ii  bbb-web                    1:2.5-6       amd64        BigBlueButton API
ii  bbb-webrtc-sfu             1:2.5-6       amd64        BigBlueButton WebRTC SFU

```

This installs the latest version of BigBlueButton 2.5-dev with Let’s encrypt certificate and the API demos. With the API demos installed, you can open `https:///` in a browser (where `` is the hostname you specified in the `bbb-install-2.5.sh` command), enter your name, and click ‘Join’ to join ‘Demo Meeting’. For more information, see the [bbb-install-2.5.sh](https://github.com/bigbluebutton/bbb-install/blob/master/bbb-install-2.5.sh) documentation.

BigBlueButton 2.5-dev is under active development. While we don’t recommend setting it up in a production environment yet, we do encourage administrators to try out the build with others and give us feedback on [our bigbluebutton-dev mailing list](https://groups.google.com/g/bigbluebutton-dev).

Development
----------

For information on developing in BigBlueButton, see [setting up a development environment for 2.5](https://docs.bigbluebutton.org/2.5/dev.html).

The build scripts for packaging 2.5 (using fpm) are located in the GitHub repository [here](https://github.com/bigbluebutton/bigbluebutton/tree/v2.5.x-release/build).

Contribution
----------

We welcome contributors to BigBlueButton 2.5! The best ways to contribute at the current time are:

* Try out [installing BigBlueButton 2.5](https://docs.bigbluebutton.org/2.5/new.html#installation) and see if you spot any issues.
* Help test a [2.5 pull request](https://github.com/bigbluebutton/bigbluebutton/pulls?q=is%3Aopen+is%3Apr+milestone%3A%22Release+2.5%22) in your development environment.
