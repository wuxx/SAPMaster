# SAPMaster V1 用户手册
* [产品介绍](#产品介绍) 
* [技术优势](#技术优势)
* [使用场景](#使用场景)
    * [系统启动](#系统启动)
    * [镜像上传](#镜像上传)
    * [镜像烧录](#镜像烧录)
    * [固件升级](#固件升级)
* [状态说明](#状态说明)
    * [蜂鸣器状态](#蜂鸣器状态)
    * [LED状态](#LED状态)
* [配置文件生成器](#配置文件生成器)
* [FAQ](#FAQ)

# 产品介绍
SAPMaster V1 （Stand Alone Programmer Master V1）是我司推出的第一代脱机烧录产品方案，强大的性能，丰富的功能，操作简单易用，烧录快速稳定，镜像加密安全存储在烧录器内部，带下载次数限制，滚码写入等功能，适合产品量产、公司之间的产品交付等使用场景。
# 技术优势
- 极速烧写，本烧录方案使用400MHz CPU实现，烧写平均速度实测为32KB/s，远高于市场目前同等价位其他方案（其他方案一般使用的是stm32系列单片机实现烧录，主频72MHz，极限速度只有28KB/s），而且本方案后续还有更多性能功能优化空间。
- 操作简洁方便，PC侧不需要安装复杂繁琐的上位机程序，只需通过在线web界面勾选生成一个镜像对应的的文本配置文件，将镜像和配置文件存入SD卡中，将SD卡插入到烧录器中，重启烧录器，即可将烧录文件上传至烧录器内部存储器中。配置文件可以在线web界面中勾选选项生成，也可以将web页面下载到本地使用，或者自己手动编辑生成配置文件，因为配置文件只是一个文本文件，只需您有有一定单片机开发经验，即可完全理解配置文件的内容。详细请点击 [配置文件生成器](https://wuxx.github.io/SAPMaster/)。
- 支持stm32全系列型号芯片烧录，具体如下：  
- [x]   stm32f0x  
- [x]   stm32f1x  
- [x]   stm32f2x  
- [x]   stm32f3x  
- [x]   stm32f4x  
- [x]   stm32f7x  
- [x]   stm32l0  
- [x]   stm32l4x  
- [x]   stm32h7x  
由于系统硬件和固件代码的优秀设计，更多型号只需少量修改即可轻松支持，您可将您的需求告知，我们的工程师可为您持续提供技术支持。
- 硬件上已经引出SWD、JTAG、串口、ICSP接口，已经为将来适配更多的目标芯片做好准备，将来只需升级固件，即可支持更多芯片的烧录，如stm8、8051、avr、imx, k40/k60, lpcxxx, dsp, at91xx, nrf51, dsp, mips, fpga/cpld等，更多目标芯片正在适配中，您可将需求告知我们，我们的工程师优先为您的平台提供技术支持。
- 支持两种烧录模式：手动按键烧录，以及自动烧录。自动烧录时，烧录器会在后台持续探测总线状态，当检测到目标正常连接后，完成烧录。
- 支持hex文件和bin文件烧录，下载次数限制，滚码写入，读保护。
- 镜像在烧录器内使用AES加密算法加密保存在烧录器内部非易失存储中，严格保证镜像的安全性。
- 使用蜂鸣器和RGB LED三色灯双重提示系统状态，简单易用。
- 支持固件升级，只需将新固件拷贝至SD卡中，将SD卡插入到烧录器中，重启烧录器，等待片刻，即可完成固件升级，固件发布在本仓库中，您可随时查询最新固件以及更多的功能。

# 使用场景
## 系统启动
烧录器通过USB方口数据线连接，USB方口数据线对烧录器仅提供5V的供电电源，对于某些不方便取电的场景，您可以使用便携电源通过USB对烧录器进行供电，以进行烧录工作。
烧录器上电数秒之后，您可观察到LED灯开始白灯闪烁，此为烧录程序正在初始化，1-2秒后，蓝灯缓慢闪烁，即表明烧录器处于就绪状态，随时可以进行烧录工作。
## 镜像上传
您需要准备两个文件：1. 镜像文件 2. 镜像对应的配置文件， 来将镜像上传至烧录器内部存储中。您需要编辑一个和镜像同名的配置文件，假若镜像名为abc.hex/abc.bin，则配置文件名需为abc.json，烧录器侧面有一SD卡槽，用于完成镜像上传以及固件升级。配置文件可以在线生成，也可自己手动编辑，详细请点击 [配置文件生成器](https://wuxx.github.io/SAPMaster/)。
将镜像和对应的配置文件放置在SD卡根目录，若根目录下存在多个镜像及配置文件，烧录器会选择按照字母排序最前的镜像进行上传，建议在根目录下只存放一个镜像进行上传。


## 镜像烧录
烧录器支持两种烧录模式：手动烧录与自动烧录，手动烧录模式下，按一次按键则进行一次烧录；自动烧录模式下，烧录器会持续探测总线，当检测到目标后执行一次烧录动作，请注意检测到目标后，烧录完成后，烧录器会等待目标和烧录器脱离，烧录动作只会执行一次。对于产品的量产，推荐使用自动烧录，快速方便。
## 固件升级
最新的烧录器固件会有性能和功能上的优化更新，若有需要，请在本git仓库的firmware目录中下载，将固件存入SD卡中（固件名需为sap.bin），将SD卡插入烧录器卡槽中，重启烧录器，观察指示灯和蜂鸣器状态即可。请注意：固件升级大概需要3-5分钟，升级过程中请不要断开电源，以免升级失败。



# 状态说明
## 蜂鸣器状态
蜂鸣器 | 说明
---|---
一声 | 镜像烧录成功
二声 | 新镜像上传成功
三声 | 镜像烧录失败
四声 | SD卡中的配置文件非法
五声 | SD卡中无有效镜像或者镜像非法
六声 | 烧录器中无有效镜像
七声 | 镜像下载次数已经耗尽
八声 | 其他未知错误

## LED状态
LED   | 整体说明| 场景说明
---       |---      |---      |
白灯闪烁  | 程序正在工作      |系统正在启动/正在烧录镜像
绿灯闪烁  | 成功    | 镜像烧录成功/新镜像上传成功
蓝灯缓慢闪烁|系统就绪，随时可以进行烧写|
红灯闪烁  | 失败    | 烧录失败/新镜像上传失败|
白灯长亮  | 固件正在升级|
绿灯常亮5s|固件升级成功
红灯常亮5s|固件升级失败
# 配置文件生成器
配置文件是一个json格式的文本文件，您可以点击
[配置文件生成器](https://wuxx.github.io/SAPMaster/)
自动生成。
以一款目前市场上较流行的单片机 stm32f103c8t6 为例说明：
```
{
    "type":"hex",           /* hex|bin 镜像文件类型为 hex，若是bin文件则填bin */
    "name":"GPIO_TEST.hex", /* 镜像文件名 */
    "class":"stm32f1x",     /* 芯片所属的stm32系列名 */
    "model":"stm32f103c8t6", /* 芯片的具体型号 */
    "interface":"swd",       /* swd|jtag|icsp 使用的烧录接口 */
    "mode":"auto",           /* auto|manual 使用自动烧录还是手动烧录 */
    "lifetime":"10000",      /* 最大烧录次数 */
    "flash_addr":"0x08000000",  /* 芯片的flash基地址，对于hex文件忽略此项，由于hex文件格式中已经有基地址 */
    "rolling_code_addr":"-1",  /* 滚码的flash地址，请注意此flash地址所在的页需空闲（因为会先擦除整页再写入滚码） */
    "rolling_code_value":"-1"  /* 滚码的初始值，若不需滚码功能，则此两项均填-1 */
}
```
# FAQ
有任何问题或者建议，请在本仓库的[Issues](https://github.com/wuxx/SAPMaster/issues)页面中提出，我们的工程师会持续跟进解决。