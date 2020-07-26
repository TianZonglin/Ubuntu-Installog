### 7. change the theme with Tweaks

**7.1 install tweaks and its extensions**

```
$ sudo apt install gnome-shell-extensions gnome-shell-extension-dash-to-panel gnome-tweaks adwaita-icon-theme-full
```

**7.2 logout and login system or reboot**

**7.3 change panel style.** 

(extensions: dash to panel) Note: with right-click, you can wake the panel-setting window, and some slight changes could be made in here.
 (sreenshot:http://i.imgur.com/OKrQ67r.png)
 
**7.4 change menu style.** 

(extension: applications menu) Note: turn on this extension could display the app manager like windows starting menu. Here I just changed the margin of the application and hide the application's icon and show the desktop's button (like windows).

**7.5 change the wallpaper.**

Till now, the basic theme set has been finished, and the style now is very similar to my windows desktop. 

### 8. unimportant changes
 
**8.1 add support of Chinese** 

1. add extra language in the system

```
Go to Settings 
-> Region & Languages
    -> manage installed language
        -> if get the message of 'installed not complete' then just install
            -> click 'Install/Remove Languages' 
                -> choose Chinese then install (maybe need double-click)
            -> then in 'Language for menu and windows' 
                -> drag Chinese up to the 1st position
-> now in 'Region & Language', the Language has been changed to Chinese automatically.   
```

Note: After reboot, System now could be displayed by Chinese.  If you get the message about 'change public folder names' like Douwloads, Pictures, Videos, then I suggest  that let the system keep the old/English name, cause chinese characters could be hard to use in terminal or code. 

2. install SogouPinyin

Note:  Download the package from Browser, [Linux_64-bit.deb.](https://pinyin.sogou.com/linux/?r=pinyin) Then, just  click the deb file and click 'install'. If you use a old Ubuntu version, just follow [this page](https://pinyin.sogou.com/linux/help.php). After that, you also need to reboot the system.
 
3. install fcitx and change input source to SogouPinyin

```
$ sudo apt install fcitx
then, go to Settings
    -> manage  installed language
        -> change the  'Input System'(default is IBus) to fictx
        -> then click  'apply system-wild'
-> Now , you'd better to reboot, then
    -> find 'keybord icon' in the task bar (default location is top-right corner)
        -> click 'configure current input method'
            -> then you could see SogouPinyin has been there. 
                 We can delete that 'Wubi' so that we just keep English and Pinyin for us.
 Now  we finished all stuff. The default change-key is single click of 'Shift'.
```

Note: the above three parts are not the same thing, please set them one by one. And always remember to reboot system or you maybe can't see the additions.

With Chinese support, we can then setting more slight changes with Tweaks (sreenshot: http://i.imgur.com/l5sLZwZ.png).


**8.2 change screen resolution** 

- connect high-resolution (second) screen 
- make a command set with xrandr of high resolution configuration, like 2k. There are 3 commands we can put them in \*.sh file,  the 3rd line is to use xrandr to set primary monitor and turn off the laptop's screen. 

```
Firstly, we need to get some specific parameters.

$ cvt 2560 1440
//the output here is what we used in xrandr below
$ xrandr -q
//check display monitors, we need to make sure the ID of primary and second screen, here are eDP-1-1(primary) and HDMI-1-2(second). 

(just 3 lines)：

xrandr --newmode "2560x1440_55.00"  284.00  2560 2744 3016 3472  1440 1443 1448 1489 -hsync +vsync
xrandr --addmode HDMI-1-2 "2560x1440_55.00"
xrandr --output HDMI-1-2 --mode "2560x1440_55.00" --output eDP-1-1 --off
```

- finally, just find a way to execute the 3 commands, you can run them with 'sh \*.sh' or let them executed automatically after we login system.

```
quick way :
    -> just put these 3 lines into the end of /etc/profile,
    -> then, reboot, you could find the moniter was switched by itself.
```

Note: the original system doesn't support higher resolution more than 1080, so we need to add new resolution and trigger the change.
  

**8.3 add support of specific software** 

like tencent qq, or redalert2, or other applications.

- method-1: install wine from Ubuntu-Software, then install windows apps with wine. With this, we could paly redalert2 or chat with windows-qq in ubuntu.
- method-2: install an android simulator, I highly recommend this one ([download link](https://www.linzhuotech.com/index.php/home/index/download.html)), it's stable and fast and could give us the same using experience of android pad, if you just want to use qq or wechat in ubuntu, you need to try this. (sreenshot: https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)

**8.4 some unessential changes with Tweaks**

theme ->  Adwaita-dark

cursor -> Adwaita-default

```
The default font setting is :
    Ubuntu/11, Ubuntu Regular/11, Sans Regular/11, Ubuntu Mono Regular/13
    the left options is the third opts and first opts, and zoom ratio is 1.0
then I set 1-3 font family to Ubuntu Medium and 4 to Ubuntu Mono Bold with zoom ratio 1.3
```

**8.5 other useful tools or softwares**

- brightness control

I use RedShift here, other similar softwares like F.lux is good as well. Using RedShift is simple:

```
-> install it with `sudo apt-get install redshift-gtk`, gtk means visual version.
-> open location service: Settings -> Privacy -> Location service -> open. (this step is ESSENTIAL)
-> open redshift, if you can't find the icon, just search it in 'applications'.
-> then, brightness will changed
-> fianlly, with its menu, you can set it open with your system.
```
