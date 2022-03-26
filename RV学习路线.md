## RV学习路线

**以下流程为个人学习经历整理，仅供参考，欢迎批评指正不足之处**

#### 1、语言与基础知识（不要求全部掌握，可以做中学）

​		Verilog HDL：硬件代码阅读、移植和编写

​		C/C++		  ：底层简单驱动代码阅读与编写

​	    Python/Tcl  ：环境运行脚本代码阅读与编写

​		Makefile	  ：Make命令

​        对指令集或者软硬件协同有一定了解，能看懂汇编更好

​		对Core架构有一定概念，例如典型的MIPS五级流水线

#### 2、TinyRISCV

​		gitee仓库     ：https://gitee.com/liangkangnan/tinyriscv

​	    B站开发视频：https://www.bilibili.com/video/BV1aT4y197su?spm_id_from=333.851.header_right.fav_list.click

​		适合入手练习，资料比较全，很友好

​		Windows下开发，环境配置简单，整个flow做下来可以学到蛮多东西

#### 3、Hbird E203

​		GitHub仓库：https://github.com/riscv-mcu/e203_hbirdv2

​		B站讲解视频：https://space.bilibili.com/398205429/channel/seriesdetail?sid=1206851

​		书籍：《手把手教你设计CPU——RISC-V处理器篇》、《RISC-V架构与嵌入式开发快速入门》

​		论坛：https://www.riscv-mcu.com/community-community.html

​		集创赛RISC-V杯赛指定题目，支撑资料多，Ubuntu开发环境可以找我copy

#### 4、Freedom core

​		GitHub仓库：https://github.com/sifive/freedom

​		sifive推出，资料很少，代码可读性不高，不适合新手，谨慎尝试

​		笔者实习的公司正是使用freedom core做为SoC核心，阅读修改代码是一件非常痛苦的事

#### 5、XiangShan SoC

​		GitHub仓库：https://github.com/OpenXiangShan/XiangShan

​		知乎：https://www.zhihu.com/people/openxiangshan

​		微信公众号：香山开源处理器

​		中科院计算所推出，笔者没有具体研究，感兴趣可以对雁栖湖微架构以及香山核心做深入研究，开源社区中资料也比较多

#### 6、Core开发

​		开发语言：chisel，Verilog（学习chisel之前需要先学习Scala）

​		chisel/Scala学习：https://blog.csdn.net/qq_34291505/article/details/86744581

​		这是国内关于chisel中文学习做得最好的文章，官方的文档可以在下面的GitHub仓库下载

​		GitHub仓库：https://github.com/chipsalliance/chisel3

​		Ubuntu开发环境可以找我copy，这个环境配置比较难搞，对sbt软件版本控制比较严格

​		使用chisel做敏捷开发前两年比较火热，中科院计算所香山处理器就使用chisel作为主要开发语言，当然Verilog也是必需的

#### 7、写在最后

​		对RV的学习和开发，个人认为chisel不是必需的，不要陷入做RISC-V，上来就要学习chisel的误区，敏捷开发仅仅是RV学习和开发的其中一条路。对于熟悉硬件的同学来说，完全可以像蜂鸟一样，在开源的代码做修改，仅使用Verilog做硬件开发。也可以围绕核心做嵌入式开发，这个视个人需求而定。笔者也才做RV开发不久，仍在学习中，期待一起变得更强！

