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

- add extra language in the system
- install Sogou pinyin

**8.2 change screen resolution** 

- connect high-resolution (second) screen 
- make a sh file with xrandr of high resolution configuration, like 2k.
- execute it after login the system

Note: the original system doesn't support higher resolution more than 1080, so we need to add new resolution and trigger the change, it's better NOT to make it into boot configuration, because that may be cause crash when initial the screen with its original low-resolution screen.
  

**8.3 add support of specific software** 

like tencent qq, or redalert2, or other applications.

- method-1: install wine from Ubuntu-Software, then install windows apps with wine. With this, we could paly redalert2 or chat with windows-qq in ubuntu.
- method-2: install an android simulator, I highly recommend this one ([download link](https://www.linzhuotech.com/index.php/home/index/download.html)), it's stable and fast and could give us the same using experience of android pad, if you just want to use qq or wechat in ubuntu, you need to try this. (sreenshot: https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)

