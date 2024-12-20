---
title: 2024A-stage4-arceos-unikernel1-Martin1847
date: 2024-12-20 19:38:11
tags:
    - author:martin1847
    - repo:https://github.com/martin1847/arceos
---

# Arceos 训练营总结

转眼间两个多月的训练营要进入尾声了。
还记得国庆回山东的高铁上，在刷`rustlings`的算法题，小根堆的实现。

从二阶段的`rCore`到组件化的`arceos`,一路下来，对OS几大部件`CPU`虚拟化、`内存`虚拟化和文件系统虚拟化有了更深刻的理解。

下面我也从这几个方面来分别做个总结。




<!-- more -->

## CPU虚拟化

了解了`CPU`的几种特权模式，以及到OS进行系统调用进行的硬件级别（汇编指令）支持。

包括通过对时钟中断的支持，完成抢占式调度（这也解释了在用户态较难实现lock）。

在CPU眼里，没有函数、没有内存分配，有的只是指令和数据。

对于高级语言而言，一个用户态程序的最终运行，是`编译器`和`os`和CPU共同协同运作的结果。

编译器负责栈的初始化，函数上下文的处理，os负责提供硬件资源的抽象、系统调用，CPU提供特权指令。

虚拟化的目的，是为了多个程序的调度，让每个程序“独占”CPU，减少了编码的心智负担。

## 内存虚拟化

这里印象深刻的是分页，页表实现。硬件层面的`MMU`和`TLB`支持。

我们实现了彻底分页，内核态和用户态是两个页表。通过分页保障了安全，也方便了应用编写。

这一块也是非常复杂的点。

TODO

## 文件系统虚拟化

了解了ELF文件格式，静态link，动态link，以及文件inode的底层细节。

TODO

设计一个高效的文件系统是个复杂的工程，本质根内存分配一样，要减少内部碎片、外部碎片，而磁盘访问速度远远不及内存，真是一件复杂的事情。