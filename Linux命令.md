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
    -shell
        + /etc/shells   システムで利用可能なシェルを確認
        + メタキャラクタ
        + * 0文字以上任意の文字列、０も含め     ls *.txt
        + ？任意１文字                          ls ?.txt
        + [　]　[]内の任意1文字                 ls [ab]*.txt a或者b开头的文件,ls [1-3].txt  1.txt和2.txt和3.txt
        + \ メタキャラクタの打ち消し
        + date > today 重定向 将date命令的结果写入today文件，覆盖原文件
        + date >> today 重定向 将date命令的结果写入today文件，不覆盖文件，续写在末尾
        + ls -l today nofile    today文件不报错，nofile文件报错
        + ls -l today nofile 2> stderr.txt  将错误信息出力到stderr.txt文件里
        + history | less    将命令行执行的结果，用另一个命令取处理，这里将history命令运行的结果用less命令打开
        + ！1   history命令显示执行履历一览，！番号是重新执行第几条命令，这里是第一条
        + alias 别名一览
        + alias la='ls -la' 给命令起个别名
        + alias lsl='ls -l | less'
        + lsl /etc
        + var=Linux 变量赋值
        + echo $var 查看变量
        + bash 重新打开一个bash，exit退出
        + 在旧的bash里定义的变量，新的bash里不能用
        + 主要变量
          + HOME ユーザーのホームディレクトリ
          + HOSTNAME　ホスト名（コンピューター名）
          + LANG　ユーザーの言語処理方式
          + PATH　コマンドを検索するディレクトリリスト
          + PS1　プロンプト書式
          + PWD　カレントディレクトリのパス
          + UID　ユーザーID
          + USER　ユーザー名
        + 環境変数
          + printenv 環境変数を表示する
          + set　シェル変数と環境変数を表示
          + export world=centos 環境変数を定義
          + 环境变量在新开的bash里能访问
        + bashの主な組み込みコマンド
          + alias   エイリアスを作成、表示する
          + bg      ジョブをバックグラウンドで実行する
          + cd      ディレクトリを移動
          + echo    引数の内容を表示する
          + exit    シェルを終了
          + export  環境変数を設定する
          + fg      ジョブをフォアグラウンドで実行する
          + history コマンド履歴一覧
          + jobs    ジョブを表示
          + kill    プロセルにシグナルを送信する
          + pwd     カレントディレクトリを表示
          + unalias エイリアスを削除する
        + 外部コマンド
          + which ls    ls命令的执行文件在哪
          + 外部命令都是在某个目录里，系统执行命令的时候先找組み込みコマンド，如果没有，就去PATH变量的目录里去找外部コマンド
          + root用户和一般用户的PATH不一样
        + ファイル検索
          + locate ファイル名   检索文件、非即时的
            + locate hosts  
            + locate *hosts*
            + locate hosts | grep '^/etc'   查找etc文件夹下的文件
            + # updatedb    ファイル名データベース更新、定期的に実行される
          + find 「検索対象パス」　「検索式」   实时检索
            + 主な検索式
                -name ファイル名指定
                -size ファイルサイズを指定
                -atime ファイルの最終アクセス日を指定
                -amin   ファイルの最終アクセス時刻を〇分前で指定する
                -mtime  ファイルの最終修正日を指定する
                -mmin   ファイルの最終更新時刻を〇分前で指定する
                -perm   ファイルのアクセル権を指定する
                -type   ファイルタイプを指定する
            + find /bin -name "c*"    在bin目录下查找c开头的文件
            + find -size -10k -mtime -1 查找文件大小在10kb以下，并且最终修正日在1天以内的文件
            + find -atime +360 -exec rm {} \;   删除360天以上没有被访问过的文件
          + ファイル内容検索
            + 正規表現  检索文件用的替代符メタキャラクタ,和シェルのメタキャラクタ有点像
              + .   a.c 「abc」[a1c]
              + *   .*  0文字以上の文字列にマッチする
              + []  [A-Z]   大文字アルファベット一文字にマッチする  [0-9][0-9]  2桁の数字にマッチする
              + ^   ^#  行頭が＃という文字にマッチする
              + $   ^$  空行にマッチする（改行のみの行）
              + \   \.TXT   「.TXT」という文字列にマッチする
            + grep [オプション]　[文字列パターン]   [検索対象ファイル]  查找文件里的内容
              + 主なオプション
                -F  文字列パターンを正規表現ではなく単なる文字列として扱う
                -c  マッチした行数だけを表示する
                -i  大文字と小文字区別しない
                -l  マッチした行のあるファイル名のみを表示する？
                -n  行番号も合わせて表示
                -v  マッチしなかった行を表示する
              + grep www /etc/services
              + grep -i www /etc/services   不区分大小写
              + grep http /etc/init.d/* 对init.d目录下的所有文件进行内容检索
              + ps ax | grep bash   在ps ax的结果中查找内容中有bash的行
              + headコマンド
                + head [-行数]　[ファイル名]    默认显示先头10行内容
                + head /etc/passwd
                + ps aux | head -5  ps aux的结果显示前5行
                + tail    [-行数]　[ファイル名]    默认显示末尾10行内容
              + sortコマンド
                + sort [オプション]　[ファイル名]   默认アルファベット昇順
                + sort sample 1文字目だけを見てソートしている
                + sort -n sample    数字を数値としてソートしたい場合　-nを付ける
                + sort -nr sample    上の降順
              + nlコマンド
                + nl sample 行番号を付けて内容を出力
              + wcコマンド
                + wc [オプション] [ファイル名]  ファイル行数、単語数、バイト数を表示する
                + wc /etc/hosts
                + ls /etc/sysconfig | wc -l /etc/sysconfig配下のファイルやディレクトリの数だけ表示


