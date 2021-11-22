## What's New

This document gives you an overview of BigBlueButton 2.3, the latest release of BigBlueButton. BigBlueButton 2.3 offers users improved usability, increased engagement, and more performance.

- **Usability**
- making common functions (such as raise hand) easier
- **Engagement**
- giving the instructor more ways to engage students
- **Performance**
- increasing overall performance and scalability

Here’s a breakdown of what’s new in 2.3

-
**Usability**

	- Non-blocking upload of presentations
	- Left/right placement of camera relative to presentation
	- User avatars
	- New playback format with search capability
	- Notifications for raise hand and guest waiting approval
	- Screen share of a Chrome tab can also share system audio
	- Notification when speaking and microphone is muted
	- Ability to switch microphone input and audio output
	- Connectivity status icon
-
**Engagement**

	- Easier creation of polls and new option to receive typed user responses
	- Assign individual users whiteboard privileges
	- Randomly select a user
-
**Performance**

	- User list and chat list now re-render only visible components
	- Refactoring of user joining sequence
	- Support for multiple nodejs processes for supporting meetings larger than 100 users
	- Whiteboard performance improvements
	- Faster queue based processing of launching recordings workers
	- Configurable pool of recording workers (default 1)
	- Faster processing of recordings

This release, by design, does not introduce any large-scale UI changes. We designed it to be very familiar to users of BigBlueButton 2.2.

Under the hood, BigBlueButton 2.3 installs on Ubuntu 18.04 64-bit, which is a much newer version of Ubuntu that brings along updates to key components

- NodeJS 12.x (LTS release of NodeJS)
- ruby 2.5
- Meteor 1.10.x
- Etherpad 1.8.13
- FreeSWITCH 1.10.6
- LibreOffice 7.0.4.2

For full details on what is new in BigBlueButton 2.3, see the release notes recent releases

- [2.3.15](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.15)
- [2.3.14](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.14)
- [2.3.13](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.13)
- [2.3.12](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.12)
- [2.3.11](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.11)
- [2.3.10](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.10)
- [2.3.9](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.9)
- [2.3.8](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.8)
- [2.3.7](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.7)
- [2.3.6](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.6)
- [2.3.5](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.5)
- [2.3.4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.4)
- [2.3.3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.3)
- [2.3.2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.2)
- [2.3.1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.1)
- [2.3.0](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3.0)
- [rc-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-rc-2)
- [rc-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-rc-1)
- [beta-5](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-beta-5)
- [beta-4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-beta-4)
- [beta-3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-beta-3)
- [beta-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-beta-2)
- [beta-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-beta-1)
- [alpha-8](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-8)
- [alpha-7](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-7)
- [alpha-6](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-6)
- [alpha-5](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-5)
- [alpha-4](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-4)
- [alpha-3](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-3)
- [alpha-2](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-2)
- [alpha-1](https://github.com/bigbluebutton/bigbluebutton/releases/tag/v2.3-alpha-1)

# Features

The following sections give details of the new features.

### New player for recordings

BigBlueButtom 2.3 has a rewritten HTML5 player for recordings that gives the user the ability to

- search through text of slides,
- view both webcam and screen share/presentation, and
- view both integrated shard notes and chat.

![Overview](https://docs.bigbluebutton.org/images/22-playback-overview.png)

The presentation area displays the current slide or screenshare.

### Layout controls

The layout controls appear in the upper right-hand corner.

![Layout](https://docs.bigbluebutton.org/images/22-playback-layout.png)

These controls let you quickly

- do a full-text search of all slides in the recording,
- swap the webcam area with the presentation area, and
- view presentation area full-screen.

### Thumbnail navigation

All slides in the recording appear as a row of thumbnails below the presentation area. The player highlights the current slide in the playback.

![Thumbnails](https://docs.bigbluebutton.org/images/22-playback-thumb.png)

You can click on any slide to jump to that segment of the playback.

![Thumbnails](https://docs.bigbluebutton.org/images/22-playback-thumbnails.png)

A screenshare icon will appear for any segment of the recording that contains a screenshare.

### Show chat/shared notes

The chat area shows all the chat and shared notes for the session.

![Chat](https://docs.bigbluebutton.org/images/22-playback-chat.png)

Click the shared notes and chat icons to switch between the views. The shared notes shows the final state of shared notes when the recording ended.

The chat messages are clickable, enabling the user to quickly advance to the recording at the point which that chat message was entered. Poll results now appear in the chat as well.

### Search

When creating the recording, BigBlueButton extracts the text for each slide.

Clicking the magnifying glass icon will bring up a search dialog box that lets enter text and show only the slides that contain that text. In the screenshot below, the user typed ‘avoc’ and found one slide contained that text.

![Search](https://docs.bigbluebutton.org/images/22-playback-search2.png)

Clicking the search icon will apply the search filter to the thumbnails. The user can then click a thumbnail to advance to that segment in the recording that has the search text on the slide.

![Search](https://docs.bigbluebutton.org/images/22-playback-results.png)

Clicking the ‘x’ button clears the search and displays all thumbnails again.

### Playback speed

The playback control lets the user adjust the playback speed for the recording.

![Search](https://docs.bigbluebutton.org/images/22-playback-speed.png)

## Usability

### Quickly choose a presentation

When you upload a presentation, the ‘+’ shows a list of all uploaded presentations, making it very easy to switch between them.

![Choose Presentation](https://docs.bigbluebutton.org/images/22-choose-presentation.png)

### Notifications of raise hand

Moderators have two additional notifications: raise hands and guest waiting.

![Moderator notifications](https://docs.bigbluebutton.org/images/23-moderator-notifications.png)

For raise hands, a persistent toast notification will appear when a student raises their hand. The notification will remain the screen as long as at least one student has their hand raised.

![multiple notifications](https://docs.bigbluebutton.org/images/23-two-students.png)

The teacher can lower individual hands by clicking on user’s avatar in the notification - for example, clicking on ‘Ma’ will lower Matthew Thomas’s hand) - or the teacher can lower all hands and close the dialog by clicking “Lower Hands”.

To make it easier to raise/lower your hand, users now have a Raise Hand button on the toolbar.

![Moderator notifications](https://docs.bigbluebutton.org/images/23-raise-hand.png)

The Raise Hand button is a one-click shortcut for a clicking on your avatar, choosing Set status, and choosing Raise hand.

### Repositioning webcams

The webcams can now appear on the left or right of the presentation, maximizing the available viewing area for the presentation.

![Repositioning webcams](https://docs.bigbluebutton.org/images/bigbluebutton-repositioning-webcams.png)

### Uploaded slides in the background

When upload slides, the presenter immediately returns to the main window and can continue to engage students as the slides upload in the background.

![BigBlueButton uploaded slides](https://docs.bigbluebutton.org/images/bigbluebutton-uploaded-slides.png)

### Network connectivity icon

A network connectivity status icon now appears in the upper right-hand corner. This icon will show green when connectivity is good, and will change when the client detects a degraded connection or loss of connection.

![BigBlueButton connectivity indicator](https://docs.bigbluebutton.org/images/23-connectivity-bad.gif)

This icon shows green when the BigBlueButton client has a stable connection. If the client looses connection to the server, the connectivity icon will turn red and the client will attempt to reconnect.

The icon is clickable. When clicked, a dialog appears that lets the user turn off webcam and/or screen share videos to reduce bandwidth.

![BigBlueButton connectivity indicator](https://docs.bigbluebutton.org/images/23-connectivity-dialog.png)

The dialog will also show a recent log of connectivity changes. Here shows the user that at 8:11 am the client detected that the network connection was degraded.

Note: The design of the network icons and color are still under development.

### User connectivity log for moderators

To help moderators see if any users are having connectivity issues, when a moderator clicks their Connectivity Status icon, they will see a log of their connectivity status as well as a log of the connectivity status for all students in their session.

![BigBlueButton connection status](https://docs.bigbluebutton.org/images/bigbluebutton-connection-status.png)

Here the screen shot shows that Kert had a small dip in connectivity at 1:04 PM and Tyler at 1:18 PM.  Note: The display is of past events, not current status.  Kert’s and Tyler’s connectivity may have reverted to normal.

This log helps instructors quickly see if network bandwidth might be an issue.  For example, if a user is saying the instructor’s audio is not sounding good, and the Connectivity status shows that user was recently shown a message that their client might be experiencing networking issues, then the poor audio is likely a result of networking issues.

### Smart Poll button with choices

The Smart Poll button now appears on the toolbar and shows the polling option.

![BigBlueButton smart polling](https://docs.bigbluebutton.org/images/bigbluebutton-smart-poll.png)

### Polling results in the chat experience

The poll results will also show in the chat. This helps make the poll results visible when the presentation is not visible, such as when sharing your screen.

![BigBlueButton connection status](https://docs.bigbluebutton.org/images/bigbluebutton-polling-results.png)

### Screen share system audio when sharing Chrome tab

When you screen share using Chrome and choose sharing a Chrome Tab, you can now include system audio from that tab. Users viewing the screen share will be able to hear any audio broadcasted from that tab.

To include the audio, choose
Chrome Tab
as check the
Share audio
option in the bottom left-hand corner.

![Screen share tab](https://docs.bigbluebutton.org/images/23-screen-share-tab.png)

### Notification of talking when muted

When talking with a muted microphone, BigBlueButton will now show a message that you are muted.

![Unmute microphone](https://docs.bigbluebutton.org/images/23-unmute-mic.png)

## Engagement

### Per-user whiteboard

You can give a specific student the ability to write on the whiteboard (instead of all students).

![BigBlueButton per-user whiteboard access](https://docs.bigbluebutton.org/images/23-give-whiteboard.png)

Once you have given an individual user whiteboard access, a pen icon appears next to their avatar.

![BigBlueButton per-user whiteboard access](https://docs.bigbluebutton.org/images/23-received-whiteboard.png)

You can revoke individual whiteboard access by clicking their avatar again and choosing “Remove whiteboard access”

![BigBlueButton per-user whiteboard access](https://docs.bigbluebutton.org/images/23-take-whiteboard.png)

When granting individual whiteboard access, a count will appear on the multi-user whiteboard icon showing you how many students you have granted access to the whiteboard.

![BigBlueButton per-user whiteboard access](https://docs.bigbluebutton.org/images/23-notification-of-whiteboard.png)

Clicking the multi-user whiteobard icon removes whiteboard access from everyone except the presenter.

### Easier editing of polling choices

The preset choices for polling – True/False, A/B/C/D, Yes/No/Abstention – are now just default labels for a given list of polling choices.

The presenter can now click the ‘+’ to add a new polling option, or the trash icon to remove a polling option.

![BigBlueButton polling typed responses](https://docs.bigbluebutton.org/images/bigbluebutton-polling-typed-response.png)

### Typed responses to polling questions

There is a new polling choice called
**User Response**
. With User Response, you can have students provide a written response to a poll question. From the user’s point of view, when prompted, they will see a dialog box in the lower right-hand corner.

![BigBlueButton polling typed responses](https://docs.bigbluebutton.org/images/23-user-reponse.png)

### Randomly choose a user

You can have BigBlueButton randomly pick a user in the class. You and the student chosen will see the choice after a brief animation.

![BigBlueButton randomly select a user](https://docs.bigbluebutton.org/images/bigbluebutton-randomly-select-a-user.png)

![BigBlueButton selected user](https://docs.bigbluebutton.org/images/bigbluebutton-selected-user.png)

You need at least two other viewers in the session.
