# Typecho-Skill-Support-Emoji-expressions / Typecho技巧：支持Emoji表情
###### 安装完 typecho，发现并不能使用 Emoji 表情，评论里的 Emoji 表情，都会显示空白，看来不是 typecho 程序的问题，typecho 还是比较健壮的，于是苗头指向了数据库。建数据库的时候使用 utf-8，utf-8 是不支持 Emoji 表情的。  要想数据库支持 Emoji 表情，就得使用 utf8mb4 编码来支持，于是我们需要修改已有数据库的编码格式，好消息是 utf8mb4 是 utf-8 的超集，完全兼容 utf-8，修改后，不会影响现有数据。

# 修改数据表编码

###### 登录服务器的 MySQL 命令行或使用 phpAdmin，输入密码，进入 MySQL，切换到 typecho 的数据库。



    use typecho数据库名;
    
###### 执行以下 sql 语句，修改 typecho 数据库中表的编码格式为 utf8mb4。

## 第一种：

    alter table typecho_comments convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_contents convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_fields convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_metas convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_options convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_relationships convert to character set utf8mb4 collate utf8mb4_general_ci;
    alter table typecho_users convert to character set utf8mb4 collate utf8mb4_general_ci;
    
###### 或者

## 第二种（推荐）：



    alter table typecho_comments convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_contents convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_fields convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_metas convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_options convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_relationships convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    alter table typecho_users convert to character set utf8mb4 collate utf8mb4_unicode_ci;
    
## 修改 config.inc.php 配置

    # 替换路径为自己的 config.inc.php 路径
    vi /home/wwwroot/www.skyqian.com/config.inc.php
    
###### 按下 i 进入 vi 的编辑模式。

###### 修改 charset 的至为 utf8mb4。

    /** 定义数据库参数 */
    $db = new Typecho_Db('Pdo_Mysql', 'typecho_');
    $db->addServer(array (
      ...
      'charset' => 'utf8mb4',  # 修改编码为 utf8mb4
      ...
    ), Typecho_Db::READ | Typecho_Db::WRITE);
    Typecho_Db::set($db);
    
###### 按下 :，输入 wq 保存文件。

###### 这样就成功为 typecho 开启的 Emoji 支持。输入一个表情试试：
