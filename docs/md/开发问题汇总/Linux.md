1、根据日志去查找错误

说明：-A:关键词之后，-C 关键词前后，-B关键词之前  ，100代码展示的行数，''中写需要查找的信息 

```linux
grep -A 100 '日志关键字' logs/app.log
```

2、实时查看日志文件

```
tail -f 文件名称
```

3、vim编写文件强制退出，再次进入出现异常（Found a [swap](https://so.csdn.net/so/search?q=swap&spm=1001.2101.3001.7020) file by the name）

```linux
//系统中产生了swap文件
vi -r 【文件名称】 恢复文件
//但是此时swap文件并没有消失，每次打开对应文件都会出现这个问题
rm删除就可以
```

4、查看磁盘空间

```
df -h
```

5、查看当前目录下面文件大小并排序

```
du -s * | sort -nr | head
du -h --max-depth=1
```

6、搜索一个文件中相关字符

```
more 文件名称
回车之后输入 /搜索的内容
```

