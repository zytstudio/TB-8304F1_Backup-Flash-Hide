# 平板TB-8304F1备份、刷机以及隐藏刷机方案整理

## 序言

​	大家好。

​	本文/视频是平板`TB-8304F1`的备份、刷机、隐藏刷机教程。

​	其他型号的学习平板的刷机也可参考本教程。

​	本人所在学校下发了学习平板供学生做题使用，型号为`TB-8304F1`，上面有`辅立码课`的应用。

​	这个平板原装系统无法安装第三方应用，无法连接电脑，设置也封得很严，没有打开`ADB`的选项，这导致了使用上的诸多不便。

​	于是，本教程将通过刷机的方式来实现解除原系统的限制，并隐藏刷机带来的更改。

## 免责申明

​	**本教程仅供学习交流使用，请勿用于任何不正当用途。本教程无任何政治倾向，教程内资料均来源于网络，下载内容完全免费。对于本教程提供的有版权的软件，请在下载后24小时内删除。请学生在通过老师和家长同意后再进行操作。对于参照本教程操作所造成的任何软件、硬件损坏以及财产损失，本人概不负责。本教程的文字版本仅在`Github`、`bilibili`以及`blog.zytstudio.top`发布，视频版本仅在`bilibili`、`AcFun`和`YouTube`发布，请勿转载。在其他平台看到的本教程均非本人发布。教程内容如有侵权，请联系本人进行删改。**

​	刷机有风险，操作需谨慎。

## 系统介绍

​	在刷机之前，先介绍一下原装系统。

​	这个平板的系统本人所在学校的大致有两个版本。

​	第一个版本上有带启动器的`辅立码课`，开机就是辅立码课的界面（如图），这个版本又有很多不同的小版本，`辅立码课`的版本与设置里的内容有细微差别。这个版本的系统删除了`WebView`，没有浏览器，而且软件没有bug（至少我还没有发现）。

​	另一个系统自带了云管控的启动器，开机是联想的开机动画，无法进入安卓设置。内置有应用商店，其中的`辅立码课`为不带启动器的版本，但也与官网的版本不同。

​	储存与内存前者一般为`16GB+2GB`，后者一般为`32GB+3GB`。

​	后者也有很多小版本，有的版本有内存清理，而有的版本没有。但是本人所在学校学校的这个系统的平板都带有浏览器。

​	后者虽然也删除了`WebView`，但是可以通过谷歌输入法进入自带的浏览器。这个浏览器只能访问`*.edu505.com`，无法下载文件。

​	后者其实不用刷机就可以访问网站，只需要买一个随身Wi-Fi，刷机后写一下静态DNS，再反向代理想要访问的网站即可。使用`JS Proxy`亦可。不过这个浏览器的内核过于老旧，一些网站可能无法正常访问。我试了一下，B站是可以正常访问并观看视频的，而`SD`的`WebUI`就访问不了。

​	后者`Recovery`中只保留了`关机`和`重启`两个选项，而前者没有删除其他选项，但是仍不建议在未刷机时使用`Recovery`中的选项进行操作。两者都无法识别外置`TF`卡。

## 正片

​	下面开始正片教程。

### 前期准备

#### 物品准备

​	首先，将平板充好电，最好充满，准备一台系统是`Windows 7`以上的电脑和一条USB数据线（学校发的一般是电源线）。

#### 安装驱动

​	需要在电脑上安装`ADB`驱动和`MTK`刷机驱动。

##### ADB驱动（可选）

​	在[玩机资源合集 (jamcz.com)](http://wanji.jamcz.com/)下载ADB驱动和ADB工具。（也可从其他渠道下载）

​	将ADB驱动解压，打开`DPInst_x64.exe`或者`DPInst_x86.exe`安装ADB驱动。

​	安装后可以连接安卓手机测试是否安装成功。

​	手机打开ADB调试后，打开设备管理器，插入手机，查看是否有ADB设备。若显示无法识别，则右键该设备，点击`更新驱动程序`，点击`浏览我的电脑以查找驱动程序`，再点击`让我从计算机上的可用驱动程序列表中选取`，取消勾选`显示兼容硬件`，厂商选择`Google`，型号选择`ADB设备`；如果厂商没有`Google`，则选择`WinUSB设备`，型号选择`ADB设备`。然后按照提示安装驱动即可。

​	将ADB工具解压，将解压出的目录添加至环境变量的`PATH`中。

​	添加后重启，打开`CMD`，输入`adb version`并回车，查看是否正常输出`ADB`版本。

##### MTK刷机驱动

​	下载`Mediatek_Driver_Auto_Installer_*.zip`，解压后打开`Install Drivers.bat`，按照提示安装驱动。安装好后重启。

​	具体方法参见`How to Install.url`中的说明。

### 备份（可选）

​	刷机前建议先备份原系统，尤其是`system`分区。此分区中存有原装系统的软件可供提取。

​	下载刷机软件`SP_Flash_Tool_v5.1748_Win.zip`和固件包`Lenovo_Tab_E8_TB-8304F1_MT8163_*.zip`，并分别解压。（也可从其他渠道下载）

​	打开`SP Flash Tool`。将语言改为中文。打开`下载`选项卡，`下载DA`选择`MTK_AllInOne_DA.bin`，`配置文件`选择固件包`Firmware`文件夹中的`MT8163_Android_scatter.txt`，`验证文件`选择`auth_sv5.auth`。

​	打开`回读`选项卡，点击`添加`，双击新添加的一项，选择一个保存的文件夹，文件名可以填写为`*.img`。用记事本打开固件包`Firmware`文件夹中的`MT8163_Android_scatter.txt`，找到`partition_name: system`这一行所在的块。在弹出的窗口中，`类型`选择`16进制`，`起始地址`填入`physical_start_addr`后的值，`长度`填入`partition_size`后的值，区域选择`EMMC_USER`，然后点击确定。

​	点击回读。然后将平板关机，此时先不要将平板连接到电脑。**关机后，同时按住平板的`音量+`与`音量-`键，同时用数据线连接电脑和平板。不要松手，直到进度条有反应后再松手。**备份过程中，不要断开电脑与平板的连接。若提示失败，则重复上述过程。

### 从备份中提取内置软件（可选）

​	此步骤需要一定的`Linux`使用经验。

​	备份后得到`*.img`文件。在`Linux`（`WSL`亦可）中打开终端（`shell`类型`bash`和`zsh`等均可），依次输入以下命令并依次回车。

```sh
cd <备份出来的文件所在的文件夹>
sudo umount /mnt/tmp
sudo rmdir /mnt/tmp
sudo mkdir /mnt/tmp
sudo mount <备份出来的文件名> /mnt/tmp
find /mnt/tmp | grep -i ".apk"
```

​	在输入`sudo`命令后，可能需要输入密码。请输入当前用户的密码（在`SUSE`中是`root`用户密码）并回车，此时输入的密码并不会在屏幕上显示。

​	在得到的应用列表中找到需要的`apk`文件，然后在终端中输入以下命令并回车，即可将需要的`apk`文件复制到主文件夹。

```sh
cp <得到的文件路径> ~
```

​	最后将镜像文件卸载，在终端中输入以下命令并回车即可。

```sh
sudo umount /mnt/tmp
```

​	若按照上述方法无法挂载`system`镜像，请尝试重新提取。若还是无法挂载，则可能是有加密或这其他防止读取的措施，本人尚未找到读取方法。

### 刷机

​	**刷机前请确认平板中重要数据已备份。**学生刷机须经过老师和家长的同意。

​	参考`备份`段中的说明下载并解压刷机软件和固件包，配置`SP Flash Tool`。打开`下载`选项卡，按照`备份`段中的说明选择`下载DA`、`配置文件`和`验证文件`。

​	<font color="Red">**将`下载`更改为`固件升级`。**</font>

​	点击`下载`按钮，然后参照`备份`段中的方法连接电脑和平板，等待刷入即可。刷入成功后，软件会显示`对勾`图标。<font color="Red">**此时请保证平板和电脑电量充足，并且在完成前请勿关机或者断开电脑与平板的连接。**</font>若提示失败，则重复上述过程。

### 刷机后续流程

​	刷机完成后断开平板与电脑的连接。开机后系统会自动进入`OOBE`，**此时不要连接Wi-Fi**，点击跳过，其他按照实际情况选择或填写即可。进入桌面后可连接Wi-Fi。

​	连接网络后，推荐打开设置，更新系统（可能需要多次更新）。

​	建议在设置中禁用或卸载平时不用的软件（如谷歌套件），以延长续航。

​	如无需隐藏刷机，则可直接从`辅立码课`官网或者本人提供的链接中的`software`文件夹中下载`辅立码课`官方版并安装，即可使用。

### 隐藏刷机（可选）

#### 刷入Magisk

​	平板进入桌面后安装`software/root`文件夹中的`mtk-easy-su-v2.1.1.apk`。打开`MTK Easy SU`，点击`ACCEPT`，然后点击右下角的`#`按钮，等待一段时间，出现提示后说明已获取临时`Root`权限。若长时间没有反应，则尝试重启或者重装软件再重复上述步骤。

​	获取临时`Root`权限后，安装`software/root`文件夹中的`magisk-v23.apk`或者`magisk-v25.apk`（也可从`Github`下载）。推荐安装`v23`版本，此版本是最后一个支持`Magisk Hide`的版本。也可尝试安装并刷入`Magisk Delta`（本人未尝试）。

​	打开设置，点击`关于平板电脑`，点击`版本号`多次，直至提示开发人员选项已开启。退回到设置主页面，点击`开发人员选项`，打开`USB调试`。

​	连接电脑与平板。电脑打开`CMD`，输入`adb start-server`并回车。平板弹出是否允许USB调试的窗口。勾选`一律允许`，点击`确定`。`CMD`中输入`adb shell`并回车，然后输入`su`并回车。此时平板提示是否允许获取`Root`权限，点击`允许`。`CMD`中依次输入以下命令并依次回车，然后关闭`CMD`。

```sh
rm -f /storage/emulated/0/boot.img
rm -f /storage/emulated/0/Download/magisk_patched-*.img
rm -f /storage/emulated/0/Download/boot-magisk.img
dd if=/dev/block/mmcblk0p8 of=/storage/emulated/0/boot.img
```

​	打开`Magisk`，提示`需要修复运行环境`，点击`取消`。

​	点击`更新`按钮，若提示是否允许存储权限，则点击`允许`。在下一个页面中点击`下一步`，然后选择`选择并修补一个文件`。在选择文件界面点击右上角的`⁝`按钮，点击`显示内置存储设备`。若没有`显示内置存储设备`，则忽略此步骤。点击左上角的`≡`，点击`Lenovo TB-8304F1`，然后在中间的选择文件界面中长按`boot.img`，点击右上角的`打开`。

​	点击`开始`。等待一段时间，提示完成后即可退出。

​	电脑打开`CMD`，依次输入以下命令并依次回车，然后关闭`CMD`。

```sh
adb shell
su
cd /storage/emulated/0/Download
mv magisk_patched-*.img boot-magisk.img
dd if=boot-magisk.img of=/dev/block/mmcblk0p8
reboot
```

​	<font color="Red">**此时请保证平板和电脑电量充足，并且在完成前请勿关机或者断开电脑与平板的连接。**</font>

​	完成后平板会重启。开机时提示`Red State`为正常现象，忽略即可。

​	开机后打开`Magisk`，检查是否已经刷入成功。若未成功则重复上述步骤。

​	**请勿开启`Zygisk`或刷入`Zygisk`模块！！！**

#### 刷入Xposed框架

​	平板安装`software/root`文件夹中的`DreamlandManager-*.apk`。（也可从`Github`下载）

​	平板下载`software/root`文件夹中的`riru-*-release.zip`与`dreamland-*.zip`。（也可从`Github`下载）

​	打开`Magisk`，打开`模块`选项卡。点击`从本地安装`。参照`刷入Magisk`段中的方法选择`riru-*-release.zip`，等待刷入。刷入完成后点击`重启`。

​	重启后再次打开`Magisk`。按照上述方法刷入`dreamland-*.zip`并重启。

​	也可尝试刷入其他框架。

#### 刷入其他模块（可选）

​	还可以通过刷入其他模块来实现隐藏`Magisk`等功能。本教程中提供了以下几个推荐的模块，可以按需求安装。

| 模块名称                | 文件名                | 功能                                                         |
| ----------------------- | --------------------- | ------------------------------------------------------------ |
| Universal SafetyNet Fix | `safetynet-fix-*.zip` | 通过`SafetyNet`检测。可以使`Netflix`等需要`SafetyNet`检测通过才能正常运行的应用正常运行。 |
| Universal GMS Doze      | `gms_*.zip`           | 用于冻结后台运行的谷歌套件以延长续航时间。                   |
| Riru - MomoHider        | `Riru-MomoHider.zip`  | 用于隐藏`Riru`。已停更，可能失效。                           |

​	安装模块的方法参见`刷入Xposed`段。

#### 安装并配置核心破解

​	由于带启动器版本的`辅立码课`没有v2签名（提取自原装系统），需要安装核心破解来安装此版本的`辅立码课`。也可通过核心破解安装其他没有签名的应用或降级应用。

​	平板安装`software/root`文件夹中的`kernel_patch_v2.1.apk`。（也可从其他渠道下载）

​	打开`核心破解`，参照`刷入Magisk`段中的方法授予`Root`权限。将四个选项全部打开。

​	打开`梦境`。打开`模块`选项卡，勾选`核心破解`。打开`应用`选项卡，勾选`Android系统`。如有弹窗提示则忽略即可。重启平板。

#### 安装Xposed Edge Pro并导入配置

​	本教程中提供的`Xposed Edge Pro`为解锁版本。建议有能力的观众或读者购买正版，支持原作者。

​	平板安装`software/root`文件夹中的`xposed_edge_pro.apk`。（正版用户请通过正版渠道安装）

​	按照`安装核心破解`段中的方法在`梦境`中开启`Xposed Edge Pro`。重启平板。

​	平板下载`software/root`文件夹中的`*.bak`。

​	打开`Xposed Edge Pro`，点击`更多`，点击`备份/导入`。若提示是否允许存储权限，则点击`允许`。在新页面中点击`读取自`，参照`刷入Magisk`段中的方法选择下载的`*.bak`。回到`Xposed Edge Pro`主界面，勾选`手势`和`按键`。

​	此配置文件中带有`冰箱`的相关操作。如果不打算安装`冰箱`，则需要在`保存的多重动作`中长按唯一的一项，点击编辑动作，然后再新的页面中点击与`冰箱`有关的动作，再点击删除即可。

​	安装与配置完成后建议先测试手势与按键是否正常触发。

#### 安装并启用冰箱（可选）

​	`冰箱`可以冻结经常再后台刷新的应用，例如`**作业帮`、`W** Office`等。使用这些软件时可以配合冰箱来延长续航并提升性能。

​	平板安装`software/root`文件夹中的`icebox.apk`。（也可从其他渠道下载）

​	打开`冰箱`，阅读协议后点击`我已阅读并理解`。点击右下角的`>`，选择`Root`，参照`刷入Magisk`段中的方法授予`Root`权限。等待配置完毕进入主页面后即可使用。

​	点击下方的`APP`按钮，勾选需要冻结的应用即可使用。

#### 安装带启动器版本的辅立码课

​	平板安装`software`文件夹中的`fuulea-with_launcher.apk`（需要先安装并配置`核心破解`）。

​	若安装失败则检查`核心破解`与`梦境`框架配置是否正确。

#### 后续工作

​	点击`○`（主屏幕）按钮，在主屏幕选择页面中选择`辅立码课`。

​	再次点击`○`（主屏幕）按钮，在主屏幕选择页面中点击`始终`按钮。

​	再次测试手势与按键是否正常工作。

#### 隐藏锁屏界面的用户图标与设置中的选项（可选）

​	本教程提供的文件中有从原装系统中提取的`Settings.apk`和从中国版系统中提取的`SystemUI.apk`。这两个应用无法直接安装。参考网上的教程可以用`Magisk`将这两个`apk`文件替换掉原系统的`apk`文件。替换后前者可以隐藏设置中的选项，后者可以隐藏锁屏界面的用户图标。

​	（待补充）

## 手势与按键说明

 - 每次解锁后自动回到主屏幕（`辅立码课`启动器）。

 - 解锁后在屏幕右侧边缘偏上的位置滑动有如下效果：

   |      | 手势                 | 效果                           |
   | :--: | -------------------- | ------------------------------ |
   |  ↑   | 向上滑动             | 回到主屏幕（`辅立码课`启动器） |
   |  ↓   | 向下滑动             | 回到上一个应用                 |
   |  ⇵   | 先向下滑动再向上滑动 | 打开启动器                     |
   |  ↡   | 向下滑动并停住       | 打开应用抽屉                   |
   |  ←   | 向左滑动             | 触发应急模式                   |

 - 关闭屏幕后按`音量键`累计达到3次以上即触发应急模式。亮屏后若未达到3次，则清空次数。

 - 应急模式有如下操作：

   - 清除后台所有程序；
   - 冻结冰箱中的应用（如果安装了冰箱）；
   - 回到主屏幕（`辅立码课`启动器）。

## 救砖指南与注意事项

​	刷机后的安装软件与刷入`Magisk`等流程可以不用电脑，只需在平板上安装`software`文件夹中的`com.termoneplus_*.apk`，然后再按照上述步骤执行命令即可（不用执行`ADB`相关的命令）。此时，电脑上不用安装`ADB`驱动与工具。

​	本教程中的`*`指代任意字符或字符串。

​	如果因不慎刷入错误的`Magisk`模块或者打开`Zygisk`导致无法开机，则可重新刷入`boot`分区。严重时也需重新刷入`system`分区。详细方法参考`刷机`段，在刷机时仅勾选上述分区，并且不用选择`固件升级`。

​	重新刷入`system`分区后需要重新安装系统更新并`Root`。`Root`后黑屏是正常现象，此时需要等待屏幕重新亮起后重新刷入修补好的`boot.img`，也可尝试直接打开`Magisk`并在提示`需要修复运行环境`时点击`确定`。然后打开`Magisk`，删除或关闭错误的模块，或者关闭`Zygisk`。重启平板。

​	如果上述方法仍然无效，可以考虑重新完全刷机。

​	**刷机时请勿选择`全部格式化和下载`，否则可能导致`SN`码丢失。**

​	请勿尝试刷入其他系统的`logo`分区，否则会导致无法启动。若已经刷入，则参照上文重新刷入该分区即可正常启动。

​	**请勿尝试在未刷机的情况下尝试恢复出厂设置或清除`userdata`分区。**有带启动器的`辅立码课`的系统重置后需要注册，而学生无法自行注册。

​	`辅立码课`原名`敏特码课`。`辅立码课`官方版最低兼容安卓`5.0`，而本人提取出的带启动器的版本最低兼容安卓`4.4`。前两者版本号均为`1.5.0`，而有些平板上原装系统中的`辅立码课`版本号为`1.5.1`。后者最低兼容安卓`6.0`，本人曾尝试过提取，但是安装后需要下载文件，总是失败，故本教程不采用。`辅立码课`还有很多其他版本，需要下载文件的都无法使用。

​	下载文件中也提供了`云管控`和`内存管理`的安装包，但是`云管控`安装后需要登录。本人所在学校下发前就已经将账号录入，学生不知道账号和密码，无法正常登录。如果知道账号和密码，也可结合云管控进行隐藏刷机。

​	本人刷机时，在`bilibili`上找到了一个刷机教程，而且该教程提供的资料比较详细，还包括了旧版的`云管控`安装包等资料。遗憾的是，本人再次查找时没有找到该视频。本教程也参考了该教程提供的方法。该教程中提供的文件本人已经保存，但是由于禁止转载，故本教程中不放出。若有需求，请联系原视频发布者。

​	本教程中提供的刷机包为官方的国际版。也有其他同学找到了官方的中国版刷机包，但是本人仍未找到。该版本没有谷歌套件，但是锁屏界面和控制中心都没有用户图标。如有需要请自行寻找。从该版本系统中提取的`SystemUI.apk`在`software`文件夹中可供下载。

​	由于本人已毕业，本教程不再更新。请有补充内容意向的读者或观众在`Github`中`Fork`本仓库进行修改。

## 相关文件下载链接

- 合集：[Index of /tablet-crack/ (zytstudiobg.top)](http://zytstudiobg.top:8012/tablet-crack/)
- SP Flash Tool：[SP Flash Tool for Windows (all versions) (spflashtools.com)](https://spflashtools.com/category/windows)
- `MTK`刷机驱动：[Mediatek_Driver_Auto_Installer_v1.1352.zip - Android Data Host](https://androiddatahost.com/276a2)
- 固件包：[Lenovo Tab E8 TB-8304F1 Stock Firmware ROM (Flash File) (firmwarefile.com)](https://firmwarefile.com/lenovo-tab-e8-tb-8304f1)
- `ADB`驱动/和工具：[玩机资源合集 (jamcz.com)](http://wanji.jamcz.com/)
- Magisk：[Releases · topjohnwu/Magisk (github.com)](https://github.com/topjohnwu/Magisk/releases)
- DreamLand：[Releases · canyie/Dreamland (github.com)](https://github.com/canyie/Dreamland/releases)
- DreamLand Manager：[Releases · canyie/DreamlandManager (github.com)](https://github.com/canyie/DreamlandManager/releases)
- Riru：[Releases · RikkaApps/Riru (github.com)](https://github.com/RikkaApps/Riru/releases)
- Riru - MomoHider：[canyie/Riru-MomoHider: A Riru module tries to make Magisk more hidden. (github.com)](https://github.com/canyie/Riru-MomoHider)
- Xposed Edge Pro（解锁版）：[【xposed】Xposed edge pro 8.0.1 专业版 - 果核剥壳 (ghxi.com)](https://www.ghxi.com/xpedge.html)
- Universal GMS Doze：[Releases · gloeyisk/universal-gms-doze (github.com)](https://github.com/gloeyisk/universal-gms-doze/releases)
- Universal SafetyNet Fix：[Releases · kdrag0n/safetynet-fix (github.com)](https://github.com/kdrag0n/safetynet-fix/releases)
- 辅立码课（官方版）：[下载辅立码课APP (fuulea.com)](http://app.fuulea.com/)

## 参考资料

1. [(GUIDE) Lenovo Tab 8 (Lenovo TB-8304F1) Root Guide | XDA Forums (xda-developers.com)](https://forum.xda-developers.com/t/guide-lenovo-tab-8-lenovo-tb-8304f1-root-guide.4291905/)
2. [Lenovo Tab E8 TB-8304F1 Stock Firmware ROM (Flash File) (firmwarefile.com)](https://firmwarefile.com/lenovo-tab-e8-tb-8304f1)
3. [canyie/Dreamland: A third-party Xposed framework implementation, supports Android 7~11. (github.com)](https://github.com/canyie/Dreamland)
4. [topjohnwu/Magisk: The Magic Mask for Android (github.com)](https://github.com/topjohnwu/Magisk)
5. [RikkaApps/Riru: Inject into zygote process (github.com)](https://github.com/RikkaApps/Riru)
6. [Releases · JunioJsv/mtk-easy-su (github.com)](https://github.com/JunioJsv/mtk-easy-su/releases)
7. [玩机资源合集 (jamcz.com)](http://wanji.jamcz.com/)
8. [gloeyisk/universal-gms-doze: Patches Google Play services app and certain processes/services to be able to use battery optimization (github.com)](https://github.com/gloeyisk/universal-gms-doze)
9. [canyie/Riru-MomoHider: A Riru module tries to make Magisk more hidden. (github.com)](https://github.com/canyie/Riru-MomoHider)
10. [kdrag0n/safetynet-fix: Google SafetyNet attestation workarounds for Magisk (github.com)](https://github.com/kdrag0n/safetynet-fix)
11. [【xposed】Xposed edge pro 8.0.1 专业版 - 果核剥壳 (ghxi.com)](https://www.ghxi.com/xpedge.html)
12. [Ice-Box-Docs | 冰箱 Ice Box 应用在线文档 (catchingnow.com)](https://iceboxdoc.catchingnow.com/)
13. [下载辅立码课APP (fuulea.com)](http://app.fuulea.com/)
14. [SP Flash Tool for Windows (all versions) (spflashtools.com)](https://spflashtools.com/category/windows)
15. [Mediatek_Driver_Auto_Installer_v1.1352.zip - Android Data Host](https://androiddatahost.com/276a2)
16. [How-to install Mediatek Drivers using the Mediatek Driver Auto Installer (gsmusbdriver.com)](https://gsmusbdriver.com/install-mediatek-driver-auto-installer)
17. https://www.bilibili.com/video/BV13G411J7u2
18. [(保姆级)高通|联发科系统固件备份·分区提取·救砖不求人！ - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv19909092?jump_opus=1)
19. [可用的 Android 版本 · ElderDrivers/EdXposed Wiki (github.com)](https://github.com/ElderDrivers/EdXposed/wiki/可用的-Android-版本)
20. [How to reset password on Lenovo TB-8304F1 - Lenovo - YouTube](https://www.youtube.com/watch?v=b7oYbMZidAc)
21. https://www.bilibili.com/video/BV1QS4y1u7mg
22. [Lenovo TB-8304F Flash File (Stock Firmware Guide) (getdroidtips.com)](https://www.getdroidtips.com/lenovo-tb-8304f-flash-file-stock-firmware-guide/)
23. [(GUIDE) Lenovo Tab 8 (Lenovo TB-8304F1) Backup boot.img Guide | XDA Forums (xda-developers.com)](https://forum.xda-developers.com/t/guide-lenovo-tab-8-lenovo-tb-8304f1-backup-boot-img-guide.4291907/)
