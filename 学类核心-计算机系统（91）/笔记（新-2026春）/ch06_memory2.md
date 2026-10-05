<h1 align='center'>第六章 虚拟存储器</h1>

[TOC]

## 6.1 虚存抽象
<img src="./imgs/image-10.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

### 6.1.1 地址空间
<img src="./imgs/image-15.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

### 6.1.2 三个问题
<img src="./imgs/image-11.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />
<img src="./imgs/image-12.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

### 6.1.3 解决方案
<img src="./imgs/image-13.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />


### 6.1.4 虚拟内存
现代处理器使用的是虚拟寻址而不是物理寻址, 也就是说CPU生成的地址是**虚拟地址**, 需要通过**地址翻译**才能得到对应的物理地址, 从而访问内存中的数据
在多任务操作系统中, 每一个正在执行的任务实际上都运行在虚拟地址空间中, 他以 **远大于主存物理空间的大小(多个虚拟地址可以映射到同一个物理地址, 其实多出来的一部分空间需要硬盘提供, 但是通过局部性原理可以实现很高的缓存命中, 不需要访问硬盘)** 进行近似于主存访问速率的存取

处理器上有一个专用硬件--内存管理单元(Memory Management Unit, MMU), 负责将虚拟地址翻译成物理地址, 以及实现虚拟内存的其他功能
<img src="./imgs/image-14.png" alt="alt text" style="border: 2px solid black;" />


#### 虚拟内存的好处
<img src="./imgs/image-16.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

## 6.2 虚存作为缓存工具
<img src="./imgs/image-18.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />
<img src="./imgs/image-19.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

### 6.2.1 页表
<img src="./imgs/image-20.png" alt="alt text" style="border: 2px solid black; zoom: 50%;" />

#### 页表的命中
<img src="./imgs/image-21.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
<img src="./imgs/image-22.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

#### 缺页处理程序

### 6.2.2 分配页面

### 6.2.3 异常中的页故障

## 6.3 虚存作为内存管理工具
<img src="./imgs/image-23.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
<img src="./imgs/image-24.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

## 6.4 虚存作为内存保护工具
<img src="./imgs/image-25.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

## 6.5 虚拟内存的地址翻译
<img src="./imgs/image-26.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

### 6.5.1 地址翻译的符号汇总
<img src="./imgs/image-27.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

### 6.5.2 地址翻译的页命中
<img src="./imgs/image-28.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

<img src="./imgs/image-29.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />

### 6.5.3 TLB -- 加速地址翻译

==接下来介绍虚拟存储器的具体运行==

<img src="./imgs/image-34.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
所有的PTE(Page Table Entry, 页表项) 保存在内存(RAM)中的.

<img src="./imgs/image-35.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
TLB(Translation Lookaside Buffer) 是一个小型的高速缓存，专门用于存储最近使用的页表项。当CPU需要进行地址翻译时，首先会检查TLB，如果TLB中有对应的页表项（TLB命中），就可以直接得到物理地址；如果没有（TLB未命中），则需要访问内存中的页表来获取页表项，然后将其加载到TLB中以加速后续的地址翻译。

### 6.5.4 TLB 命中
<img src="./imgs/image-36.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
TLB 不命中的概率通常较低，因为程序的局部性原理（temporal and spatial locality）使得最近使用的页表项很可能在TLB中。

### 6.5.5 页表的多级结构
页表很大:
<img src="./imgs/image-37.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
为了节省内存，现代操作系统通常使用多级页表结构，例如两级或三级页表。这种结构将页表分成多个层次，每层页表只包含指向下一层页表的指针，只有在需要访问某个页时才会分配对应的页表项，从而节省了大量的内存空间。
<img src="./imgs/image-38.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
例如两级页表:
<img src="./imgs/image-39.png" alt="alt text" style="border: 2px solid black; zoom: 67%;" />
