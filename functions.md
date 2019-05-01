
# 函数

> OS X 特定 Bash 风格的好用函数集合。[Awesome OS X Command Line](https://github.com/nusr/awesome-macos-command-line-zh) 的一部分。

- [函数](#%E5%87%BD%E6%95%B0)
  - [开发者](#%E5%BC%80%E5%8F%91%E8%80%85)
    - [应用图标](#%E5%BA%94%E7%94%A8%E5%9B%BE%E6%A0%87)
      - [创建应用图标](#%E5%88%9B%E5%BB%BA%E5%BA%94%E7%94%A8%E5%9B%BE%E6%A0%87)
    - [助手功能](#%E5%8A%A9%E6%89%8B%E5%8A%9F%E8%83%BD)
      - [向用户询问密码](#%E5%90%91%E7%94%A8%E6%88%B7%E8%AF%A2%E9%97%AE%E5%AF%86%E7%A0%81)
  - [访达](#%E8%AE%BF%E8%BE%BE)
    - [获取最前面的访达窗口的路径](#%E8%8E%B7%E5%8F%96%E6%9C%80%E5%89%8D%E9%9D%A2%E7%9A%84%E8%AE%BF%E8%BE%BE%E7%AA%97%E5%8F%A3%E7%9A%84%E8%B7%AF%E5%BE%84)
    - [打印访达中选中的文件](#%E6%89%93%E5%8D%B0%E8%AE%BF%E8%BE%BE%E4%B8%AD%E9%80%89%E4%B8%AD%E7%9A%84%E6%96%87%E4%BB%B6)
    - [将当前访达文件目录设置为分栏视图](#%E5%B0%86%E5%BD%93%E5%89%8D%E8%AE%BF%E8%BE%BE%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E8%AE%BE%E7%BD%AE%E4%B8%BA%E5%88%86%E6%A0%8F%E8%A7%86%E5%9B%BE)
    - [将当前访达文件目录设置为图标视图](#%E5%B0%86%E5%BD%93%E5%89%8D%E8%AE%BF%E8%BE%BE%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E8%AE%BE%E7%BD%AE%E4%B8%BA%E5%9B%BE%E6%A0%87%E8%A7%86%E5%9B%BE)
    - [将当前访达文件目录设置为列表视图](#%E5%B0%86%E5%BD%93%E5%89%8D%E8%AE%BF%E8%BE%BE%E6%96%87%E4%BB%B6%E7%9B%AE%E5%BD%95%E8%AE%BE%E7%BD%AE%E4%B8%BA%E5%88%97%E8%A1%A8%E8%A7%86%E5%9B%BE)
  - [License](#license)

## 开发者

### 应用图标

#### 创建应用图标

由 1024 x 1024 图片快速创建应用图标的函数。

```bash
function mkicns() {
    if [[ -z "$@" ]]; then
        echo "Input file missing"
    else
        filename=${1%.*}
        mkdir $filename.iconset
        sips -z 16 16   $1 --out $filename.iconset/icon_16x16.png
        sips -z 32 32   $1 --out $filename.iconset/icon_16x16@2x.png
        sips -z 32 32   $1 --out $filename.iconset/icon_32x32.png
        sips -z 64 64   $1 --out $filename.iconset/icon_32x32@2x.png
        sips -z 128 128 $1 --out $filename.iconset/icon_128x128.png
        sips -z 256 256 $1 --out $filename.iconset/icon_128x128@2x.png
        sips -z 256 256 $1 --out $filename.iconset/icon_256x256.png
        sips -z 512 512 $1 --out $filename.iconset/icon_256x256@2x.png
        sips -z 512 512 $1 --out $filename.iconset/icon_512x512.png
        cp $1 $filename.iconset/icon_512x512@2x.png
        iconutil -c icns $filename.iconset
        rm -r $filename.iconset
    fi
}
```

### 助手功能

#### 向用户询问密码

使用 AppleScript 创建密码输入框，对用户更友好。

```bash
function gui_password {
    if [[ -z $1 ]]; then
        gui_prompt="Password:"
    else
        gui_prompt="$1"
    fi
    PW=$(osascript <<EOF
    tell application "System Events"
        activate
        text returned of (display dialog "${gui_prompt}" default answer "" with hidden answer)
    end tell
EOF
    )

    echo -n "${PW}"
}

```

## 访达

### 获取最前面的访达窗口的路径

```bash
function finder_path {
    osascript -e 'tell application "Finder"'\
        -e "if (${1-1} <= (count Finder windows)) then"\
        -e "get POSIX path of (target of window ${1-1} as alias)"\
        -e 'else' \
        -e 'get POSIX path of (desktop as alias)'\
        -e 'end if' \
        -e 'end tell';
}
```

### 打印访达中选中的文件

```bash
selected() {
    osascript <<EOT
        tell application "Finder"
            set theFiles to selection
            set theList to ""
            repeat with aFile in theFiles
                set theList to theList & POSIX path of (aFile as alias) & "\n"
            end repeat
            theList
        end tell
EOT
}
```

### 将当前访达文件目录设置为分栏视图

```bash
function column_view {
    osascript -e 'set cwd to do shell script "pwd"'\
      -e 'tell application "Finder"'\
      -e "if (${1-1} <= (count Finder windows)) then"\
      -e "set the target of window ${1-1} to (POSIX file cwd) as string"\
      -e "set the current view of the front Finder window to column view"\
      -e 'else' -e "open (POSIX file cwd) as string"\
      -e "set the current view of the front Finder window to column view"\
      -e 'end if' -e 'end tell';
}
```

### 将当前访达文件目录设置为图标视图

```bash
function icon_view {
    osascript -e 'set cwd to do shell script "pwd"'\
      -e 'tell application "Finder"'\
      -e "if (${1-1} <= (count Finder windows)) then"\
      -e "set the target of window ${1-1} to (POSIX file cwd) as string"\
      -e "set the current view of the front Finder window to icon view"\
      -e 'else' -e "open (POSIX file cwd) as string"\
      -e "set the current view of the front Finder window to icon view"\
      -e 'end if' -e 'end tell';
};
```

### 将当前访达文件目录设置为列表视图

```bash
function list_view {
  osascript -e 'set cwd to do shell script "pwd"'\
    -e 'tell application "Finder"'\
    -e "if (${1-1} <= (count Finder windows)) then"\
    -e "set the target of window ${1-1} to (POSIX file cwd) as string"\
    -e "set the current view of the front Finder window to list view"\
    -e 'else' -e "open (POSIX file cwd) as string"\
    -e "set the current view of the front Finder window to list view"\
    -e 'end if' -e 'end tell';\
}
```

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
