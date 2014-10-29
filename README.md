#目录
* 1.什么是整洁的代码？
* 2.有意义的命名
	* 2.1 名副其实
	* 2.2
* 3.分支条件语句
	* 3.1 
	* 3.2
	* 3.3 
* 4.方法/函数
	* 4.1
	* 4.2
* 5.类
	* 5.1
	* 5.2
	* 5.3
* 6.注释
	* 6.1
	* 6.2
	* 6.3
* 7.错误处理
	* 7.1 C语言风格
	* 7.2 Golang风格
	* 7.3 基于java异常体系
	* 7.4 数据库事务处理原则
* 8.面向对象六大设计原则:OCP
	* 8.1 合成复用原则
	* 8.2 责任单一原则
	* 8.3 李氏替代原则
	* 8.4 迪米罗法则
	* 8.5 依赖倒置原则
	* 8.6 接口隔离原则

##什么是整洁的代码?
<b> Bjarne Stroustrup，C++之父：</b>
 
* 我喜欢优雅、高效的代码 
* 逻辑应该是清晰的，bug难以隐藏；
* 依赖最少，易于维护；
* 错误处理完全根据一个明确的策略；
* 性能接近最佳化，避免代码混乱和无原则的优化；
* 整洁的代码只做一件事。

<b> Grady Booch，《面向对象分析与设计》作者：</b> 

* 整洁的代码是简单、直接的；
* 整洁的代码，读起来像是一篇写得很好的散文；
* 整洁的代码永远不会掩盖设计者的意图，而是具有少量的抽象和清晰的控制行。

<b> Dave Thomas，OTI公司创始人，Eclipse战略教父：</b> 

* 整洁的代码可以被除了原作者之外的其他开发者阅读和改善；
* 具备单元测试和验收测试；
* 有一个有意义的名字；
* 使用一种方式来做一件事情；
* 最少的依赖，并明确定义；
* 提供了一个清晰的、最小的API；
* 应该根据语言特性，在代码中单独显示必要的信息，而不是所有的信息。

<b> Michael Feathers，《修改代码的艺术》作者：</b> 

* 整洁的代码看起来总是像很在乎代码质量的人写的；
* 没有明显的需要改善的地方；
* 代码的作者似乎考虑到了所有的事情。

<b>Ward Cunningham，Wiki和Fit创始人，极限编程联合创始人，Smalltalk和面向对象的思想领袖：</b> 

* 当你读代码时，你发现每个程序都如你期待的那样
* 你可以称之为漂亮的代码
* 代码完美展现了该编程语言的设计目的

<b><font color=red>
总之，整洁的代码的特点： 

* 容易与其他人协作（简单、意图明确、良好的抽象、不出意料、合适的名称）
* 针对现实世界，比如，有一个清晰的错误处理策略
* 代码作者显然很关心软件和其他开发者（针对双方的可读性和可维护性）
* 最小化（做一件事，最小的依赖）
* 以最合适的方式解决问题

</b>
</font>


#从变量命名谈起

## 把信息装到名字中
>关键思想：`把信息装到名字中`

避免使用“空洞”的词，比如
```python
def getPage(url):
```

get这个词没有表达出更多的信息，这个方法是从本地缓存得到一个页面，还是从数据库中，或者是从互联网中？如果是从互联网中，更专业的名字是 `downloadPage()` 

再比如：
```java
class BinaryTree {
	int size();
}
```
你期望size()返回什么呢？树的高度，节点数，还是树在内容中占的空间？
问题在于，size()名字承载了太多的信息，太泛。更好的名字是，`height()`, `numberNode()`,`memeoryBytes()`

## 使用具体的名字代替抽象的名字

## 带单位的变量

```java
start(int delay)   									delay -> delaySecs 
createCache(int size)								size -> sizeMb
throttleDownload(float limit)						limit -> limitKps
rotate(float angle) 								angle -> degreesCw
```
再举几个例子：
```java
int d // 消逝的时间，以日计
```
就没有下面这个几个名字好：
```java
int elapsedTimeInDays;
int daysSinceCreate;
int daysSinceModification;
int fileAgeInDays
```

## 做有意思的区分
```c
char *copyChars(char *a1, char *a2);
```
vs
```c
char * strcpy(char *dest, char *src);
```
哪一个方法（函数）更好？毫无疑问是第二个，见名知意。

如果在项目中出现一个类叫 `Product`, `ProductInfo`, `ProductData`。名字虽然不同，但是意思却无法区别。

* variable 一词永远都不应该出现在变量名中
* table 一词永远都不应该出现在表名中
* nameString 比name好吗？

```java
getActiveAccount();
getActiveAccountInfo();
getActiveAccountDate();
```
只看名字使用者能知道该调用哪一个方法吗？
如果缺少明确约定：

* moneyAmount就和money没有任何区别
* costomerInfo就和customer没有任何却别
* accountDate就和account没有任何区别
* theMessage就和message没有任何却别


## 避免魔术

## 注释
>关键思想：`注释的目的是尽量帮助读者了解的和作者一样多。`

>`当你写代码时，在你的脑海里会有很多有价值的信息。当其他人读你的代码时，这些信息已经丢失了，他们所见到的只是眼前的代码。`

## 不要给不好的名字添加注释--应该把名字改好
举例：
```java
// Releases the handle for this key. This doesn't modify the actual registry.
void delteRegistry(RegistryKey key);
```
deleteRegitry() 这个名字听起来像是一个危险的函数（它会删除注册表？！）注释里写道“它不会改动真正的注册表”是想澄清困惑。

其实，我们可以用一个更加自我说明的名字，就像：
```java
void relaseRegistryHandle(RegistryKey key);
```
通常来讲，你不需要“拐杖式注释”--试图粉饰可读性差的代码的注释。
* 好代码 > 坏代码 + 好注释

## 加入导演评论

## 为代码中瑕疵写注释

## 给常量加注释

# 分支条件语句
> 关键思想: `把条件、循环以及其他对控制流的改变做得越自然越好，运用一种方式使读者不用停下来重读你的代码`

## 把控制流变得易读

```java
if (length >= 10)
```
```java
if (10 <= length)
```
对绝大多数程序员来说，第一段更容易读。那么，下面的两段呢？
```java
while (bytesReceived < bytesExpected)
```
```java
while (bytes_expected > bytes_received)
```
仍然是第一段更容易读。可为什么是这样？通用规则是什么？这么决定是写成 a > b 好些，还是 a < b 好些？
>原则如下：

* 比较的左侧："被询问"的表达式，它的值更倾向于不断的变化
* 比较的右侧： 用来做比较的表达式，它的值更倾向于常量

## 语句块的顺序
```java
if (a == b) {
	// case one
} else {
	// case two
}
```
也可以写成
```java
if (a != b) {
	// case two
} else {
	// case one
}
```
之前你可能没有想过太多，但在有些情况下有理由相信其中一种顺序比另一种好：
* 首先处理正逻辑而不是负逻辑的情况。
* 首先处理掉简单的情况，这种方式可能还会使得if和else在屏幕之内都可见。
* 首先处理有趣的或者可疑的情况
有时候这些倾向性之间会有冲突，那么就要靠自己判断了。请记住：“没有银弹”。

##最小化嵌套
```java
if (userResult == SUCCESS) {
	if (permissionResult != SUCCESS) {
		reply.writeErrors("error reading permissions");
		reply.done();
		return;
	}
	replay.writeErrors("");
} else {
	replay.wirteErrors(userResult);
}
replay.done();

```
通过提早返回来减少嵌套：
```java
if (userResult != SUCCESS) {
	replay.wirteErrors(userResult);
	reply.done();
	return;
}

if (permissionResult != SUCCESS) {
	reply.writeErrors("error reading permissions");
	reply.done();
	return;
}

replay.wirteErrors("");
reply.done();

```
## 减少循环内的嵌套
```java
for (int i = 0; i < results.size(); i++) {
	if (result[i] != null) {
		nonNullCount++;
		if (results[i].name != "") {
			System.out.println("considerint candidate...");
			...
		}
	}
}
```
在循环中提早返回的技术是continue
```java
for (int i = 0; i < results.size(); i++) {
	if (result[i] == null) {
		continue;		
	}
	nonNullCount++;
	if (results[i].name != "") {
		System.out.println("considerint candidate...");
		...
	}
}
```
### 拆分超长表达式,用作解释的变量
``` python
if line.split(':')[0].strip() == "root" :
	# do something
```
和上面是同样的代码，但是现在有了一个解释变量。
``` python
username = if line.split(':')[0].strip()
if username == "root":
	# do somethong...
```
### 拆分超长表达式,总结变量
```java
if (request.userId == document.ownerId) {
	// user can edit this document...
}
...
if (request.userId != document.ownerId) {
	// document is read only
}
```
第一种做法：
```java
final boolean userOwnsDocument = (request.userId == document.ownerId);

if (userOwnsDocument) {
	// user can edit this document
}
```
第二种做法：
```java
boolean userCanEdit() {
	return request.userId == document.ownerId;
}

if (userCanEdit()) {
	// user can edit this document...
}
```

### 减少没有价值的临时变量

```python
now = datetime.datetime.now();
root_message.last_view_time = now
```

```python
root_message.last_view_time = datetime.datetime.now();
```





##

##有问题反馈
在阅读过过程中有任何问题，欢迎反馈给我，可以用以下联系方式跟我交流

* 邮件(jinlei.wjl#alibaba-inc.com, 把#换成@)
* QQ: 692548668


##捐助开发者
在兴趣的驱动下,写一个`免费`的东西，有欣喜，也还有汗水，希望你喜欢我的作品，同时也能支持一

##感激
感谢以下的几本书的作者,排名不分先后

* [Code Complate]() 
* [Clean Code]()
* [Refactor:improving the design of the existing code]()
* [The Art of Readable Code]()

##关于作者

 王金雷
