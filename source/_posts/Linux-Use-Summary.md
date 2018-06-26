---
title: Linux Use Summary
date: 2018-01-27 16:01:46
categories: study
tags:
---

### 目标：在Linux服务器B上访问服务器A上指定的文件系统 ###
- - -
1.首先要配置服务器A

编辑/etc/exports,加入:

/home    192.168.1.1(rw)    #IP是服务器B的地址, 目录是要共享出的目录

2.然后启动nfs服务:

/etc/init.d/nfs start

3.到服务器B上就可以挂载了

mount 192.168.1.1:/hoome /mnt

进入服务器B的/mnt目录就可以看到服务器A上的/home目录的内容了

这样就可以在服务器B上像访问本地目录一样访问服务器A的目录了

### mysql 添加用户 ###
- - -
```bash
$ grant all privileges on *.* to alen@localhost identified by '1234';
$ flush privileges;
$ select Host,User,Password from mysql.user;
```

### 拷贝 ###
- - -
``` bash
$ scp -r . user@host:/home/user/game_server/x86_64pc-linux-debug/bin/
```

### git安装和使用 ###
- - -
1. 通过git –-version查看系统带的版本，Cento6.5自带的是git版本是1.7.1

    ```bash
    $ yum remove git
    ```

2. 安装前环境配置

    ```bash
    $ yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidoc xmlto perl-devel perl-CPAN autoconf*
    ```

3. 下载git2.2.1并将git添加到环境变量中

    ```bash
    $ wget https://github.com/git/git/archive/v2.2.1.tar.gz
    $ tar zxvf v2.2.1.tar.gz
    $ cd git-2.2.1
    $ make configure
    $ ./configure --prefix=/usr/local/git --with-iconv=/usr/local/libiconv
    $ make all doc
    $ make install install-doc install-html
    $ echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc
    $ source /etc/bashrc
    ```

4. 查看版本号

    ```bash
    $ git --version
    ```
    > git version 2.2.1

5. 使用

    ```bash
    $ git checkout -b <本地分支名> origin/<远程分支名>  本地新建分支, 把此分支放入其中
    $ git push origin --delete alen-gmd-server 删除远程分支
    $ git branch -D alen-gmd-server 强制删除本地分支
    $ git push origin --delete alen-gmd-server 删除远程分支
    $ git fetch -p  在本地删除远程已经删除的分支
    $ git branch -m old_name new_name
    $ git reset HEAD . 撤销所有的已经add的文件
    $ git add -A 它会把我们未通过 git rm 删除的文件全部stage
    ```

6. git不用输入用户名和密码

	``` bash
	$ git config --global credential.helper store
	$ git pull /git push (这里需要输入用户名和密码，以后就不用啦)
	```
    push你的代码 (git push), 这时会让你输入用户名和密码, 这一步输入的用户名密码会被记住, 下次再push代码时就不用输入用户名密码 ! 这一步会在用户目录下生成文件.git-credential记录用户名密码的信息。

### sublime个性化设置 ###
- - -
Sublime Text3 3143 注册码,亲测可用!
```js
—– BEGIN LICENSE —–
TwitterInc
200 User License
EA7E-890007
1D77F72E 390CDD93 4DCBA022 FAF60790
61AA12C0 A37081C5 D0316412 4584D136
94D7F7D4 95BC8C1C 527DA828 560BB037
D1EDDD8C AE7B379F 50C9D69D B35179EF
2FE898C4 8E4277A8 555CE714 E1FB0E43
D5D52613 C3D12E98 BC49967F 7652EED2
9D2D2E61 67610860 6D338B72 5CF95C69
E36B85CC 84991F19 7575D828 470A92AB
—— END LICENSE ——
```

Ctrl+P 打开搜索框。
举个栗子：
1、输入当前项目中的文件名，快速搜索文件，
2、输入@和关键字，查找文件中函数名，
3、输入：和数字，跳转到文件中该行代码，
4、输入#和关键字，查找变量名。

Sublime Text3 user_setting
```js
{
        "auto_complete_commit_on_tab": false,
        "auto_complete_delay": 0,
        "auto_complete_with_fields": true,
        "auto_find_in_selection": true,
        "auto_indent": true,
        "auto_match_enabled": true,
        "bold_folder_labels": true,
        "caret_style": "wide",
        "color_scheme": "Packages/Boxy Theme/schemes/Boxy Tomorrow.tmTheme",
        "default_line_ending": "unix",
        "fade_fold_buttons": false,
        "fold_buttons": true,
        "font_face": "Courier New",
        "font_size": 19,
        "highlight_line": true,
        "highlight_modified_tabs": true,
        "hot_exit": false,
        "ignored_packages":
        [
                "Vintage"
        ],
        "line_padding_bottom": 1,
        "line_padding_top": 1,
        "match_brackets_angle": true,
        "match_brackets_content": true,
        "match_tags": true,
        "remember_open_files": true,
        "smart_indent": true,
        "tab_size": 8,
        "theme": "Boxy Tomorrow.sublime-theme",
        "theme_accent_numix": true,
        "theme_autocomplete_item_selected_colored": true,
        "theme_dropdown_atomized": true,
        "theme_find_panel_materialized": true,
        "theme_grid_border_size_xs": true,
        "theme_popup_border_visible": true,
        "theme_quick_panel_border_visible": true,
        "theme_quick_panel_item_selected_colored": true,
        "theme_scrollbar_colored": true,
        "theme_scrollbar_line": true,
        "theme_sidebar_disclosure": true,
        "theme_tab_selected_transparent": true,
        "theme_tab_selected_underlined": true,
        "theme_tab_size_lg": true,
        "theme_unified": true,
        "translate_tabs_to_spaces": true,
        "trim_automatic_white_space": true,
        "trim_trailing_white_space_on_save": true,
        "word_separators": "./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}`~?",
        "word_wrap": "false"
}
```


linux下mysql忘记root密码解决方法:

如果使用 MySQL 数据库忘记了root账号密码，可以通过调节配置文件，跳过密码的方式登数据库，

在数据库里面修改账号密码，一般默认的账号是 root

1、编辑 MySQL 配置文件 my.cnf

注意： 以实际 my.cnf 配置文件路径为准

vim /etc/my.cnf

[mysqld]
skip-grant-tables

2、重启 MySQL 服务

注意：以实际 MySQL 启动脚本路径为准

service mysqld restart 或者 /etc/init.d/mysqld restart

若报错，注意观察my.cnf配置文件中的内容

3、登陆数据库

/usr/bin/mysql 输入如下命令：

注意：以实际 MySQL 执行文件路径为准

mysql> mysql
mysql> USE mysql;
mysql> UPDATE user SET Password=PASSWORD("新密码") where User='root';
mysql> flush privileges ;
mysql> quit

4、删除或者注释第一步骤中添加的 skip-grant-tables

5、重启 MySQL 服务

service mysqld restart 或者 /etc/init.d/mysqld restart

6、使用新密码测试
