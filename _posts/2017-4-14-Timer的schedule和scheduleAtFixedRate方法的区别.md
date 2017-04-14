---
layout: post
title:  Timer的schedule和scheduleAtFixedRate方法的区别 
date:   2017-4-14 10:59:00 +0800
categories: Java
tag: Timer
---
* content
{:toc}


Timer的schedule和scheduleAtFixedRate方法的区别
==================

在java中，Timer类主要用于定时性、周期性任务 的触发，这个类中有两个方法比较难理解，那就是schedule和scheduleAtFixedRate方法，在这里就用实例分析一下

1. schedule方法：“fixed-delay”；如果第一次执行时间被delay了，随后的执行时间按 照 上一次 实际执行完成的时间点 进行计算 

1. scheduleAtFixedRate方法：“fixed-rate”；如果第一次执行时间被delay了，随后的执行时间按照 上一次开始的 时间点 进行计算，并且为了”catch up”会多次执行任务,TimerTask中的执行体需要考虑同步



- schedule方法的执行：

          下一次的执行时间点=上一次程序执行完成的时间点+间隔时间



- 当换成scheduleAtFixedRate方法的执行结果如下：

		 下一次的执行时间点=上一次程序开始执行的时间点+间隔时间

  并且因为前一个任务要执行6秒，而当前任务已经开始执行了，因此两个任务间存在重叠，需要考虑线程同步