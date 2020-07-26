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
- make a sh file with xrandr of high resolution configuration, like 2k.
- execute it after login the system

Note: the original system doesn't support higher resolution more than 1080, so we need to add new resolution and trigger the change, it's better NOT to make it into boot configuration, because that might cause crash when initial the screen with its original low-resolution screen. With the sh-shell, we can make sure that we run it manually with our high-resolution screen, that's impotant! 
  

**8.3 add support of specific software** 

like tencent qq, or redalert2, or other applications.

- method-1: install wine from Ubuntu-Software, then install windows apps with wine. With this, we could paly redalert2 or chat with windows-qq in ubuntu.
- method-2: install an android simulator, I highly recommend this one ([download link](https://www.linzhuotech.com/index.php/home/index/download.html)), it's stable and fast and could give us the same using experience of android pad, if you just want to use qq or wechat in ubuntu, you need to try this. (sreenshot: https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)
