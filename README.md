![AngularJS](./static/AngularJS-large.png)

>`AngularJS`最初是由Miško Hevery和Adam Abrons于2009年开发，后来成为了`Google`的项目。`AngularJS`弥补了HTML在构建应用方面的不足，通过使用标识符（directives）结构，来扩展Web应用中的HTML词汇，使开发者可以使用HTML来声明动态内容，从而使得Web开发和测试工作变得更加容易。

## AngularJS是什么？
AngularJS是一个构建动态WEB应用程序的框架。它允许你使用HTML作为模板语言，并允许你扩展HTML的语法来清晰简洁的实现你的应用程序组件。AngularJS的数据绑定和依赖注入可以省掉很多你必须要编写的代码。

通常，我们是通过以下技术来解决静态网页技术在构建动态应用上的不足：

* **类库**
类库是一些函数的集合，它为你写的WEB应用提供了可重用的方法来帮助你快速实现某个功能，它只有在你需要的时候被调用。比如：jQuery等
* **框架**
框架是一种特殊的、已经实现了的WEB应用，你只需要对它填充具体的业务逻辑。这里框架是起主导作用的，由它来根据具体的应用逻辑来调用你的代码。框架有：durandal、ember等。

AngularJS试图去创建新的HTML标签来尝试补足HTML本身在构建应用方面的缺陷。AngularJS通过使用我们称为指令(directives)的结构，让浏览器能够识别新的语法。例如：

* 使用双大括号\{\{\}\}语法进行数据绑定(Data binding)
* 使用DOM控制结构来实现迭代、显示、隐藏DOM片段
* 支持表单和表单验证
* 将新的行为附加到DOM元素，比如DOM事件处理
* 将HTML分组成可重用的组件
