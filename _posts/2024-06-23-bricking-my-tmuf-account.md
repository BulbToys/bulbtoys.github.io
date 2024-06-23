## How researching TrackMania United Forever got my account bricked

My love for TrackMania stems all the way back to the late 2000s and early 2010s, when my uncle bought me this little old game called TrackMania Sunrise for new years. As my second or third ever racing game (after Need for Speed: Carbon and Undercover), I instantly fell in love with it, especially its unique Stunts mode which eventually made its way to TMUF, as well as the unforunately long forgotten Crazy mode (that I've been meaning to make a documentary about for the longest time, with a bunch of drafted scripts now collecting dust for years lol). Here's a screenshot of me playing on an online server 14 years ago:

![A screenshot of a TrackMania Sunrise's multiplayer scoreboard.](https://bulbtoys.github.io/media/sunrise_multiplayer.png)

Sadly, all good things must come to an end. TrackMania Original's official website and master server were killed off a couple years back, and it seems like TrackMania Sunrise's online mode is inaccessible as of late as well. On the other hand, TrackMania Nations and United Forever are still going strong, even after 16 years, seeing over a thousand concurrent players every single day. I started playing TMNF during the second half of 2010 (before FreeZone was a thing!), somewhere around the time I took the above screenshot, and my uncle eventually bought me TMUF for my birthday a few years later. I've mostly been playing it on-and-off for the past decade, a few weeks of activity followed by a few months of inactivity and repeat ad infinitum, but I've been really obsessed with it lately, especially the recent Kackiest Kacky event.

TMF (referring to both Nations and United, as they both share the same online space) is probably the purest example of barely-maintained abandonware that I could think of - account creation is broken unless you enable TLS 1.0, its web services API is effectively locked out due to certificate revocations and the master server kinda just does what it wants at times. It probably didn't help that the TrackMania Exchange, the biggest community site dedicated to hosting over a million user-generated maps/tracks, suffered from a security breach in 2021, prompting similar sites like TM-Forum (the official forum for old TrackMania titles) and TrackMania Carpark (for hosting user-generated vehicle skins) to be taken down alongside it. TM-Forum never saw the light of day again, killing off a sizeable portion of knowledge as well as the most reliable way of communicating and discussing the old games, with its sister ManiaPlanet forum (for the slightly newer TM2/MP titles) permanently closing account registrations around the time of the breach. Fortunately, the Carpark was revitalized into the Maniapark a little less than a year ago, with most of its old content having been carried over!

There have been numerous occasions where I wanted to research a game, only to miss that train years after its departure. Seeing as TMF is practically on life support, I've been trying to dig out as many interesting parts of the game that I could, archived or active. I've been exploring the very few functional Manialinks left over, as well as learning to make my own. I didn't find anything too interesting, but I was sad to find that ManiaSpace (basically the same as the TrackMania Exchange but in the form of a Manialink, and much less popular and powerful) had been down as of recent months. I've also managed to find quite some interesting pages pertaining to the `official.trackmania.com` domain through the Wayback Machine's URL prefix lookup. At the time, these were fully-or-partially functional without having to rely on Wayback Machine backups, more on that in a bit.

Remember how I mentioned that TMO's official website was down? Well, it was, or so I thought - while I'm pretty sure it used to reside on `trackmania.com` (though I could very much be misremembering - I haven't accessed the website in ages), it was happily sitting on `official.trackmania.com` instead. I've tried logging in, but I'm pretty sure I quickly gave up, either because I couldn't remember my login details or the certificate revocation fiasco was just too annoying to deal with. I planned to revisit it at some point, only to find out that, mysteriously, a couple days after my scavenger hunt, the entire domain was taken down, alongside all its pages that I previously mentioned.

Either way, I was messing around with potential exploits revolving around tags - to put it shortly, tags are basically awards players can put next to their profile picture in-game - these are usually given out by players (bronze, silver or gold tier, each with their own respective price tag) or organizations (which costs a hefty sum of coppers to make, but they get a discount for any future tag creations, as well as (presumably) the ability to create Nadeo tier tags as well) and are created using the Player Page. They show up next to your profile picture, in the player list or in the top-left, as well as your profile. Coincidentially, after creating and giving myself a "glitched" tag, I've noticed my game behaving very weirdly. The following list of symptoms that I've managed to find can be observed (but are not necessarily limited to):
1. The Main Menu screen is missing the "ManiaZone" advertisement in the middle, the Explore button on the left panel, as well as the ability to share the game and add buddies on the right
2. The top taskbar is missing the Manialink browser button, my Copper count, and the messaging button
3. The Profile screen is missing the ability to manage Tags, and I am unable to change my nickname or my profile picture, nor am I able to add groups
4. The email on my Profile screen is reset each time the game is launched
5. The ability to search for multiplayer servers by name or filtering them by game mode is lost
6. I show up as "Not ranked" in any multiplayer server I join, with 0 ladder points (the Player Page shows my ladder point count correctly), and when anyone opens my profile, my location is not set and my statistics are reset
7. Official rankings in singleplayer are missing
8. The buttons to start Official races and see rankings in singleplayer are missing
9. Since the two Manialink browser buttons are inaccessible, the only way to access Manialinks is to use a $h link (from chat for example). Typing out any Manialink in the URL field will incorrectly prefix them with "http://", for example "http://manialink:home"

![Screenshots of the above side effects.](https://bulbtoys.github.io/media/tmuf_bricked.png)

Turns out, practically all of these are "features" dictated by the master server. Here are all the features I've found from calls to `CGameMasterServer::GetFeatureFromName`:
- "AbuseOnInvalidReplay" - ???
- "AccountConversion" - the ability to convert your Nations account to a United account using an activation key
- "Buddies" - the ability to add buddies, send invite links, or see if they're online
- "BuddiesMaxCount" - the maximum amount of buddies you can have (for United accounts, it's default to 64, and each additional slot costs 100 coppers)
- "ChangeAvatar" - the ability to change your avatar
- "ChangeNickName" - the ability to change your nickname
- "Coppers" - the ability to see (or use) your Coppers
- "Favourites" - the ability to manage your favorite servers 
- "FavouritesMaxCount" - the maximum amount of favorite servers you're allowed to have (think it's 25 for United and 5 for Nations)
- "FilterGameMode" - the ability to search for servers based off their gamemode
- "FindPlayers" - the ability to search for players based on their name
- "FindServers" - the ability to search for servers based on their name
- "Groups" - the ability to manage your groups from your profile
- "Maniacodes" - the ability to access Maniacodes (think of them like Manialink scripts)
- "ManialinksAnywhere" - i assume this was responsible for it incorrectly adding the "http://" prefix
- "ManialinksBrowser" - i assume this hid the Manialink browser buttons
- "Maniazone" - displays the main-menu advertisements
- "MaxGroupsCount" - the maximum amount of groups you're able to be in
- "Messenger" - the ability to message
- "MoveFromLeague" - the ability to change your zone (country/city)
- "OfficialRecords" - the ability to access official rankings or play official races
- "PersonnalDatas" - ???
- "PlayerPage" - the ability to see your Player Page from in-game
- "Referee" - the ability to become a referee on a game server
- "SendInvalidReplay" - ???
- "SendInvalidReplayNull" - ???

Wait a second... Aren't uploaded tags stored on `official.trackmania.com`? Uh oh...

![A tag creation form, showing the above URL for the preview.](https://bulbtoys.github.io/media/tag_creation.png)

Turns out, this affected the previews of created tags shown on the Player Page as well, showing up as black. It is important to note that these tags are perfectly functional in-game however.

![A list of my owned tags from the Player Page, the last one showing up as fully black.](https://bulbtoys.github.io/media/tag_list.png)

Before all this had happened, a few days ago I've noticed another player having similar issues (unranked, missing location) as I did, but I didn't think much of it - I figured that was merely the side-effect of having the game open for too long or something lmao. But, as soon as I started seeing the same symptoms with my own account, I first tried to Google my issue to no avail. Eventually, I ended up doing the unthinkable, joining a public Discord server, specifically the TrackMania one, to see if anyone had similar issues before. As it turns out, this same person already made a post in the server, which was a massive sigh of relief for me. Turns out, someone had gifted them a normal tag a couple days prior, which was an *even bigger* sigh of relief considering I thought my glitched tag had something to do with it lmao. Eventually I reached out to them and, while we've been discussing the details of the bug, I went to have lunch and, in the span of my 15 minute absense, all of those dead `official.trackmania.com` links suddenly started working and our accounts went back to normal.

Even though there's a happy end to the story, I still can't help but think in how poor of a state the game is in, though it's understandable - their main focus right now is on a game not one but two generations newer which has a much more active (and regularly paying) playerbase. Hell I'd go so far as to say that it's a miracle the master servers are up at all - yeah there are over a thousand concurrent players at any given moment but the game is nearly 16 years old by now! Then again, Sunrise and Original's master servers were kept up even when there were maybe one-two people playing monthly, so I doubt TrackMania Forever will be going away any time soon. Still would be nice to get some of these kinks ironed out though.

---

I made this blog over two months ago to document my technical findings and revelations. I've been terribly busy with college lately, as well as other projects and games as well, and I've kinda just pushed this blog to the side because of it, never really having any motivation to write anything here. Truth be told, making this blog post was slightly exhausting lol, it took several days out of my already cramped schedule but I enjoyed it nonetheless. I think I'm just used to rambling in people's Discord DMs, which are usually considerably less formal than the traditional blogging format that I've been trying to follow in this post. I might play around with that at some point, even if it makes my blog posts seem much more informal, but in the meantime, I hope you've enjoyed reading or at least found some of the things mentioned here interesting - if you did, feel free to leave a comment below (or otherwise tell me about it), any sort of feedback whatsoever is greatly appreciated and will motivate me to make more and better posts in the future. Please let me know if I've especially went a bit too off-topic with this one, I tend to get carried away when writing walls of text and I can't tell whether I've gone too far or not, even after writing it haha! In either case, thank you so much for sticking to the end with me <3