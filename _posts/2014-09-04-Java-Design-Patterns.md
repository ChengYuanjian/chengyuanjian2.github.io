---
layout:         post
title:          Java 设计模式
description:    Java 23中设计模式说明和示例
keywords: Java, Design
category: Java
tags: [Java]
---

设计模式`Design pattern`是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。 毫无疑问，设计模式于己于他人于系统都是多赢的，设计模式使代码编制真正工程化，设计模式是软件工程的基石，如同大厦的一块块砖石一样。项目中合理的运用设计模式可以完美的解决很多问题，每种模式在现在中都有相应的原理来与之对应，每一个模式描述了一个在我们周围不断重复发生的问题，以及该问题的核心解决方案。

<!-- more -->

------------------

在Java中，有23种设计模式，可分为三大类：

* 1.__创建型Creational Patterns(5)__：抽象工厂`Abstract Factory`，工厂方法`Factory Method`，建造者`Builder`，原型`Prototype`，单例`Prototype`

* 2.__结构型Structural Patterns(7)__：适配器`Adapter`，桥接`Bridge`，复合`Composite`，装饰`Decorator`，外观`Facade`，享元`Flyweight`，代理`Proxy`

* 3.__行为型Behavorial Patterns(11)__：责任链`Chain Of Responsibility`，命令`Command`，解释器`Interpreter`，迭代`Iterator`，中介`Mediator`，备忘`Memento`，观察者`Observer`，状态`State`，策略`Strategy`，模板方法`Template Method`，访问者`Visitor`

此外，还有两类：并发型模式和线程池模式。用一个图片来整体描述一下：

![设计模式之间的关系图](http://dl.iteye.com/upload/attachment/0083/1179/57a92d42-4d84-3aa9-a8b9-63a0b02c2c36.jpg "设计模式之间的关系图【来源于网络】")

-------------------

###1.工厂方法|Factory Method

工厂方法模式分为三种：

* 普通工厂模式，就是建立一个工厂类，对实现了同一接口的一些类进行实例的创建。如图：

![普通工厂模式](http://dl.iteye.com/upload/attachment/0083/1180/421a1a3f-6777-3bca-85d7-00fc60c1ae8b.png)

* 多个工厂方法模式，是对普通工厂方法模式的改进，在普通工厂方法模式中，如果传递的字符串出错，则不能正确创建对象，而多个工厂方法模式是提供多个工厂方法，分别创建对象。

![多个工厂方法模式](http://dl.iteye.com/upload/attachment/0083/1181/84673ccf-ef89-3774-b5cf-6d2523cd03e5.jpg)

* 静态工厂方法模式，将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。

{% highlight java %}
public class SendFactory {
	
	public static Sender produceMail(){
		return new MailSender();
	}
	
	public static Sender produceSms(){
		return new SmsSender();
	}
}
{% endhighlight %}

总体来说，工厂模式适合：凡是出现了大量的产品需要创建，并且具有共同的接口时，可以通过工厂方法模式进行创建。

---------------------------

###2.抽象工厂|Abstract Factory

工厂方法模式有一个问题就是，类的创建依赖工厂类，也就是说，如果想要拓展程序，必须对工厂类进行修改，这违背了闭包原则，所以，从设计角度考虑，有一定的问题，如何解决？就用到抽象工厂模式，创建多个工厂类，这样一旦需要增加新的功能，直接增加新的工厂类就可以了，不需要修改之前的代码。

![抽象工厂](http://img.my.csdn.net/uploads/201211/29/1354159363_7245.PNG)

这个模式的好处就是，如果你现在想增加一个新功能只需做一个实现类，实现Sender接口，同时做一个工厂类，实现Provider接口，就OK了，无需去改动现成的代码，拓展性较好。

---------------------------

###3.单例模式|Singleton

在Java应用中，单例对象能保证在一个JVM中，该对象只有一个实例存在。

{% highlight java%}
public class SingletonTest {

	private static SingletonTest instance = null;

	private SingletonTest() {
	}

	private static synchronized void syncInit() {
		if (instance == null) {
			instance = new SingletonTest();
		}
	}

	public static SingletonTest getInstance() {
		if (instance == null) {
			syncInit();
		}
		return instance;
	}
}
{% endhighlight %}

---------------------------

###4.建造者模式|Builder

工厂类模式提供的是创建单个类的模式，而建造者模式则是将各种产品集中起来进行管理，用来创建复合对象，所谓复合对象就是指某个类具有不同的属性。

{% highlight java %}
public class Builder {
	
	private List<Sender> list = new ArrayList<Sender>();
	
	public void produceMailSender(int count){
		for(int i=0; i<count; i++){
			list.add(new MailSender());
		}
	}
	
	public void produceSmsSender(int count){
		for(int i=0; i<count; i++){
			list.add(new SmsSender());
		}
	}
}
{% endhighlight %}

可以看出，建造者模式将很多功能集成到一个类里，这个类可以创造出比较复杂的东西。所以与工长模式的区别就是：工厂模式关注的是创建单个产品，而建造者模式则关注创建复合对象。

---------------------------

###5.原型模式|Prototype

原型模式虽然是创建型的模式，但是与工厂模式没有关系。该模式的思想就是将一个对象作为原型，对其进行复制、克隆，产生一个和原对象类似的新对象。



* [Java 23中设计模式示例代码](http://www.fluffycat.com/Java-Design-Patterns/)
