---
title: "Mac命令行操作合集"
description: "速查手册"
pubDate: "Dec 09 2025"
heroImage: "/blog-placeholder-3.jpg"
---

# Mac 命令行操作大全（速查手册）

> 说明：本手册以 **zsh + Terminal** 为默认环境（macOS Catalina 及之后版本默认 shell 为 zsh）。

---

## 目录

1. [终端与基础操作](#终端与基础操作)  
2. [获取帮助](#获取帮助)  
3. [文件与目录操作](#文件与目录操作)  
4. [权限与用户管理](#权限与用户管理)  
5. [文本查看与处理](#文本查看与处理)  
6. [搜索与查找](#搜索与查找)  
7. [进程与作业管理](#进程与作业管理)  
8. [网络相关命令](#网络相关命令)  
9. [系统信息与资源](#系统信息与资源)  
10. [磁盘与文件系统](#磁盘与文件系统)  
11. [压缩与打包](#压缩与打包)  
12. [软件安装与包管理（Homebrew）](#软件安装与包管理homebrew)  
13. [Shell 环境与配置](#shell-环境与配置)  
14. [脚本与定时任务](#脚本与定时任务)  
15. [macOS 特有命令](#macos-特有命令)  
16. [Git 基础操作（常用）](#git-基础操作常用)  
17. [常用快捷键与技巧](#常用快捷键与技巧)  
18. [常见命令组合示例](#常见命令组合示例)  

---

## 终端与基础操作

### 打开终端

- Spotlight：`Command + Space` → 输入 `Terminal` → 回车  
- Finder：`应用程序` → `实用工具` → `终端`  
- 当前目录快速打开终端：  
  - Finder 中：右键 → “在文件夹中打开新终端”（需要系统设置或第三方工具）

### 常见基础命令

    pwd          # 显示当前所在目录
    ls           # 列出当前目录内容（简略）
    ls -l        # 详细信息（权限、大小、时间）
    ls -a        # 包含隐藏文件
    ls -lah      # 详细 + 人类可读大小

---

## 获取帮助

    man 命令名       # 查看命令的详细手册
    man ls

    ls --help        # 很多命令支持的简易帮助
    grep --help

    whatis ls        # 简短说明（需要 whatis 数据库）
    apropos network  # 按关键字搜索 man 手册

**man 页面常用快捷键：**

- `↑ / ↓`：上下滚动  
- `Space`：下一页  
- `b`：上一页  
- `/关键字`：向下搜索  
- `n` / `N`：下/上一个匹配  
- `q`：退出  

---

## 文件与目录操作

### 路径与目录

    pwd          # 显示当前目录

    cd /path/to/dir
    cd ~         # 回到主目录
    cd ..        # 上一级目录
    cd -         # 返回上一次所在目录

### 创建 / 删除 / 移动 / 复制

    mkdir new_folder
    mkdir -p a/b/c      # 递归创建多级目录

    rmdir empty_folder  # 删除空目录

    rm file.txt         # 删除文件
    rm -i file.txt      # 删除前逐个确认
    rm -r folder        # 递归删除目录及其内容
    rm -rf folder       # 强制递归删除（谨慎）

    cp a.txt b.txt
    cp a.txt ~/Documents/

    cp -r dir1 dir2     # 复制目录（递归）

    mv a.txt b.txt      # 重命名文件
    mv a.txt ~/Documents/
    mv dir1 dir2        # 移动/重命名目录

### 时间戳与空文件

    touch new.txt       # 创建空文件或更新时间戳

### 查看文件内容

    cat file.txt        # 输出全部内容
    less file.txt       # 分页查看（推荐）

    head file.txt       # 前 10 行
    head -n 50 file.txt # 前 50 行

    tail file.txt       # 后 10 行
    tail -n 50 file.txt # 后 50 行

    tail -f app.log     # 实时查看追加内容（日志）

### 打开文件或目录（macOS 特有）

    open file.pdf       # 用默认程序打开
    open .              # Finder 打开当前目录

    open -a "Visual Studio Code" .
    open -a "TextEdit" note.txt

    open -R file.txt    # 在 Finder 中显示该文件

---

## 权限与用户管理

### 查看权限

    ls -l

示例输出：

    -rw-r--r--  1 user  staff   1234 Dec  9 10:00 file.txt

- 第一列：权限（`r` 读 / `w` 写 / `x` 执行）  
- 之后：所有者、组、大小、时间、文件名  

### 修改权限 chmod

    chmod 755 script.sh     # rwxr-xr-x

    chmod u+x script.sh     # 给所有者加执行权限
    chmod o-w file.txt      # 去掉其他人写权限

### 修改所有者 / 用户组（需 sudo）

    sudo chown newuser file.txt
    sudo chown -R newuser:staff myfolder
    sudo chgrp staff file.txt

### 用户信息

    whoami    # 当前用户
    id        # uid、gid、组信息
    groups    # 所属组列表

### sudo 与管理员权限

    sudo 命令           # 以管理员身份执行
    sudo -v             # 延长 sudo 认证时间
    sudo !!             # 重新执行上一条命令但加上 sudo

---

## 文本查看与处理

### 基本输出

    echo "Hello, world"
    printf "Name: %s, Age: %d\n" "Alex" 18

### grep 文本搜索

    grep "keyword" file.txt        # 搜索包含关键字的行
    grep -i "keyword" file.txt     # 忽略大小写
    grep -n "keyword" file.txt     # 显示行号

    grep -R "keyword" .            # 递归搜索（当前目录及子目录）

### sed 文本替换

    sed 's/old/new/' file.txt      # 每行第一次匹配
    sed 's/old/new/g' file.txt     # 每行全局匹配

    sed -i '' 's/old/new/g' file.txt   # 直接修改文件（macOS 语法）

### awk 文本处理

    awk '{print $1, $3}' file.txt          # 按空格分隔，打印 1、3 列
    awk -F, '{print $1, $2}' data.csv      # 指定分隔符为逗号
    awk '$3 > 100 {print $1, $3}' data.txt # 条件过滤

### sort / uniq / wc / cut / tr

    sort file.txt                 # 排序
    sort -r file.txt              # 逆序排序

    sort file.txt | uniq          # 去重（已排序）
    sort file.txt | uniq -c       # 统计重复次数

    wc -l file.txt                # 行数
    wc -w file.txt                # 单词数
    wc -c file.txt                # 字节数
    wc -lwc file.txt              # 行 + 词 + 字节

    cut -f2 file.txt              # 以制表符分隔，取第 2 列
    cut -d: -f1,3 file.txt        # 以 : 为分隔符，取 1、3 列

    tr 'A-Z' 'a-z' < in.txt > out.txt  # 大写转小写

### xargs / tee

    cat files.txt | xargs rm      # 按行删除文件（谨慎）

    command | tee log.txt         # 同时输出到屏幕和文件
    command | tee -a log.txt      # 追加写入

---

## 搜索与查找

### find 文件搜索

    find . -name "file.txt"
    find . -name "*.log"

    find . -size +100M            # 大于 100M 的文件
    find . -type f -name "*.sh"   # 仅文件

    find . -name "*.tmp" -print   # 先打印检查
    find . -name "*.tmp" -delete
    find . -name "*.tmp" -exec rm {} \;

### Spotlight 命令行（mdfind）

    mdfind "关键字"
    mdfind "kMDItemKind == 'PDF' && kMDItemFSName == '*报告*'"

### locate（可能需先建立数据库）

    locate filename

### which / type

    which python
    which ls

    type cd        # 判断是否为内建、别名或外部命令
    type ls

---

## 进程与作业管理

### 查看进程

    ps aux                 # 查看所有进程
    ps aux | grep appname

    top                    # 实时查看 CPU、内存情况

（可安装 `htop`：`brew install htop` → `htop`）

### 终止进程

    kill 1234              # 发送 SIGTERM
    kill -9 1234           # 强制终止（SIGKILL，谨慎）

    killall Finder
    killall "Google Chrome"

### 后台作业与控制

    long_command &         # 在后台运行

    jobs                   # 查看当前 shell 的后台作业
    fg %1                  # 将作业放到前台

在前台运行的命令中：

- `Ctrl + Z`：挂起并放到后台  
- 然后：  

    bg %1                  # 后台继续运行

---

## 网络相关命令

### 基础网络测试

    ping 8.8.8.8
    ping www.apple.com     # Ctrl + C 停止

    traceroute www.apple.com   # 路由跟踪（如提示需 sudo，则用 sudo）

### IP / DNS 信息

    ifconfig                   # 查看所有网络接口
    ipconfig getifaddr en0     # 获取 en0 接口 IP（Wi-Fi）

    scutil --dns               # 查看 DNS 配置

### HTTP 请求（curl）

    curl https://example.com                   # 简单 GET
    curl -o page.html https://example.com      # 保存到文件
    curl -I https://example.com                # 只看响应头

    curl -X POST -d "name=alex&age=18" https://example.com/api

    curl -X POST -H "Content-Type: application/json" \
         -d '{"name":"alex","age":18}' \
         https://example.com/api

（`wget` 如需使用：`brew install wget`）

### SSH / SCP / SFTP

    ssh user@server
    ssh -p 2222 user@server

    scp file.txt user@server:/path/
    scp -r folder user@server:/path/

    scp user@server:/path/file.txt .
    sftp user@server

---

## 系统信息与资源

    sw_vers                         # macOS 版本
    uname -a                        # 内核与系统信息

    system_profiler SPHardwareDataType   # 硬件概况

    uptime                          # 已开机时长

    who                             # 当前登录用户
    last                            # 登录历史

### CPU / 内存 / 磁盘使用率

    top          # 实时查看 CPU/内存

    df -h        # 各卷磁盘使用情况
    du -sh *     # 当前目录下各子目录大小

---

## 磁盘与文件系统

### diskutil（管理磁盘）

    diskutil list                  # 列出所有磁盘与分区
    diskutil info /dev/disk2s1     # 查看卷信息

    diskutil mount /dev/disk2s1    # 挂载
    diskutil unmount /dev/disk2s1  # 卸载

### dmg 镜像（hdiutil）

    hdiutil attach file.dmg        # 挂载 dmg
    hdiutil detach /Volumes/VolumeName

    hdiutil create -volname "MyData" -srcfolder folder -ov -format UDZO mydata.dmg

---

## 压缩与打包

### zip / unzip

    zip file.zip file.txt          # 压缩单个文件
    zip -r archive.zip folder/     # 压缩目录

    unzip archive.zip
    unzip archive.zip -d target_dir

### tar

    tar -czvf archive.tar.gz folder/   # 打包并压缩

    tar -xzvf archive.tar.gz           # 解压
    tar -tzvf archive.tar.gz           # 只查看文件列表

---

## 软件安装与包管理（Homebrew）

### 安装 Homebrew（如未安装）

（建议从官网获取最新命令：https://brew.sh）

示例：

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

安装完按提示将 brew 路径（如 `/opt/homebrew/bin`）加入 PATH。

### 常用 brew 命令

    brew --version            # 查看版本
    brew search pkgname       # 搜索软件
    brew install wget         # 安装
    brew uninstall wget       # 卸载
    brew list                 # 已安装软件列表

    brew update               # 更新 brew 自身
    brew upgrade              # 更新全部软件
    brew upgrade wget         # 更新单个软件

    brew info wget            # 软件详情
    brew cleanup              # 清理旧版本

---

## Shell 环境与配置

### 查看 / 切换 Shell

    echo $SHELL        # 当前 shell
    cat /etc/shells    # 可用 shell 列表

    chsh -s /bin/zsh   # 切换默认 shell 为 zsh

### 常用配置文件

- zsh：`~/.zshrc`  
- bash：`~/.bash_profile` 或 `~/.bashrc`

    source ~/.zshrc    # 修改配置后重新加载

### 环境变量与 PATH

    echo $PATH

    export MY_VAR="hello"                  # 临时环境变量
    export PATH="/usr/local/bin:$PATH"     # 临时添加路径

写入 `~/.zshrc` 可永久生效，例如：

    export PATH="/usr/local/bin:$PATH"

### 别名 alias

    alias ll='ls -lah'
    alias gs='git status'

    unalias ll          # 删除别名

持久化写入：

    echo "alias ll='ls -lah'" >> ~/.zshrc

---

## 脚本与定时任务

### 可执行脚本示例

    cat > hello.sh << 'EOF'
    #!/bin/zsh
    echo "Hello from script"
    EOF

    chmod +x hello.sh
    ./hello.sh

### cron 定时任务（传统）

    crontab -e     # 编辑当前用户 crontab
    crontab -l     # 查看当前用户 crontab

例子：

    * * * * * /path/to/script.sh
    # 分 时 日 月 周  命令

macOS 上更复杂任务可使用 `launchd` / `launchctl`（此处略）。

---

## macOS 特有命令

### open

    open .                             # Finder 打开当前目录
    open /Applications                 # 打开应用程序目录
    open file.pdf                      # 默认应用打开文件
    open -a "Google Chrome" https://example.com
    open -R file.txt                   # 在 Finder 中显示文件

### 剪贴板

    echo "Hello" | pbcopy
    cat file.txt | pbcopy

    pbpaste > output.txt               # 从剪贴板输出到文件

### 系统语音朗读

    say "Hello, this is macOS"

    say -v "Ting-Ting" "你好，欢迎使用命令行"

### 截图

    screencapture ~/Desktop/screen.png         # 截全屏
    screencapture -i ~/Desktop/window.png      # 交互式截取窗口/区域
    screencapture -x ~/Desktop/silent.png      # 静默截图

### 防止睡眠

    caffeinate              # 防睡，直到 Ctrl + C
    caffeinate command      # 在命令执行期间防睡

### defaults（修改偏好设置，谨慎）

    defaults read com.apple.finder           # 读取 Finder 偏好

    defaults write com.apple.finder ShowPathbar -bool true
    killall Finder                           # 重启 Finder 生效

---

## Git 基础操作（常用）

    git init                     # 初始化仓库
    git status                   # 查看状态

    git add file.txt             # 暂存单个文件
    git add .                    # 暂存所有修改

    git commit -m "message"      # 提交

    git log                      # 查看提交记录
    git diff                     # 查看差异

    git branch                   # 查看分支
    git checkout -b new-branch   # 创建并切换新分支
    git checkout main            # 切回 main 分支

    git remote add origin URL    # 添加远程仓库
    git push -u origin main      # 推送到远程
    git pull                     # 拉取远程更新

---

## 常用快捷键与技巧

### Terminal / Shell 快捷键

- `Ctrl + A`：光标移到行首  
- `Ctrl + E`：光标移到行尾  
- `Ctrl + U`：删除光标前内容  
- `Ctrl + K`：删除光标后内容  
- `Ctrl + W`：删除光标前一个单词  
- `Ctrl + L`：清屏（等同于 `clear`）  
- `Ctrl + C`：终止当前命令  
- `Ctrl + D`：结束输入 / 退出 shell（在空行）  

### 历史命令

    history          # 查看历史记录
    !123             # 执行第 123 条命令
    !!               # 执行上一条命令

- `↑ / ↓`：在历史命令中翻页  
- `Ctrl + R`：按关键字搜索历史命令（增量搜索）  

---

## 常见命令组合示例

### 清理日志 / 缓存文件

    find . -name "*.log.old" -print     # 先检查
    find . -name "*.log.old" -delete    # 再删除（谨慎）

### 查找大文件

    find . -type f -size +100M -exec ls -lh {} \; | sort -k 5 -h

### 实时查看日志并过滤关键字

    tail -f app.log | grep "ERROR"

### 搜索代码中的关键字（递归）

    grep -R "TODO" .
    grep -R --include="*.py" "import pandas" .

### 批量重命名（简单示例）

    for f in *.txt; do
      mv "$f" "${f%.txt}.md"
    done

### 快速搭建静态文件 HTTP 服务（Python 3）

    python3 -m http.server 8000
    # 浏览器访问：http://localhost:8000

---

> 已覆盖 macOS 上常见命令行主干内容，可按个人习惯在对应章节继续补充自己的常用命令与脚本。

