上一章：[Chapter3：角色定义](Chapter3%EF%BC%9A%E8%A7%92%E8%89%B2%E5%AE%9A%E4%B9%89.md)
___
# 函数实现
## 函数的基本结构
函数的基本结构和python中的函数极为类似：
```python
func 函数名(所接受的参数):[
	函数命令
	return <执行命令所返回的值>
]
```
下面是一个示例：
```python
func add(num):[
	将获取到的num进行相加
	return <added>
]
```
在这个函数中，参数是`num`，函数命令是`将获取到的num进行相加`，返回的结果是`added`。

我们可以在[GPT代码解释器](prompts/GPT%E4%BB%A3%E7%A0%81%E8%A7%A3%E9%87%8A%E5%99%A8.md)这个prompt中实现这个功能：
![Pasted image 20230731095332](../attachments/Pasted%20image%2020230731095332.png)

发现了？你可以将参数定义为一个参数，而GPT自己会进行理解并执行功能。我们这里可以再换一下，让GPT相加出来一个句子。
![Pasted image 20230731095740](../attachments/Pasted%20image%2020230731095740.png)
而且你也会发现，**GPT自身可以接受多个实际参数，不论它们是否含义真的对的上形式参数**。
# 基本功能
## 基础函数(basic_functions)
基础函数一般是**对于GPT的输出格式所要求的通用函数**，在代码解释器中分别是say、block和sep，分别对应的是打印字符、代码块和分隔符。
**这类函数往往在多个提示词中均可使用。**

## 初始化函数(\_\_initfunctions\_\_)
而text_0和model等函数一般用作初始化函数，放在`__initfunctions__`中，功能是**让GPT产生初始化信息**。

# 功能
该类函数是让GPT执行自己在提示词中的职能的函数，而代码解释器能作为模板的原因就是：
**它的功能函数很少，可以让我们只修改少量函数即可添加功能函数投入使用。**

**在功能函数中，传递的参数除了实际参数，函数也可以作为参数的一部分**，一般该类形参被命名为`func`，如下是一个示例：
```python
	        func TUI(self,func):[
	                self.say("name:"<name>"\nversion:"<version>"\nauthor:"<author>"\n代码执行结果:\n"<block><func><block>)
	        ],
```
函数`TUI`将会接收一个函数作为参数放在`<func>`中产生结果，也就有了如下的有name、version和author的输出：
![Pasted image 20230731100635](../attachments/Pasted%20image%2020230731100635.png)
否则：
![Pasted image 20230731100700](../attachments/Pasted%20image%2020230731100700.png)

一般在提示词对于功能函数的嵌套是在让GPT按照格式输出文本这一功能函数内，如我的[GPT题目解决老师](prompts/GPT%E9%A2%98%E7%9B%AE%E8%A7%A3%E5%86%B3%E8%80%81%E5%B8%88.md)中就有如下功能函数：
![Pasted image 20230731101015](../attachments/Pasted%20image%2020230731101015.png)
在该功能函数中，将上面基本所有的功能函数都作为实际功能的一部分，不过并没有在参数中将函数作为参数进行传递，理由我在前言中也说了：
“**部分在编程中的严格要求在函数类提示词中即使并没有按照相关的要求写提示词，GPT也可以很好的理解并执行功能**。”
___
下一章：[Chapter5：规则](Chapter5%EF%BC%9A%E8%A7%84%E5%88%99.md)