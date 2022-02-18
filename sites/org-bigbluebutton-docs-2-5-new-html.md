What's New
----------

![](https://docs.bigbluebutton.org/images/25-header.png)

Overview
==========

This document gives you an overview of BigBlueButton 2.5.

*Note:* This document is DRAFT and will be expanded upon as 2.5 development goes through alpha, beta, and release.

What’s new
----------

BigBlueButton 2.5 offers users improved usability, increased engagement, and more performance.

* **Usability** - making common functions (such as raise hand) easier
* **Engagement** - giving the instructor more ways to engage students
* **Performance** - increasing overall performance and scalability

Here’s a breakdown of what’s new in 2.5

* **Usability**

### Screenshot of current slide with annotations ###

### Easier setup of breakout rooms ###

Breakout rooms remember previous rooms assignments and can automatically populate the rooms

### Improved experience when changing the duration of breakout rooms after their creation ###

Support for both extending and reducing the duration, notification in the main room and in each breakout room

### Whiteboard improvements ###

Fill shape

### Webcam pinning ###

### Improvements to Guest Lobby ###

Private guest lobby message, display of waiting time, moving users back to the lobby, display position in waiting line

* **Engagement**

### Text message broadcasting to breakout rooms ###

### Randomly select user without repetitions ###

### Learning Analytics Dashboard improvements ###

Newly introduced Timeline with slide thumbnails and improved display of user emoji timing

* **Administration**

### All package scripts are included in the source code repository ###

### Polling support for multiple answers per question ###

* **Performance**

### Improved scaling of webcams and screenshare ###

We have switched to a different media server - [mediasoup](https://mediasoup.org/) (instead of Kurento) for handling WebRTC video streams (webcams and screenshare) and listen only.
For analysis on mediasoup vs. Kurento, see [BigBlueButton World - BigBlueButton’s Media Stack and the Road Ahead](https://youtu.be/SBO5iWLs0KE). Note that Kurento is still installed on the system and still plays a role in the recording of media.

Under the hood, BigBlueButton 2.5 installs on Ubuntu 18.04 64-bit, and the following key components have been updated

* Java 11
* Meteor 2.5

For full details on what is new in BigBlueButton 2.5, see the release notes. Recent releases:

* [alpha-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.5-alpha-1)

Features
==========

The following sections give details of the new features.

Usability
----------

Engagement
----------

Installation
----------

For server requirements, BigBlueButton 2.5 needs similar [minimum server requirements](https://docs.bigbluebutton.org/2.5/install.html#minimum-server-requirements) as 2.4.

To install 2.5, use [bbb-install-2.5.sh](https://github.com/bigbluebutton/bbb-install/blob/master/bbb-install-2.5.sh). For example, the following command installs BigBlueButton 2.5-dev using `bbb.example.com` as the hostname and `notice@example.com` as the email for Let’s Encrypt (you would substitute these values for your own hostname and email address). Notice the version is `-v bionic-250`, which will install the latest officially published release (alpha/beta/etc) of BigBlueButton 2.5. If you instead use `-v bionic-25-dev`, you will be installing/updating to the very latest build tracking the source code from branch `v2.5.x-release`.

```
wget -qO- https://ubuntu.bigbluebutton.org/bbb-install-2.5.sh | bash -s -- -v bionic-250 -s bbb.example.com -e notice@example.com  -a -w

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

This installs the latest version of BigBlueButton 2.5-dev with Let’s encrypt certificate and the API demos. With the API demos installed, you can open https:/// in a browser (where  is the hostname you specified in the `bbb-install-2.5.sh` command), enter your name, and click 'Join' to join 'Demo Meeting'. For more information, see the [bbb-install-2.5.sh](https://github.com/bigbluebutton/bbb-install/blob/master/bbb-install-2.5.sh) documentation.

BigBlueButton 2.5-dev is under active development. While we don’t recommend setting it up in a production environment, we do encourage administrators to try out the build with others and give us feedback on [our bigbluebutton-dev mailing list](https://groups.google.com/g/bigbluebutton-dev).

Development
----------

Follow [Development for 2.5](https://docs.bigbluebutton.org/2.5/dev.html)

Contribution
----------

We welcome contributors to BigBlueButton 2.5!
The best ways to contribute at the current time are:

* Try out installing BigBlueButton 2.5 and see if you spot any issues
* Help test a [2.5 pull request](https://github.com/bigbluebutton/bigbluebutton/pulls?q=is%3Aopen+is%3Apr+milestone%3A%22Release+2.5%22) in your development environment
