# Typecho-Skill-Support-Emoji-expressions
安装完 typecho，发现并不能使用 Emoji 表情，评论里的 Emoji 表情，都会显示空白，看来不是 typecho 程序的问题，typecho 还是比较健壮的，于是苗头指向了数据库。建数据库的时候使用 utf-8，utf-8 是不支持 Emoji 表情的。  要想数据库支持 Emoji 表情，就得使用 utf8mb4 编码来支持，于是我们需要修改已有数据库的编码格式，好消息是 utf8mb4 是 utf-8 的超集，完全兼容 utf-8，修改后，不会影响现有数据。
