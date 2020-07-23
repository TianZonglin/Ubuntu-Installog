## Full steps of Ubuntu installation (with GL stuff)

### laptop info

- MSI GE62 490, with a Nvidia Gefore 960M graphics card
- core is intel i7-6700HQ with inside graphics card
- single system (ubuntu)

### install system

1. **prepare a usb installer (with another computer).** Note: official iso ([ubuntu-18.04.4-desktop-amd64.iso](https://releases.ubuntu.com/18.04/ubuntu-18.04.4-desktop-amd64.iso))
2. **turn off the secure boot in BIOS**
3. **follow and finish the standard installation process.** Note: do NOT set grub (eg. nomodeset) if you can install smoothly. After setting ubuntu's configration, you can log into the new Ubuntu system (now, with the core graphics card and drivers)
4. **agree the 1st time update require.** Note: when you first get into the Ubunutu, you may get a update information, DO agree that, the principle is that we agree all updates during the process of installation, but after we get a stable and complete system, then we stop update anything, try to keep the system having no change, if not, there might be some conflict between the new updates and the old drivers. 
5. **reboot**

### install nvidia dirver
 
1. **add repository then we can check devices**

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
$ sudo ubuntu-drivers devices
note： we get the recommendation version here！
```

2. **install drivers in APP** (Software and Updates)

```
Software and Updates ->
    additional drivers ->
        select the recommandation version ->
            apply
```

3. **do NOT set blacklist of nouveau or set grub.** Note: all stuff could be handled automatically by system if we use this way to install the drivers, we do nothing then it would be worked very well with nvidia drivers!


Now, the installation of Nvidia driver was finished. You can use `nvidia-smi` to test if it's ok (sreenshot:http://i.imgur.com/GgfSqCM.png) or just check the system information and see the dirvers name. (sreenshot:http://i.imgur.com/Euj6tQy.png)
 
### install cuda-toolkit

1. **select cuda-10_\* or other version** (here I selet 10.0)
 (sreenshot:http://i.imgur.com/6xPtxju.png)

2. **execute**

```
$ sudo chmod 777 cuda-10_\*.run
$ sudo sh cuda-10_\*.run
```

3. **during this process.** Note: we have installed the driver by ourselves, so here say no. 

```
Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 410.48?
(y)es/(n)o/(q)uit: n
```

4. **test samples**
 
```
$ cd /usr/local/cuda/samples
$ make
  (10 minutes later)
$ cd /usr/local/cuda/samples/bin/x86_64/linux/release
$ ./deviceQuery
```

(sreenshot:http://i.imgur.com/jJ7vpNw.png)
 
5. **extra IMPORTANT config.** Note: add two environment params into /etc/profile, if not, maybe you could get the error says: libcudart.so.10.0: cannot open shared object file: No such file or directory

```
export PATH=/usr/local/cuda/bin:$PATH 
export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/cuda/lib64/
```
 
Now cuda installation is finished, actually with samples' test, we can also make sure that the GPU driver worked well.

### install GL stuff

1. **for GL/gl.h use:**

```
sudo apt install mesa-common-dev
```

2. **GL/glu.h:**

```
sudo apt install libglu1-mesa-dev freeglut3-dev
```

3. **others: **

```
libglfw3-dev libgles2-mesa-dev libglew-dev 
```

4. **just use all-in-one command.** Note: they are all necessary to install, and maybe you need to install more libs, it's up to your code.

```
$ sudo apt install mesa-common-dev freeglut3-dev libglfw3-dev libgles2-mesa-dev libglew-dev 
```

### install project stuff

1. **base tools**

```
$ sudo apt install vim
$ sudo apt install cmake
```

2. **rebuild project**

```
$ cd ProjectionExplain/LIBRARY/glui-master
$ rm CMakeCache.txt
$ make clean
$ mkdir build
$ cmake ..
$ make install
$ cd ProjectionExplain/
$ make clean
$ make 
$ ./projwiz -f DATA/segmentation lamp
```

All stuff about GL-project has been done!
 (sreenshot:http://i.imgur.com/rDCtEId.png)

### install personal softwares

- **screenshot: flameshot**

```
use `sudo apt-get install flameshot`
set the shortcut
 (sreenshot:http://i.imgur.com/id2PPYj.png)
```

- **vscode**

```
install it directly in APP (Ubuntu Software).
 (sreenshot:http://i.imgur.com/W971ERc.png)

then, we can program code with vsc
  - open folder (ProjectionExplain)
  - Terminal->new terminal->make && ./projwiz -f DATA/segmentation lamp
```

### change theme with Tweaks

1. **install tweaks and its extensions**

```
$ sudo apt install gnome-shell-extensions gnome-shell-extension-dash-to-panel gnome-tweaks adwaita-icon-theme-full
```

2. **logout and login system or reboot**
3. **change panel style.** (extensions: dash to panel) Note: with right-click, you can wake the panel-setting window, and some slight changes could be made in here.
 (sreenshot:http://i.imgur.com/OKrQ67r.png)
4. **change menu style.** (extension: applications menu) Note: turn on this extension could display the app manager like windows starting menu. Here I just changed the applications margin and hide the applications icon and show desktop's button (like windows).
5. **change the wallpaper.**

Till now, the basic theme setting has been finished, and the style now is very similar with my windows desktop. 




### Ubuntu Using Tips

- **updates.** just delay the update checking (I don't know how to stop it)! do NOT cancel the 'update from', unless you would get errors when you install new packages/tools/...
 (sreenshot:http://i.imgur.com/w7Kvc7X.png)

- **when desktop crash.** like stucking when turn off some windows or stucking after running something for a long time. When this happened, do NOT shutdown the system by cut down the power! that's a dangerous behavior, system core maybe ruined by this.
the right way is: Ctrl+Alt+F2/3/4, log into the tty2/3/4, then restart gdm/lightdm, or rollback the wrong options here if you remember. Or do nothing, just wait the system rerun again, sometimes it could be reworked after waiting a while.












