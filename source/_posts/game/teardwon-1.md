---
title: Teardown Analysis
date: 2020-07-10 03:05:36
tags: 
- 拆解分析
- 游戏设计
categories: 
- 学习
typora-root-url: ..\..
---



Teardown Analysis `拆解分析`，该方法源自B站UP **鱼一元001** `UID:618369` ，非常感谢~

那么如何去拆解分析一款游戏呢？

- **举原作者中的 case 阴阳师 为例**|原链接： [挺进游戏公司01](https://www.bilibili.com/video/BV1GJ411y7fj)
  *原视频中没有讲如何去着手分析，作为一个学习者，要学会分析别人的思考过程。*
  ![image-20200714155230876](/images/teardwon-1/image-20200714155230876.png)

  <center>图1</center>

  ![image-20200714155553449](/images/teardwon-1/image-20200714155553449.png)

  <center>图2</center>
  
  ![image-20200714161013960](/images/teardwon-1/image-20200714161013960.png)
  
  <center>图3</center>
  
  ![image-20200714161233561](/images/teardwon-1/image-20200714161233561.png)
  
  <center>图4</center>
  
  ![image-20200714161426048](/images/teardwon-1/image-20200714161426048.png)
  
  <center>图5</center>
  
  ![image-20200714161605301](/images/teardwon-1/image-20200714161605301.png)

  <center>图6</center>
  
  ![image-20200715110109733](/images/teardwon-1/image-20200715110109733.png)
  
  <center>图7</center>
  
  - 首先分析下游戏中有几个系统组成，每个系统的层级关系是怎样子的。
    如阴阳师最大的三个系统：橙色的战斗系统、绿色的式神系统、蓝色角色系统。
    每个系统里又包括许多的子系统，如上图所示中三大系统里面就包含很多子系统。
  - 找出核心系统和核心资源的循环，做如上图 core loop 模型
  - 画出各个系统之间的资源流向导图。
  - 继续拆解子系统，如图2上半部分是式神的召唤，下半部分是子系统之间的关系 
    每个子系统还可以再拆的详细点，如副本条件及时间、资源等
  - Aim Map：标记出最重要的系统几个系统的目的（收入/活跃/社交留存等）
  - Target Map：标记出不同类型玩家，分别对哪些系统感兴趣
  - 游戏在发行方面做了哪些工作，或者还可以再细分下工作具体内容

