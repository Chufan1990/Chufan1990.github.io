---
layout: post
title: 构造函数总结 constructor
date: 2017-08-23
categories: blog
tags: [Class, constructor, C++]
description: 总结构造函数的使用及注意事项
---

## 构造的存在意义

1. 在实例化的对象时，需要对对象中的数据进行初始化。

- 首先构造一个类	

	```
	class Tank
	{
		private:
			int m_iPosX;
			int m_iPosY;
		public:
			void init()
			{
				m_iPosX = 0;
				m_iPosY = 0;
			}
	};
	```
	
- 实例两个对象，并通过```void init()``` 初始化对象

	```
	int main()
	{
		Tank t1;
		t1.init();
		Tank t2;
		t2.init();

		return 0;
	};
	```

2. 对象初始化类型: 
- 1. 有且仅有一次
- 2. 根据条件初始化
	
3. 构造函数 - 避免初始化函数误操作

- 1. 构造函数在对象实例化时被自动调用
- 2. 构造函数与类同名
- 3. 构造函数没有返回值 （ 不用写void)
- 4. 构造函数可以有多重载形式
- 5. 实例化对象时仅用到一个构造函数
- 6. 当用户没有定义构造函数时，编译器自动生成一个构造函数

## 构造函数的种类

* 无参构造函数
```
class Student
{
	public:
		Student(){m_strName = "jim";}
	private:
		string m_strName;
};
```

* 有参构造函数
```
class Student
{
	public:
		Student(string name)
		{m_strName = name;}
	private:
		string m_strName;
};
```

* 重载构造函数（需遵循重载函数的规则）
```
class Student
{
	public:
		Student(){m_strName = "jim";}
		Student(string name)
		{m_strName = name;}
	private:
		string m_strName;
};
```

* 默认构造函数: 不需要传递参数的构造函数

### 初始化列表
```
class Student
{
	public:
		Student(): m_strName("jim"), m_iAge(10){}
	private:
		string m_strName;
		int m_iAge;
};
```

1. 初始化列表的热点
> 
> 初始化列表先于构造函数执行
> 
> 初始化列表只能用于构造函数
> 
> 初始话列表可以同时初始化多个数据成员
> 

2. 初始化列表存在的必要性
```
class Circle
{
	public:
		Circle(){m_dPi = 3.14;}		// 编译报错，不能给const第二次赋值
	private:
		const double m_dPi;		// 圆周率pi为固定值
};
```
```
class Circle
{
	public:
		Circle():m_dPi(3.14){}		// 编译通过，使用初始化列表初始化const
	private:
		const double m_dPi;
};
```
- 另一种形式
```
class Circle
{
	public:
		Circle(double pi):m_dPi(pi){}	// 编译通过，传入的形参通过初始化列表进行赋值
	private:
		const double m_dPi;
};
```



