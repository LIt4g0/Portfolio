# *Idle Miner*

<img src="Images\BugStomper3.png" width="50%"/>

Worked as **Gameplay Programmer**  and **Everything else!**\
*2025 January 13 - 2025 February 28*

This game was developed during a solo assignment at Yrgo, we where tasked to make a mobile game in Unity with the optional challenge to include Firebase database system for online functionalities like saving or multiplayer. I decided to redo a prototype I did back in 2021 but for mobile and with some multiplayer functionality. The game is an idle game about mining ore from asteroids in space, it is heavily inspired by EVE Online's mining gameplay. 

## Gameplay
<table>
  <tr>
    <td ><img src="Images\BugStomper2.png"/></td>
    <td ><img src="Images\BugStomper1.png"/></td>
  </tr>
</table>

The gameplay evolved quite a bit from the prototype, originally you would just click an asteroid, automatically mine it, click to mouse to mine faster and upgrade. In this version I added the ability to control your ship, making it orbit an asteroid or even fly over to another player, this movement has zero effect on the mining but seeing as the game is an idle game it is nice to fly around and look at some of your co-miners while mining! One big design change I ended up doing was taking away the ability to click to mine, as this never matched the feel I wanted the game to have. It was not supposed to be about tapping the screen fast with multiple fingers to mine at lightning fast speeds. So I removed the ability to tap the screen, which felt like a risk as most players who had tested it had mostly played that way. But when I removed it, it opened up the time and focus for players to use abilites with cooldowns and plan their upgrades better. It also perfectly represented the feel I was always going for, idle atmospheric beautiful space mining with chill tunes. The game had also gained complexity in other parts. Since mining from the same asteroids as other player you would gain a bonus. I then implemented a more compelling method of active play, as asteroids would gradually break down and parts of different rarity will break off, you can now tap any of these pieces to gain ore directly. As a last layer of complexity I added a time based mini game that would start when an asteroids core is exposed after detoriating the shell. When the core is exposed you can mine directly from it and your laser's focus crystal gains heat and this multiplies your mining amount and slowly depletes. So you would want to spend your cooldowns when a core is exposed. The final layer of complexity would come from the explosion of the core, spawning core pieces that you can directly tap to gain the rare ore.

In short the game is about clicking an asteroid and watching your ship mine it slowly, as you mine buy and use your upgrades stratigically.
** Show gifs of mining gameplay **

## Game Design
The game design was initially pretty much the same as my old prototype, you click and asteroid, your ship starts mining it. You can click to mine faster and when you deplete the ore in the asteroid you get a little extra as a resource. The original game was however intended for PC and had a full inventory and ship equipment system, with selling the different ore type etc. I decided to simplify the system for the mobile version, so you only have two types of ores and upgrade ranks. You use the regular ore to incrementally upgrade your mining laser, the rare ore will be used to gain new abilities and high level upgrades. I designed a progresssion system that increased costs of upgrades exponentially, this was stored in a scriptable object so each upgrade could have their own cost and cost curve with the option to manually set a new curve at any level range you want. It turned out to be quite a flexible system, intended to help with quick rebalancing of upgrades costs as the player would by design upgrade their ship to mine exponentially faster I would need to adjust this often as I added new upgrades and playtested. The system also allows for changing these values at any time, so if I did a patch and increased or lowered the cost the save file of players would be unaffected, and only the cost of their next upgrade and up would be effected. 
** Show progression script **

## Unity's action and event system
I chose to focus on using Unity's action event system during this project to try and evolve my default Unity workflow. It also makes each script and gameobject more work in a vacuum as there will be no missing references errors. Rather than manually assigning references most of the games gameobjects communicate by sending out and listening to events. This felt like an upgrade in most cases because using just hard coded references quickly gets messy and hard to troubleshoot. Now I could easily access any event from any script and also send out events from any script. The risk here of course would be that some scripts could have invoked an event that they should not do. But as this was a solo project this never occured. If I were to use this approach on a game developed by a team there would have to be restrictions as to which script could invoke which messages. A very good example of a use case for the event system was when the game saves, my save manager simply sent out an event that all objects storing relevant save that was subscribed to. They then returned the appropriate save data to the save manager. For example, the level of my upgrades were stored in one script, while the contents of my cargohold was stored in another script. This was then gathered neatly by just invoking one event from the save manager.
** Show script with good example of actions usage **

## Online Functionality
I was quite excited to try my hands on some online functionality so even though it was an optional assignment to include Firebase I chose to inlcude it. Since the game originally was inspired by a MMO it only felt fitting to add some multiplayer functionality. Due to the limited time I initally planned to just include a shared rank that would multiply every players mining efficiency when it ranked up. This would be leveled up based on how much total ore all players had mined. I also included a login system where the save files would be saved to the online database as well (we were using Firebase). Whenever the game was saved, the progress bar would update serverside based on how much ore the player had mined since the last save. It is represented in game as a big experience bar which I chose to name Megaproject. So all players are working on this Megaproject collectively by just playing the game, no extra effort needed. Just a nice little extra incentive. The implementation of this went very smooth, so next I implemented and online check to prevent the offline mining progress of players from cheating by adjusting their phones time and date. It would now use the server time to compare. Next I chose to implement a simulated multiplayer experience, where other players avatars could spawn into your area and mine together with you, giving you perks if you both mined from the same asteroid, that presented some challenges but it all worked out fine. I now realized that it wouldn't be that hard to add actual multiplayer, where the other players actually where in the same position and mining the same asteroid as you saw them in game in real time. However as I had limited time left at this point and the fact that it wouldn't add any new functionality I chose to hold off on this and focus on giving the game a bit more polish.
** Show some script that show online functionality **




## Art and more
While I am definitely no artist I do often find fun in designing every piece of the games I make, and in the case of this game I did everything in the game except for some UI art and the music. I love to dabble with Magica Voxel, and that is where I designed the space ship and asteroids. I spent a lot of time handcrafting the different pieces of the asteroid that would fall off, it was fun and refreshing to focus on something else and it helped add some juice to the game. The mining laser sound was mixed in Audacity from a guitar line I recorded and a sound effect that sounds like crackling electricity. The space skybox background is generated in a software called Spacescape. Laser and particle effects are made with Unity's particle system. I also worked a little in Unity shader graph to create the light cone spotlight seen in the game.
** Show gif of asteroid breaking apart **




## Release date?
Here is a link to the latest playable version for Android: 

I hope to do some major balancing fixes and polish during the summer of 2025 to then release this game for free on Android Store and Itch.io this fall.

I also have a dream of creating a much more complex version with the same gameplay at it's core for PC. Here the focus would be a real living economy, either simulated or a purely multiplayer driven economy similar to EVE Online. If you want to help me build this game or fund it I would love to hear from you!

## Tools used:
Unity
VS Code
Firebase
Magica Voxel
Blender


