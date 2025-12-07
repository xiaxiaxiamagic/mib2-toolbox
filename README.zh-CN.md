# MIB2 High 工具箱
[English](README.md) | 简体中文

为您的 MIB2 HIGH 系统提供高度定制的终极工具箱。

注意：该屏幕存在损坏 MIB2 HIGH 机头的风险。开发者不对因本工具箱给任何人或事物造成的麻烦负责。我们从未有意伤害任何人、车辆或品牌。请谨慎使用工具，别当混蛋。

注意 2：这 **不是** 适用于所有需求和固件版本的通用越狱方案。

注意 3：如果你想借此牟利：别当混蛋，别收费。这个项目是我们在空闲时间出于对社区的热爱所做的。我在测试时冒着砖机的风险，并投入了大量研究时间。与其赚钱，不如用你的知识支持这个项目，或者考虑给一点[小额捐赠](https://paypal.me/chillout1)或成为 [Patreon](https://patreon.com/jille)。

# 需求
- 阅读完整 README
- 至少一颗健康的大脑
- 一台 MIB2 HIGH 或 MIB2.5 HIGH 机头。它 **不** 适用于 MIB1 或 MIB2 Standard 机头。Discover Media / Composition Media 不是 MIB2 HIGH！如果是 MIB2 Standard，请查看 [olli991/mib-std2-pq-zr-toolbox](https://github.com/olli991/mib-std2-pq-zr-toolbox) 项目。
- 1 张空的、**FAT32 格式** 的 SD 卡，容量足够。大于 1GB 的都可以。
- 一些可以保存备份的空间。

## 可选需求
- 如果要解压/压缩图形容器（canim/mcf），需要 Python 3
- 如果要自制绿菜单文件或脚本，需要文本编辑器
- 如果要自定义图形文件，需要图片编辑软件

# 如何安装
- 如果你之前安装过旧版本（V4.0 之前），在尝试安装前请清空 SD 卡。
- 从仓库下载所有文件，可以通过 git clone 或 GitHub “Download zip” 然后解压。
- 将所有文件和文件夹放到一张空 SD 卡上，建议容量 >1GB。
- 将 SD 卡插入 MIB2 机头的任一插槽。
- 确保机头里只有一张 SD 卡，否则脚本不知道该看哪张卡。
- 按住 MIB2 的 MENU 键，直到出现服务屏幕。
- 选择“Software updates/versions”菜单，然后点击右上角的“Update”按钮。
- 选择 SD 卡并选择 MQB Coding MIB2 Toolbox。
- 让机头运行完整的软件更新。它会重启几次，然后显示一个列出很多模块为 N/A 的界面。Toolbox 一行应该是 Y。此时可以点击右上角的返回按钮。
- 完成后，它会要求连接电脑并清除错误代码。这不是必须的，可以点击“Cancel”。
- 机头会再重启一次，回到主车机菜单。安装完成。
- 按住 MENU 键进入 TESTMODE。在旧版本上可以按住 MENU 大约 10 秒进入开发者菜单。
- 进入 Green Developer Menu。
- 你会看到一个名为“mqbcoding”的额外菜单。看到它说明安装成功。
- 进入 mqbcoding，你将看到以下内容：

![The MQB Coding toolbox menu](https://i.imgur.com/wGUZ4xw.png)

- 搞定。
- 玩得开心！

# 如何手动安装
- 将 mib2-toolbox 放到 SD 卡上，然后插入 MIB 机头的 SD1 插槽。
- 连接机头的调试控制台（通过 USB 口的 D-Link Dub-E100 或 ASIX AX88179，或机头背面的串口接口）。
- 登录。
- 挂载 SD 卡：
  * `mount -uw /net/mmx/fs/sda0`
- 运行 finalScript：
  * `sh /net/mmx/fs/sda0/Toolbox/final/finalScripts.sh`

- 按住 MENU 键进入 TESTMODE。在旧版本上可以按住 MENU 大约 10 秒进入开发者菜单。
- 进入 Green Developer Menu。
- 你会看到一个名为“mqbcoding”的额外菜单。看到它说明安装成功。
- 搞定。
- 玩得开心！

# 绿菜单界面概览：

```
MQBCoding Main
|
+---Customization                       # Customization features
|   +---Adaptations                     # Adaptation channels
|       +---CarDeviceBUSAssignment
|       +---CarFunctionsList_BAP
|       +---CarFunctionsList_CAN
|       +---CarMenuOperation
|       +---HMI_FunctionBlockingTable
|       +---RCCAdaptions
|       +---VariantInfo
|       +---VehicleConfiguration
|       +---WLAN
|   +---Advanced                        # Import shadow file, FECs pf.conf and such
|   +---AndroidAuto                     # Android Auto custom apps patch
|   +---Coding                          # Long coding editor
|   +---Display                         # Displaymanager and other related features
|   +---GreenMenu                       # Import new GreenMenu screens and scripts
|   +---Language                        # Replacing language data
|   +---Navigation                      # Navigation tweaks, mapstyles switching
|   +---Privacy                         # Privacy features
|   +---Skin                            # Skin graphics import
|   +---Sounds                          # Sounds import (experimental)
|   +---Startup                         # Startup graphics import
|   +---Updates                         # Custom SWDL modes and emergency
|   +---Various                         # Various tweaks
|
+---Disclaimer                          # Some wise words
|
+---Dump                                # Dump various data to SD-card
|
+---History                             # Version history of the Toolbox
|
+---MIB_Information                     # Information about the unit
|   +---Password                        # Password finder
|
+---Uninstall                           # Uninstalls and or cleans up the MIB Toolbox
```

# 如何使用新界面
若需按绿菜单分类查看每个工具箱脚本的用途、预期输入/输出、存储影响及备份提示，请参阅 [docs/scripts.md](docs/scripts.md)。
多数界面都有说明，或在运行脚本时会显示信息。建议始终在插槽 1 中插入 SD 卡。

## dump
这里可以导出自定义机头所需的各种内容。确保已插入 SD 卡。

## customization
### androidauto
此界面有两个按钮：
- 修补 Android Auto 以启用自定义第三方应用。手机不需要 root。
- 恢复原始 gal.json，以防你不喜欢补丁或出现问题。

### skin
此界面让你为 6 个皮肤文件夹分别安装新的 images.mcf，来源于 SD 卡上的 SkinFiles 文件夹。使用导出的文件作为参考。不要安装针对其他固件的文件，否则 **会** 破坏图形和功能。
此界面也能从备份中恢复皮肤。

## greenmenu
此界面可从 SD 卡的 GreenMenu 文件夹导入新的 .esd 文件。

# 如何使用工具
在 Tools 文件夹里你会找到一些工具：
- extract-canim.py

这些是用于解压启动屏幕文件（.canim 文件）的 Python 脚本，有两种格式。如果其中一个脚本无法解压你的 canim，试试另一个。两者用法相同：extract_canim.py <filename> <outdir>，例如：

```extract_canim.py test.canim .\testfiles\```

- extract-mcf.py

这是一个解压皮肤容器（mcf）的 Python 脚本，使用方法与 canim 解压类似：extract_mcf.py <filename> <outdir>，例如：

 ```extract_mcf.py images.mcf .\extracted\```


- compress-canim.py

这是压缩启动屏幕的脚本。确保使用与你解压时相同的压缩方法。用法：compress-canim.py <original-file> <new-file> <imagesdir>，例如：

```compress-canim.py test.canim modified.canim .\testfiles\```

- compress-mcf.py
这是压缩 MCF 容器的脚本。用法：compress-mif.py <original-file> <new-file> <imagesdir>，例如：

```compress-mcf.py images.mcf images2.mcf .\extracted\```

- extract-cff.py
此脚本可以解压 images.cff 文件（导航图标和材质的容器）。用法：extract-cff.py <output dir>，例如：

```extract-cff.py images.cff c:\extracted\```


## 常见问题
如果遇到问题，请参阅 [F.A.Q.](https://github.com/jilleb/mib2-toolbox/blob/master/FAQ.md)。

## 支持的固件版本
该工具箱可能不适用于所有固件版本，但当前的 SD 卡安装方式在大多数固件上基本兼容。
