

1、chmod 777 helloworld.sh 给该脚本赋予权限，之后可以通过./helloworld.sh 执行脚本

2、向文件中追加文本 echo "文本内容" >> XXX.txt



3、shell中的变量

系统变量

自定义变量

![image-20231216160639294](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231216160639294.png)

撤销变量：unset A

自定义只读变量：readonly B=1

默认变量都是字符串类型，不能直接进行运算，1+1 执行之后 还是1+1，有文本较长，中间有空格，需要给""

![image-20231216161042049](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231216161042049.png)

将变量提升为全局变量：export 变量名称



特殊变量

$0:代表脚本名称

$1-9:代表第一到第九个参数

$#：获得所有参数的个数

$*：将所有参数拿到

$@：将所有参数拿到

![image-20231216162507402](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231216162507402.png)

$?：查看上一条命令是否执行成功

![image-20231216162752531](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231216162752531.png)

运算符

![image-20231217123644327](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217123644327.png)

expr 和运算符之间要有空格

![image-20231217123807941](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217123807941.png)

条件判断

![image-20231217124228031](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217124228031.png)

![image-20231217124339305](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217124339305.png)



流程控制

![image-20231217130545010](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217130545010.png)



case

![image-20231217131349598](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217131349598.png)



for循环

语法1

![image-20231217132356885](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217132356885.png)

语法2：注意$*是一次性拿到所有参数赋值，$@是一个一个拿

![image-20231217135033458](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217135033458.png)

while循环

![image-20231217140117889](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217140117889.png)

read读取控制台输入

![image-20231217141024654](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217141024654.png)



系统函数

basename：删掉前面所有的路径包括最后一个'/'，将文件名字显示出来

dir：删除文件名称，拿到文件所在目录的绝对路径

![image-20231217141640989](C:\Users\wujunhong\AppData\Roaming\Typora\typora-user-images\image-20231217141640989.png)



自定义函数

1、函数必须先定义，再使用，shell是从上到下执行，函数的定义必须在前

2、函数的返回值，使用$?获得，可以显示加return返回，如果不加，将以最后一条命令的运行结果作为返回值

