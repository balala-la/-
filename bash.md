# Linux

查看历史命令：

```bash
history
```



## 常用命令

查看当前目录文件清单

```dash
ls		--list(默认不显示隐藏文件)
ls -l	
ls -la	--l:显示详细清单 a:显示所有文件
ls -l fileName/dirName --查看指定文件/文件夹的信息
```

查看当前所处文件夹路径

```dash
pwd
```

清空终端所有显示

```dash
clear
```





## 光标移动快捷键

切换上一个命令

```bash
ctrl + p
```

切换下一条命令

```bash
ctrl + n --next
```

光标前移

```bash
ctrl + b
```

光标后移

```bash
ctrl + b
```

光标移至最前

```bash
ctrl + a
```

光标移至最后

```bash
ctrl + e --end
```

删除光标后字符

```bash
ctrl + d --delete
```

删除光标前字符

```bash
ctrl + h 
```

删除光标前全部字符

```bash
ctrl + u
```



## 目录切换命令

返回上一级菜单

```dash
cd ..
```

切换到用户目录

```dash
cd 
```

```dash
cd ~
```

两个历史目录间切换

```dash
cd -
```

切换到目标目录

```dash
cd dirName			--相对路径
cd /home/lee/...	--绝对路径
```



## 文件/目录的增删改查操作

新建目录

```dash
mkdir dirName
```

新建多层目录

```dash
mkdir dirName -p
```

删除目录(当文件夹为空时)

```dash
rmdir dirName
```

删除目录(当文件夹非空时)

```dash
rm dirName -ri --r:递归操作 i:提示
```

新建文件

```touch
touch fileName --若文件已存在则更新文件的最后修改日期，不覆盖内容
```

删除文件

```dash
rm fileName
```

复制文件/目录

```dash
cp sourse_fileName/dirName tag_fileName/dirName
	--源文件					目标文件
```

修改文件/目录名字

```bash
mv old_fileName new_fileName 
```

移动文件/目录

```bash
mv old_fileName path	--当第二个参数是路径的话，mv执行移动操作
```

文件和目录属性命令

```bash
wc fileName
od fileName
du fileName/dirName -h
df fileName/dirName -h
```



## 查看文件内容

1. cat
2. more
3. less
4. head
5. tail



## 文件软/硬链接

创建文件软链接

```bash
ln -s fileName linkName
--软链接以文件绝对路径为好
--软链接文件占用连接名所需字节
```

创建文件硬链接

```bash
ln fileName linkName
--硬链接不占空间,与原文件指定同一i结点
```



## 文件/目录权限管理

查看当前登录用户

```bash
whoami
```

文字设定法

```bash
chmod [+|-|=]ugo fileName/dirName
```

数字设定法

```bash
chmod [ugo][+|-|=][rwx] fileName/dirName
```

修改文件所有者

```bash
chown userName filePath
```

修改文件所属组

```bash
chgrp groupName filePath
```





## 文件查找/检索

1. 按文件属性查找

- 按文件名

```bash
find Path -name "fileName"
```

- 按文件大小

```bash
find Path -size "[-|+]size"
find Path -size "[-|+]size" -size "[-|+]size"	--取中间范围
```

- 按文件类型

```bash
find Path -type f/b/d/c/s/p/l
```



2. 按文件内容查找

```bash
grep -r "String" Path
```



## 压缩文件

gzip压缩

```bash
gzip fileName	--只能压缩文件，不能打包,后缀.gz
```

gunzip解压缩

```bash
gunzip fileName	--不能解压缩其他压缩格式文件
```



bzip2压缩

```bash
bzip2 fileName		--只能压缩文件，不能打包，后缀.bz2
```

bunzip2解压缩

```bash
bunzip2 fileName	--不能解压缩其他压缩格式文件
```



tar压缩

```bash
tar zcvf tag_fileName.tar.gz Source_fileName	--可以打包多个压缩文件
```

>参数含义：
>
>c -- 创建
>x -- 释放
>v -- 显示提示信息
>f -- 指定压缩文件的名字
>
>z -- 使用gzip方式压缩文件  -- .gz
>j -- 使用bzip2方式压缩文件 -- .bz2

tar解压缩

```bash
tar zxvf fileName.tar.gz
```

tar解压缩到指定目录

```bash
tar zxvf fileName.tar.gz -C dirName/
```

> -C	Content目录



rar压缩

```bash

```





zip压缩

```bash

```

