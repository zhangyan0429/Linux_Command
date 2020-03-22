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




