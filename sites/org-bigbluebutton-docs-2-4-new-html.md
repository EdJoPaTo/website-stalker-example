What's New
----------

![](https://docs.bigbluebutton.org/images/24-header.png)

Overview
==========

This document gives you an overview of BigBlueButton 2.4.0, which was released on December 20, 2021.

What’s new
----------

BigBlueButton 2.4 offers users improved usability, increased engagement, and more performance.

* **Usability** - making common functions (such as raise hand) easier
* **Engagement** - giving the instructor more ways to engage students
* **Performance** - increasing overall performance and scalability

Here’s a breakdown of what’s new in 2.4

* **Usability**

  * Ability to extend the duration of ongoing breakout rooms
  * Ability to set the name of the breakout rooms as you create them
  * Reduced mirror effect when sharing screen
  * Improved view of external video sharing for viewers
  * Recording includes polling result
  * Moderator messages in the public chat are easier to distinguish
  * Webcam background blur

* **Engagement**

  * Improved Layout Manager with focus on presentation vs focus on webcams
  * Presenter can set viewers’ layout
  * Hide voter’s name from moderators
  * Indicate who is sharing webcam

* **Performance**

This release, by design, does not introduce any large-scale UI changes. We designed it to be very familiar to users of BigBlueButton 2.3.

Under the hood, BigBlueButton 2.4 installs on Ubuntu 18.04 64-bit, and the following key components have been updated

* Node 14.x (LTS release of Node)
* Meteor 2.5

For full details on what is new in BigBlueButton 2.4, see the release notes. Recent releases:

* [2.4.0](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4.0)
* [rc-7](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-7)
* [rc-6](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-6)
* [rc-5](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-5)
* [rc-4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-4)
* [rc-3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-3)
* [rc-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-2)
* [rc-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-rc-1)
* [beta-4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-beta-4)
* [beta-3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-beta-3)
* [beta-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-beta-2)
* [beta-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-beta-1)
* [alpha-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-alpha-2)
* [alpha-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.4-alpha-1)

Features
==========

The following sections give details of the new features.

Usability
----------

### Ability to extend the duration of ongoing breakout rooms ###

As a moderator you can see the Extend button at the bottom of the Breakouts panel:![Extend breakout](https://docs.bigbluebutton.org/images/24-extend-breakout-1.png)

Selecting it will display the controls to extend the breakouts time by five or minutes or longer.![Extend breakout](https://docs.bigbluebutton.org/images/24-extend-breakout-2.png)

The time is added to all running breakout rooms.![Extend breakout](https://docs.bigbluebutton.org/images/24-extend-breakout-3.png)

### Ability to set the name of the breakout rooms as you create them ###

When creating breakout rooms you can edit the name of each room![Set name for breakout](https://docs.bigbluebutton.org/images/24-breakout-name-1.png)

![Set name for breakout](https://docs.bigbluebutton.org/images/24-breakout-name-2.png)

### Reduced mirror effect when sharing screen ###

Up to and including BigBlueButton 2.3.x the HTML5 client would show mirror effect to the presenter when the presenter was sharing their entire window. This caused confusion and was often interpreted as a bug.![Reduced mirror effect](https://docs.bigbluebutton.org/images/24-reduced-mirror-effect-before.png)

In BigBlueButton 2.4 we have introduced a simplified screen which informs the presenter of which window is shared, without creating mirror effect.![Reduced mirror effect](https://docs.bigbluebutton.org/images/24-reduced-mirror-effect-after.png)

### Improved view of external video sharing for viewers ###

Viewers no longer see the progress bar of videos. There are custom volume control and custom refresh video buttons.

![External video - custom controls for volume and refresh](https://docs.bigbluebutton.org/images/24-external-video-viewer.png)

### Recording’s public chat includes polling result ###

Meetings which included polling have improved poll results summary in the recording.

![Recording - polling result](https://docs.bigbluebutton.org/images/24-recording-polling-result.png)

### Recording’s public chat includes links to external videos shared in the meeting ###

Meetings which included external video sharing (YouTube, Vimeo, etc) have links to the video resource in the recording’s public chat.

![Recording - external video](https://docs.bigbluebutton.org/images/24-recording-external-video.png)

### Moderator messages in the public chat are easier to distinguish ###

Chat messages sent by moderators stand out in the public chat, allowing to be distinguished easily. The emphasis is optional (settings.yml chat parameter `moderatorChatEmphasized`)

![Moderator bolded text](https://docs.bigbluebutton.org/images/24-chat-font-moderator.png)

### Alerts when user leaves ###

The Notifications section in Settings has a new option for audio/popup alert when a user leaves the session.

![User leaves alert](https://docs.bigbluebutton.org/images/24-user-leaves-alert.png)

### Webcam background blur ###

In the webcam preview window prior to sharing webcam you can select between several backgrounds (or no background blur)

No blur (default)![Background blur for webcam](https://docs.bigbluebutton.org/images/24-background-blur-1.png)

Replacing the background![Background blur for webcam](https://docs.bigbluebutton.org/images/24-background-blur-2.png)

Blurring the background![Background blur for webcam](https://docs.bigbluebutton.org/images/24-background-blur-3.png)

Engagement
----------

### Improved Layout Manager ###

Under Settings there is a new section of controls related to layout. A dropdown allows for the selection of one of: Smart Layout, Focus on presentation or Focus on webcams.

![Layout dropdown](https://docs.bigbluebutton.org/images/24-layout-dropdown.png)

Focus on presentation - webcams are visible but more compact, allowing for the majority of the area to be reserved for the presentation. Focus on video has the reverse effect - the presentation is visible but on small area under the chat.

![Layout](https://docs.bigbluebutton.org/images/24-focus-on-presentation.png)

### Presenter can set viewers’ layout ###

The presenter has an extra set of controls in the Settings modal. Aside from being able to set their own layout, there is an extra option to “push” that layout to the rest of the participants in the meeting.

![Pushing layout](https://docs.bigbluebutton.org/images/24-push-layout.png)

### Learning Dashboard ###

Moderators (teachers) are now able to view student participation and engagement throughout the session. The Learning Dashboard gives moderators a live view (updated every 10 seconds) of user metrics that include

* When they joined the session
* How long there have been in the session
* Time talking
* Time sharing their webcam
* How many messages, emojis, and raise hand events they have done
* current status (online/offline)
* Response to all polls

Teachers can use this dashboard to track engagement and learning (based on respose to polls) during the session to questions such as

* Which students are participating in the session (and which are not)?
* Based on the poll results, which students are learning (and which are not)?

Teachers are automatically logged in as moderators when joining from their LMS. They can launch the Learning Dashboard by selecting “Learning Dashboard” under the gear icon.

![Learning Dashboard](https://docs.bigbluebutton.org/images/24-learning-dashboard.png)

The screen shot below shows three (3) participants, two (2) polls, one raise hand, and overall activity score (calculated based on who is most active in talking, chatting, responding polls, using emojis, and raising hands).

![Learning Dashboard-2](https://docs.bigbluebutton.org/images/24-learning-dashboard-2.png)

This screen shot shows each user’s response to polls. Note: Anonymous is for any poll that the instructors indicated would be anonymous and not track user’s responses.

![Learning Dashboard-3](https://docs.bigbluebutton.org/images/24-learning-dashboard-3.png)

### Hide voter’s name from moderators ###

BigBlueButton 2.4 supports pseudo-anonymous polls - meaning polls for which the presenter/moderator is not informed about the voting option of the viewers. Server administrators (anyone with access to the BigBlueButton server) can still find information to connect the answer to the user. Big thanks to @tibroc and @schrd who sent pull requests for this feature!

Set the poll to be “anonymous” when creating it:![Anonymous poll](https://docs.bigbluebutton.org/images/24-anonymous-poll-1.png)

Voters will see that it is anonymous:![Anonymous poll](https://docs.bigbluebutton.org/images/24-anonymous-poll-2.png)

The presenter will not know who voted what:![Anonymous poll](https://docs.bigbluebutton.org/images/24-anonymous-poll-3.png)

### Indicate who is sharing webcam ###

BigBlueButton 2.4 introduces an indicator for users who are sharing their webcam. This is particularly helpful when webcam pagination is enabled there is no way of knowing whose webcam you would see on the other “pages”.

![Anonymous poll](https://docs.bigbluebutton.org/images/24-webcam-indicator.png)

Performance
----------

### mediasoup ###

This release also contains initial support for using [mediasoup](https://mediasoup.org/) instead of Kurento for handling WebRTC video streams (webcams and screenshare) and listen only. See these [steps](https://github.com/bigbluebutton/bbb-webrtc-sfu/wiki/Back-of-the-envelope-calculations:-mediasoup) for enabling mediasoup on your setup of 2.4-rc-2 (or later).

For analysis on Medisoup vs. Kurento, see [BigBlueButton World - BigBlueButton’s Media Stack and the Road Ahead](https://youtu.be/SBO5iWLs0KE).

Experimental
----------

***Note*** These features below are experimental and incomplete and should *not* be used for a production server. They are primarily included for developers testing new capabilities that many appear in subsequent releases to 2.4.

### Faster audio activation using fullaudio bridge (experimental) ###

With BigBlueButton 2.4-rc-4 (or later) you can switch the way full audio (microphone) is handled on the backend. By default we use SipJS but we are working on connecting to Kurento (and later mediasoup) and then to FreeSWITCH rather than directly to FreeSWITCH. **The result is a faster audio connection (because media server supports trickle ICE) and fewer audio errors (because we don’t need to track SIP state in client anymore)**. This audio setup currently **does not support echo test**, so it needs to be disabled when using.

If you want to try this (keep in mind it is still experimental), you need to add the following block in the bbb-webrtc-sfu’s configuration to enable `fullaudio` via SFU:

```
  - path: ./lib/audio/FullAudioProcess.js
    name: fullaudio
    dedicated: true
    ipc:
      mode: native
      options:
        # inboundChannel: to-sfu-audio
        # outboundChannel: from-sfu-audio

```

The recommended way to add this would be to use the [override file](https://docs.bigbluebutton.org/admin/configuration-files.html) `/etc/bigbluebutton/bbb-webrtc-sfu/production.yml` (note that array configurations are merged by replacement, so we need to pass the full array)

```
modules:
  - path: ./lib/mcs-core/process.js
    name: core
    dedicated: true
    # IPC can be either native|redis right now. Defaults to native
    ipc:
      mode: native
      options:
      # inboundChannel: to-mcs-core
      # outboundChannel: from-mcs-core
  - path: ./lib/screenshare/ScreenshareProcess.js
    name: screenshare
    dedicated: true
    ipc:
      mode: native
      options:
      # inboundChannel: to-sfu-screenshare
      # outboundChannel: from-sfu-screenshare
  - path: ./lib/video/VideoProcess.js
    name: video
    dedicated: true
    ipc:
      mode: native
      options:
      # inboundChannel: to-sfu-video
      # outboundChannel: from-sfu-video
  - path: ./lib/listen-only/listen-only-process.js
    name: audio
    dedicated: true
    ipc:
      mode: native
      options:
      # inboundChannel: to-sfu-audio
      # outboundChannel: from-sfu-audio
  - path: ./lib/audio/FullAudioProcess.js
    name: fullaudio
    dedicated: true
    ipc:
      mode: native
      options:
        # inboundChannel: to-sfu-audio
        # outboundChannel: from-sfu-audio

```

Once `fullaudio` is defined in bbb-webrtc-sfu, there are two ways of opting in.
A) Using API parameters you can have specific meetings use `fullaudio` by passing:
CREATE parameter `meta_fullaudio-bridge=fullaudio` to override the default `sipjs` value
and
JOIN parameter `userdata-bbb_skip_check_audio=true` to disable echo test for that user.

B) You can change the defaults in the settings for bbb-html5 by overriding `settings.yml`Again, the recommended way is to use an [override file](https://docs.bigbluebutton.org/admin/configuration-files.html) `/etc/bigbluebutton/bbb-html5.yml` (you will likely want to merge it carefully with your existing file).

```
public:
  media:
    audio:
      defaultFullAudioBridge: fullaudio
  app:
    skipCheck: true

```

After a restart of BigBlueButton (`sudo bbb-conf --restart`) you can try out this audio join method. Reverting to the default options can be achieved by removing the override sections (and passed API parameters) and restart of BigBlueButton.

Installation
----------

For server requirements, BigBlueButton 2.4 needs similar [minimum server requirements](https://docs.bigbluebutton.org/2.4/install.html#minimum-server-requirements) as 2.3.

To install 2.4, use [bbb-install.sh](https://github.com/bigbluebutton/bbb-install). For example, the following command installs BigBlueButton 2.4-dev using `bbb.example.com` as the hostname and `notice@example.com` as the email for Let’s Encrypt (you would substitute these values for your own hostname and email address). Notice the version is `-v bionic-240`, which will install the latest officially published release (alpha/beta/etc) of BigBlueButton 2.4. If you instead use `-v bionic-24-dev`, you will be installing/updating to the very latest build tracking the source code from branch `v2.4.x-release`.

```
wget -qO- https://ubuntu.bigbluebutton.org/bbb-install.sh | bash -s -- -v bionic-240 -s bbb.example.com -e notice@example.com  -a -w

```

After installation finishes, you should see the following installed packages (your version numbers may be slightly different).

```
# dpkg -l | grep bbb-
ii  bbb-apps-akka             2.4.0-10     all    BigBlueButton Apps (Akka)
ii  bbb-config                1:2.4.0-9    amd64  BigBlueButton configuration utilities
ii  bbb-demo                  1:2.4.0-2    amd64  BigBlueButton API demos
ii  bbb-etherpad              1:2.4.0-1    amd64  The EtherPad Lite components for BigBlueButton
ii  bbb-freeswitch-core       2:2.4.0-2    amd64  BigBlueButton build of FreeSWITCH
ii  bbb-freeswitch-sounds     1:1.6.7-3    amd64  FreeSWITCH Sounds
ii  bbb-fsesl-akka            2.4.0-5      all    BigBlueButton FS-ESL (Akka)
ii  bbb-html5                 1:2.4.0-1254 amd64  The HTML5 components for BigBlueButton
ii  bbb-libreoffice-docker    1:2.4.0-1    amd64  BigBlueButton setup for LibreOffice running in docker
ii  bbb-mkclean               1:0.8.7-4    amd64  Clean and optimize Matroska and WebM files
ii  bbb-playback              1:2.4.0-1    amd64  BigBlueButton playback
ii  bbb-playback-presentation 1:2.4.0-1    amd64  BigBluebutton playback of presentation
ii  bbb-record-core           1:2.4.0-3    amd64  BigBlueButton record and playback
ii  bbb-web                   1:2.4.0-8    amd64  BigBlueButton API
ii  bbb-webrtc-sfu            1:2.4.0-5    amd64  BigBlueButton WebRTC SFU

```

This installs the latest version of BigBlueButton 2.4-dev with Let’s encrypt certificate and the API demos. With the API demos installed, you can open https:/// in a browser (where  is the hostname you specified in the `bbb-install.sh` command), enter your name, and click 'Join' to join 'Demo Meeting'. For more information, see the [bbb-install.sh](https://github.com/bigbluebutton/bbb-install) documentation.

BigBlueButton 2.4-dev is under active development. While we don’t recommend setting it up in a production environment, we do encourage administrators to try out the build with others and give us feedback on [our bigbluebutton-dev mailing list](https://groups.google.com/g/bigbluebutton-dev).

Development
----------

Follow [Development for 2.4](https://docs.bigbluebutton.org/2.4/dev.html)

Contribution
----------

We welcome contributors to BigBlueButton 2.4!
The best ways to contribute at the current time are:

* Help localize BigBlueButton 2.4 on [Transifex project for BBB 2.4](https://www.transifex.com/bigbluebutton/bigbluebutton-v24-html5-client/dashboard/)
* Try out installing BigBlueButton 2.4 and see if you spot any issues
* Help test a [2.4 pull request](https://github.com/bigbluebutton/bigbluebutton/pulls?q=is%3Aopen+is%3Apr+milestone%3A%22Release+2.4%22) in your development environment
