# macos

# 设置ctrl位置
安装https://github.com/tekezo/Karabiner-Elements
然后complex modifications -> add rule 使用https://madogiwa.github.io/KE-complex_modifications/ 中的"Caps and return to ctrl. Ctrl to caps."
simple modifications -> add item

left_command -> left_option
left_option -> left_command
right_command -> right_option
right_option -> right_command

# mac聚焦搜索 spotlight
   command+enter 打开文件所在路径
   
# mac 输入 希腊字母
Command + Ctrl + Space


# mac 安装 parallel desktop

需要先关闭SIP：
1. 重启电脑之后按住Command+R进入Recovery Mode
2. 在Recovery Mode下的终端输入 csrutil disable
3. 安装parellel desktop
4. 再次重启电脑 csrutil enable
4. 终端输入命令（注意要一模一样！！）: sudo codesign --sign - --force --deep /Applications/Parallels\ Desktop.app
