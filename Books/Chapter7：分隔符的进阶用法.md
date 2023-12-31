上一章：[Chapter6：封装](Chapter6%EF%BC%9A%E5%B0%81%E8%A3%85.md)
___
# 分隔符到底有哪些用法？
我们在[第二章](Chapter2%EF%BC%9A%E5%88%86%E9%9A%94%E7%AC%A6.md)的时候就已经解释了分隔符是用来让GPT识别语言块的，这只是一个基本概括，实际的分隔符还有更多的用法，分别是：强调、说明和利用分隔符自身的含义。

我们接下来将进一步展示这些用法。
# 强调
强调在函数类提示词中用的并不多，一般来说在跟GPT平时进行沟通的时候用的更多，比如下面这样：
![Pasted image 20230801080402](../attachments/Pasted%20image%2020230801080402.png)
在上面这个提示词中，**两个连续的大括号`{{}}`中包裹的是我们所强调的操作**，要求GPT进行最大提示(maximizing prompts)进行分析等操作。

# 说明
**说明一般是会利用到分隔符自身的含义的**，比如小括号`()`，在我们上面的提示词中，小括号则起到解释说明什么是“最大提示”(最大化提示(maximizing prompts)是一种用于提高自然语言生成模型的性能和多样性的技术，它通过在输入中添加一些特定的符号或词语来引导模型生成更优质或更有创意的输出。)

也可以不利用分隔符本身的含义，不过一般这样就是直接利用分隔符对指定的词汇进行解释了，比如这样:`"最大化提示:maximizing prompts"`
就是直接对词汇进行解释，也能起到相同的效果。

# 利用分隔符自身的含义
**可以说函数类提示词的关键就在于GPT模型可以理解分隔符自身的含义**
这方面的例子很多，我只举出部分。

比如在**角色定义中，角色的版本、名称等都是字符串，因此是利用字典的数据格式，双引号`""`进行分隔来实现的角色定义**。

**在功能模块中，函数的形参是利用的小括号`()`进行包裹，随后后方像python一样接上引号，也可以让模型很好的理解如何实现功能。**
___
下一章：[Chapter8：函数进阶](Chapter8%EF%BC%9A%E5%87%BD%E6%95%B0%E8%BF%9B%E9%98%B6.md)