# 给mac添加右键菜单“Open With VSCode”
1. command + n 打开 “自动操作” 应用程序，点击“新建文稿”
2. 选择快速操作
   1. 在左侧面板选择“实用工具”；然后找到”运行 Shell 脚本“后双击，在右侧“服务”收到选定选择文件夹，位置 “Finder（访达）.app”；“运行 Shell 脚本”的面板里，Shell选择 “/bin/bash“，传递输入选择 “作为自变量”，然后修改 Shell 脚本，如图![openWithVSCode][openWithVSCodePic]
   2. 按顺序操作，复制以下内容到 Shell 脚本中
    ```
    for f in "$@"
    do
        open -a "Visual Studio Code" "$f"
    done
    ```
   3. Command + s 保存为 「Open With VSCode」
      1. 小插曲：保存时报Operation not permitted，查资料后得知与Mac OS升级有关，解决方案如下
         1. 左上角点击选择‘系统偏好设置’
         2. 选择“安全性与隐私”
         3. 选择 隐私-->“完全磁盘访问权限”
         4. 点击左下角按钮获得管理员操作权限
         5. 把出问题的应用程序加到““完全磁盘访问权限””列表中
   4. 好了，现在试试在 Finder 里右键一个文件，就可以直接看到「Open With VSCode」菜单，右键一个文件夹，就可以看到「服务」-「Open With VSCode」菜单了

# Mac Finder中显示、隐藏 隐藏文件
- “Shift + command + 。“ || “Shift + command + .“快捷键（即无需判断中英文输入法状态）