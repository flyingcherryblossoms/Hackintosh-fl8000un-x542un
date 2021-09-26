# Hackintosh-fl8000un-x542un

​    华硕fl8000un 黑苹果OC 引导： [EFI的Github地址](https://github.com/flyingcherryblossoms/Hackintosh-fl8000un-x542un)

​    通过fl8000uq的EFI完善给fl8000un

> https://github.com/KKKIIINNN/ASUS-FL8000UQ-Hackintosh

​    使用前建议先看看，原版的README，我只是加了几个驱动。

支持Catalina和BigSur，其余未测试

## 配置

| 配置     | 型号                               |
| -------- | ---------------------------------- |
| 处理器   | i7-8550U Kaby Lake                 |
| 核显     | Intel Graphics UHD620              |
| 独显     | GeForce MX150                      |
| 内存     | 4G× DDR4 2400MHz/16Gx DDR4 2400MHz |
| 硬盘     | 512G SSD/1T HDD                    |
| 声卡     | Realtek ALC294                     |
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

2. 蓝牙开关需要先关闭Wi-Fi，不然会卡住。

3. USB网络共享的驱动有一个问题，每次重新连接，网络设置里就多一个选项，要重新恢复到1开始：

   终端执行

   ```shell
   sudo rm /Library/Preferences/SystemConfiguration/N*
   ```

