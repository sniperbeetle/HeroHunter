# KrunkerMultihack
http://krunker.io v1.4.7

## Features
- [x] Aimbot (hold right mouse button)
- [x] Snaplines esp & name esp
- [x] No visual recoil
- [x] No quick scope delay -> gives quick scope points but is not accurate as scoping at the start since it is server sided
- [x] No weapon swap delay
- [x] Perfect bunnyhop / slidejump (hold mouse button 5)
- [x] Anti cheat measures
- [x] Every day is sunny
- [x] Auto reload
- [x] Recoil control ~ new
- [x] Visibility check
- [x] Auto shoot & scope
- [ ] Aimbot prediction
- [ ] Menu
- [ ] Configurable keybindings
- [ ] Box esp

Gameplay: https://youtu.be/R6LBPZxtf3A
[![Alt text](https://github.com/hrt/KrunkerMultihack/blob/master/screenshot.png?raw=true)](https://www.youtube.com/watch?v=Fvmn3Obuelo)


Came across the game this morning and quit it this evening: 


Load this extension on chrome and you're good to go.

# How does it work
The game loads a file generally called ```game.js```. We abuse the powers of the local user to use our altered version of ```game.js``` which patches certain functions. For example we can have name esp (see players through walls) by removing a simple check during a loop to render player information:

```if (!tmpObj.inView) continue;```

# Anti cheat
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

In an attempt to avoid updates which could potentially blacklist this cheat, this extension blocks all javascript files from krunker.io. Obviously this is also trivial to bypass: for example, they could be running javascript remotely since things like ```Array.from(document.scripts).filter(x=>x.src&&/js\/game\.[^\.]+\.js\?build=.+/.test(x.src)).length?'checkin':'loadin'``` are sent to the client through websockets - not necessarily for anti cheating.
