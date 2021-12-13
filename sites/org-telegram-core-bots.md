Bots: An introduction for developers
==========

Bots are third-party applications that run inside Telegram. Users can interact with bots by sending them messages, commands and [inline requests](#inline-mode). You control your bots using HTTPS requests to Telegram's [Bot API](/bots/api).

>
>
> The [full API reference](/bots/api) for **developers** is available [here](/bots/api).
>
>

### [](#1-what-can-i-do-with-bots)1. What can I do with bots? ###

[![](/file/811140663/1/uHVzwsRJz3Y/a499733c59840694ca "A chat with a bot also showing search results from the @gif inline-bot")](/file/811140081/1/VldnlW70g2I/a140b0216e7d156ebc)

To name just a few things, you could use bots to:

* **Get customized notifications and news**. A bot can act as a smart newspaper, sending you relevant content as soon as it's published.

* **Integrate with other services**. A bot can enrich Telegram chats with content from external services.
  [**Gmail Bot**](https://t.me/gmailbot), [**GIF bot**](https://t.me/gif), [**IMDB bot**](https://t.me/imdb), [**Wiki bot**](https://t.me/wiki), [**Music bot**](https://t.me/music), [**Youtube bot**](https://t.me/youtube), [**GitHubBot**](https://t.me/githubbot)

* **Accept payments from Telegram users**. A bot can offer paid services or work as a virtual storefront. [Read more »](/bots/payments)
  [**Demo Shop Bot**](https://t.me/shopbot), [**Demo Store**](https://t.me/teststore)

* **Create custom tools**. A bot may provide you with alerts, weather forecasts, translations, formatting or other services.
  [**Markdown bot**](https://t.me/Bold), [**Sticker bot**](https://t.me/sticker), [**Vote bot**](https://t.me/vote), [**Like bot**](https://t.me/like)

* **Build single- and multiplayer games**. A bot can offer rich [HTML5 experiences](/bots/games), from simple arcades and puzzles to 3D-shooters and real-time strategy games.
  [**GameBot**](https://t.me/gamebot), [**Gamee**](https://t.me/gamee)

* **Build social services**. A bot could connect people looking for conversation partners based on common interests or proximity.

* **Do virtually anything else**. Except for dishes — bots are terrible at doing the dishes.

### [](#2-how-do-bots-work)2. How do bots work? ###

At the core, Telegram Bots are special accounts that do not require an additional phone number to set up. Users can interact with bots in two ways:

* Send messages and [commands](#commands) to bots by opening a chat with them or by adding them to groups.
* Send requests directly from the input field by typing the bot's @username and a query. This allows sending content from [inline bots](/bots/inline) directly into any chat, group or channel.

Messages, commands and requests sent by users are passed to the software running on your servers. Our intermediary server handles all encryption and communication with the Telegram API for you. You communicate with this server via a simple HTTPS-interface that offers a simplified version of the Telegram API. We call that interface our [Bot API](/bots/api).

>
>
> A detailed description of the Bot API is available on [this page »](/bots/api)
>
>

### [](#3-how-do-i-create-a-bot)3. How do I create a bot? ###

[![](/file/811140763/1/PihKNbjT8UE/03b57814e13713da37 "The Botfather. Click for hi-res picture")](/file/811140327/1/zlN4goPTupk/9ff2f2f01c4bd1b013)

There's a… bot for that. Just talk to [BotFather](https://t.me/botfather) (described [below](#6-botfather)) and follow a few simple steps. Once you've created a bot and received your authentication token, head down to the [Bot API manual](/bots/api) to see what you can teach your bot to do.

>
>
> You may also like to check out some **code examples** [here »](/bots/samples)
>
>

### [](#4-how-are-bots-different-from-humans)4. How are bots different from humans? ###

* Bots have no online status and no last seen timestamps, the interface shows the label **'bot'** instead.
* Bots have limited cloud storage — older messages may be removed by the server shortly after they have been processed.
* Bots can't initiate conversations with users. A user **must** either add them to a group or send them a message first. People can use `t.me/<bot_username>` links or username search to find your bot.
* Bot usernames always end in 'bot' (e.g. [@TriviaBot](https://t.me/triviabot), [@GitHub\_bot](https://t.me/githubbot)).
* When added to a group, bots do not receive all messages by default (see [Privacy mode](#privacy-mode)).
* Bots never eat, sleep or complain (unless expressly programmed otherwise).

---

### [](#5-bot-perks)5. Bot perks ###

Telegram bots are unique in many ways — we offer [two](#keyboards) [kinds](#inline-keyboards-and-on-the-fly-updating) of keyboards, additional interfaces for [default commands](#global-commands) and [deep linking](#deep-linking) as well as [text formatting](/bots/api#formatting-options), [integrated payments](#payment-platform) and more.

#### [](#inline-mode)Inline mode ####

Users can interact with your bot via [**inline queries**](/bots/api#inline-mode) straight from the **text input field** in **any** chat. All they need to do is start a message with your bot's username and then type a query.

Having received the query, your bot can return some results. As soon as the user taps one of them, it is sent to the user's currently opened chat. This way, people can request content from your bot in any of their chats, groups or channels.

Check out this [blog](https://telegram.org/blog/inline-bots) to see a sample inline bot in action. You can also try the [@sticker](https://t.me/sticker) and [@music](https://t.me/music) bots to see for yourself.

[![](/file/811140558/1/POjp00-nHqE/50d0312845a05e6da9 "New input field")](/file/811140558/1/POjp00-nHqE/50d0312845a05e6da9)

We've also implemented an easy way for your bot to [switch between inline and PM modes](/bots/inline#switching-inline-pm-modes).

>
>
> [Read more about the Inline Mode »](/bots/inline)
>
>

#### [](#payment-platform)Payment platform ####

You can use bots to **accept payments** from Telegram users around the world.

* Send invoices to **any chat**, including to groups and channels.
* Create invoices that can be **forwarded** and used by **multiple buyers** to order things.
* Use [inline mode](/bots/inline) to help users show your goods and services to their friends and communities.
* Allow **tips** from users with preset and custom amounts.
* Accept payments from users on mobile or **desktop apps**.
* Try [@ShopBot](https://t.me/shopbot) to create a test invoice – or start a message with `@ShopBot ...` in any chat for an **inline invoice**.
* Check out [Demo Shop](https://telegram.org/teststore) for an example of a [Telegram Channel](https://telegram.org/tour/channels) used as **virtual storefront**.

>
>
> [Read more about the Payments Platform »](/bots/payments)
>
>

#### [](#gaming-platform)Gaming platform ####

Bots can offer their users **HTML5 games** to play solo or to compete against each other in groups and one-on-one chats. The platform allows your bot to keep track of **high scores** for every game played in every chat. Whenever there’s a new leader in the game, other playing members in the chat are notified that they need to step it up.

[![](/file/811140306/1/dkciuEDbpxU.193188/8a0a21b6e9d111be4c "Game in a chat")](/file/811140306/1/dkciuEDbpxU.193188/8a0a21b6e9d111be4c) [![](/file/811140426/1/ZCw3vu_v8s0.109692/04efd9e88644939a4f "In-game scoreboard and sharing button")](/file/811140426/1/ZCw3vu_v8s0.109692/04efd9e88644939a4f)

Since the underlying technology is HTML5, the games can be anything from simple arcades and puzzles to multiplayer 3D-shooters and real-time strategy games. Our team has created a couple of simple demos for you to try out:

* [Math Battle](https://t.me/gamebot?game=MathBattle)
* [Lumberjack](https://t.me/gamebot?game=Lumberjack)
* [Corsairs](https://t.me/gamebot?game=Corsairs)

You can also check out the [**@gamee**](https://t.me/gamee) bot that has more than 20 games.

>
>
> [Read more about the Gaming Platform »](https://telegram.org/blog/games)
>
>

#### [](#keyboards)Keyboards ####

Traditional chat bots can of course be taught to understand human language. But sometimes you want some more formal input from the user — and this is where **custom keyboards** can become extremely useful.

Whenever your bot sends a message, it can pass along a special keyboard with predefined reply options (see [ReplyKeyboardMarkup](/bots/api/#replykeyboardmarkup)). Telegram apps that receive the message will display your keyboard to the user. Tapping any of the buttons will immediately send the respective command. This way you can drastically simplify user interaction with your bot.

We currently support text and emoji for your buttons. Here are some custom keyboard examples:

[![](/file/811140184/1/5YJxx-rostA/ad3f74094485fb97bd "Keyboard for a poll bot")](/file/811140184/1/5YJxx-rostA/ad3f74094485fb97bd) [![](/file/811140880/1/jS-YSVkDCNQ/b397dfcefc6da0dc70 "Keyboard for a calculator bot. Because you can.")](/file/811140880/1/jS-YSVkDCNQ/b397dfcefc6da0dc70) [![](/file/811140733/2/KoysqJKQ_kI/a1ee46a377796c3961 "Keyboard for a trivia bot")](/file/811140733/2/KoysqJKQ_kI/a1ee46a377796c3961)

>
>
> For more technical information on custom keyboards, please consult the [Bot API manual](/bots/api) (see [sendMessage](/bots/api#sendmessage)).
>
>

#### [](#inline-keyboards-and-on-the-fly-updating)Inline keyboards and on-the-fly updating ####

There are times when you'd prefer to do things without sending any messages to the chat. For example, when your user is changing settings or flipping through search results. In such cases you can use Inline Keyboards that are integrated directly into the messages they belong to.

Unlike with custom reply keyboards, pressing buttons on inline keyboards doesn't result in messages sent to the chat. Instead, inline keyboards support buttons that work behind the scenes: [callback buttons](/bots/2-0-intro#callback-buttons), [URL buttons](/bots/2-0-intro#url-buttons) and [switch to inline buttons](/bots/2-0-intro#switch-to-inline-buttons).

[![](/file/811140217/1/NkRCCLeQZVc/17a804837802700ea4 "Callback buttons in @music")](/file/811140217/1/NkRCCLeQZVc/17a804837802700ea4) [![](/file/811140659/1/RRJyulbtLBY/ea6163411c7eb4f4dc "More callback buttons in @music")](/file/811140659/1/RRJyulbtLBY/ea6163411c7eb4f4dc) [![](/file/811140999/1/2JSoUVlWKa0/4fad2e2743dc8eda04 "A URL button")](/file/811140999/1/2JSoUVlWKa0/4fad2e2743dc8eda04)

When callback buttons are used, your bot can update its existing messages (or just their keyboards) so that the chat remains tidy. Check out these sample bots to see inline keyboards in action: [@music](https://t.me/music), [@vote](https://t.me/vote), [@like](https://t.me/like).

>
>
> [Read more about inline keyboards and on-the-fly editing »](/bots/2-0-intro#new-inline-keyboards)
>
>

#### [](#commands)Commands ####

Commands present a more flexible way to communicate with your bot. The following syntax may be used:

```
/command
```

A command must always start with the '/' symbol and may not be longer than 32 characters. Commands can use latin letters, numbers and underscores. Here are a few examples:

```
/get_messages_stats
/set_timer 10min Alarm!
/get_timezone London, UK
```

Messages that start with a slash are always passed to the bot (along with replies to its messages and messages that @mention the bot by username). Telegram apps will:

* Suggest a list of supported commands with descriptions when the user enters a '/' (for this to work, you need to have provided a list of commands to the [BotFather](#6-botfather)). Tapping on a command in the list immediately sends the command.
* Show an additional **(/)** button in the input field in all chats with bots. Tapping it types a '/' and shows the list of commands.
* Highlight **/commands** in messages. When the user taps a highlighted command, the command is sent at once.

[![](/file/811140845/2/rNUxpcGDeQU/05eaaf20b0dbaf9cb3 "Suggested commands")](/file/811140845/2/rNUxpcGDeQU/05eaaf20b0dbaf9cb3) [![](/file/811140315/2/gf7_D2HbeyM/e3ca2de4de7918f826 "Notice the new button in the input field, right next to the sticker button")](/file/811140315/2/gf7_D2HbeyM/e3ca2de4de7918f826) [![](/file/811140029/1/s5zv4fbWdhw/a04aefa0ee0557f16a "Suggested commands for multiple bots")](/file/811140029/1/s5zv4fbWdhw/a04aefa0ee0557f16a)

If multiple bots are in a group, it is possible to add bot usernames to commands in order to avoid confusion:

```
/start@TriviaBot
/start@ApocalypseBot
```

This is done automatically when commands are selected via the list of suggestions. Please remember that your bot needs to be able to process commands that are followed by its username.

##### [](#global-commands)Global commands #####

In order to make it easier for users to navigate the bot multiverse, we ask all developers to support a few basic commands. Telegram apps will have **interface shortcuts** for these commands.

* **/start** - begins interaction with the user, e.g., by sending a greeting message. This command can also be used to pass additional parameters to the bot (see [Deep linking](#deep-linking))
* **/help** - returns a help message. It can be a short text about what your bot can do and a list of commands.
* **/settings** - (if applicable) returns the bot's settings for this user and suggests commands to edit these settings.

Users will see a **Start** button when they first open a conversation with your bot. **Help** and **Settings** links will be available in the menu on the bot's profile page.

[![](/file/811140979/2/yD8AphHbahk/7662d14f4e0442ae3a "An empty conversation with a bot")](/file/811140979/2/yD8AphHbahk/7662d14f4e0442ae3a) [![](/file/811140479/2/1c2zUWhR7sA/98889b2a45f8e42a35 "A bot's profile page, featuring 'Help' and 'Settings' buttons")](/file/811140479/2/1c2zUWhR7sA/98889b2a45f8e42a35)

#### [](#formatting-bold-italic-fixed-width-text-and-inline-links)Formatting: bold, italic, fixed-width text and inline links ####

You can use bold, italic or fixed-width text, as well as inline links in your bots' messages. Telegram clients will render them accordingly.

>
>
> [Read more in the Bot API manual »](bots/api#formatting-options)
>
>

#### [](#privacy-mode)Privacy mode ####

Bots are frequently added to groups in order to augment communication between human users, e.g. by providing news, notifications from external services or additional search functionality. This is especially true for work-related groups. Now, when you share a group with a bot, you tend to ask yourself “How can I be sure that the little rascal isn't selling my chat history to my competitors?” The answer is — **privacy mode**.

A bot running in privacy mode will not receive all messages that people send to the group. Instead, it will only receive:

* Messages that start with a slash '/' (see [Commands](#commands) above)
* Replies to the bot's own messages
* Service messages (people added or removed from the group, etc.)
* Messages from channels where it's a member

On one hand, this helps some of us sleep better at night (in our tinfoil nightcaps), on the other — it allows the bot developer to save a lot of resources, since they won't need to process tens of thousands irrelevant messages each day.

Privacy mode is enabled by default for all bots, except bots that were added to the group as **admins** (bot admins always receive all messages). It can be disabled, so that the bot receives all messages like an ordinary user (the bot will need to be **re-added** to the group for this change to take effect). We only recommend doing this in cases where it is absolutely necessary for your bot to work — users can always see a bot's current privacy setting in the group members list. In most cases, using the [force reply](/bots/api#forcereply) option for the bot's messages should be more than enough.

[So what messages exactly will my bot get? »](/bots/faq#what-messages-will-my-bot-get)

#### [](#deep-linking)Deep linking ####

Telegram bots have a [deep linking](https://en.wikipedia.org/wiki/Deep_linking) mechanism, that allows for passing additional parameters to the bot on startup. It could be a command that launches the bot — or an authentication token to connect the user's Telegram account to their account on some external service.

Each bot has a link that opens a conversation with it in Telegram — `https://t.me/<bot username>`. You can add the parameters **start** or **startgroup** to this link, with values up to 64 characters long. For example:

```
https://t.me/triviabot?startgroup=test
```

`A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. We recommend using [base64url](https://en.wikipedia.org/wiki/Base64#The_URL_applications) to encode parameters with binary and other types of content.

Following a link with the **start** parameter will open a one-on-one conversation with the bot, showing a START button in the place of the input field. If the **startgroup** parameter is used, the user is prompted to select a group to add the bot to. As soon as a user confirms the action (presses the START button in their app or selects a group to add the bot to), your bot will receive a message from that user in this format:

```
/start PAYLOAD
```

`PAYLOAD` stands for the value of the **start** or **startgroup** parameter that was passed in the link.

##### [](#deep-linking-example)Deep linking Example #####

Suppose the website example.com would like to send notifications to its users via a Telegram bot. Here's what they could do to enable notifications for a user with the ID `123`.

1. [Create a bot](#6-botfather) with a suitable username, e.g. @ExampleComBot
2. Set up a [webhook](/bots/api#setwebhook) for incoming messages
3. Generate a random string of a sufficient length, e.g. `$memcache_key = "vCH1vGWJxfSeofSAs0K5PA"`
4. Put the value `123` with the key `$memcache_key` into Memcache for 3600 seconds (one hour)
5. Show our user the button `https://t.me/ExampleComBot?start=vCH1vGWJxfSeofSAs0K5PA`
6. Configure the webhook processor to query Memcached with the parameter that is passed in incoming messages beginning with `/start`. If the key exists, record the chat\_id passed to the webhook as **telegram\_chat\_id** for the user `123`. Remove the key from Memcache.
7. Now when we want to send a notification to the user `123`, check if they have the field **telegram\_chat\_id**. If yes, use the [sendMessage](/bots/api#sendmessage) method in the [Bot API](/bots/api) to send them a message in Telegram.

#### [](#location-and-number)Location and Number ####

Some bots need extra data from the user to work properly. For example, knowing the user's location helps provide more relevant geo-specific results. The user's phone number can be very useful for integrations with other services, like banks, etc.

Bots can ask a user for their **location** and **phone number** using special buttons. Note that both phone number and location request buttons will only work in private chats.

[![](/file/811140587/2/jaowDLZg2l0/5ba3f7d7fd5c6c28dc "Phone number and location sharing buttons")](/file/811140587/2/jaowDLZg2l0/5ba3f7d7fd5c6c28dc)

When these buttons are pressed, Telegram clients will display a confirmation alert that tells the user what's about to happen.

>
>
> [Manual: Number and location buttons »](/bots/api#keyboardbutton)
>
>

---

### [](#6-botfather)6. BotFather ###

>
>
> Jump to top to learn everything about [Telegram bots »](#)
>
>

[BotFather](https://t.me/botfather) is the one bot to rule them all. It will help you create new bots and change settings for existing ones.

#### [](#creating-a-new-bot)Creating a new bot ####

Use the **/newbot** command to create a new bot. The BotFather will ask you for a name and username, then generate an authentication token for your new bot.

The **name** of your bot is displayed in contact details and elsewhere.

The **Username** is a short name, to be used in mentions and t.me links. Usernames are 5-32 characters long and are case insensitive, but may only include Latin characters, numbers, and underscores. Your bot's username **must** end in 'bot', e.g. 'tetris\_bot' or 'TetrisBot'.

The **token** is a string along the lines of `110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw` that is required to authorize the bot and send requests to the [Bot API](/bots/api). Keep your token secure and store it safely, it can be used by anyone to control your bot.

#### [](#generating-an-authentication-token)Generating an authentication token ####

If your existing token is compromised or you lost it for some reason, use the **/token** command to generate a new one.

#### [](#botfather-commands)Botfather commands ####

The remaining commands are pretty self-explanatory:

* **/mybots** — returns a list of your bots with handy controls to edit their settings
* **/mygames** — does the same for your games

**Edit bots**

* **/setname** – change your bot's name.
* **/setdescription** — change the bot's **description**, a short text of up to 512 characters, describing your bot. Users will see this text at the beginning of the conversation with the bot, titled 'What can this bot do?'.
* **/setabouttext** — change the bot's **about info**, an even shorter text of up to 120 characters. Users will see this text on the bot's profile page. When they share your bot with someone, this text is sent together with the link.
* **/setuserpic** — change the bot's profile pictures. It's always nice to put a face to a name.
* **/setcommands** — change the list of commands supported by your bot. Users will see these commands as suggestions when they type `/` in the chat with your bot. Each command has a name (must start with a slash ‘/’, alphanumeric plus underscores, no more than 32 characters, case-insensitive), parameters, and a text description. Users will see the list of commands whenever they type '/' in a conversation with your bot.
* **/deletebot** — delete your bot and free its username.

**Edit settings**

* **/setinline** — toggle [inline mode](/bots/inline) for your bot.
* **/setinlinegeo** - request location data to provide [location-based inline results](/bots/inline#location-based-results).
* **/setjoingroups** — toggle whether your bot can be added to groups or not. Any bot must be able to process private messages, but if your bot was not designed to work in groups, you can disable this.
* **/setprivacy** — set which messages your bot will receive when added to a group. With privacy mode disabled, the bot will receive all messages. We recommend leaving [privacy mode](#privacy-mode) enabled. You will need to re-add the bot to existing groups for this change to take effect.

**Manage games**

* **/newgame** — create a new [game](/bots/games).
* **/listgames** — get a list of your games.
* **/editgame** — edit a game.
* **/deletegame** — delete an existing game.

>
>
> Please note, that it may take **a few minutes** for changes to take effect.
>
>

#### [](#status-alerts)Status alerts ####

Millions choose Telegram for its speed. To stay competitive in this environment, your bot also needs to be responsive. In order to help developers keep their bots in shape, Botfather will send status alerts if it sees something is wrong.

We will be checking the number of replies and the request/response conversion rate for popular bots (\~300 requests per minute: but don't write this down as the value may change in the future). If we get abnormally low readings, you will receive a notification from Botfather.

##### [](#responding-to-alerts)Responding to alerts #####

By default, you will only get one alert per bot per hour. Each alert has the following buttons:

* **Fixed.** Use this if you found an issue with your bot and fixed it. If you press the fix button, we will resume sending alerts in the regular way so that you can see if your fix worked within 5-10 minutes instead of having to wait for an hour.
* **Support.** Use this to open a chat with [@BotSupport](https://t.me/botsupport) if you don't see any issues with your bot or if you think the problem is on our side.
* **Mute for 8h/1w.** Use this if you can't fix your bot at the moment. This will disable all alerts for the bot in question for the specified period of time. We do not recommend using this option since your users may migrate to a more stable bot. You can unmute alerts in your bot's settings via Botfather.

##### [](#monitored-issues)Monitored issues #####

We will currently notify you about the following issues:

**1.**

```
Too few **private messages** are sent compared to previous weeks: **{value}**
```

Your bot is sending much fewer messages than it did in the previous weeks. This is useful for newsletter-style bots that send out messages without prompts from the users. The larger the value, the more significant the difference.

**2.**

```
Too few replies to incoming **private messages**. Conversion rate: **{value}**
```

Your bot is not replying to all messages that are being sent to it (the request/response conversion rate for your bot was too low for at least two of the last three 5-minute periods). To provide a good user experience, please respond to all messages that are sent to your bot. Respond to *message* [updates](https://core.telegram.org/bots/api#update) by calling *send…* methods (e.g. [sendMessage](https://core.telegram.org/bots/api#sendmessage)).

**3.**

```
Too few answers to **inline queries**. Conversion rate: **{value}**
```

Your bot is not replying to all inline queries that are being sent to it, calculated in the same way as above. Respond to *inline\_query* [updates](https://core.telegram.org/bots/api#update) by calling [answerInlineQuery](/bots/api#answerinlinequery).

**4.**

```
Too few answers to **callback queries**. Conversion rate: **{value}**
Too few answers to **callback game queries**. Conversion rate: **{value}**
```

Your bot is not replying to all callback queries that are being sent to it (with or without games), calculated in the same way as above. Respond to *callback\_query* [updates](https://core.telegram.org/bots/api#update) by calling [answerCallbackQuery](/bots/api#answercallbackquery).

>
>
> Please note that the status alerts feature is still being tested and will be improved in the future.
>
>

---

That's it for the introduction. You are now definitely ready to proceed to the [**BOT API MANUAL**](/bots/api).

If you've got any questions, please check out our [**Bot FAQ »**](/bots/faq)
