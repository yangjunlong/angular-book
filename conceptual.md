# 概念大纲

| 概念 | 描述 | 
|:---------------------------|:---------------| 
| Template | 模板，带有附加标记的HTML | 
| Directives | 指令， 使用自定义属性和元素扩展html | 
| Model | 模型，在视图中显示给用户的数据，以及用户交互的数据。 | 
| Scope | 作用域， 模型的上下文，以便控制器、指令和表达式可以访问它。 |
| Expressions | 表达式，从作用域中访问变量、函数 |
| Compiler | 编译器，用来解析模板实例化指令和表达式 |
| Filter | 过滤器，将表达式的值格式化后显示给用户 |
| View | 视图 |
| Data Binding | 数据绑定，在模型和视图之间同步数据 |
| Controller | 控制器 视图背后的业务逻辑|
| Dependency Injection | 依赖注入，创建和连接对象和函数 |
| Injector | 依赖注入容器 |
| Module | 模块，应用程序的不同部分的容器，包括控制器、服务、过滤器、配置注射器的指令。 |
| Service | 服务，独立于视图的可重用业务逻辑 

## 第一个例子：Data binding

在下面的例子中，我们将建立一个表单来计算不同货币的发票成本。

数量和成本作为输入字段，它们值的乘积即为发票总额：

[index.html]()
```html
<div ng-app ng-init="qty=1;cost=2">
  <b>Invoice:</b>
  <div>
    Quantity: <input type="number" min="0" ng-model="qty">
  </div>
  <div>
    Costs: <input type="number" min="0" ng-model="cost">
  </div>
  <div>
    <b>Total:</b> {{qty * cost | currency}}
  </div>
</div>
```

<iframe src="./example/invoice.html" style="width: 100%; height: 250px;"></iframe>

试试上面的实时预览，然后让我们回头看一下这个例子，解释下为什么会有这样的结果。

上面的文件看起来像普通的HTML，带有一些新的标记。在AngularJS中，像这样的一个文件被称之为模板(template)。当AngularJS启动你的应用程序，他会通过编译器(compiler)解析和处理模板中这些新标签。已加载，被转换和渲染的DOM被称作视图。

![concepts-databinding](./static/img/concepts-databinding1.png)

第一种新的标记是指令(directives)，他们应用特殊的行为到HTML中的属性或元素。在上面的例子中，我们在html标签中使用了`ng-app`这个属性，用来自动初始化APP。AngularJS还为输入元素定义了一个指令，增加了元素额外的行为。`ng-model`指令存储/更新输入字段的值到变量中

> 自定义指令访问DOM：如果您需要直接访问DOM，您应该为此编写一个自定义指令。

第二种新的标记是双大括号`{{ expression | filter }}`: 当编译器遇到这个标记时，它将用标记的目标值替换它。模板中的表达式类似JavaScript代码片段用来读写AngularJS中的变量(注意这些变量不是全局变量)。就像JavaScript中的函数作用域一样，AngularJS提供了一个scope为表达式访问变量。

**AngularJS中的表达式有如下特点：**

* 只能在其所属作用域内部
> 所有的表达式都在其所属的作用域内部执行，并有访问本地$scope的权限。
* 允许未定义
> 在html中可以使用未在angularJS定义的变量，不会抛出异常
* 不能使用流控制
> 不能使用任何流控制包括条件语句，如if/else
* 过滤器
> 可以接收过滤器和过滤器链，使用 | 符号连接过滤器

上面的例子还包含了一个过滤器(filter)，过滤器将表达式的值格式化后显示给用户，在上面的例子中过滤器`currency` 格式化数值为货币形式。

上面例子最重要的是AngularJS提供了数据实时绑定：不论输入表单中的值如何变化，表达式的值都会自动重新计算并更新到页面上。这背后的概念就是：`双向数据绑定`。

## 添加UI逻辑：Controllers

让我们为这个例子添加一些逻辑，允许我们输入和计算不同货币的成本，并支付发票。

```html
<!doctype html>
<html>
  <head>
    <script src="../static/lib/angularjs/1.6.5/angular.js"></script>
  </head>
  <body>
    <div ng-app="invoice1" ng-controller="InvoiceController as invoice">
      <b>Invoice:</b>
      <div>
        Quantity: <input type="number" min="0" ng-model="invoice.qty" required >
      </div>
      <div>
        Costs: <input type="number" min="0" ng-model="invoice.cost" required >
        <select ng-model="invoice.inCurr">
          <option ng-repeat="c in invoice.currencies">{{c}}</option>
        </select>
      </div>
      <div>
        <b>Total:</b>
        <span ng-repeat="c in invoice.currencies">
          {{invoice.total(c) | currency:c}}
        </span><br>
        <button class="btn" ng-click="invoice.pay()">Pay</button>
      </div>
    </div>

    <script type="text/javascript">
      angular.module('invoice1', [])
      .controller('InvoiceController', function InvoiceController() {
        this.qty = 1;
        this.cost = 2;
        this.inCurr = 'EUR';
        this.currencies = ['USD', 'EUR', 'CNY'];
        this.usdToForeignRates = {
          USD: 1,
          EUR: 0.74,
          CNY: 6.09
        };

        this.total = function total(outCurr) {
          return this.convertCurrency(this.qty * this.cost, this.inCurr, outCurr);
        };
        this.convertCurrency = function convertCurrency(amount, inCurr, outCurr) {
          return amount * this.usdToForeignRates[outCurr] / this.usdToForeignRates[inCurr];
        };
        this.pay = function pay() {
          window.alert('Thanks!');
        };
      });
    </script>
  </body>
</html>
```
<iframe src="./example/invoice1.html" style="width: 100%; height: 250px;"></iframe>
