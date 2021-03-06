# 第五章 构建中的设计
设计不太可能在构建之前完成。
## 5.1 设计挑战
* 设计是一个邪恶的(wicked)问题：只能通过解决这个问题或部分解决问题才能清楚的定义这个问题。
真正的程序和学生作业的区别。
* 设计是一个草率的过程
会犯错；好的方案很精妙；“足够好”很难定义。
* 设计关乎权衡和优先级
* 设计牵涉约束
* 设计是非决定性的
* 设计是一个启发式的过程：没有银弹
* 设计是自然发生的

## 5.2 关键设计概念
### 软件的首要技术法则：管理复杂性
#### 偶然的和本质的困难
此划分来自亚里士多德的哲学。
偶然的：笨拙的语法、非交互式的计算机、难以一起工作的工具；
本质的：与真实世界复杂、无序的接口，异常情况，精确性，准确定义真实世界如何运行。
#### 管理复杂性的重要性
失败的原因：糟糕的需求/计划/管理，失控的复杂性管理。
程序太大，人类无法一次性理解。问题分级后易于理解（如包管理），保持从程序短小，写代码时考虑人类的极限。
#### 如何消灭复杂性
* 减少每个人脑中需要一次性处理的固有复杂性。
* 防止不必要复杂性的增殖。

### 描述设计的特征
* 最小复杂度：聪明的 vs 简单易维护的。
* 易维护：为代码维护者编程，自解释的设计。
* 松耦合：不同部分之间的联系尽量少。
* 可扩展性：更改时减少创伤。
* 可复用性
* 高扇入：充分复用底层模块
* 中低扇出：不过度依赖其他部分
* 可移植性
* 精简：没有多余部分
* 分层化：隔离变化
* 标准技术

### 设计的层次
#### 第1层：软件系统
#### 第2层：划分子系统或包
子系统间的通信必须加以限制，否则会不断熵增，一篇混乱，可以先紧后松。常见的子系统：
* 商业规则
* 用户接口
* 数据存取
* 系统依赖

#### 第3层：划分类
包括接口。大项目由子系统划分，定义一些外部函数；小项目由系统直接划分。
#### 第4层：划分例程
可能会引起第3层的修改。
#### 第5层：例程内设计

## 5.3 设计建造的砖块：启发式
一个不断试错的过程。
### 找到现实世界的对象
* 标识对象和其属性
* 决定改对象能干啥
* 决定每个对象能对其他对象干啥
* 决定对象各部分的可见性
* 决定对象的公开接口

一个迭代过程：重新组织，类的细节修改。

### 组织一致的抽象
在不同的层次忽略细节。集合=>抽象。基类、接口。
* 函数层次
* 类层次
* 包或子系统层次

### 封装实现细节
### 继承——当继承简化设计时使用
### 信息隐藏
* 结构化设计：黑盒
* 面向对象设计：封装、模块化、抽象

#### 秘密和隐私权
#### 两种策略
* 隐藏复杂性使你的大脑不需要考虑它，除非特别关注时
* 隐藏更改源，隔离变化

#### 信息隐藏的障碍
* 分布过广的信息
* 环形依赖
* 不当的全局数据
* 担心性能损失

#### 信息隐藏的价值
启发性的力量，设计好的公共接口。问正确的问题：这个类需要隐藏什么？

### 标示易变区域
标示=>分割=>隔离
* 商业规则
* 硬件依赖
* 输入输出
* 非标准语言特性
* 设计和构建困难的区域
* 状态变量：使用枚举代替bool值；使用存取函数代替直接访问。
* 数据大小限制

#### 预期不同程度的变化
先找出最小子集，再做功能性、质量性改进。

### 保持松耦合
#### 耦合标准
* 大小：模块间联系的数量，如函数的参数个数，类的公开方法数量；
* 可见性：明确引用，胜过更改全局变量。
* 可变性：容易改变连接，被不同的模块调用。

#### 耦合的种类
* 简单数据参数耦合：模块间传递了简单数据类型。常见、可接受。
* 简单对象耦合： 一个对象初始化了另一个对象。合理。
* 对象参数耦合：对象1需要对象2向其传递对象3。耦合较紧密。
* 语义耦合
    * 模块1传递了一个标志给模块2，告诉模块2应该去干啥。如果模块2定义了一个数据类型来表示该标志，则合理。
    * 模块2使用模块1更改过的全局变量。有时序假设，不好。
    * 模块1在调用某函数前必须先调用初始化函数。
    * 模块1传递对象给模块2，知道模块2将使用对象的部分方法，只对对象进行部分初始化。
    * 模块1传递基类给模块2，模块2知道模块1实际传递的是派生类，强制转化后使用。

危险:使用了编译器无法检测的方法使用别的类。
一旦使用了，你就得自己负责正确性。

### 寻找一般的设计模式
* 模式通过已经准备好的抽象来降低复杂性
* 模式使一般解决方案制度化以减少错误
* 模式通过建议设计选择提供启发性价值
* 模式通过提升设计语言测层次使沟通更流畅

### 其他的启发式方法
* 高内聚
* 构建继承体系
* 正式化类协议
* 职责分配
* 为测试设计
* 避免失败
* 有意识的选择绑定时间
* 使控制点集中
* 使用暴力方法
* 画图示
* 保持设计模块化

### 启发性方法指导
    Polya's How to Solve It

不要卡在一个小问题上，你不需要一次性解决所有的设计问题。

## 5.4 设计实践
### 迭代
发现不顶用的设计。
### 分治
### 自顶向下与自底向上
两种方法论应当结合使用。自顶向下容易入手，但是有时底层的复杂性会影响到上层；自底向下难入手，但是能及早的管理复杂性，使得上层设计更容易。
### 试验原型
### 协作设计
* 起身去问协作者
* 和协作者坐在一起用白板讨论草图
* 结对编程
* 开会向其他协作者讲解设计
* 正式的审查
* 冷处理自己的设计，再回头看
* 求助公司外的人，在论坛上提问

### 多少设计才足够？
一般来说，越细越好；设计文档不是越多越好。

### 记录你的设计工作

* 在代码中插入设计文档
* 在Wiki中记录设计的讨论和决定
* 写e-mail总结
* 拍照
* 保存设计海报
* 使用“类-职责-协作”卡片
* 在适当的细节层次使用UML图

## 5.5 对流行方法学的评论
不要过多关注设计方法学，关注设计本身，不设计或事无巨细的设计都不可取，还是要具体情况具体分析。
