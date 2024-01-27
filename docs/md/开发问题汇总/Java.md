## 1、@jsonField 和@JsonProperty的区别？

解决问题：json和对象之间转化

@jsonField注解-----从属于fastjson包

json转对象：JSON.toJSONString(实体类)

对象转json：JSON.parseObject(字符串,实体类.class)

@JsonProperty------从属于jackson包

json转对象：ObjectMapper().writeValueAsString(实体类)

对象转json：ObjectMapper().readValue(字符串)

## 2、git将某一次提交合并到特定分支

```
找到提交的commit 号 -->切换目标分支-->git cherry-pick  commit号 -->git push
```

## 3、注解汇总

```
1、@SuppressWarnings({"all"})  //取消一些编译器产生的警告对代码左侧行列的遮挡
2、@Scope("prototype") //默认情况下，从bean工厂所取得的实例为Singleton（bean的singleton属性） Singleton: Spring容器只存在一个共享的bean实例，默认的配置。 Prototype: 每次对bean的请求都会创建一个新的bean实例。二者选择的原则：有状态的bean都使用Prototype作用域，而对无状态的bean则应该使用singleton作用域。
3、@PostConstruct：Java自带的注解，在方法上加该注解，会在项目启动的时候执行这个方法，也可以理解为在spring容器启动的时候执行，可作为一些数据的常规化加载，比如数据字典之类的。@PostConstruct注解的方法将会在依赖注入完成后被自动调用。
4、@Value("${inter.cfg-dev:dev}")，将配置文件中名为"inter.cfg-dev"的属性值注入到当前的Java代码中，如果找不到该属性，则使用默认值"dev"。
```

## 4、bitmap数据结构、布隆过滤器

BitMap非常适合对整型的海量数据进行查询统计、排序、去重；适合对两个集合做交集、并集运算，但不支持非运算，如果需要进行非运算则需要提供一个全量的BitMap才行。

## 5、状态机

https://blog.csdn.net/qq_45443879/article/details/123992480

状态机的使用场景：工作流业务，**每一种状态都和变化前的状态以及执行的操作有关**

订单状态机表示了一笔订单的生命周期，按照一定的方向通过触发不同的事件去产生数据流转的过程

状态机的四要素：状态-->事件-->动作-->转换 

状态机需要具备：前置状态+操作（事件触发）+后置状态

状态（现态）：当前的状态

事件（条件）：当事件被满足后竟会触发一个动作，或者执行一次状态的迁移

动作：条件被满足后执行的动作，当条件满足后，也可以不执行任何动作，直接迁移到新状态

转换（次态）：条件满足后要迁移往的新状态。“次态”是相对于“现态”而言的，“次态”一旦被激活，就转变成新的“现态”了。

## 6、日志信息

```Java
    private static final Logger log = LoggerFactory.getLogger(OrderItemNode.class);
    使用指定的类XXX初始化日志对象，方便在日志输出的时候，可以打印出日志信息所属的类。
```

## 7、对象之间属性拷贝相关问题

```Java
//代理对象和普通对象之间的属性不能相互拷贝，需要先把被代理的对象拿出来
Object nodeObj = ((Advised)singleNode).getTargetSource().getTarget();
```



## 8、spring boot错误

1、测试类报 bean无法注入的问题：需要保证主类和测试类目录结构一致

2、远程debug

```
java -Xdebug -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 -jar demo.jar

```

## 9、大数的精确计算：BigDecimal

在创建BigDecimal对象的时候，参数一般建议使用String

https://blog.csdn.net/haiyinshushe/article/details/82721234



## 10、多线程 正确追踪日志方法

首先，`MDC.put("TRACE_ID", arg.getBodyStr("PAYBILL_ID"))`将一个名为"TRACE_ID"的key和"PAYBILL_ID"的value保存到当前线程的MDC中。这里的"PAYBILL_ID"可能是一个请求或交易的唯一标识，通过将其与线程绑定，可以在后续的日志输出中更方便地跟踪该请求或交易的日志信息。

接着，程序会执行其他操作，这期间可能会有其他线程被执行。但是由于MDC中保存的信息是与线程绑定的，因此不会互相干扰。

最后，`MDC.remove("TRACE_ID")`将"TRACE_ID"从当前线程的MDC中删除，以免对后续线程的日志输出产生影响。

总的来说，这段代码用来在日志中记录请求或交易的关键信息，帮助在后续的调试和排查问题时更容易地定位和追踪相关日志信息。

## 11、isEmpty 和isBlank 的区别

1.isEmpty 没有忽略空格参数，是以是否为空和是否存在为判断依据。

2.isBlank 是在 isEmpty 的基础上进行了为空（字符串都为空格、制表符、tab 的情况）的判断。（一般更为常用）
3.如果允许包含空格,则使用isEmpty判空。

## 12、调用链、鹰眼

## 13、XXL-JOB

## 14、切面、拦截器、过滤器

## 15、不同仓库、分支代码同步

```shell
仓库同步
#/bin/sh
source_git=`cat git.txt | grep "source_git=" | awk -F"=" '{print $2}' `
target_git=`cat git.txt | grep "target_git=" | awk -F"=" '{print $2}' `
path=${source_git##*/}
echo $path
echo "git clone --bare $source_git"
git clone --bare  $source_git
cd   $path
git remote add origin2  $target_git
git  push --mirror $target_git
```

```shell
分支同步
#/bin/sh
source_git=`cat git.txt | grep "source_git=" | awk -F"=" '{print $2}' `
target_git=`cat git.txt | grep "target_git=" | awk -F"=" '{print $2}' `
syc_branchs=`cat git.txt | grep "syc_branchs=" | awk -F"=" '{print $2}' `
path=${source_git##*/}
path2=${path%.*}
if [ ! -d "$path2" ];then
 echo "文件夹不存在,$path2 "
 git clone  $source_git
 cd   $path2
 git remote add origin2  $target_git
else
  echo "文件夹已经存在$path2 "
  cd   $path2 
fi
  res_branchs=$syc_branchs
  array=(${res_branchs//,/ }) 
  for branch in ${array[@]}
	do
	echo "推送的分支,$branch "
	git fetch -p origin
    git checkout -b $branch origin/$branch 
	git checkout	$branch
    git pull --force origin $branch:$branch  --allow-unrelated-histories
    git push -f origin2 $branch:$branch
  done
```

需要读取的文件

```shell
source_git=http://oauth2:XN9GySsMZB8BJJQGSY6h@git.si-tech.com.cn:9002/xiongml/test.git
target_git=http://oauth2:TTstxWKtNZrWcPMFHvxU@172.18.232.31/xiongml/test.git
syc_branchs=dev,test,master
```

## 16、idea激活码

```javascript

```

## 17、幂等性校验

场景（因为重复提交导致的数据不安全）

1、前端重复提交

用户注册，用户创建商品等操作，前端都会提交一些数据给后台服务，后台需要根据用户提交的数据在数据库中创建记录。如果用户不小心多点了几次，后端收到了好几次提交，这时就会在数据库中重复创建了多条记录。这就是接口没有幂等性带来的 bug。

2、接口超时重试

对于给第三方调用的接口，有可能会因为网络原因而调用失败，这时，一般在设计的时候会对接口调用加上失败重试的机制。如果第一次调用已经执行了一半时，发生了网络异常。这时再次调用时就会因为脏数据的存在而出现调用异常。

3、消息重复消费

在使用消息中间件来处理消息队列，且手动 ack 确认消息被正常消费时。如果消费者突然断开连接，那么已经执行了一半的消息会重新放回队列。

当消息被其他消费者重新消费时，如果没有幂等性，就会导致消息重复消费时结果异常，如数据库重复数据，数据库数据冲突，资源重复等。

解决方案

1、唯一索引 – 保证插入的数据只有一条
2、token机制 – 每次接口请求前先获取一个token，然后在请求的时候在请求的header体中加上这个token，后台进行验证，如果验证通过删除token，未通过校验，则提示token无效
3、悲观锁 – 获取数据的时候加锁(锁表或锁行)
4、乐观锁 – 基于版本号version实现, 在更新数据那一刻校验数据
5、分布式锁 – redis(jedis、redisson)或zookeeper实现
6、状态机 – 状态变更, 更新数据时判断状态

## 18、Activiti工作流

## 19、maven项目后出现‘parent.relativePath’ of POM错误时的解决方法

在pom文件中的spring-boot-starter-parent依赖中添加<relativePath/>属性

