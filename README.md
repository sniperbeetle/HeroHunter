# Krunker Multihack
Hero Hunter v1.4.9

Discontinued because of some humans. Checkout my patreon tho ayy https://www.patreon.com/hrt


## How to install

<s>0. Download the latest release [here](https://github.com/hrt/HeroHunter/releases/download/1.0/HeroHunter.zip) and extract it.
1. Visit chrome://extensions (via omnibox or menu -> Tools -> Extensions).
2. Enable Developer mode by ticking the checkbox in the upper-right corner.
3. Click on the "Load unpacked extension..." button.
4. Select the extracted directory.
5. Now play krunker.io and you should notice a difference.

Toggle menu on/off with insert/home/delete

## Features
- [x] Aimbot (hold right mouse button)
- [x] Fake Lag ~ that annoying lagger who no one can hit
- [x] Snaplines esp & name esp & weapon esp
- [x] Perfect bunnyhop / slidejump (hold mouse button 5)
- [x] Anti cheat measures
- [x] Auto reload
- [x] Recoil control
- [x] Visibility check
- [x] Auto shoot & scope
- [x] Menu
- [x] Configurable keybindings
- [x] Fix auto shoot / quick scope for snipers
- [x] No death delay
- [x] Auto respawn
- [x] Box esp
- [x] Third person
- [x] Anti Aim
- [x] Auto wall (penetrate)
- [x] Everyday is sunny
- [x] 360 bot

Gameplay: https://www.youtube.com/watch?v=-UGY3wrfor0
[![Alt text](https://github.com/hrt/KrunkerMultihack/blob/master/screenshot2.png?raw=true)](https://www.youtube.com/watch?v=-UGY3wrfor0)
[![Alt text](https://github.com/hrt/KrunkerMultihack/blob/master/screenshot.png?raw=true)](https://www.youtube.com/watch?v=-UGY3wrfor0)


Came across the game this morning and quit it this evening: 


Load this extension on chrome and you're good to go.

## How does it work
The game loads a file generally called ```game.js```. We abuse the powers of the local user to use our altered version of ```game.js``` which patches certain functions. For example we can have name esp (see players through walls) by removing a simple team check during a render loop to show player cards: ```if (!tmpObj.inView) continue;```

## Anti cheat
Their "anti script" is mainly the last few lines of the js file ```zip.js```. Any script that is loaded with a source from ```jsdelivr``` or ```raw.githack.com``` gets flagged. This is easy to avoid if need be.

```
setInterval(function() {
    document.querySelectorAll("script[src*='jsdelivr'], script[src*='raw.githack.com']").length && (document.body.innerHTML = "<div style='font-size:28px;margin-top:30px;width:100%;text-align:center'>SCRIPT DETECTED</div>")
}, 1E4);
```


The anti script also checks if certain classes are defined under the ```window``` object:

```
window.chH = function(a) {
    try {
        null == window.hack && null == window.iUb && null == window.hags && null == window.aimbot && null == window.nxtrun && null == window.KrunkAimDotTK && null == window.wallHackEnabled || !a.socket || (a.send("hc"), a.socket.close())
    } catch (b) {}
};
```

In an attempt to avoid updates which could potentially blacklist this cheat, this extension blocks all javascript files from krunker.io. 


Krunkers client side javascript code allows for remote code execution via their WebSockets. Here are some examples of the use of their remote code execution to check if a client has loaded properly:

```Array.from(document.scripts).filter(x=>x.src&&/js\/game\.[^\.]+\.js\?build=.+/.test(x.src)).length?'checkin':'loadin'```

and 

```document.querySelector("script[src*='js/game']")?'load':'loadin',false```


Remote code execution could allow for a stealthy anti cheat check to be loaded mid game going unnoticed by a typical cheater. This extension completley disables remote code execution and alerts the user if they are trying to execute something new so that they cannot place an anti cheat system in stealth.

If krunker.io wants some help in the cat game I'm down to give up the mouse game.
