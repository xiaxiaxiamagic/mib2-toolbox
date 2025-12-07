# Toolbox 脚本与 Green Menu 对照

本节按 Green Menu 菜单分组，汇总 `Toolbox/scripts` 中可调用的脚本。每个条目列出用途、预期输入/输出、对存储的影响以及推荐的备份或断电保护操作。所有安装或补丁类脚本默认需要在 SD1 中插入含 Toolbox 的 FAT32 SD 卡，执行前可用 `ls /net/mmx/fs/sd*/Toolbox` 或 `mount | grep mmx` 确认卡已被识别并可写。

> **通用提示**：所有脚本都会在 `/net/mmx/fs/sd?0` 进行读写，运行前务必确保 SD 卡已正确插入；涉及系统分区写入或闪存的操作建议在车辆供电稳定（最好连接稳压电源）的环境下进行。

## MQBCoding 主菜单

- **`update_toolbox.sh`**：用更新包覆盖 Toolbox 自身文件。输入为 SD 卡根目录下的当前仓库内容，输出为更新后的 Toolbox 目录（覆盖 SD 上的同名文件）。会向 SD 写入，无系统分区写入，建议先备份 SD 卡内容或制作镜像；更新过程中避免拔卡。

## Customization → Advanced

- **`copy_fec.sh`**：从 `/Custom/FEC/FecContainer.fec` 覆盖设备内的 FEC 容器。读 SD 写入 `/net/rcc/mnt/efs-persist/FEC`，会在 SD 上自动生成备份（`Backup/<版本>/<FAZIT>/FEC`）。需备份：运行前建议先执行 `dump_fec.sh` 或复制现有 FEC 目录。
- **`copy_gem.sh`**：安装自定义 `GEM.jar`（来源 `/Custom/GEM`）。写入系统分区并在 SD 建立备份目录。建议先备份原始 `GEM.jar`（脚本会自动在 SD 备份一份）。需备份。
- **`install_lsdjxe.sh`**：从 `/Custom/LSD` 链接并安装自定义 `lsd.jxe`。写系统分区且在 SD 备份，运行前可额外手动保存 `lsd.jxe`。需备份。
- **`privacy_shadow.sh`**：用 `/Custom/Shadowfile/shadow` 覆盖 shadow 密码文件。高风险，会修改认证配置；SD 会保存备份。需备份并确保供电。
- **`import_hosts.sh`**：从 `/Custom/Hosts/hosts` 覆盖 hosts 文件，写系统分区并自动备份到 SD。建议先确认文件格式。需备份。
- **`import_pf.sh`**：从 `/Custom/pf.conf/pf.conf` 更新防火墙配置，写系统分区并备份到 SD。需备份。
- **`flash_ifs.sh`**：从 `/Custom/IFS/ifs-root.ifs` 重新刷写 ifsroot。高风险，会写闪存且脚本提示禁止断电；执行前务必确保 SD 卡在位并保持供电稳定。推荐提前运行 `dump_ifs.sh` 及 `dump_eeprom.sh` 作为备份。需断电保护、需备份。
- **`sshd_install.sh`**：启用 SSHD 服务（可使用 SD 根目录的 `id_rsa.pub` 配置免密登录）。写系统分区配置并创建备份。建议先备份 `/var/etc/ssh` 相关配置。
- **`install_java_logging.sh`** / **`uninstall_java_logging.sh`**：开启或关闭 Java/HMI 日志到 SD1。会修改日志配置文件并写 SD；启用前确认 SD 有充足空间，建议备份配置文件（脚本已写入 SD 备份）。

## Customization → AndroidAuto

- **`patch_gal.sh`**：修改 `gal.json` 以允许第三方 Android Auto 应用。输入 `/Custom/AndroidAuto/gal.json`（若存在）或当前系统配置，输出至系统分区并在 SD 备份。高风险更改通信配置，运行前备份原始文件（`dump_androidAuto.sh`）。需备份。
- **`recovery_aapatch.sh`**：恢复原版 `gal.json`。读取 SD 备份或原系统副本，写回系统。确保 SD 上存在备份。

## Customization → Navigation

- **`import_mapstyles.sh`**：从 `/Custom/MapStyles` 导入地图样式（需配合具体品牌/地区包）。写系统分区，建议先运行 `dump_mapstyles.sh` 备份。需备份。
- **`patch_mapstylestoSD_*.sh`（AU/VW/SK/SE/BY/PO）**：将地图样式重定向到 SD 卡特定子目录，减少内部存储占用。会修改导航配置并依赖 SD 可写。执行前备份导航配置与现有样式（`dump_mapstyles.sh`），执行后需确保 SD 持续插入。
- **`install_nav_active_ignore.sh` / `uninstall_nav_active_ignore.sh`**：切换导航激活检查补丁。写入导航进程配置，建议先备份相关配置（`dump_pf.sh`、`dump_persistence.sh`）。需备份。

## Customization → Privacy

- **`privacy_cleanhistory.sh`**：清理隐私记录（调用清除历史的系统命令）。主要删除用户数据，不写系统分区。建议在 SD 上保留必要数据后执行。
- **`privacy_shadow.sh`**：同 Advanced 段，覆盖 shadow，风险和备份要求相同。

## Customization → Sounds

- **`install_ringtones.sh`**：从 `/Custom/Ringtones` 安装电话铃声。写入音频资源并备份到 SD。建议先运行 `dump_ringtones.sh`。需备份。
- **`install_systemsounds.sh`**：从 `/Custom/SystemSounds` 更新系统提示音，写入系统分区并自动备份。需备份。

## Customization → Skin

- **`install_skins_VW_SK_SE.sh`** / **`install_skin_AU_PO_BE_LA.sh`** / **`install_skin_car_AU_PO_BE_LA.sh`**：按品牌/车型从 `/Custom/SkinFiles` 安装皮肤 `images.mcf`。写系统分区并在 SD 上生成备份目录。高风险（图形资源损坏会导致界面异常），建议先运行对应 `dump_skins.sh`。需备份。
- **`recovery_skins.sh`**：用 SD 备份恢复原皮肤。需确保 SD 上存在备份。无额外写系统以外的存储。
- **`util_reboot.sh`**：重启设备以应用皮肤更改。仅触发重启，无存储写入。

## Customization → Language

- **`install_language_VW_SK_SE.sh`**：从 `/Custom/Language` 导入语言包。写系统语言数据并备份到 SD。需备份。
- **`recovery_language.sh`**：从 SD 备份恢复语言文件。需确保备份存在。

## Customization → Display

- **`info_displaymanager.sh`**：显示显示管理器信息，无写入操作。

## Customization → Various

- **`import_gracenote.sh`**：从 `/Custom/Gracenote` 导入数据库，写系统分区并备份。数据量大，确保 SD 空间充足。需备份。
- **`patch_googleearth.sh`**：修改 Google Earth 相关配置。写系统分区，建议事先备份相关文件（`dump_pf.sh`/`dump_hosts.sh`）。需备份。
- **`patch_menumode.sh`**：切换菜单模式。写系统配置，建议先备份受影响文件（`dump_engdefs.sh`）。需备份。
- **`install_rsdb.sh`**：安装 RSDB 数据，写系统分区并备份。需备份。
- **`set_nosslcheck.sh` / `unset_nosslcheck.sh`**：启用或关闭 SSL 校验跳过。写配置文件，建议备份 `/etc/ssl` 相关配置。需备份。
- **`set_DataOverDLink.sh` / `set_DataOverSIM.sh`**：切换数据出口到 D-Link 网卡或内置 SIM。写网络配置，建议先备份并确保对应硬件已连接（`ifconfig -a` 查看接口）。需备份。
- **`util_showOnlineRouterStatus.sh`**：显示在线路由状态，不修改存储。

## Customization → VIM（视频播放限制）

- **`patch_vim199.sh`** / **`patch_vim06.sh`**：应用不同版本的视频行车限制补丁。写系统安全配置，执行前备份相关模块（`dump_engdefs.sh`）。需备份。

### VIM 高级

- **`patch_vim_advanced.sh`**：高级 VIM 补丁脚本，允许更多定制。写系统安全配置，强烈建议事先备份受影响文件并在稳定供电下操作。需备份、需断电保护。

## Customization → AndroidAuto（补充）

已在上方列出 `patch_gal.sh` 与 `recovery_aapatch.sh`；其余 Android Auto 相关配置建议在运行前确认手机与车机兼容。

## Customization → GreenMenu

- **`install_esd.sh`**：从 `/Custom/GreenMenu` 导入新的 ESD 屏幕定义到 `/eso/hmi/engdefs`。写系统分区并在 SD 建立备份，建议先运行 `dump_engdefs.sh`。需备份。

## Customization → Startup

- **`install_canim.sh`**：从 `/Custom/Startup` 安装启动动画 (`*.canim`)。写系统分区并备份到 SD。建议先 `dump_splashscreen.sh`，并确保 SD 可写。需备份。
- **`install_forcedcanim.sh`**：与前者类似但强制覆盖所有品牌动画。风险更高，需备份且保持供电。

## Customization → Sounds（系统提示）

已列出安装脚本；对应卸载/恢复使用 `dump_systemSounds.sh` 备份后手动回写。

## AndroidAuto（主类目）

参见上文 Customization → AndroidAuto。

## Dump

所有 Dump 脚本均以 SD 卡为输出，不写系统分区；需要 SD 卡可写空间。

- **`dump_all.sh`**：批量执行各类 dump，输出到 SD（含皮肤、音频、数据库、配置等）。
- **图形类**：`dump_skins.sh`、`dump_splashscreen.sh`、`dump_mapstyles.sh`。
- **声音类**：`dump_systemSounds.sh`、`dump_ringtones.sh`、`dump_tts.sh`。
- **数据库类**：`dump_radiostation.sh`、`dump_gracenote.sh`。
- **系统类**：`dump_androidAuto.sh`、`dump_storage.sh`（生成 storage1/2.raw，大体积）、`dump_eeprom.sh`、`dump_fec.sh`、`dump_hosts.sh`、`dump_ifs.sh`、`dump_shadow.sh`、`dump_persistence.sh`。
- **开发/资源类**：`dump_lsdjxe.sh`、`dump_gem.sh`、`dump_bundles.sh`、`dump_engdefs.sh`、`dump_ipod.sh`、`dump_pf.sh`。

## MIB Information → Password

- **`find_password.sh`**：查找/显示设备密码。只读操作，无存储写入。

## Display

- **`info_displaymanager.sh`**：与 Display 分类一致，仅信息查询。

## Privacy

- **`privacy_cleanhistory.sh`**、**`privacy_shadow.sh`**：见上文。

## Sounds

- **`install_ringtones.sh`**、**`install_systemsounds.sh`**：见上文。

## Startup

- **`install_canim.sh`**、**`install_forcedcanim.sh`**：见上文。

## Updates

- **`set_skipMostPopup.sh` / `unset_skipMostPopup.sh`**：开启或关闭 SWDL 自定义升级模式提示。写系统更新配置，建议先备份相关文件（`dump_engdefs.sh`）。需备份。

## Uninstall

- **`util_clean_old.sh`**：清理旧版本残留。写系统分区，建议先备份 `/eso/hmi/engdefs` 与 `/net/mmx/mnt` 中 Toolbox 目录。需备份。
- **`util_clean.sh`**：执行当前 Toolbox 清理，移除定制文件。写系统分区，建议提前运行 `dump_*` 系列以保存数据。需备份。
- **`util_uninstall.sh`**：卸载 Toolbox 并恢复系统脚本。高风险操作，写系统分区，建议确保 SD 上已有完整备份并在稳定供电环境下运行。需备份、需断电保护。

## Utilities（共享工具脚本）

以下脚本通常被其他脚本调用，不直接在 Green Menu 中呈现，但在排错时可参考：

- **`util_mountsd.sh`**：检测并可写挂载含 Toolbox 的 SD 卡。
- **`util_mountsys.sh` / `util_unmountsys.sh`**：以读写或只读方式挂载系统分区。
- **`util_backup.sh`**：基于 `TOPIC`、`MIBPATH`、`SDPATH` 等环境变量创建 SD 备份目录并复制源文件/目录。
- **`util_copy.sh`**：将 SD 上的自定义文件复制到目标路径后重新挂载系统为只读。
- **`util_dump.sh`**、**`util_crc16.sh`**：通用 dump/校验工具，被各 dump 脚本复用。
- **`util_clean.sh`、`util_clean_old.sh`、`util_uninstall.sh`**：卸载相关辅助。
- **`util_info.sh`**：输出版本、品牌等信息供日志使用。
- **`util_reboot.sh`**、**`util_mountsd.sh`**、**`util_unmountsys.sh`** 等：执行重启或挂载操作。
- **`util_showOnlineRouterStatus.sh`**：网络状态检查。

