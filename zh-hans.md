![](https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/2020-07-28-22-24-15.png)



**[English Version](https://github.com/TianZonglin/Ubuntu-Installog/blob/master/README.md)**

## Ubuntu及GL环境安装手册 

这是一份完整的Ubuntu安装手册，可以帮助你快速初始化系统到可用状态，此手册包含两部分，包括Ubuntu系统的安装及配置、及GL相关开发环境的初始化。为了使行文更加清晰，文中插图全部以链接形式呈现，该手册仍然在完善中并已开源在Github。

<!-- TOC -->
additions:

sudo apt-get install redshift redshift-gtk


- [0. 机器信息](#0-机器信息)
- [1. 安装系统](#1-安装系统)
    - [1.1 准备USB启动盘](#11-准备usb启动盘)
    - [1.2 在BIOS中关闭 Secure Boot](#12-在bios中关闭-secure-boot)
    - [1.3 按正常步骤安装完系统](#13-按正常步骤安装完系统)
    - [1.4 第一次进入桌面后更新系统，然后重启](#14-第一次进入桌面后更新系统然后重启)
- [2. 安装英伟达驱动](#2-安装英伟达驱动)
    - [2.1 添加软件源并查看](#21-添加软件源并查看)
    - [2.2 通过软件和更新直接安装](#22-通过软件和更新直接安装)
    - [2.3 不要设置 nouveau 黑名单或者设置 grub 启动项](#23-不要设置-nouveau-黑名单或者设置-grub-启动项)
- [3. 安装 cuda-toolkit](#3-安装-cuda-toolkit)
    - [3.1 选择版本，这里我用的 cuda-10_\*.run](#31-选择版本这里我用的-cuda-10_\run)
    - [3.2 执行](#32-执行)
    - [3.3 跳过显卡安装](#33-跳过显卡安装)
    - [3.4 测试 Samples](#34-测试-samples)
    - [3.5 其他重要的配置](#35-其他重要的配置)
- [4. 安装 GL 相关环境、库](#4-安装-gl-相关环境库)
    - [4.1 GL/gl.h](#41-glglh)
    - [4.2 GL/glu.h](#42-glgluh)
    - [4.3 others](#43-others)
    - [4.4 以上直接一次性安装](#44-以上直接一次性安装)
- [5. 安装项目所需软件并重构](#5-安装项目所需软件并重构)
    - [5.1 基础工具](#51-基础工具)
    - [5.2 重新构建](#52-重新构建)
- [6. 安装日程必备软件](#6-安装日程必备软件)
    - [6.1 截屏工具： flameshot](#61-截屏工具-flameshot)
    - [6.2 开发工具：vscode](#62-开发工具vscode)
- [7. 使用 Tweaks 修改主题](#7-使用-tweaks-修改主题)
    - [7.1 安装 Tweaks 及其扩展 extensions](#71-安装-tweaks-及其扩展-extensions)
    - [7.2 更改顶部菜单栏样式](#72-更改顶部菜单栏样式)
    - [7.3 修改壁纸](#73-修改壁纸)
    - [7.4 修改面板到底部，并把图标放到桌面](#74-修改面板到底部并把图标放到桌面)
- [8. 不重要的配置](#8-不重要的配置)
    - [8.1 添加中文支持](#81-添加中文支持)
    - [8.2 更改副屏分辨率](#82-更改副屏分辨率)
    - [8.3 添加一些未适配的应用](#83-添加一些未适配的应用)
    - [8.4 Tweaks的一些不重要的美化设置](#84-tweaks的一些不重要的美化设置)
    - [8.5 其他实用的配置及软件](#85-其他实用的配置及软件)
        - [8.5.1 屏幕亮度控制](#851-屏幕亮度控制)
        - [8.5.2 Vscode配置](#852-vscode配置)

<!-- /TOC -->

### 0. 机器信息

- MSI GE62 490, 显卡英伟达960M（笔记本）
- CPU: intel i7-6700HQ，带核显
- 单系统安装（ubuntu-18.04-LTS）

### **1. 安装系统**

#### **1.1 准备USB启动盘**

注意：本文使用的官方镜像为 [ubuntu-18.04.4-desktop-amd64.iso](https://releases.ubuntu.com/18.04/ubuntu-18.04.4-desktop-amd64.iso)。

#### **1.2 在BIOS中关闭 Secure Boot**

#### **1.3 按正常步骤安装完系统**

注意：如果你可以正常走完安装流程进入桌面，那就**不需要**修改 grub 的任何信息（例如nomodeset）。正常情况下，安装完后拔出USB启动盘，应该可以顺利进入桌面（此时系统运行在核显驱动下）。
 
#### **1.4 第一次进入桌面后更新系统，然后重启**

注意：当你第一次进入Ubuntu桌面时，可能会弹出系统及软件的更新，请同意更新，否则会影响后续操作。不过，当我们在安装完全部所需环境、软件之后，就不再需要更新了，尤其是尽量**不进行**系统级的更新，否则我们稍后安装的显卡驱动可能会因此出现异常。
 
### **2. 安装英伟达驱动**
 
#### **2.1 添加软件源并查看**

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
$ sudo ubuntu-drivers devices
```

注意：这里会输出你的机器适配的显卡驱动，并且会有一个 recommend 推荐项，我们稍后就安装这个推荐版本。

#### **2.2 通过软件和更新直接安装**

```
Software and Updates ->
    additional drivers ->
        select the recommandation version ->
            apply
```

注意：安装显卡驱动的方式有很多，较新版本的Ubuntu完全可以在“软件和更新”中直接进行显卡驱动的安装。无需下载安装文件，无需通过命令安装。

#### **2.3 不要设置 nouveau 黑名单或者设置 grub 启动项**

注意：使用此种方式安装显卡驱动，配置完全由系统完成，我们不用做任何设置。在‘软件与更新’内完成显卡安装后，重启系统。

重启后进入桌面（此时正常情况下是会顺利启动的），此时用 `nvidia-smi` 可以测试显卡信息，截图：[http://i.imgur.com/GgfSqCM.png](http://i.imgur.com/GgfSqCM.png)，此外还可以直接通过系统信息来查看是否已加载英伟达显卡，截图：[http://i.imgur.com/Euj6tQy.png](http://i.imgur.com/Euj6tQy.png)。


### **3. 安装 cuda-toolkit**

**（第3、4、5节和我自己的开发需求有关，一般使用可以跳过这几节！）**

#### **3.1 选择版本，这里我用的 cuda-10_\*.run** 

（截图： [http://i.imgur.com/6xPtxju.png](http://i.imgur.com/6xPtxju.png)）

#### **3.2 执行**

```
$ sudo chmod 777 cuda-10_\*.run
$ sudo sh cuda-10_\*.run
```

#### **3.3 跳过显卡安装**

注意：我们在前面已经安装过显卡了，这里务必要回答 NO。

```
Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 410.48?
(y)es/(n)o/(q)uit: n
```

#### **3.4 测试 Samples**
 
```
$ cd /usr/local/cuda/samples
$ make
  (10 minutes later)
$ cd /usr/local/cuda/samples/bin/x86_64/linux/release
$ ./deviceQuery
```

（截图： [http://i.imgur.com/jJ7vpNw.png](http://i.imgur.com/jJ7vpNw.png)）
 
#### **3.5 其他重要的配置**

注意：别忘了添加环境变量到 `/etc/profile`，如果不添加的话，后面使用Cuda会出现 `libcudart.so.10.0: cannot open shared object file: No such file or directory` 这种错误。

```
export PATH=/usr/local/cuda/bin:$PATH 
export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/cuda/lib64/
```

到此为止，英伟达显卡驱动和Cuda已经全部安装完毕。并且也通过测试来确保了安装的正确。

### **4. 安装 GL 相关环境、库**

**（第3、4、5节和我自己的开发需求有关，一般使用可以跳过这几节！）**

#### **4.1 GL/gl.h**

```
sudo apt install mesa-common-dev
```

#### **4.2 GL/glu.h**

```
sudo apt install libglu1-mesa-dev freeglut3-dev
```

#### **4.3 others**

```
libglfw3-dev libgles2-mesa-dev libglew-dev libeigen3-dev
```

#### **4.4 以上直接一次性安装**

注意：这些库对我都是必须的，但这是取决于项目需求。
 
```
$ sudo apt install mesa-common-dev freeglut3-dev libglfw3-dev libgles2-mesa-dev libglew-dev libeigen3-dev
```

### **5. 安装项目所需软件并重构**

**（第3、4、5节和我自己的开发需求有关，一般使用可以跳过这几节！）**

#### **5.1 基础工具**

```
$ sudo apt install vim
$ sudo apt install cmake
```

#### **5.2 重新构建**

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

此时项目已经构建完毕并可以成功运行！
 （截图： [http://i.imgur.com/rDCtEId.png](http://i.imgur.com/rDCtEId.png)）

### **6. 安装日程必备软件**

#### **6.1 截屏工具： flameshot**

使用 `sudo apt-get install flameshot` 完成安装，并如截图所示进行配置（截图： [http://i.imgur.com/id2PPYj.png](http://i.imgur.com/id2PPYj.png)）。

#### **6.2 开发工具：vscode**

**..更多相关配置在 8.5 小节..**

直接在 Ubuntu 的‘软件与更新’内安装Vscode（截图： [http://i.imgur.com/W971ERc.png](http://i.imgur.com/W971ERc.png)）。

然后，对于 Cmake 项目，Vscode更多的充当编辑器的作用，搭配 terminal 进行构建即可。以前文项目为例：
  - 在Vscode中打开项目文件夹 (ProjectionExplain)
  - 在Vscode中打开终端，Terminal->new terminal
  - 在Vscode代码区编辑代码，在终端内构建->make && ./projwiz -f DATA/segmentation lamp



### **7. 使用 Tweaks 修改主题**

#### **7.1 安装 Tweaks 及其扩展 extensions**

```
$ sudo apt install gnome-shell-extensions gnome-shell-extension-dash-to-panel gnome-tweaks adwaita-icon-theme-full
```

在这之后需要注销或者重启生效。
 
#### **7.2 更改顶部菜单栏样式**

扩展名称：applications menu。 
注意：开启此扩展可以使应用菜单栏变得和Windows风格一致。扩展->设置内的选项都可能会被用到，可以自己探索一下。

#### **7.3 修改壁纸**

#### **7.4 修改面板到底部，并把图标放到桌面**

Ubuntu 的dock默认的风格更像是 OSX 系统，Tweaks允许我们修改其成为 Windows 风格（在底部）。另外，像Windows那样，我们把图标也放在桌面上。

首先对 dock 样式进行修改：

```
打开 Tweaks -> Extensions 
      -> 打开 'applications menu' 
      -> 打开 'Dash to panel' -> 打开设置
            -> Location and Style
                  -> panel location -> bottom
                  -> panel size -> 45px
                  -> icons margin -> 5px
                  -> indicator -> open settings
                        -> height -> 0px (we hide it by this)
                  -> clock location -> right
                  -> task panels -> left
            -> Behaviors
                  -> 关闭 'favoriate applications'
                  -> 关闭 'applications icon'
                  -> 打开 'show desktop'
                  -> 关闭 'cancel applications' group'
```

对于图标问题：

Ubuntu 默认的图标路径有好几个，下面是几个可能包含图标的路径，我们只需要将这些图标复制到桌面即可。**注意：**你会发现复制之后图标变成了 \*.desktop 文件，我们只需要双击它们，然后点击‘信任并启动’，之后它们就会变回图标的样子了。
 
```
/usr/share/applications
/var/lib/snapd/desktop/applications
~/.local/share/applications
```

至此，基础的主题修改已经完成，目前为止，你的 Ubuntu 看起来应该非常接近 Windows 了。（截图： [http://i.imgur.com/y7safc9.png](https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/2020-07-2823849238944.png)）


### **8. 不重要的配置**
 
#### **8.1 添加中文支持**

- **第一步给系统添加中文**

```
打开 Settings 
-> Region & Languages
    -> manage installed language
        -> 如果弹出 'installed not complete'，那么先完成安装
            -> 点击 'Install/Remove Languages' 
                -> 选择 Chinese 然后安装（可能需要双击）
            -> 然后在 'Language for menu and windows' 
                -> 拖拽 Chinese 到排名第一的位置
-> 现在在 'Region & Language'中，语言已经自动的变为中文了
```

注意：上述操作完并重启后，系统才会变成中文。一般会弹出一个 'change public folder names' 询问弹框，就是问你要不要修改那几个公共文件夹的名字，强烈建议不要修改，即保持默认英文名称，这对于很多 bash 操作是很有利的。

- **安装搜狗输入法**

注意：从官网下载安装包 [Linux_64-bit.deb.](https://pinyin.sogou.com/linux/?r=pinyin)，如果你用的是比较老的 Ubuntu 系统，请参照 [此页面](https://pinyin.sogou.com/linux/help.php) 进行安装。
 
- **安装 fcitx 并修改输入源为 SogouPinyin**

```
$ sudo apt install fcitx

然后打开 Settings
    -> manage installed language
        -> 修改 'Input System'(默认是IBus) 为 fcitx
        -> 然后点击 'apply system-wild'
-> 现在最好是重启一次，然后
    -> 在任务栏找到一个小键盘图标，
        -> 点击'configure current input method'
            -> 然后应该能发现搜狗输入法，还有些别的输入法
                 我们可以删掉其余的输入法，只保留搜狗输入法和英文输出
现在就完成全部输入法配置了，默认的切换键是 ‘单次Shift’
```

注意：

以上三部分是不同的，请一步步来，并且在过程中如果没发现新增项，请尝试重启系统。有了中文支持，我们可以进一步对 Tweaks 进行配置。 （截图： [http://i.imgur.com/l5sLZwZ.png](http://i.imgur.com/l5sLZwZ.png)）


#### **8.2 更改副屏分辨率**

- 连接你的副屏，我的副屏是2k屏，笔记本是1080的，所以输出分辨率最大只有1080，我们需要手动修改它；
- 新建个 sh 文件，里面包含重置分辨率的命令，这样只需要每次重启后设置自动执行，即可自动变为2k的输出。 下面需要做些准备工作来确定最后写入 sh 文件的三行命令的参数。

```
首先是得到本机指定分辨率的渲染参数

$ cvt 2560 1440
//下面的"2560x1440_55.00"就是从这里获得的
$ xrandr -q
//这里查看副屏对应的显示器编号，下面的"HDMI-1-2"就是从这来的。 

写入文件的三行：

xrandr --newmode "2560x1440_55.00"  284.00  2560 2744 3016 3472  1440 1443 1448 1489 -hsync +vsync
xrandr --addmode HDMI-1-2 "2560x1440_55.00"
xrandr --output HDMI-1-2 --mode "2560x1440_55.00" --output eDP-1-1 --off
```

- 文件写好后，你可以手动去执行，当然如前所述，使之开机自动运行是最好的。

```
quick way :
    -> 将这三行命令放入 /etc/profile 文件内的最末尾；
    -> 重启后会发现可以自动得到 2k 的分辨率。
```

注意：这样写的弊端在于，你必须保证2k副屏后再重启，如果你不用副屏了，你必须从 profile 里去掉这三行命令，否则会出错的。
  

#### **8.3 添加一些未适配的应用**

像是微信、QQ等聊天工具，或者红警等游戏，对于这些软件，默认是没有支持的，但仍然可以通过一些方法安装。

- 方法一：在‘软件与更新’中安装 Wine，然后通过 Wine 来安装 Windows 应用。
- 方法二：安装安卓模拟器，通过模拟器来使用QQ等软件，这里我推荐 [这个模拟器](https://www.linzhuotech.com/index.php/home/index/download.html)，渲染速度和稳定性都还是不错的。（截图： [img/Cache_32799f853a0e21fe..jpg](https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/Cache_32799f853a0e21fe..jpg)）
- **方法三：墙裂推荐！**这里直接下载封装了精简 Wine 环境的 QQ 软件包，即可以使用QQ，无需多余安装 Wine 也无需其他预先配置，只需要下载对应的 AppImage 文件，然后启动即可使用！

方法三步骤：（[Github地址](https://github.com/askme765cs/Wine-QQ-TIM)）

```
//首先去release下载文件

$ chmod a+x TIM-x86_64.AppImage

//通过命令直接启动
$ ./TIM-x86_64.AppImage.AppImage
```

注意，尽量选择TIM，QQ在我机器上测试发现有点问题。

如果你想通过图标点击来启动之，那么可以自己新建一个图标文件来完成，然后将此图标文件放到`~/.local/share/applications`，之后，在系统软件搜索界面你就能搜到你刚才添加的图标了（也就是个应用启动器），如果你想把它放到桌面，只需要将其复制到桌面，双击一下（选信任并启动）就行了。下面是制作 QQ 图标的步骤：

首先，获取图片（qq.png）然后创建 desktop 图标文件。

```
$ wget https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/qq.png
$ vim QQ.desktop
```

然后，复制并保存以下内容到你的图标文件中，注意修改路径。

```
[Desktop Entry]
Name=QQ
Exec=/home/tzloop/Downloads/TIM-x86_64.AppImage
Icon=/home/tzloop/Downloads/qq.png
Type=Application
StartupNotify=true
```

然后右键这个文件，在权限页面，勾选“允许作为应用执行”，最后将这个图标文件复制到指定路径。

```
$ sudo cp /home/tzloop/Downloads/QQ.desktop ~/.local/share/applications
```


#### **8.4 Tweaks的一些不重要的美化设置**

- 主题 ->  Adwaita-dark
- 指针 -> Adwaita-default

字体设置，默认的字体及大小为 `Ubuntu/11, Ubuntu Regular/11, Sans Regular/11, Ubuntu Mono Regular/13`
这里我把前三项设置为了 `Ubuntu Medium` 字号不变，然后把整体的 `zoom ratio` 设置为了 1.3.

#### **8.5 其他实用的配置及软件**

##### **8.5.1 屏幕亮度控制**

我使用 RedShift 软件来控制，相同的软件还有很多，像是 F.lux 等等也是很棒的。安装 RedShift 的步骤：

```
-> install it with `sudo apt-get install redshift-gtk`, gtk means visual version.
-> open location service: Settings -> Privacy -> Location service -> open. (this step is ESSENTIAL)
-> open redshift, if you can't find the icon, just search it in 'applications'.
-> then, brightness will be changed
-> finally, with its menu, you can set it open with your system.
```
 
##### **8.5.2 Vscode配置**
 
**@主题**
 
 `File -> Preferences -> Color Theme`，我选择暗蓝色的 `Tomorrow Night Blue` 主题。

**@字体**
 
 `File -> Preferences -> Settings`，通过`search` （搜索 `font`）来定位。我推荐直接用JSON进行编辑，编辑内容如下： 

 ```
{
    "terminal.integrated.fontFamily": "monospace",
    "editor.fontWeight": "600",
    "editor.fontFamily": "monospace",
    "editor.fontSize": 15.5,
    "terminal.integrated.fontSize": 12,
    "workbench.colorTheme": "Tomorrow Night Blue"
}

以上组合在我的2K高分屏上工作的很好，推荐使用。

```

如果你想让你的编码字体和 Windows 上的VSCode字体一致，那么你得首先安装 Windows 使用的字体，安装字体的步骤如下：

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

**@终端的位置**

在设置中搜索 `location`，找到 `Workbench › Panel: Default Location` ，将其修改为 Right，因为我想让代码区有更高的视野，同时代码也不会很长也就是不需要很大的宽度，即右侧部分可以来放置终端。

**@在左侧文件树视图内文件的排序规则**
 
在设置中搜索 `explorer.sortOrder`，并将其设置为按 `type` 排序，这对于混杂不同类型文件的项目来说很方便，相同种类的文件被放在一起。
 
最后修改完配置的Vscode截图长这样：[http://i.imgur.com/g7OehEL.png](http://i.imgur.com/g7OehEL.png)。
 
##### **8.5.3 picgo**
 
如果你希望方便的上传、分享你的截图或图片，那么一定要试试 PicGo，其在 Ubuntu 上的安装使用和之前的 TIM.AppImage 非常类似，具体如下：

```
首先获得图标 picgo.png 并创建你的图标文件

$ wget https://raw.githubusercontent.com/TianZonglin/tuchuang/master/img/opic.png
$ vim QQ.desktop

然后复制以下内容到图标文件内，改成你的路径。

[Desktop Entry]
Name=PicGO
Exec=/home/tzloop/Downloads/PicGo.AppImage
Icon=/home/tzloop/Downloads/opic.png
Type=Application
StartupNotify=true

然后右键->权限页->允许作为应用执行
最后复制到所需要的路径中
```

如果你想直接上传你剪切板内的图片，那么在Ubuntu上你还需要安装个软件，通过 `sudo apt install xclip` 直接安装即可，下面是 PicGo 配置 Github 图床的步骤：

```
repository name -> GITHUBACCOUNT/tuchuang
branch name -> master
token -> get a new one from Github (Settings -> Developer Settings -> Personal access tokens)
storage path -> img/
custom domain name -> https://cdn.jsdelivr.net/gh/GITHUBACCOUNT/tuchuang
```

 
##### **8.5.4 安装并配置 git**

- **settings**

安装非常简单，直接用 `sudo apt install git` 进行安装，然后配合 Github，接下来设置免密。注意：Github只是一种 git server，其他的诸如 gitlab 等同理。

```
$ ssh-keygen -t rsa -C "YOUREMAIL"
$ vim ~/.ssh/id_rsa.pub
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_rsa

```

然后去 Github -> Settings -> SSH and GPG keys -> New SSH key，然后把 rsa.pub 的内容拷贝到 key 这里。

```
$ git config --global user.name "YOURUSERNAME"
$ git config --global user.email "YOUREMAIL"
```

至此，我们已完成免密设置，之后我们提交代码就不用进行账号验证了。（这只是ssh方式，https需要额外的设置）
 
- **同步代码的案例（我的方法）** 

在 Github 新建一个仓库并命名为你项目名称，然后通过 `git clone git@xx.git` 将此空项目克隆到你的电脑，最后，将原项目的内容全部移动到此空文件夹内，然后执行以下语句，即可完成第一次提交。

```
git add -A
git commit -m "`date +%Y-%m-%d,%H:%m`" 
git push -u origin master -f
```

现在你的代码应该已经可以在 Github 上可见了，如果你想控制提交的部分，你还需要修改/创建 `.gitignore` 文件。

我通常将其放在 sh 文件内，并在文件内的第一行添加 `#!/bin/sh`，这样就可以通过一行命令直接运行这三行命令，当然如果你想自动地、周期性的备份你的代码，你可以用 `crontab` 来将这个 sh 设置为周期性执行，这样你就无需手动备份啦！ 

##### **8.5.5 远程桌面软件**
 
对于Ubuntu用户来说，好的远程桌面软件也是十分重要的，这里我强烈推荐 AnyDesk，这是个非常轻量。易安装的远程桌面软件，没有 Vnc 那种额外的设置，只需要下载、安装，即可使用。

使用 Anydesk 首先要去官网（[here](https://anydesk.com/zhs/downloads/linux) ）下载 ，之后安装之，安装后即可使用。
 
### **X. Ubuntu使用注意事项**

#### **X.1 对于更新**

在安装完所有驱动软件环境之后，尽量不进行系统更新，或者推迟它，不要尝试在设置中停止更新，因为我没找到，而且实际上我把软件更新给停了，给我造成好大不便，所以只需要记住关掉每次的更新弹窗即可。（不要动截图这里的东西：[http://i.imgur.com/w7Kvc7X.png](http://i.imgur.com/w7Kvc7X.png)）

#### **X.2 对于死机**

对 Ubuntu 来说，死机更多时候是桌面卡死，也就是假死，系统并没有死机，tty仍然可以进入，这时候**切记不要**断电重启，这种硬重启会给内核带来不明影响，说不定这样之后你系统就启动不了啦！

正确的方法是：`Ctrl+Alt+F2/3/4`，进入 `tty2/3/4`，然后 `restart gdm/lightdm`，或者你如果记得你先前的错误操作，那么在此处回滚即可，亦或是等着什么也不做，有些情况下系统会在一段时间后从死机中恢复的。

