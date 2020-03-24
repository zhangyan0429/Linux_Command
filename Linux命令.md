# 命令


 - 基本命令
    + pwd 查看当前所在目录
    + cat [文件名]  显示文本文件
    + less [文件名] 将文件显示在一页里（显示长文本用），按q结束，还有more命令和less命令差不多
    + cd 回到自己的用户文件夹
    + cd - 回到上一个工作目录
    + cd ~回到自己的用户文件夹
    + localectl set-keymap us 设置键盘布局为美式
    + ls -i 显示所有文件和文件夹的iノード番号
    + ln date/images/cat.jpg neko1.jpg  给cat.jpg做一个link叫neko1.jpg
    + ln -s date/images/cat.jpg neko2.jpg シンボリックリンクを作成 它指向cat.jpg文件
    + cp [文件名] [新文件名]    复制文件到当前目录
    + cp [文件名] [目录]    复制文件到指定目录，文件名与原文件名相同
    + mv [原文件名] [移动位置]  文件移动
    + mv [原文件名] [新文件名]  文件重命名
    + mkdir [目录名]    创建目录    mkdir sub
    + mkdir -p [目录名]   创建嵌套的目录  mkdir -p top/sub
    + cp -r [原目录] [新目录]  复制文件夹
    + mv [原目录] [新目录]  移动文件夹  mv sub new(如果当前目录里有new文件夹，那么这个命令就是把sub移动到new文件夹下，不然就是改名为new)
    + mv [原目录] [新目录]  修改目录名  mv sub sup(把sub改名为sup)
    + rm -r [目录]  删除文件夹（不管文件夹里有没有文件）
    + rmdir [目录]  删除文件夹（如果文件夹里有文件，则不能删除）

  - 压缩文件
    + gzip [要压缩的文件]   压缩文件，压缩后生成.gz后缀，原文件被删除
    + gunzip [要解冻的压缩文件] 解冻之后压缩文件啊会被删除
    + gunzip -c [要解冻的文件] > 解冻后的文件名（就是去掉.gz）  这个是保留压缩文件的解冻方式
  
  - 压缩アーカイブ
    + tar cvf [アーカイブファイル名]　ディレクトリ名    アーカイブ作成
    + tar xvf アーカイブ名.tar　アーカイブ展開
    + tar czvf [アーカイブファイル名.tar.gz] アーカイブ名   直接将文件夹压缩成存档再压缩成.gz   (原存档保留)
    + tar xzvf アーカイブファイル名.tar.gz  直接解冻压缩文件    （原压缩文件保留）

  - User
    + user信息文件存在 /etc/passwd里，有三种user，rootuser 系统user，一般user
    + id 查看当前user信息
    + su -  切换到root用户，可以用root专用命令，为root环境，如果没有[-]则只是用root权限，必须exit！
    + su zhangyan 切换到自己的id
    + groups 查看当前user的所属组
    + groups zhangyan 查看zhangyan的所属组
    + useradd 用户名 添加用户（只能root添加）自动在home文件夹内创建一个user同名的文件夹
    + 如果想在home创建user同名文件夹的时候自动在文件夹里生成文件的话，在/etc/skel文件夹里放文件就行，这个文件夹是user文件夹的雏形
    + passwd 修改用户密码 root用户有权随意更改一般用户的密码
    + userdel 用户名    删除用户，需要root权限，home下的user文件夹会保留
    + userdel -r 用户名 删除用户，连同home下的user文件夹也删除
    + groupadd smile    创建一个名为smile的group，用root权限
    + usermod -G smile zhangyan 将zhangyan加入到smile组里
    + groupdel smile    删除组，不能删除用户默认组 
    + group信息存在/etc/group文件里 ，这个文件里不显示用户默认组，/etc/passwd文件里显示用户默认组

  - 所有者和所有者group
    + chown [-R] 用户名 文件名  修改文件的所有者
    + chown -R zhangyan archive 将archive文件夹包括文件夹内的文件的所有者变更为zhangyan，-R的意思是包括文件夹内的所有文件
    + chgrp [-R] 组名   文件名  修改文件的所属组
    + chgrp [-R] smile archive  将archive文件夹的所属组改为smile
    + chown [-R] zhangyan:smile archive同时修改所属用户和组
    + ls -ld 文件夹名   查看文件夹信息
    + [-rwxrwxr-x] パーミッション　-通常ファイル、rwx所有者権限、rwx所有グループ権限、r-x他ユーザ権限
    + 読み取り権 = 4
    + 書き込み権 = 2
    + 実行権 = 1

    + 读取权：
      + 对文件可以用cat
      + 对文件夹可以显示文件夹里的文件一览，但会报错，可以用ls -ld，不能用cd，也不能用cat访问文件夹里的文件
    + 写入权：
      + 对文件可以更改内容
      + 对文件夹内的文件可以作成，删除，即使没有访问文件夹内的文件的权限，只要有对文件夹的写入权，就可以删除文件夹内的文件
    + 执行权：
      + 对文件可以执行，可以cat
      + 对文件夹可以cd进去，还能移动
    + 修改权限：
      + chmod [-R] 权限 文件名或文件夹名
        + chmod 644 today.txt [rw-r--r--]
        + chmod 755 archive   [rwxr-xr-x]
      + chmod g+w today.txt 给所属组添加一个写入权
        + 操作对象：u所有者，g所属组，o其他用户，a所有用户
        + 操作：+添加，-删除，=权限指定
        + 访问权：r，w，x
      + chmod go-x archive 删除所有者以外的所有用户的执行权
  - viエディター
        + vi    打开viEditor
        + vi test.txt   打开编辑器并打开test.txt文本
        + 刚一进来就是命令模式
        + 命令模式下【：q】是退出，【：q！】是不保存退出
        + esc是切换到命令模式，命令模式下的命令
          + h：光标左移
          + j：下移
          + k：上移
          + l：右移
          + 0：光标移到行首
          + $：光标移到行尾
          + gg：光标移到文件头
          + G：光标移到文件尾
        + 切换到插入模式
          + i：从光标位置开始输入
          + I（大写i）：光标移到行首开始输入
          + o：从当前行向下插一行输入
          + O（大写o）：从当前行向上插一行输入
          + a：从光标右侧输入
          + A；将光标移至行末从右开始输入
        + 文件保存和关闭
          + [:w]    是保存
          + [:wq]   保存并退出
          + [:q!]   不保存退出
          + [ZZ]    保存并退出
        + 剪切，复制，粘贴
        + [dd]  剪切
        + [yy]  复制
        + [p]   粘贴
        + [x]   剪切光标右边一个字符
        + [X]（大写x）   剪切光标左边一个字符
        + [3dd] 剪切3行
        + [3yy] 复制3行
        + [3j]  向下3行
        + [u]   撤销上次操作
        + [ctrl + R]    撤销上次的撤销
        + [/文字]   检索特定文字，如果检索出结果是复数个，按n查看下一个，N是查看上一个
        + [/]   是从光标往下查找，[?]是从光标往上查找




chown testfile fred
chgrp testfile develop
751
rw-r--r--
chmod 755 sample
iIoOaA
esc
bce



