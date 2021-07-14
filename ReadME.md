# Hackintosh-fl8000un-x542un
​	华硕fl8000un 黑苹果OC驱动

​	通过fl8000uq的EFI完善给fl8000un

> （感谢🙏：https://github.com/KKKIIINNN/ASUS-FL8000UQ-Hackintosh）

​	使用前建议先看看，原版的README，我只是加了几个驱动。

​	折腾了两天，先安装Big Sur，用了黑果小兵的10.4镜像，显示正常，但驱动就很迷幻，有时候有有时候没有，还容易掉盘，无奈选择了Catalina，发现Catalina下驱动就很稳👍。

同步博客：[卡西莫多的礼物](quosimodo.cn)

## 折腾的过程

​	Big Sur折腾过程中，触摸板和显示是没有问题的。

出现的驱动问题如下：

* 声卡

* 有线网络

* 无线网络

* 蓝牙

​	由于有线网络和无线网络都没有，这就很不方便我们查资料，所以我百度找到安卓手机USB共享网络给Mac的方法，要装一个驱动，开始找的版本因为Bigsur修改了安全机制不能直接安装，因此我直接去[GitHub issue](https://github.com/jwise/HoRNDIS/issues/102#issuecomment-551255547)上找了一个不用权限的修改版本，放仓库了，可以直接用。

1. 首先是声卡没有声音，fl8000un的声卡为ALC294，支持的layout如下（[AppleACL](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs)）：

   | Vendor  | Codec                                                        | Revisions and layouts             | MinKernel | MaxKernel |
   | ------- | ------------------------------------------------------------ | --------------------------------- | --------- | --------- |
   | Realtek | [ALC294](https://github.com/acidanthera/AppleALC/tree/master/Resources/ALC294) | layout 11, 12, 13, 21, 22, 28, 66 | 13 (10.9) | —         |

   我改成了11，有声音了。

2. 接着是有线网卡，也没有驱动，插上去没有反应，于是我找到之前驱动过的Realtek8111驱动给替换上去了，然后解决了这个驱动问题。

3. 接下来按照小时光的教程：

   * [AR9565 MAC11.0黑苹果WIFI驱动教程](https://www.longzc.cn/index.php/archives/330)

   * [AR9565 MAC11.0黑苹果WIFI驱动教程](https://www.longzc.cn/index.php/archives/330)

   修复了蓝牙和Wi-Fi驱动

BigSur每次重启驱动和磁盘都可能掉，于是装了Catalina还是黑果小兵的镜像，发现刚才配置的EFI完美运行，好起来了XDM。仓库里放了折腾过程的几个版本，你们可以自己试试Big Sur。要安装还是建议Catalina。
