上一章：[Chapter7：分隔符的进阶用法](Chapter7%EF%BC%9A%E5%88%86%E9%9A%94%E7%AC%A6%E7%9A%84%E8%BF%9B%E9%98%B6%E7%94%A8%E6%B3%95.md)
___
# 函数分类
在函数类提示词中，**函数我分为两类，一类是输出函数，另一类是功能函数。**

**输出函数：让模型按照指定的格式输出内容。**

基本函数中的`say`函数就是一个最基本的输出函数。

代码解释器中的TUI也是一个输出函数，它指定了模型的输出格式和在指定的未知插入函数与变量。
```python
	    func TUI(self,func):[
	            self.say("name:"<name>"\nversion:"<version>"\nauthor:"<author>"\n代码执行结果:\n"<block><func><block>)
        ],
```
![[../attachments/Pasted image 20230801105252.png]]
**功能函数：模型在执行提示词后可以执行的功能。一般嵌套在输出函数中。**

我们的[概念解释GPT](prompts/GPT%E9%A2%98%E7%9B%AE%E8%A7%A3%E5%86%B3%E8%80%81%E5%B8%88.md)中用于举出例子的函数就是一个功能函数：
```python
			func eg(self,ques,subjO):[ 
				根据<ques>和<subjO>举出3个这个概念的正确使用例子和3个错误使用例子。
				return <eg_s>
			],
```

`sy`也是一个功能函数，不过同时也是一个输出函数，它使得`say`函数的内容可以嵌套进`TUI`函数内。
```python
	    func sy(self,text):[
	        return self.TUI(self.say(text))
      ],
```
![[../attachments/Pasted image 20230801105308.png]]
# 函数编写规则
函数我们在[第四节](Chapter4%EF%BC%9A%E5%8A%9F%E8%83%BD%E5%AE%9E%E7%8E%B0.md)中说过了功能是实现功能的主要手段，同时简单介绍了一下如何编写函数，现在我们就来深入说一下怎么编写函数。
**函数的组成有4部分**：
- **函数定义**
- **函数名**
- **形式参数**
- **命令**
- **返回值(可选)**
**就像这样**：
```python
func 函数名(所接受的参数):[
	函数命令
	return <执行命令所返回的值>
]
```

我们依旧拿[GPT代码解释](prompts/GPT%E4%BB%A3%E7%A0%81%E8%A7%A3%E9%87%8A%E5%99%A8.md)器中的一个函数作为示例进行解析。
```python
			func model(self):[
				获取你的自然语言模型的名称
				return <model_name>
			],
```
在这个示例中，`func`为函数定义，`model`为函数名，它的形参为`self`，即对象本身，命令为`获取你的自然语言模型的名称`，返回`model_name`。
我们看一下执行时的函数和结果：
```python
        func text_0(self):[
			    model_name = self.model()
	            say("您好，我是基于"+<model_name>+"的自然语言编程解释器Kiball，您现在可以对我输入函数和参数了。")
```
![Pasted image 20230801091706](../attachments/Pasted%20image%2020230801091706.png)
看看Claude那边的反应：
![Pasted image 20230801092331](../attachments/Pasted%20image%2020230801092331.png)
略有瑕疵，不过在起到演示作用的方面是没有问题的。

# 函数使用规则
**函数的使用规则与python相同，使用`函数名(实际参数)`来使用函数，但是相对并没有那么严谨。**

GPT是根据上下文来生成对话，因此：
![[../attachments/Pasted image 20230801102006.png]]
**可以看见我们函数使用时既没有正确使用`add()`，也没有传入参数，但是依旧可以正常使用功能。**

同理，我们有时候甚至在定义函数的时候可以连形参都不需要。
![[../attachments/Pasted image 20230801102240.png]]

**不过为了保证在复杂prompt中GPT可以正确的识别参数并传入，最好还是正确的定义和使用函数，以免出现识别错误导致功能不符合预期的问题**。

# 函数的嵌套使用
**功能函数一般不会单独使用，而是嵌套在一个输出函数中。嵌套的格式一般为`...<函数名>...`。**
其中`...`所代表的是输出函数的内容，`<函数名>`函数名中一般为功能函数的函数名，不建议在输出函数中嵌套输出函数，**因为GPT也正是因为不严谨所以有可能会丢失所嵌套输出函数。**

下方是[](prompts/Claude%E7%BF%BB%E8%AF%91%E6%9C%BA.md#3.1.1(CN))中一个输出函数中嵌套功能函数的示例：
```python
			func trans(subj,text,lang_1,lang_2):[
				自动以当前学科的语境对文本进行翻译
				return <text_trans>
			],
			
			func TUI(self,functions):[
				按照TUI的格式进行翻译
				say("源语种:"<lang_1>"|学科"<subj>"|目标语种:"<lang_2>"\n"+"翻译:"+<sep>+<trans>+<sep>+"当前学科中的易混词汇:"+<block>+<clear_words>+<block>+"当前学科中的专业词汇缩写:"+<block>+<terminology_trans>+<block>+"Kiball的自我提示:"+<block>+"我将继续以'源语种-自我提示'的格式继续进行翻译"+<block>)
				],
```
在该函数中，`trans`是一个功能函数，用于根据当前的学科和目标语种进行翻译。
输出结果：
![[../attachments/Pasted image 20230801112451.png]]
还不错。

# 如何编写出优秀的输出函数？
