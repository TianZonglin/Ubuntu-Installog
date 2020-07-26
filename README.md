![](https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/fjdsuiohoviwe23424.png)

## Full steps of Ubuntu installation (with GL stuff)

This doc includes two parts of [Installations](https://github.com/TianZonglin/Ubuntu-Installog/blob/master/Installations.md) and [PersonalSettings](https://github.com/TianZonglin/Ubuntu-Installog/blob/master/PersonalSettings.md).

### 0. laptop info

- MSI GE62 490, with an Nvidia GeForce 960M graphics card
- the core is intel i7-6700HQ with an inside graphics card
- single system (ubuntu)

### 1. install the system

**1.1 prepare a USB installer (with another computer).** 

Note: official iso ([ubuntu-18.04.4-desktop-amd64.iso](https://releases.ubuntu.com/18.04/ubuntu-18.04.4-desktop-amd64.iso))

**1.2 turn off the secure boot in BIOS**

**1.3 follow and finish the standard installation process.** 

Note: do NOT set grub (eg. nomodeset) if you can install smoothly. After setting ubuntu's configuration, you can log into the new Ubuntu system (now, with the core graphics card and drivers)

**1.4 agree the 1st time update require.** 

Note: when you first get into the Ubunutu, you may get a piece of update information, DO agree that, the principle is that we agree with all updates during the process of installation, but after we get a stable and complete system, then we stop update anything, try to keep the system having no change, if not, there might be some conflict between the new updates and the old drivers. 

**1.5 reboot**

### 2. install nvidia dirver
 
**2.1 add repository then we can check devices.** 

Note：we get the recommendation version here！

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
$ sudo ubuntu-drivers devices
```

**2.2 install drivers in APP** (Software and Updates)

```
Software and Updates ->
    additional drivers ->
        select the recommandation version ->
            apply
```

**2.3 do NOT set blacklist of nouveau or set grub.** 

Note: all stuff could be handled automatically by system if we use this way to install the drivers, we do nothing then it would be worked very well with Nvidia drivers!

Now, the installation of the Nvidia driver was finished. You can use `nvidia-smi` to test if it's ok (sreenshot:http://i.imgur.com/GgfSqCM.png) or just check the system information and see the drivers name. (sreenshot:http://i.imgur.com/Euj6tQy.png)
 
### 3. install cuda-toolkit

**3.1 select cuda-10_\* or another version** (here I select 10.0)

(sreenshot:http://i.imgur.com/6xPtxju.png)

**3.2 execute**

```
$ sudo chmod 777 cuda-10_\*.run
$ sudo sh cuda-10_\*.run
```

**3.3 during this process.** Note: we have installed the driver by ourselves, so here say no. 

```
Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 410.48?
(y)es/(n)o/(q)uit: n
```

**3.4 test samples**
 
```
$ cd /usr/local/cuda/samples
$ make
  (10 minutes later)
$ cd /usr/local/cuda/samples/bin/x86_64/linux/release
$ ./deviceQuery
```

(sreenshot:http://i.imgur.com/jJ7vpNw.png)
 
**3.5 extra IMPORTANT config.** 

Note: add two environment params into /etc/profile, if not, maybe you could get the error says: libcudart.so.10.0: cannot open shared object file: No such file or directory

```
export PATH=/usr/local/cuda/bin:$PATH 
export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/cuda/lib64/
```
 
Now cuda installation is finished, actually, with samples' test, we can also make sure that the GPU driver worked well.

### 4. install GL stuff

**4.1 for GL/gl.h use:**

```
sudo apt install mesa-common-dev
```

**4.2 GL/glu.h:**

```
sudo apt install libglu1-mesa-dev freeglut3-dev
```

**4.3 others:**

```
libglfw3-dev libgles2-mesa-dev libglew-dev 
```

**4.4 just use all-in-one command.** Note: they are all necessary to install, and maybe you need to install more libs, it's up to your code.

```
$ sudo apt install mesa-common-dev freeglut3-dev libglfw3-dev libgles2-mesa-dev libglew-dev 
```

### 5. install project stuff

**5.1 base tools**

```
$ sudo apt install vim
$ sudo apt install cmake
```

**5.2 rebuild project**

```
$ cd ProjectionExplain/LIBRARY/glui-master
$ rm CMakeCache.txt
$ make clean
$ mkdir build && cd build
$ cmake ..
$ make install
$ cd ProjectionExplain/
$ make clean
$ make 
$ ./projwiz -f DATA/segmentation lamp
```

All stuff about GL-project has been done!
 (sreenshot:http://i.imgur.com/rDCtEId.png)

### 6. install personal software

**6.1 screenshot: flameshot**

use `sudo apt-get install flameshot`

set the shortcut
 (sreenshot:http://i.imgur.com/id2PPYj.png)

**6.2 vscode**

install it directly in APP (Ubuntu Software).
 (sreenshot:http://i.imgur.com/W971ERc.png)

then, we can program code with vsc
  - open folder (ProjectionExplain)
  - Terminal->new terminal->make && ./projwiz -f DATA/segmentation lamp

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

Note: After reboot, System now could be displayed by Chinese.  If you get the message about 'change public folder names' like Douwloads, Pictures, Videos, then I suggest  that let the system keep the old/English name, cause chinese characters could be hard to use in terminal or code. (sreenshot: http://i.imgur.com/l5sLZwZ.png)

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


**8.2 change screen resolution** 

- connect high-resolution (second) screen 
- make a sh file with xrandr of high resolution configuration, like 2k.
- execute it after login the system

Note: the original system doesn't support higher resolution more than 1080, so we need to add new resolution and trigger the change, it's better NOT to make it into boot configuration, because that might cause crash when initial the screen with its original low-resolution screen. With the sh-shell, we can make sure that we run it manually with our high-resolution screen, that's impotant! 
  

**8.3 add support of specific software** 

like tencent qq, or redalert2, or other applications.

- method-1: install wine from Ubuntu-Software, then install windows apps with wine. With this, we could paly redalert2 or chat with windows-qq in ubuntu.
- method-2: install an android simulator, I highly recommend this one ([download link](https://www.linzhuotech.com/index.php/home/index/download.html)), it's stable and fast and could give us the same using experience of android pad, if you just want to use qq or wechat in ubuntu, you need to try this. (sreenshot: https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)




  
### X. Ubuntu Using Tips

**X.1 updates.** 

just delay the update checking (I don't know how to stop it)! do NOT cancel the 'update from', or you would get errors when you install new packages/tools/...
 (sreenshot:http://i.imgur.com/w7Kvc7X.png)

**X.2 when desktop crash.** 

like stucking when turning off some windows or stucking after running something for a long time. When this happened, do NOT shut down the system by cut down the power! that's a dangerous behavior, system core may be ruined by this.

the right way is: Ctrl+Alt+F2/3/4, log into the tty2/3/4, then restart gdm/lightdm, or rollback the wrong options here if you remember. Or do nothing, just wait for the system rerun again, sometimes it could be reworked after waiting a while.


[**中 文 版 本**](https://www.cz5h.com/article/483a.html) 












