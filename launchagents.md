# 自启动服务

> 各种有用的自启动服务例子。 [Awesome OS X Command Line](https://github.com/nusr/awesome-macos-command-line-zh) 的一部分

- [自启动服务](#%E8%87%AA%E5%90%AF%E5%8A%A8%E6%9C%8D%E5%8A%A1)
  - [基本例子](#%E5%9F%BA%E6%9C%AC%E4%BE%8B%E5%AD%90)
    - [定时工作模板](#%E5%AE%9A%E6%97%B6%E5%B7%A5%E4%BD%9C%E6%A8%A1%E6%9D%BF)
    - [按照日历定期工作模板](#%E6%8C%89%E7%85%A7%E6%97%A5%E5%8E%86%E5%AE%9A%E6%9C%9F%E5%B7%A5%E4%BD%9C%E6%A8%A1%E6%9D%BF)
    - [监控文件夹模板](#%E7%9B%91%E6%8E%A7%E6%96%87%E4%BB%B6%E5%A4%B9%E6%A8%A1%E6%9D%BF)
  - [Homebrew](#homebrew)
    - [定时更新 Homebrew](#%E5%AE%9A%E6%97%B6%E6%9B%B4%E6%96%B0-homebrew)
  - [License](#license)

## 基本例子

### 定时工作模板

每5分钟运行一次。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.touchsomefile</string>
    <key>ProgramArguments</key>
    <array>
        <string>touch</string>
        <string>/tmp/helloworld</string>
    </array>
    <key>StartInterval</key>
    <integer>300</integer>
</dict>
</plist>
```

### 按照日历定期工作模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.touchsomefile</string>
    <key>ProgramArguments</key>
    <array>
        <string>touch</string>
        <string>/tmp/helloworld</string>
    </array>
    <key>StartCalendarInterval</key>
    <dict>
        <key>Minute</key>
        <integer>45</integer>
        <key>Hour</key>
        <integer>13</integer>
        <key>Day</key>
        <integer>7</integer>
    </dict>
</dict>
</plist>
```

### 监控文件夹模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.watchhostconfig</string>
    <key>ProgramArguments</key>
    <array>
        <string>syslog</string>
        <string>-s</string>
        <string>-l</string>
        <string>notice</string>
        <string>somebody touched /etc/hostconfig</string>
    </array>
    <key>WatchPaths</key>
    <array>
        <string>/etc/hostconfig</string>
    </array>
</dict>
</plist>
```

## Homebrew

### 定时更新 Homebrew

为了使用通知系统，这个功能需要先安装[terminal-notifier](https://github.com/julienXX/terminal-notifier)。可以通过 `brew install terminal-notifier` 安装 terminal-notifier。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.homebrew-upgrade</string>
    <key>ProcessType</key>
    <string>Background</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/sh</string>
        <string>-c</string>
        <string>/usr/local/bin/brew update &amp;&amp; /usr/local/bin/brew upgrade &amp;&amp; /usr/local/bin/terminal-notifier -title 'Homebrew Upgrader' -message 'Homebrew upgraded!' -appIcon http://cdn.curvve.com/wp-content/uploads/2013/09/homebrew_osx_logo.png</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>StandardErrorPath</key>
    <string>/tmp/com.example.homebrew-upgrade.stderr</string>
    <key>StandardOutPath</key>
    <string>/tmp/com.example.homebrew-upgrade.stdout</string>
    <key>StartCalendarInterval</key>
    <array>
        <dict>
            <key>Hour</key>
            <integer>8</integer>
        </dict>
    </array>
</dict>
</plist>
```

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
