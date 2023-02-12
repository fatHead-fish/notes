# JSX简介

```jsx
const element = <h1>Hello,world!</h1>
```

上面code称为JSX,是一个JavaScript的语法扩展.我们建议在React中配合使用JSX,JSX可以很好地描述UI应该呈现出它应有的交互的本质形式.JSX可能会使人联想到模版语言,但它具有JavaScript的全部功能.

## 为什么使用JSX?

React认为渲染逻辑本质上与其他UI逻辑存在耦合,比如,在UI中需要绑定处理事件、在某些时刻状态发生变化时需要通知到UI,以及需要在UI中展示准备好点的数据.

React并没有采用将标记与逻辑分离到不同文件这种人为的分离方式,而是通过将两者共同存放在称之为“组件”的松散耦合单元之后,来实现`关注点分离` .

React不强制要求使用JSX,但是大多数人发现,在JavaScript代码中将JSX和UI放在一起时,会在视觉上有辅助作用.他还可以使React显示更多的错误和警告消息.

## 在JSX中嵌入表达式

在JSX语法中,你可以在大括号中放置任何有效的JavaScript表达式.

## JSX也是一个表达式

在编译之后,JSX表达式会被转为普通JavaScript函数调用,并且对其取值后得到JavaScript对象.

也就是说,你可以在if语句和 for循环的代码块中使用JSX,将JSX赋值给变量,把JSX当作参数传入,以及从函数中返回JSX

## JSX中指定属性

可以通过使用引号,来将属性值指定为字符串字面量

也可以使用大括号,来在属性中插入一个JavaScript表达式

在属性中嵌入JavaScruipt表达式时,不要在大括号外面加入引号,你应该仅使用引号(对于字符串值)或大括号(对于表达式)中的一个,对于同一属性不能同时使用这种符号.

```ts
警告⚠️:
	因为JSX语法上更接近JavaScript而不是HTML,所以React DOM使用cameCase(小驼峰命名)来定义属性的名称,而不使用HTML属性名称的命名约定
例如,JSX里的clas变成了className,而tabindex而变为tabIndex
```

## 使用JSX指定子元素

假如一个标签里面没有内容,你可以使用`/>` 来闭合标签,就像XML语法一样:

```ts
const element = <img src={name}/>
```

JSX标签能够包含很多子元素

## JSX防止注入攻击

可以安全地在JSX当中插入用户输入内容:

```ts
const title = response.potentiallyMalicousInput
//直接使用是安全的
const element = <h1>{title}</h1>
```

React DOM在渲染所有输入内容之前,默认会进行转义.它可以确保在你的应用中,永远不会不会注入那些并非自己明确编写的内容.所有的内容在渲染之前都被转换成了字符串.这样可以有效得防止`XXS	(cross-site-scripting,跨站脚本)`攻击.

## JSX表示对象

Babel会把JSX转译成一个名为`React.createElement()`函数调用.

以下两种示例代码完全等效:

```ts
const element = (
	<h1 className="greeting">
  	hello,world
  </h1>
)
```

```jsx
const element = React.createElement(
	'h1',
  {className:'greeting'},
  'hello,world'
)
```

React.createElement() 会预先先执行一些检查,以帮助你编写无错代码,但实际上它创建了一个这样的对象:

```ts
//注意,这是简化过的结构
const element = {
  type:'h1',
  props:{
    className:'greeting',
    children:'hello,world'
  }
}
```

这些对象被称为“React元素”,它们描述了你希望在屏幕上看到的内容,React通过读取这些对象,然后使用它们来构建DOM以及保持随时更新.