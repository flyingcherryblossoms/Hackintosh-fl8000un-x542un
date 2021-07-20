# Hackintosh-fl8000un-x542un

​    华硕fl8000un 黑苹果OC引导

​    通过fl8000uq的EFI完善给fl8000un

> （感谢🙏：https://github.com/KKKIIINNN/ASUS-FL8000UQ-Hackintosh）

​    使用前建议先看看，原版的README，我只是加了几个驱动。

​    折腾了两天，先安装Big Sur，用了黑果小兵的10.4镜像，显示正常，但驱动就很迷幻，有时候有有时候没有，还容易掉盘，无奈选择了Catalina，发现Catalina下驱动就很稳👍。

[同步博客](quosimodo.cn)

## 配置

| 配置   | 型号                                 |
| ---- | ---------------------------------- |
| 处理器  | i7-8550U Kaby Lake                 |
| 核显   | Intel Graphics UHD620              |
| 独显   | GeForce MX150                      |
| 内存   | 4G× DDR4 2400MHz/16Gx DDR4 2400MHz |
| 硬盘   | 512G SSD/1T HDD                    |
| 声卡   | Realtek ALC294                     |
| 无线网卡 | AR956x                             |

## 哪些工作

在Catalina上：

- [x] 触控板

- [x] 声卡

- [x] 有线网卡

- [x] 无线网卡（工作缓慢）

- [x] 蓝牙（开关蓝牙前请先关闭WI-FI，不然会卡住）

- [x] 集成显卡

- [ ] 独立显卡（无法驱动）

已知问题：休眠出现不亮屏问题

## 使用说明

* BIOS关闭`VT-d`

* BIOS关闭`CSM`

* BIOS关闭`Secure Boot`

* BIOS关闭`Fast Boot`

* 解锁`CFG Lock`：
  
  [教程：BIOS华硕官网有](https://www.bilibili.com/read/cv6167464/)
  
  1. 将U盘格式化为FAT32格式；
  
  2. 打开CFG文件夹，将里面的EFI文件复制到U盘中，重启按ESC键选择U盘启动；
  
  3. 输入命令`setup_var_3 0x527 0x00`即可解锁CFG Lock。

* 安装使用安装的EFI：就是fl8000uq的EFI，可以直接去上面的链接下载，仓库里也有

* 安装完成使用配置好驱动的EFI（Catalina文件夹下）

## 注意事项

1. HDPI开启（Big Sur不保证成功）：
   
   * 关机
   * 开机进入Open Core选择Recovery模式->终端->输入`csrutil disable`：输出Successful ... 则操作成功
   * 重新开机：下载或者`git clone https://github.com/xzhih/one-key-hidpi`，进入文件夹打开`hdpi.command`，开启hdpi
   * 关机
   * 开机进入Open Core选择Recovery模式->终端->输入`csrutil enable`：输出Successful ... 则操作成功
     * 重新开机，输入`csrutil status`如果显示disable，需要在开机进OC时候，reset nvram（可能会丢失OC引导，需要重新添加引导），在进Recovery`csrutil enable`，重启，即可开启SIP。

2. USB定制请参考黑果小兵的教程：[Hackintool(Intel FB Patcher) USB定制视频](https://blog.daliansky.net/Intel-FB-Patcher-USB-Custom-Video.html)

3. 蓝牙开关需要先关闭Wi-Fi，不然会卡住。

4. USB网络共享的驱动有一个问题，每次重新连接，网络设置里就多一个选项，要重新恢复到1开始：
   
   终端执行
   
   ```shell
   sudo rm /Library/Preferences/SystemConfiguration/N*
   ```

## 折腾的过程

​    Big Sur折腾过程中，触摸板和显示是没有问题的。

出现的驱动问题如下：

* 声卡

* 有线网络

* 无线网络

* 蓝牙

​    由于有线网络和无线网络都没有，这就很不方便我们查资料，所以我百度找到安卓手机USB共享网络给Mac的方法，要装一个驱动，开始找的版本因为Bigsur修改了安全机制不能直接安装，因此我直接去[GitHub issues](https://github.com/jwise/HoRNDIS/issues/102#issuecomment-551255547)上找了一个不用权限的修改版本，放仓库了，可以直接用。

1. 首先是声卡没有声音，fl8000un的声卡为ALC294，支持的layout如下（[AppleACL](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs)）：
   
   | Vendor  | Codec                                                                          | Revisions and layouts             | MinKernel | MaxKernel |
   | ------- | ------------------------------------------------------------------------------ | --------------------------------- | --------- | --------- |
   | Realtek | [ALC294](https://github.com/acidanthera/AppleALC/tree/master/Resources/ALC294) | layout 11, 12, 13, 21, 22, 28, 66 | 13 (10.9) | —         |
   
   我改成了11，有声音了。

2. 接着是有线网卡，也没有驱动，插上去没有反应，于是我找到之前驱动过的Realtek8111驱动给替换上去了，然后解决了这个驱动问题。

3. 接下来按照小时光的教程：
   
   * [AR9565 MAC11.0黑苹果WIFI驱动教程](https://www.longzc.cn/index.php/archives/330)
   
   * [AR9565 MAC11.0黑苹果WIFI驱动教程](https://www.longzc.cn/index.php/archives/330)
   
   修复了蓝牙和Wi-Fi驱动

​    BigSur每次重启驱动和磁盘都可能掉，于是装了Catalina还是黑果小兵的镜像，发现声卡正常驱动就没有替换layout，然后剩下的步骤和之前一样，发现驱动完美运行。仓库里放了折腾过程的几个版本，你们可以自己试试Big Sur。要安装还是推荐Catalina。
