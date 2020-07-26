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

Note: After reboot, System now could be displayed by Chinese.  If you get the message about 'change public folder names' like Downloads, Pictures, Videos, then I suggest that let the system keep the old/English name, cause Chinese characters could be hard to use in terminal or code. 

2. install SogouPinyin

Note:  Download the package from Browser, [Linux_64-bit.deb.](https://pinyin.sogou.com/linux/?r=pinyin) Then, just click the deb file and click 'install'. If you use an old Ubuntu version, just follow [this page](https://pinyin.sogou.com/linux/help.php). After that, you also need to reboot the system.
 
3. install fcitx and change the input source to SogouPinyin

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
 Now we finished all stuff. The default change-key is the single click of 'Shift'.
```

Note: the above three parts are not the same thing, please set them one by one. And always remember to reboot the system or you maybe can't see the additions.

With Chinese support, we can then set more slight changes with Tweaks (screenshot: http://i.imgur.com/l5sLZwZ.png).


**8.2 change screen resolution** 

- connect high-resolution (second) screen 
- make a command set with xrandr of high-resolution configuration, like 2k. There are 3 commands we can put them in \*.sh file,  the 3rd line is to use xrandr to set primary monitor and turn off the laptop's screen. 

```
Firstly, we need to get some specific parameters.

$ cvt 2560 1440
//the output here is what we used in xrandr below
$ xrandr -q
//check display monitors, we need to make sure the ID of the primary and second screen, here are eDP-1-1(primary) and HDMI-1-2(second). 

(just 3 lines)：

xrandr --newmode "2560x1440_55.00"  284.00  2560 2744 3016 3472  1440 1443 1448 1489 -hsync +vsync
xrandr --addmode HDMI-1-2 "2560x1440_55.00"
xrandr --output HDMI-1-2 --mode "2560x1440_55.00" --output eDP-1-1 --off
```

- finally, just find a way to execute the 3 commands, you can run them with 'sh \*.sh' or let them executed automatically after we login system.

```
quick way :
    -> just put these 3 lines into the end of /etc/profile,
    -> then, reboot, you could find the monitor was switched by itself.
```

Note: the original system doesn't support higher resolution more than 1080, so we need to add new resolution and trigger the change.
  

**8.3 add support of specific software** 

like tencent qq, or redalert2, or other applications.

- method-1: install wine from Ubuntu-Software, then install windows apps with wine. With this, we could paly redalert2 or chat with windows-qq in ubuntu.
- method-2: install an android simulator, I highly recommend this one ([download link](https://www.linzhuotech.com/index.php/home/index/download.html)), it's stable and fast and could give us the same using-experience of the android pad, if you just want to use qq or wechat in ubuntu, you need to try this. (screenshot: https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)

**8.4 some unessential changes with Tweaks**

theme ->  Adwaita-dark

cursor -> Adwaita-default

```
The default font setting is :
    Ubuntu/11, Ubuntu Regular/11, Sans Regular/11, Ubuntu Mono Regular/13
    the extra options are the third selection and first selection, and the zoom ratio is 1.0
then I set 1-3 font family to Ubuntu Medium and 4 to Ubuntu Mono Bold with zoom ratio 1.3
```

**8.5 other useful tools and settings**

- **brightness control**

I use RedShift here, other similar software like F.lux is good as well. Using RedShift is simple:

```
-> install it with `sudo apt-get install redshift-gtk`, gtk means visual version.
-> open location service: Settings -> Privacy -> Location service -> open. (this step is ESSENTIAL)
-> open redshift, if you can't find the icon, just search it in 'applications'.
-> then, brightness will be changed
-> finally, with its menu, you can set it open with your system.
```
 
 - **vscode preferances**
 
 @theme
 
 File -> Preferences -> Color Theme, I'd like to use `Tomorrow Night Blue`, which is also a kind of dark theme but could also work well in the day time.
 
 @font
 
 File -> Preferences -> Settings, then we use 'search' (search 'font') to locate the items that we need to change, I'd like to set these parameters by JSON format, and the programming stuff settings are as below:
 
 ```
{
    "terminal.integrated.fontFamily": "monospace",
    "editor.fontWeight": "600",
    "editor.fontFamily": "monospace",
    "editor.fontSize": 15.5,
    "terminal.integrated.fontSize": 12,
    "workbench.colorTheme": "Tomorrow Night Blue"
}
I like this combination, it worked very well in my 2k screen.
```

If you want to make the font same with vscode in Windows (specifically, it's Consolas), then you need to install new fonts manually, you can't use new fonts if you don't install them at first.

```
$ wget https://down.gloriousdays.pw/Fonts/Consolas.zip
$ unzip Consolas.zip
$ sudo mkdir -p /usr/share/fonts/consolas
$ sudo cp consola*.ttf /usr/share/fonts/consolas/
$ sudo chmod 644 /usr/share/fonts/consolas/consola*.ttf
$ cd /usr/share/fonts/consolas
$ sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv
//check the installed fonts
$ fc-list  
```

@terminal's location

Just search 'location' in settings and change `Workbench › Panel: Default Location` from bottom to left, because I want to have more vertical space to read long codes while we usually don't write long sentences/codes in lines, so it has more free horizontal space that we can settle the terminal. 

 @files display order in Explorer (left area)
 
Just search 'explorer.sortOrder' in settings and set it sorted by 'type', it's useful for some make/cmake projects, which has a lot of \*.cpp or \*.o files, they're mixed in the default setting, but it should be sorted by type so that we can have a clear group of different files.
 
The final view of vscode in my Ubuntu like this: (screenshot: http://i.imgur.com/g7OehEL.png)
 
