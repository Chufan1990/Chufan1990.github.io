---
layout: post
title: 构造函数总结 constructor
date: 2017-08-23
categories: blog
tags: [Class, constructor, C++]
description: 总结构造函数的使用及注意事项
---

## 1. 构造的存在意义

	在实例化的对象时，需要对对象中的数据进行初始化。

	首先构造一个类	

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
	
	实例两个对象，并通过```void init()``` 初始化对象

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

 	对象初始化类型: 
		× 1. 有且仅有一次
		× 2. 根据条件初始化
	
	
