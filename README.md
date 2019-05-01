<h1><img src="https://cdn.rawgit.com/herrbischoff/awesome-macos-command-line/cab824f0/assets/logo.svg" alt="Awesome macOS Command Line" width="600"></h1>

> 精心为 OS X 挑选的 shell 命令和工具。
>
> _“You don’t have to know everything. You simply need to know where to find it when necessary.” (John Brunner)_

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![Build Status](https://travis-ci.org/herrbischoff/awesome-macos-command-line.svg?branch=master)](https://travis-ci.org/herrbischoff/awesome-macos-command-line)

更多好用的终端工具，请参阅姐妹项目 [Awesome Command Line Apps](https://github.com/herrbischoff/awesome-command-line-apps)。

[English]([README.md](https://github.com/herrbischoff/awesome-macos-command-line)) | 中文

## Caffeinating

When you find something helpful in here, you could buy me a coffee. I spend a lot of time and effort on curating this list. Keeping me properly caffeinated accelerates things. And it would really make my day. Kindness of strangers and all that. If you can't or won't, no hard feelings. It's available completely free for a reason. Still, it would be awesome.

Patreon: https://www.patreon.com/herrbischoff

## 目录

- [外形](#外形)
    - [透明度](#透明度)
    - [桌面背景](#桌面背景)
- [Applications](#applications)
    - [App Store](#app-store)
    - [Apple Remote Desktop](#apple-remote-desktop)
    - [Contacts](#contacts)
    - [Google](#google)
    - [iTunes](#itunes)
    - [Mail](#mail)
    - [Safari](#safari)
    - [Sketch](#sketch)
    - [Skim](#skim)
    - [Terminal](#terminal)
    - [TextEdit](#textedit)
    - [Visual Studio Code](#visual-studio-code)
- [Backup](#backup)
    - [Time Machine](#time-machine)
- [Developer](#developer)
    - [Vim](#vim)
    - [Xcode](#xcode)
- [Dock](#dock)
- [Documents](#documents)
- [Files, Disks and Volumes](#files-disks-and-volumes)
    - [APFS](#apfs)
    - [Disk Images](#disk-images)
- [Finder](#finder)
    - [Desktop](#desktop)
    - [Files and Folders](#files-and-folders)
    - [Layout](#layout)
    - [Metadata Files](#metadata-files)
    - [Opening Things](#opening-things)
- [Fonts](#fonts)
- [Functions](#functions)
- [Hardware](#hardware)
    - [Bluetooth](#bluetooth)
    - [Harddisks](#harddisks)
    - [Hardware Information](#hardware-information)
    - [Infrared Receiver](#infrared-receiver)
    - [Power Management](#power-management)
- [Input Devices](#input-devices)
    - [Keyboard](#keyboard)
- [Launchpad](#launchpad)
- [Media](#media)
    - [Audio](#audio)
    - [Video](#video)
- [Networking](#networking)
    - [Bonjour](#bonjour)
    - [DHCP](#dhcp)
    - [DNS](#dns)
    - [Hostname](#hostname)
    - [Network Preferences](#network-preferences)
    - [Networking Tools](#networking-tools)
    - [SSH](#ssh)
    - [TCP/IP](#tcpip)
    - [TFTP](#tftp)
    - [Wi-Fi](#wi-fi)
- [Package Managers](#package-managers)
- [Printing](#printing)
- [Security](#security)
    - [Application Firewall](#application-firewall)
    - [Gatekeeper](#gatekeeper)
    - [Passwords](#passwords)
    - [Physical Access](#physical-access)
    - [Wiping Data](#wiping-data)
- [Search](#search)
    - [Find](#find)
    - [Locate](#locate)
- [System](#system)
    - [AirDrop](#airdrop)
    - [AppleScript](#applescript)
    - [Basics](#basics)
    - [Clipboard](#clipboard)
	- [Date and Time](#date-and-time)
    - [FileVault](#filevault)
    - [Information/Reports](#informationreports)
    - [Install OS](#install-os)
    - [Kernel Extensions](#kernel-extensions)
    - [LaunchAgents](#launchagents)
    - [LaunchServices](#launchservices)
    - [Login Window](#login-window)
    - [Memory Management](#memory-management)
    - [Notification Center](#notification-center)
    - [QuickLook](#quicklook)
    - [Remote Apple Events](#remote-apple-events)
    - [Root User](#root-user)
    - [Safe Mode Boot](#safe-mode-boot)
    - [Screenshots](#screenshots)
    - [Software Installation](#software-installation)
    - [Software Update](#software-update)
    - [Software Version](#software-version)
    - [Spotlight](#spotlight)
    - [System Integrity Protection](#system-integrity-protection)
- [Terminal](#terminal)
    - [Alternative Terminals](#alternative-terminals)
    - [Shells](#shells)
    - [Terminal Fonts](#terminal-fonts)
- [Glossary](#glossary)
    - [Mac OS X, OS X, and macOS Version Information](#mac-os-x-os-x-and-macos-version-information)


## 外形

### 透明度

#### 菜单和窗口的透明度设置

```bash
# 减小透明度
defaults write com.apple.universalaccess reduceTransparency -bool true

# 恢复默认透明度
defaults write com.apple.universalaccess reduceTransparency -bool false
```


### 桌面背景

#### 设置桌面背景

```bash
# Up to Mountain Lion
osascript -e 'tell application "Finder" to set desktop picture to POSIX file "/path/to/picture.jpg"'

# Since Mavericks
sqlite3 ~/Library/Application\ Support/Dock/desktoppicture.db "update data set value = '/path/to/picture.jpg'" && killall Dock
```


## 应用

### App Store

#### 列出所有从 App Store 下载的应用

```bash
# 通过 find
find /Applications -path '*Contents/_MASReceipt/receipt' -maxdepth 4 -print |\sed 's#.app/Contents/_MASReceipt/receipt#.app#g; s#/Applications/##'

# 通过 Spotlight
mdfind kMDItemAppStoreHasReceipt=1
```

#### 显示调试菜单

Works up to Yosemite.
```bash
# 开启
defaults write com.apple.appstore ShowDebugMenu -bool true

# 关闭 (默认)
defaults write com.apple.appstore ShowDebugMenu -bool false
```


### 苹果远程桌面

#### 唤醒手册
```bash
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -help
```

#### 唤醒和睡眠 ARD Agent 和 Helper
```bash
# 激活并且重启 ARD Agent 和 Helper
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -restart -agent -console

# 睡眠并且停止远程管理服务
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -stop
```

#### 开启和关闭远程桌面共享
```bash
# 给予所有用户完全的接入权限
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -configure -allowAccessFor -allUsers -privs -all

# 关闭 ARD Agent 和删除所有用户的接入权限
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -configure -access -off
```

#### 删除苹果远程桌面设置
```bash
sudo rm -rf /var/db/RemoteManagement ; \
sudo defaults delete /Library/Preferences/com.apple.RemoteDesktop.plist ; \
defaults delete ~/Library/Preferences/com.apple.RemoteDesktop.plist ; \
sudo rm -r /Library/Application\ Support/Apple/Remote\ Desktop/ ; \
rm -r ~/Library/Application\ Support/Remote\ Desktop/ ; \
rm -r ~/Library/Containers/com.apple.RemoteDesktop
```

### 交流

#### 调试模式
```bash
# 开启
defaults write com.apple.addressbook ABShowDebugMenu -bool true

# 关闭 (默认)
defaults write com.apple.addressbook ABShowDebugMenu -bool false
```

### Google

#### 卸载 Google 更新
```bash
~/Library/Google/GoogleSoftwareUpdate/GoogleSoftwareUpdate.bundle/Contents/Resources/ksinstall --nuke
```

### iTunes

#### 键盘媒体健
This works up to Yosemite. System Integrity Protection was introduced in El Capitan which prevents system Launch Agents from being unloaded.
```bash
# 停止响应按键
launchctl unload -w /System/Library/LaunchAgents/com.apple.rcd.plist

# 响应按键 (默认)
launchctl load -w /System/Library/LaunchAgents/com.apple.rcd.plist
```

From El Capitan onwards, you can either disable SIP or resort to a kind of hack, which will make iTunes inaccessible to any user, effectively preventing it from starting itself or its helpers. Be aware that for all intents and purposes this will trash your iTunes installation and may conflict with OS updates down the road.
```bash
sudo chmod 0000 /Applications/iTunes.app
```

### 邮件

#### 将附件显示为图标

```bash
defaults write com.apple.mail DisableInlineAttachmentViewing -bool yes
```

#### 真空邮件索引
The AppleScript code below will quit Mail, vacuum the SQLite index, then re-open Mail. On a large email database that hasn't been optimized for a while, this can provide significant improvements in responsiveness and speed.
```applescript
(*
Speed up Mail.app by vacuuming the Envelope Index
Code from: http://web.archive.org/web/20071008123746/http://www.hawkwings.net/2007/03/03/scripts-to-automate-the-mailapp-envelope-speed-trick/
Originally by "pmbuko" with modifications by Romulo
Updated by Brett Terpstra 2012
Updated by Mathias Törnblom 2015 to support V3 in El Capitan and still keep backwards compatibility
Updated by Andrei Miclaus 2017 to support V4 in Sierra
*)

tell application "Mail" to quit
set os_version to do shell script "sw_vers -productVersion"
set mail_version to "V2"
considering numeric strings
    if "10.10" <= os_version then set mail_version to "V3"
    if "10.12" <= os_version then set mail_version to "V4"
    if "10.13" <= os_version then set mail_version to "V5"
    if "10.14" <= os_version then set mail_version to "V6"
end considering

set sizeBefore to do shell script "ls -lnah ~/Library/Mail/" & mail_version & "/MailData | grep -E 'Envelope Index$' | awk {'print $5'}"
do shell script "/usr/bin/sqlite3 ~/Library/Mail/" & mail_version & "/MailData/Envelope\\ Index vacuum"

set sizeAfter to do shell script "ls -lnah ~/Library/Mail/" & mail_version & "/MailData | grep -E 'Envelope Index$' | awk {'print $5'}"

display dialog ("Mail index before: " & sizeBefore & return & "Mail index after: " & sizeAfter & return & return & "Enjoy the new speed!")

tell application "Mail" to activate
```

### Safari

#### 改变默认字体
```bash
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2StandardFontFamily Georgia
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DefaultFontSize 16
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2FixedFontFamily Menlo
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DefaultFixedFontSize 14
```

#### 开启开发者菜单以及网络检查
```bash
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true && \
defaults write com.apple.Safari IncludeDevelopMenu -bool true && \
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true && \
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true && \
defaults write -g WebKitDeveloperExtras -bool true
```

#### 获取当前网页数据
其他选项: `get source`, `get text`.
```bash
osascript -e 'tell application "Safari" to get URL of current tab of front window'
```

#### 使用 Backspace/Delete 返回上一页
```bash
# 开启
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2BackspaceKeyNavigationEnabled -bool YES

# 关闭
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2BackspaceKeyNavigationEnabled -bool NO
```

### Sketch

#### 导出压缩 SVG
```bash
defaults write com.bohemiancoding.sketch3 exportCompactSVG -bool yes
```

### Skim

#### 关闭自动加载弹窗
去掉弹窗并设置默认自动加载

```bash
defaults write -app Skim SKAutoReloadFileUpdate -boolean true
```
### 终端

#### 焦点跟随鼠标
```bash
# 开启
defaults write com.apple.Terminal FocusFollowsMouse -string YES

# 关闭
defaults write com.apple.Terminal FocusFollowsMouse -string NO
```

### 文本编辑

#### 将文本编辑设置为纯文本的默认打开方式 Use Plain Text Mode as Default
```bash
defaults write com.apple.TextEdit RichText -int 0
```

### Visual Studio Code

#### 解决 VSCode Vim 按键重复
```bash
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
```

## 备份

### 时间机器

#### 改变备份间隔
备份间隔改为30分钟，单位是秒。
```bash
sudo defaults write /System/Library/LaunchDaemons/com.apple.backupd-auto StartInterval -int 1800
```

#### 本地备份
本地备份时，时间机器备份卷不可用。
```bash
# 查看状态
defaults read /Library/Preferences/com.apple.TimeMachine MobileBackups

# 开启 (默认)
sudo tmutil enablelocal

# 关闭
sudo tmutil disablelocal
```

Since High Sierra, you cannot disable local snapshots. Time Machine now always creates a local APFS snapshot and uses that snapshot as the data source to create a regular backup, rather than using the live disk as the source, as is the case with HFS formatted disks.

#### 防止时间机器提示将新的硬盘启动器作为本分卷
```bash
sudo defaults write /Library/Preferences/com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true
```

#### 显示时间机器的日志
这个脚本将输出过去12个小时时间机器的备份活动。
```bash
#!/bin/sh

filter='processImagePath contains "backupd" and subsystem beginswith "com.apple.TimeMachine"'

# show the last 12 hours
start="$(date -j -v-12H +'%Y-%m-%d %H:%M:%S')"

echo ""
echo "[History (from $start)]"
echo ""

log show --style syslog --info --start "$start" --predicate "$filter"

echo ""
echo "[Following]"
echo ""

log stream --style syslog --info --predicate "$filter"
```

#### 充电时切换备份
```bash
# 查看状态
sudo defaults read /Library/Preferences/com.apple.TimeMachine RequiresACPower

# 开启 (默认)
sudo defaults write /Library/Preferences/com.apple.TimeMachine RequiresACPower -bool true

# 关闭
sudo defaults write /Library/Preferences/com.apple.TimeMachine RequiresACPower -bool false
```

#### 验证备份
Beginning in OS X 10.11, Time Machine records checksums of files copied into snapshots. Checksums are not retroactively computed for files that were copied by earlier releases of OS X.
```bash
sudo tmutil verifychecksums /path/to/backup
```

## 开发这

### Vim

#### 编译 Sane Vim
通过 Homebrew 编译出完整 Mac Vim，包括覆盖系统的 Vim。
```bash
brew install macvim --HEAD --with-cscope --with-lua --with-override-system-vim --with-luajit --with-python
```

#### Neovim
通过 Homebrew 安装现代化的 Vim 替代品。
```bash
brew install neovim
```

### Xcode

#### 安装没有命令行工具的 Xcode
```bash
xcode-select --install
```

#### 删除所有不可用的模拟器
```bash
xcrun simctl delete unavailable
```

## 程序坞

#### 将最近使用的程序添加到程序坞
```bash
defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }' && \
killall Dock
```

#### 添加间隔符的无名文件夹
```bash
defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = {}; "tile-type"="small-spacer-tile"; }' && \
killall Dock
```

#### 添加空格
```bash
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}' && \
killall Dock
```

#### 添加小空格
```bash
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="small-spacer-tile";}' && \
killall Dock
```

#### 根据用户最近的使用自动重排
```bash
# 开启 (默认)
defaults write com.apple.dock mru-spaces -bool true && \
killall Dock

# 关闭
defaults write com.apple.dock mru-spaces -bool false && \
killall Dock
```

#### 图标弹跳
全局设置当唤醒应用时，是否弹跳图标。

```bash
# 开启 (默认)
defaults write com.apple.dock no-bouncing -bool true && \
killall Dock

# 关闭
defaults write com.apple.dock no-bouncing -bool false && \
killall Dock
```

#### 锁住程序坞大小
```bash
# 开启
defaults write com.apple.Dock size-immutable -bool yes && \
killall Dock

# 关闭 (默认)
defaults write com.apple.Dock size-immutable -bool no && \
killall Dock
```

#### 重置程序坞
```bash
defaults delete com.apple.dock && \
killall Dock
```

#### 改变程序坞大小
完全改变程序坞主体大小。要调整大小，将 **0** 改为整数

```bash
defaults write com.apple.dock tilesize -int 0 && \
killall Dock
```

#### 滚动手势
Use your touchpad or mouse scroll wheel to interact with Dock items. Allows you to use an upward scrolling gesture to open stacks. Using the same gesture on applications that are running invokes Exposé/Mission Control.
```bash
# Enable
defaults write com.apple.dock scroll-to-open -bool true && \
killall Dock

# Disable (Default)
defaults write com.apple.dock scroll-to-open -bool false && \
killall Dock
```

#### 启用自动掩藏

``` bash
defaults write com.apple.dock autohide -bool true && \
killall Dock
```

#### 设置自动显示和掩藏的延迟时间
浮点数定义了显示和掩藏的延迟时间(单位毫秒)。
```bash
defaults write com.apple.dock autohide-time-modifier -float 0.4 && \
defaults write com.apple.dock autohide-delay -float 0 && \
killall Dock
```

#### 显示掩藏 APP 的图标
```bash
# 开启
defaults write com.apple.dock showhidden -bool true && \
killall Dock

# 关闭 (默认)
defaults write com.apple.dock showhidden -bool false && \
killall Dock
```

####  仅显示启动的应用程序图标
```bash
# 开启
defaults write com.apple.dock static-only -bool true && \
killall Dock

# 关闭 (默认)
defaults write com.apple.dock static-only -bool false && \
killall Dock
```

## 文档

#### 将文件转换为 HTML
支持的格式有纯文本、富文本(rtf)以及微软的 Word(doc/docx)。
```bash
textutil -convert html file.ext
```

## 文件、磁盘和卷

#### 创建一个空文件
创建一个 10 GB 的空文件。
```bash
mkfile 10g /path/to/file
```

#### 禁止突发动作感应
当你使用的是 SSD 时，这个设置是无用的。
```bash
sudo pmset -a sms 0
```

#### 弹出所有可安装的卷
唯一可以向访达发送 AppleScript 命令的方法。
```bash
osascript -e 'tell application "Finder" to eject (every disk whose ejectable is true)'
```

#### 修复文件权限
你可以不依赖图形化磁盘工具修复文件权限
```bash
sudo diskutil repairPermissions /
```
> Beginning with OS X El Capitan, system file permissions are automatically protected. It's no longer necessary to verify or repair permissions with Disk Utility. ([Source](https://support.apple.com/en-us/HT201560))

#### 设置启动卷
```bash
# Up to Yosemite
bless --mount "/path/to/mounted/volume" --setBoot

# From El Capitan
sudo systemsetup -setstartupdisk /System/Library/CoreServices
```

#### 示所有附加的磁盘和分区
```bash
diskutil list
```

#### 查看文件系统的使用率

连续显示文件使用信息。
```bash
sudo fs_usage
```
### APFS

Available since High Sierra. There is no central utility and usage is inconsistent as most functionality is rolled into `tmutil`.

#### Convert Volume from HFS+ to APFS
```bash
/System/Library/Filesystems/apfs.fs/Contents/Resources/hfs_convert /path/to/file/system
```

#### 创建新的 APFS 文件系统
```bash
/System/Library/Filesystems/apfs.fs/Contents/Resources/newfs_apfs /path/to/device
```

#### 创建快照
```bash
tmutil localsnapshot
```

#### 删除快照
```bash
tmutil deletelocalsnapshots com.apple.TimeMachine.2018-01-26-044042
````

#### 列出所有快照

```bash
tmutil listlocalsnapshots /
```

#### 挂载快照
快照是只读的。
```bash
mkdir ~/mnt
/System/Library/Filesystems/apfs.fs/Contents/Resources/mount_apfs -s com.apple.TimeMachine.2018-01-26-044042 / ~/mnt
```

### 磁盘映像

#### 从文件内容创建磁盘映像

将安装的应用程序转换为二进制包。
```bash
hdiutil create -volname "Volume Name" -srcfolder /path/to/folder -ov diskimage.dmg
```
如果你想加密磁盘映像：
```bash
hdiutil create -encryption -stdinpass -volname "Volume Name" -srcfolder /path/to/folder -ov encrypted.dmg
```
打包前，你要输入密码。为了直接输入密码不弹窗：
```bash
echo -n YourPassword | hdiutil create -encryption -stdinpass -volname "Volume Name" -srcfolder /path/to/folder -ov encrypted.dmg
```

#### 将磁盘映像刻录为 DVD
这个命令可以应用在 .iso 、.img 和 .dmg 文件上。
```bash
hdiutil burn /path/to/image_file
```

#### 禁止磁盘映像验证
```bash
defaults write com.apple.frameworks.diskimages skip-verify -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true
```

#### 制作 OS X 启动卷
```bash
bless --folder "/path/to/mounted/volume/System/Library/CoreServices" --bootinfo --bootefi
```

#### 挂载磁盘映像
```bash
hdiutil attach /path/to/diskimage.dmg
```

#### 卸载磁盘映像
```bash
hdiutil detach /dev/disk2s1
```

#### 将磁盘映像写入到卷中
就像磁盘工具的恢复功能。
```bash
sudo asr -restore -noverify -source /path/to/diskimage.dmg -target /Volumes/VolumeToRestoreTo
```


## 访达

### 桌面

#### 显示外部媒体
外部的 HDs 、thumb drives 等等。
```bash
# 开启
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true && \
killall Finder

# 关闭 (默认)
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool false && \
killall Finder
```

#### 显示内部媒体
自建的 HDs 或者 SSDs。
```bash
# 开启
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true && \
killall Finder

# 关闭 (默认)
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool false && \
killall Finder
```

#### 显示可移动媒体

CDs 、DVDs 、iPods 等等。
```bash
# 开启
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true && \
killall Finder

# 关闭 (默认)
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool false && \
killall Finder
```

#### 显示网络卷

AFP 、SMB、 NFS、 WebDAV 等等。
```bash
# 开启
defaults write com.apple.finder ShowMountedServersOnDesktop -bool true && \
killall Finder

# 关闭 (默认)
defaults write com.apple.finder ShowMountedServersOnDesktop -bool false && \
killall Finder
```

### 文件和文件夹

#### 清除所有访问控制列表(ACLs)
```bash
sudo chmod -RN /path/to/folder
```

#### 在访达掩藏文件夹
```bash
chflags hidden /path/to/folder/
```
#### 显示所有文件的扩展名
```bash
defaults write -g AppleShowAllExtensions -bool true
```

#### 显示掩藏文件
```bash
# 显示所有
defaults write com.apple.finder AppleShowAllFiles true

# 恢复文件的默认显示
defaults write com.apple.finder AppleShowAllFiles false
```

#### 删除保护标签
```bash
sudo chflags -R nouchg /path/to/file/or/folder
```

#### 在访达中显示全路径
```bash
defaults write com.apple.finder _FXShowPosixPathInTitle -bool true
```

#### 取消隐藏用户文件夹
```bash
chflags nohidden ~/Library
```

#### 增加最近访问文件数量
```bash
defaults write -g NSNavRecentPlacesLimit -int 10 && \
killall Finder
```

### 布局

#### 显示退出访达按钮
显示 退出访达的默认快捷键是 <kbd>Cmd</kbd> + <kbd>Q</kbd> 。

```bash
# 开启
defaults write com.apple.finder QuitMenuItem -bool true && \
killall Finder

# 关闭 (默认)
defaults write com.apple.finder QuitMenuItem -bool false && \
killall Finder
```

#### 平滑滚动
对旧 Mac 会弄乱动画很有用。
```bash
# 开启
defaults write -g NSScrollAnimationEnabled -bool false

# 关闭 (默认)
defaults write -g NSScrollAnimationEnabled -bool true
```

#### 橡皮筋滚动
```bash
# 禁止
defaults write -g NSScrollViewRubberbanding -bool false

# 关闭 (默认)
defaults write -g NSScrollViewRubberbanding -bool true
```

#### 展开默认保存面板
```bash
defaults write -g NSNavPanelExpandedStateForSaveMode -bool true && \
defaults write -g NSNavPanelExpandedStateForSaveMode2 -bool true
```

#### 桌面图标可见性
```bash
# 掩藏图标
defaults write com.apple.finder CreateDesktop -bool false && \
killall Finder

# 显示图标(默认)
defaults write com.apple.finder CreateDesktop -bool true && \
killall Finder
```

#### 路径栏
```bash
# 显示
defaults write com.apple.finder ShowPathbar -bool true

# 掩藏 (默认)
defaults write com.apple.finder ShowPathbar -bool false
```

#### 滚动条可见性
Possible values: `WhenScrolling`, `Automatic` and `Always`.
```bash
defaults write -g AppleShowScrollBars -string "Always"
```

#### 状态栏
```bash
# 显示
defaults write com.apple.finder ShowStatusBar -bool true

# 掩藏 (默认)
defaults write com.apple.finder ShowStatusBar -bool false
```

#### 默认保存到磁盘
设置默认保存地址是本地磁盘，而不是 iCloud 。
```bash
defaults write -g NSDocumentSaveNewDocumentsToCloud -bool false
```

#### 当当前文件夹设置为默认搜索范围
```bash
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"
```

#### 设置访达的默认文件夹
```bash
defaults write com.apple.finder NewWindowTarget -string "PfLo" && \
defaults write com.apple.finder NewWindowTargetPath -string "file://${HOME}"
```

#### 设置侧边栏图标大小
将大小设置为中等大小。
```bash
defaults write -g NSTableViewDefaultSizeMode -int 2
```

### 元数据文件

#### 禁止在网络卷创建元数据文件
避免创建 `.DS_Store` 以及 AppleDouble 文件。
```bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```

#### 禁止在 USB 卷创建元数据文件
避免创建 `.DS_Store` 以及 AppleDouble 文件。
```bash
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
```

### 打开文件

#### 改变访达的工作文件夹
如果同时打开了多个窗口，选择最上面。
```bash
cd "$(osascript -e 'tell app "Finder" to POSIX path of (insertion location as alias)')"
```

#### 打开 URL
```bash
open https://github.com
```

#### 打开文件
```bash
open README.md
```

#### 打开应用程序
你可以加上 `-a` 打开应用程序。
```bash
open -a "Google Chrome" https://github.com
```

#### 打开文件夹
```bash
open /path/to/folder/
```

#### 打开当前文件夹
```bash
open .
```

## 字体

#### 清空当前用户字体缓存
为了清除所有用户的字体缓存，在命令前加上 `sudo`。
```bash
atsutil databases -removeUser && \
atsutil server -shutdown && \
atsutil server -ping
```

#### 获取 SF Mono 字体
你需要先下载和安装 Xcode 8 beta，之后所有应用都可以使用。
```bash
cp -v /Applications/Xcode-beta.app/Contents/SharedFrameworks/DVTKit.framework/Versions/A/Resources/Fonts/SFMono-* ~/Library/Fonts
```

对于 Sierra 之前的版本，它们包含 Terminal.app 中。
```bash
cp -v /Applications/Utilities/Terminal.app/Contents/Resources/Fonts/SFMono-* ~/Library/Fonts
```

## 函数

请看 [这个文件](functions.md).

## 硬件

### 蓝牙

```bash
# 查看状态
defaults read /Library/Preferences/com.apple.Bluetooth ControllerPowerState

# 开启 (默认)
sudo defaults write /Library/Preferences/com.apple.Bluetooth ControllerPowerState -int 1

# 禁止
sudo defaults write /Library/Preferences/com.apple.Bluetooth ControllerPowerState -int 0 && \
sudo killall -HUP blued
```

### 硬盘

#### 强制启用修剪
开启非苹果 SSD 的修剪。从 Yosemite 开始可用。
```bash
forcetrim
```

### 硬件信息

#### 列出所有硬件端口
```bash
networksetup -listallhardwareports
```

#### 剩余电池百分比
```bash
pmset -g batt | egrep "([0-9]+\%).*" -o --colour=auto | cut -f1 -d';'
```

#### 剩余电池时间
```bash
pmset -g batt | egrep "([0-9]+\%).*" -o --colour=auto | cut -f3 -d';'
```

#### 显示已连接设备的 UDID
```bash
system_profiler SPUSBDataType | sed -n -e '/iPad/,/Serial/p' -e '/iPhone/,/Serial/p'
```

#### 显示当前屏幕分辨率
```bash
system_profiler SPDisplaysDataType | grep Resolution
```

#### 显示 CPU 品牌信息
```bash
sysctl -n machdep.cpu.brand_string
```

### 红外接收器

```bash
# Status
defaults read /Library/Preferences/com.apple.driver.AppleIRController DeviceEnabled

# Enable (Default)
defaults write /Library/Preferences/com.apple.driver.AppleIRController DeviceEnabled -int 1

# Disable
defaults write /Library/Preferences/com.apple.driver.AppleIRController DeviceEnabled -int 0
```

### 电池管理

#### 禁止电脑休眠
Prevent sleep for 1 hour:
```bash
caffeinate -u -t 3600
```

#### 显示所有电池设置
```bash
sudo pmset -g
```

#### 15分钟无活动后显示器睡眠
```bash
sudo pmset displaysleep 15
```

#### 30分钟无活动后显示器睡眠
```bash
sudo pmset sleep 30
```

#### 检查系统睡眠剩余时间
```bash
sudo systemsetup -getcomputersleep
```

#### 将系统睡眠剩余时间设置为 60 分钟
```bash
sudo systemsetup -setcomputersleep 60
```

#### 完全关闭系统睡眠
```bash
sudo systemsetup -setcomputersleep Never
```

#### 系统冻结时自动重启
```bash
sudo systemsetup -setrestartfreeze on
```

#### 充电时显示铃声
当 MagSafe 连接时，播放 IOS 充电声音。
```bash
# 开启
defaults write com.apple.PowerChime ChimeOnAllHardware -bool true && \
open /System/Library/CoreServices/PowerChime.app

# 关闭 (默认)
defaults write com.apple.PowerChime ChimeOnAllHardware -bool false && \
killall PowerChime
```


## 输入设备

### 键盘

#### 自动纠正
```bash
# 禁止
defaults write -g NSAutomaticSpellingCorrectionEnabled -bool false

# 开启 (默认)
defaults write -g NSAutomaticSpellingCorrectionEnabled -bool true

# 显示状态
defaults read -g NSAutomaticSpellingCorrectionEnabled
```

#### 全键盘访问
对话框启用 Tab 。
```bash
#  仅限文本框和列表 (默认)
defaults write NSGlobalDomain AppleKeyboardUIMode -int 0

# 所有控件
defaults write NSGlobalDomain AppleKeyboardUIMode -int 3
```

#### 按键重复
禁止默认的 "press and hold" 行为。
```bash
# 开启按键重复
defaults write -g ApplePressAndHoldEnabled -bool false

# 禁止按键重复
defaults write -g ApplePressAndHoldEnabled -bool true
```

#### 按键重复频率
设置非常快的按键频率，根据个人品味调整。
```bash
defaults write -g KeyRepeat -int 0.02
```

## 启动台

#### 重设启动台布局
你需要重启程序坞，因为启动台与它紧密相连。
```bash
# Yosemite 之前的版本
rm ~/Library/Application\ Support/Dock/*.db && \
killall Dock

# El Capitan及以上的版本
defaults write com.apple.dock ResetLaunchPad -bool true && \
killall Dock
```

## 媒体

### 音频

#### 将音频文件转换为 iPhone 铃声。
```bash
afconvert input.mp3 ringtone.m4r -f m4af
```

#### 从文本创建音频书
使用 **Alex** 声音，将单纯的 UTF-8 文本文件转换为 AAC。
```bash
say -v Alex -f file.txt -o "output.m4a"
```

#### 开机禁用声音
```bash
sudo nvram SystemAudioVolume=" "
```

#### 静音音频输出
```bash
osascript -e 'set volume output muted true'
```

#### 设置音量
```bash
osascript -e 'set volume 4'
```

#### 播放音频文件
你可以播放所有 QuickTime 支持的音频格式。
```bash
afplay -q 1 filename.mp3
```

#### 使用系统默认声音讲述文本
```bash
say 'All your base are belong to us!'
```

### 视频

#### QuickTime 自动播放视频
```bash
defaults write com.apple.QuickTimePlayerX MGPlayMovieOnOpen 1
```


## 网络

### Bonjour

#### Bonjour 服务
```bash
# 禁止
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array-add "-NoMulticastAdvertisements"

# 开启 (默认)
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array "/usr/sbin/mDNSResponder" "-launchd"
```

### DHCP

#### 更新 DHCP 租约
```bash
sudo ipconfig set en0 DHCP
```

#### 显示 DHCP 信息
```bash
ipconfig getpacket en0
```

### DNS

#### 清除 DNS 缓存
```bash
sudo dscacheutil -flushcache && \
sudo killall -HUP mDNSResponder
```

### 域名

#### 设置电脑域名
```bash
sudo scutil --set ComputerName "newhostname" && \
sudo scutil --set HostName "newhostname" && \
sudo scutil --set LocalHostName "newhostname" && \
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.smb.server NetBIOSName -string "newhostname"
```

### 网络设置

#### 网络位置
在网络设置中切换网络位置。
```bash
# 查看状态
scselect

# 切换网络位置
scselect LocationNameFromStatus
```

#### 设置静态 IP 地址
```bash
networksetup -setmanual "Ethernet" 192.168.2.100 255.255.255.0 192.168.2.1
```

### 网络工具

#### 查看网络地址是否可以访问
```bash
ping -o github.com
```

#### 解决路由问题
```bash
traceroute github.com
```

### SSH

#### 将私钥密码永久添加到 SSH 代理
> Prior to macOS Sierra, ssh would present a dialog asking for your passphrase and would offer the option to store it into the keychain. This UI was deprecated some time ago and has been removed.
>
> Instead, a new UseKeychain option was introduced in macOS Sierra allowing users to specify whether they would like for the passphrase to be stored in the keychain. This option was enabled by default on macOS Sierra, which caused all passphrases to be stored in the keychain.
>
> This was not the intended default behavior, so this has been changed in macOS 10.12.2. ([Source](https://developer.apple.com/library/archive/technotes/tn2449/_index.html))
```bash
ssh-add -K /path/to/private_key
```
Then add to `~/.ssh/config`:
```bash
Host server.example.com
    IdentityFile /path/to/private_key
    UseKeychain yes
```

#### 远程登录
```bash
# 开启远程登录
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist

# 关闭远程登录
sudo launchctl unload -w /System/Library/LaunchDaemons/ssh.plist
```

### TCP/IP

#### 显示使用特定端口的应用程序
输出所有使用 80 端口的应用程序。
```bash
sudo lsof -i :80
```

#### 显示外部 IP 地址
仅当你的 ISP 没有替换 DNS 请求(一般不会)。
```bash
dig +short myip.opendns.com @resolver1.opendns.com
```
在所有网络中都可使用的替代方法。
```bash
curl -s https://api.ipify.org && echo
````

### TFTP

#### 启动原生的 TFTP Daemon
文件将从 `/private/tftpboot` 启动。
```bash
sudo launchctl load -F /System/Library/LaunchDaemons/tftp.plist && \
sudo launchctl start com.apple.tftpd
```

### Wi-Fi

#### 加入 Wi-Fi 网络
```bash
networksetup -setairportnetwork en0 WIFI_SSID WIFI_PASSWORD
```

#### 扫描可用的接入点
创建 airport 轻松接入的符号链接。
```bash
sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/local/bin/airport
```
运行无线扫描：
```bash
airport -s
```

#### 显示当前的 SSID
```bash
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}'
```

#### 显示本地 IP 地址
```bash
ipconfig getifaddr en0
```

#### 显示 Wi-Fi 的连接历史
```bash
defaults read /Library/Preferences/SystemConfiguration/com.apple.airport.preferences | grep LastConnected -A 7
```

#### 显示 Wi-Fi 网络密码

Exchange SSID with the SSID of the access point you wish to query the password from.
```bash
security find-generic-password -D "AirPort network password" -a "SSID" -gw
```

#### 开启 Wi-Fi 适配器
```bash
networksetup -setairportpower en0 on
```

## 包管理器

- [Fink](http://www.finkproject.org) - Unix 开源软件的全部 Darwin 世界，有点过时。
- [Homebrew](https://brew.sh) - OS X缺少的包管理器，最流行的选择。
- [MacPorts](https://www.macports.org) - Compile, install and upgrade either command-line, X11 or Aqua based open-source software. Very clean, it's what I use.


## 打印

#### 清除打印队列
```bash
cancel -a -
```

#### 默认展开打印面板
```bash
defaults write -g PMPrintingExpandedStateForPrint -bool true && \
defaults write -g PMPrintingExpandedStateForPrint2 -bool true
```

#### 打印完成后停止打印机
```bash
defaults write com.apple.print.PrintingPrefs "Quit When Finished" -bool true
```


## 安全

### 应用防火墙

#### 防火墙服务
```bash
# Show Status
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate

# Enable
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on

# Disable (Default)
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate off
```

#### 将应用添加到防火墙
```bash
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /path/to/file
```

### 网关

#### 添加网关异常
```bash
spctl --add /path/to/Application.app
```

#### 删除网关异常
```bash
spctl --remove /path/to/Application.app
```

#### 管理网关
```bash
# 查看状态
spctl --status

# 开启 (默认)
sudo spctl --master-enable

# 关闭
sudo spctl --master-disable
```

### 密码

#### 产生安全的密码并且复制到剪贴板
```bash
LC_ALL=C tr -dc "[:alnum:]" < /dev/urandom | head -c 20 | pbcopy
```

### 物理访问

#### 启动屏幕保护程序

```bash
# Sierra 之前
open /System/Library/Frameworks/ScreenSaver.framework/Versions/A/Resources/ScreenSaverEngine.app

# Sierra 之后
/System/Library/CoreServices/ScreenSaverEngine.app/Contents/MacOS/ScreenSaverEngine
```


#### 锁屏
```bash
/System/Library/CoreServices/Menu\ Extras/User.menu/Contents/Resources/CGSession -suspend
```

#### 屏幕锁定
```bash
# 查看状态
defaults read com.apple.screensaver askForPasswordDelay

# 开启 (默认)
defaults write com.apple.screensaver askForPasswordDelay -int 0

# 禁止 (Integer = 锁屏的延迟秒数)
defaults write com.apple.screensaver askForPasswordDelay -int 10
```

#### 屏幕保护密码
```bash
# 查看状态
defaults read com.apple.screensaver askForPassword

# 开启
defaults write com.apple.screensaver askForPassword -int 1

# 关闭 (默认)
defaults write com.apple.screensaver askForPassword -int 0
```

### 擦除数据

Note: The `srm` command appears to have been removed on MacOS after 10.9. There is a note on an [Apple support page](https://support.apple.com/en-us/HT201949) hinting as to why:
> With an SSD drive, Secure Erase and Erasing Free Space are not available in Disk Utility. These options are not needed for an SSD drive because a standard erase makes it difficult to recover data from an SSD.

#### 安全删除文件
```bash
srm /path/to/file
```

#### 安全删除文件夹
```bash
srm -r /path/to/folder/
```

#### 安全强制删除文件夹
```bash
srm -rf /path/to/complete/destruction
```


## 搜索

### 查找

#### 递归删除 .DS_Store 文件
```bash
find . -type f -name '*.DS_Store' -ls -delete
```

### 定位

#### 建立定位数据库
```bash
sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
```

#### 通过定位查询
`-i`修饰符意味着搜索对大小写敏感。
```bash
locate -i *.jpg
```


## 系统

### AirDrop

```bash
# 开启 AirDrop 在 Ethernet 以上版本 以及不支持 Mac 版本
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# 开启 (默认)
defaults remove com.apple.NetworkBrowser DisableAirDrop

# 关闭
defaults write com.apple.NetworkBrowser DisableAirDrop -bool YES
```

### AppleScript

#### 执行 AppleScript
```bash
osascript /path/to/script.scpt
```

### 基础

#### 比较两个文件夹
```bash
diff -qr /path/to/folder1 /path/to/folder2
```

#### 复制较大的文件并且显示进度条

Make sure you have `pv` installed and replace `/dev/rdisk2` with the appropriate write device or file.
```bash
FILE=/path/to/file.iso pv -s $(du -h $FILE | awk '/.*/ {print $1}') $FILE | sudo dd of=/dev/rdisk2 bs=1m
```

#### 修复 Sane Shell
In case your shell session went insane (some script or application turned it into a garbled mess).
```bash
stty sane
```

#### 重启
```bash
sudo reboot
```

#### 关机
```bash
sudo poweroff
```

#### 显示 OS 版本信息
```bash
sw_vers
```

#### 开机时间
显示上次开机到现在过去的时间。
```bash
uptime
```

### 剪贴板

####  复制数据到剪贴板
```bash
cat whatever.txt | pbcopy
```

#### 将剪贴板数据转换为纯文本
```bash
pbpaste | textutil -convert txt -stdin -stdout -encoding 30 | pbcopy
```

#### 将剪贴板内容中的 Tab 转换为空格
```bash
pbpaste | expand | pbcopy
```

#### 复制剪贴板的数据
```bash
pbpaste > whatever.txt
```

#### 删除剪贴板重复内容以及排序
```bash
pbpaste | sort | uniq | pbcopy
```

### 文件库

#### 重启自动解锁文件库
If FileVault is enabled on the current volume, it restarts the system, bypassing the initial unlock. The command may not work on all systems.
```bash
sudo fdesetup authrestart
```

#### 文件库服务
```bash
# 查看状态
sudo fdesetup status

# 开启
sudo fdesetup enable

# 禁止 (默认)
sudo fdesetup disable
```

### 信息/报告

#### 产生高级系统和性能报告
```bash
sudo sysdiagnose -f ~/Desktop/
```

### 安装系统

#### 创建安装启动器
```bash
# Mojave
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction --downloadassets

# High Sierra
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ High\ Sierra.app

# Sierra
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ Sierra.app

# El Capitan
sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app

# Yosemite
sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ OS\ X\ Yosemite.app
```

* For confirmation before erasing the drive, remove `–-nointeraction` from the command.
* The optional `–-downloadassets` flag is new in Mojave. It downloads assets which may be required during installation, like updates.
* The `–-applicationpath` flag is deprecated since Mojave and will throw an error if used.

### 内核扩展

#### 展示加载的内核扩展
```bash
sudo kextstat -l
```

#### 加载内核扩展
```bash
sudo kextload -b com.apple.driver.ExampleBundle
```

#### 卸载内核扩展
```bash
sudo kextunload -b com.apple.driver.ExampleBundle
```

### 自启动服务


请看 [这个文件](launchagents.md).


### 自启动服务

#### 重建自启动服务数据库
To be independent of OS X version, this relies on `locate` to find `lsregister`. If you do not have your `locate` database built yet, [do it](#创建定位数据库).
```bash
sudo $(locate lsregister) -kill -seed -r
```

### 登录窗口

#### 设置登录窗口文本
```bash
sudo defaults write /Library/Preferences/com.apple.loginwindow LoginwindowText "Your text"
```

### 内存管理

#### 清除内存缓存
```bash
sudo purge
```

#### 显示内存统计
```bash
# One time
vm_stat

# Table of data, repeat 10 times total, 1 second wait between each poll
vm_stat -c 10 1
```

### 通知中心

#### 通知中心服务
```bash
# 关闭
launchctl unload -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist && \
killall -9 NotificationCenter

# 启动 (默认)
launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist
```

### 快速浏览

#### 快速浏览文件
```bash
qlmanage -p /path/to/file
```

### 远程苹果事件
```bash
# 查看状态
sudo systemsetup -getremoteappleevents

# 开启
sudo systemsetup -setremoteappleevents on

# 禁止 (默认)
sudo systemsetup -setremoteappleevents off
```

### Root 用户

```bash
# 开启
dsenableroot

# 禁止
dsenableroot -d
```

### 安全模式启动

```bash
# 查看状态
nvram boot-args

# 开启
sudo nvram boot-args="-x"

# 禁止
sudo nvram boot-args=""
```

### 截图

#### 延迟截图
3 秒后截图为 JPEG 文件，并且在预览中展示。
```bash
screencapture -T 3 -t jpg -P delayedpic.jpg
```

#### 保存截图到给定位置
设置保存地址为桌面。
```bash
defaults write com.apple.screencapture location ~/Desktop && \
killall SystemUIServer
```

#### 设置截图文件格式
设置截图文件格式为 `png`，可选的格式有 `bmp`, `gif`, `jpg`, `jpeg`, `pdf`, `tiff` 。
```bash
defaults write com.apple.screencapture type -string "png"
```

#### 禁止截图阴影
```bash
defaults write com.apple.screencapture disable-shadow -bool true && \
killall SystemUIServer
```

#### 设置截图的默认文件名

截图文件名的时间戳保持不变。
```bash
defaults write com.apple.screencapture name "Example name" && \
killall SystemUIServer
```

### 软件安装

#### 安装 PKG
```bash
installer -pkg /path/to/installer.pkg -target /
```

### 软件更新

#### 更新所有可以更新的软件
```bash
sudo softwareupdate -ia
```

#### 设置软件更新检查的时间间隔

将软件更新检查的时间间隔设置为天，而不是默认的周。
```bash
defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1
```

#### 显示所有可以更新的软件
```bash
sudo softwareupdate -l
```

#### 设置软件更新服务器
This should only be done for testing purposes or unmanaged clients. To use network-wide, either correctly set up DNS along with [Apple SUS service](http://krypted.com/mac-security/using-the-software-update-service-on-mountain-lion-server/) and bind your clients via OpenDirectory. Alternatively, use [Reposado](https://github.com/wdas/reposado) together with correct network DNS settings to make resolution transparent. [Margarita](https://github.com/jessepeterson/margarita) looks nice to have as well.
```bash
# Use own SUS
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate CatalogURL http://su.example.com:8088/index.sucatalog

# Reset to Apple SUS
sudo defaults delete /Library/Preferences/com.apple.SoftwareUpdate CatalogURL
```

### 软件版本

#### 显示系统的版本号
```bash
sw_vers -productVersion
```

### 聚焦

#### 聚焦索引
```bash
# 禁止
mdutil -i off -d /path/to/volume

# 关闭 (默认)
mdutil -i on /path/to/volume
```

#### 擦除聚焦索引并重建
```bash
mdutil -E /path/to/volume
```

#### 通过聚焦搜索
```bash
mdfind -name 'searchterm'
```

#### 显示聚焦索引元数据
```bash
mdls /path/to/file
```

### 系统完整性保护

#### 禁止系统完整性保护
Reboot while holding <kbd>Cmd</kbd> + <kbd>R</kbd>, open the Terminal application and enter:
```bash
csrutil disable && reboot
```

#### 开启系统完整性保护
Reboot while holding <kbd>Cmd</kbd> + <kbd>R</kbd>, open the Terminal application and enter:
```bash
csrutil enable && reboot
```

### 时间和日期

#### 列出所有时区
```bash
sudo systemsetup -listtimezones
```

#### 设置时区
```bash
sudo systemsetup -settimezone Europe/Berlin
```

#### 网络时间设置时钟
```bash
# 查看状态
sudo systemsetup getusingnetworktime

# 开启 (默认)
sudo systemsetup setusingnetworktime on

# 关闭
sudo systemsetup setusingnetworktime off
```



## 终端

#### Ring Terminal Bell
Rings the terminal bell (if enabled) and puts a badge on it.
```bash
tput bel
```

### 替代终端

- [iTerm2](https://iterm2.com) - A better Terminal.app.
- [kitty](https://sw.kovidgoyal.net/kitty/) - Modern, GPU-accelerated terminal emulator.

### Shells

#### Bash
安装最新版本的 Bash，并且设置为用户的默认的 shell
```bash
brew install bash && \
echo $(brew --prefix)/bin/bash | sudo tee -a /etc/shells && \
chsh -s $(brew --prefix)/bin/bash
```

- [Homepage](https://www.gnu.org/software/bash/) - OS X 以及 Unix 类似系统的默认 shell 。
- [Bash-it](https://github.com/Bash-it/bash-it) - 社区驱动 Bash 框架，类似 Oh My Zsh

#### fish
安装最新版本的 fish，并且设置为用户的默认的 shell
```bash
brew install fish && \
echo $(brew --prefix)/bin/fish | sudo tee -a /etc/shells && \
chsh -s $(brew --prefix)/bin/fish
```

- [Homepage](http://fishshell.com) -  一个对 OS X 、Linux 用户友好的智能 shell,支持更多系统。
- [The Fishshell Framework](https://github.com/oh-my-fish/oh-my-fish) - 提供核心基础结构，允许您扩展或修改 shell 外观的软件包。
- [Installation & Configuration Tutorial](https://github.com/ellerbrock/fish-shell-setup-osx) - 怎样通过 Fisherman、Powerline Fonts、 iTerm2 和 Budspencer Theme 安装 Fish Shell。

#### Zsh
安装最新版本的 Zsh，并且设置为用户的默认的 shell
```bash
brew install zsh && \
sudo sh -c 'echo $(brew --prefix)/bin/zsh >> /etc/shells' && \
chsh -s $(brew --prefix)/bin/zsh
```

- [Homepage](http://www.zsh.org) - Zsh is a shell designed for interactive use, although it is also a powerful scripting language.
- [Oh My Zsh](http://ohmyz.sh) - An open source, community-driven framework for managing your Zsh configuration.
- [Prezto](https://github.com/sorin-ionescu/prezto) - A speedy Zsh framework. Enriches the command line interface environment with sane defaults, aliases, functions, auto completion, and prompt themes.
- [zgen](https://github.com/tarjoilija/zgen) - Another open source framework for managing your zsh configuration. Zgen will load oh-my-zsh compatible plugins and themes and has the advantage of both being faster and automatically cloning any plugins used in your configuration for you.

### 终端字体

- [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) - A family of four fixed-width fonts designed with coding in mind.
- [Codeface](https://github.com/chrissimpkins/codeface) - A gallery and repository of monospaced fonts for developers.
- [DejaVu Sans Mono](https://dejavu-fonts.github.io/) - A font family based on the Vera Fonts.
- [Hack](http://sourcefoundry.org/hack/) - Hack is hand groomed and optically balanced to be your go-to code face.
- [Inconsolata](http://levien.com/type/myfonts/inconsolata.html) -  A monospace font, designed for code listings and the like.
- [Input](http://input.fontbureau.com) - A flexible system of fonts designed specifically for code.
- [Meslo](https://github.com/andreberg/Meslo-Font) - Customized version of Apple's Menlo font.
- [Operator Mono](https://www.typography.com/fonts/operator/overview/) - A surprisingly usable alternative take on a monospace font (commercial).
- [Powerline Fonts](https://github.com/powerline/fonts) - Repo of patched fonts for the Powerline plugin.
- [Source Code Pro](https://adobe-fonts.github.io/source-code-pro/) - A monospaced font family for user interfaces and coding environments.


## 词汇表

### Mac OS X、OS X 以及 macOS 的版本信息

版本                    | 名称           | 发布日期       | 最新版本
-------------------------- | ------------------ | ------------------ | -------------------------------------
Rhapsody Developer Release | Grail1Z4 / Titan1U | August 31, 1997    | DR2 (May 14, 1998)
Mac OS X Server 1.0        | Hera               | March 16, 1999     | 1.2v3 (October 27, 2000)
Mac OS X Developer Preview | n/a                | March 16, 1999     | DP4 (April 5, 2000)
Mac OS X Public Beta       | Kodiak             | September 13, 2000 | n/a
Mac OS X 10.0              | Cheetah            | March 24, 2001     | 10.0.4 (June 22, 2001)
Mac OS X 10.1              | Puma               | September 25, 2001 | 10.1.5 (June 6, 2002)
Mac OS X 10.2              | Jaguar             | August 24, 2002    | 10.2.8 (October 3, 2003)
Mac OS X 10.3              | Panther            | October 24, 2003   | 10.3.9 (April 15, 2005)
Mac OS X 10.4              | Tiger              | April 29, 2005     | 10.4.11 (November 14, 2007)
Mac OS X 10.5              | Leopard            | October 26, 2007   | 10.5.8 (August 5, 2009)
Mac OS X 10.6              | Snow Leopard       | August 28, 2009    | 10.6.8 v1.1 (July 25, 2011)
Mac OS X 10.7              | Lion               | July 20, 2011      | 10.7.5 (September 19, 2012)
OS X 10.8                  | Mountain Lion      | July 25, 2012      | 10.8.5 (12F45) (October 3, 2013)
OS X 10.9                  | Mavericks          | October 22, 2013   | 10.9.5 (13F1112) (September 18, 2014)
OS X 10.10                 | Yosemite           | October 16, 2014   | 10.10.5 (14F27) (August 13, 2015)
OS X 10.11                 | El Capitan         | September 30, 2015 | 10.11.6 (15G31) (July 18, 2016)
macOS 10.12                | Sierra             | September 20, 2016 | 10.12.6 (16G29) (July 19, 2017)
macOS 10.13                | High Sierra        | September 25, 2017 | 10.13.6 (17G65) (July 9, 2018)
macOS 10.14                | Mojave             | September 24, 2018 | 10.14 (18A391) (September 24, 2018)


## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
