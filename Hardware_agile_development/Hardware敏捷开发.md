## Hardware 敏捷开发

#### 0、什么是敏捷开发？

​	简化开发流程

​	加快开发周期

​	减少不必要文件输出

​	加速研发迭代



#### 1、现代数字电路设计语言

​	**Verilog HDL/VHDL**：语言描述繁琐、缺乏一致性检查、参数化能力差、无clock domain和power

​	**HLS**：C model to Verilog；C model 描述存在限制

​	**Systemverilog**：Verilog可综合子集



#### 2、敏捷开发的主角——Chisel

​	Constructing Hardware In a Scala Embedded Language: Based on Scala（JVM）

​	天生的高级玩具——Scala

​	诞生于UC Berkeley，与RISC-V架构同时产生，支持OOP，函数式编程， 高抽象级别

​    Chisel将硬件构造原语添加到**Scala编程语言**中，为设计者提供了现代编程语言的强大功能，以编写**复杂的、可参数化**的电路生成器，从而**生成可综合的Verilog**

​	**Chisel to Firrtl transformer to Verilog**

​    https://github.com/freechipsproject/chisel3



#### 3、Chisel的特点

​	**Hardware construction language** (not C to Gates)：硬件构建语言

​	**Algebraic construction and wiring**

​	**Embedded in the Scala programming language**：内嵌于Scala程序设计语言

​	**Abstract data types and interfaces**：抽象的数据类型和接口

​	**Bulk connections**：端口的批量连接

​	**Hierarchical + object oriented + functional construction**：分层+面向对象+函数构建

​	**Highly parameterizable using metaprogramming in Scala**：通过使用Scala的元编程实现高度的参数化

​	**Supports layering of domain specific languages**

​	**Sizeable standard library including floating-point unit**s：具有包含浮点单元在内的、可以调整大小的标准库

​	**Multiple clock domains**：支持多时钟域

​	**Generates high-speed C++-based cycle-accurate software simulator**：能够产生高速的、基于C++的周期精确软件模拟器

​	**Generates low-level Verilog designed to pass on to standard ASIC or FPGA tools**：能够产生Verilog设计，从而在标准的ASIC、FPGA工具中使用



#### 4、常见的开源RISC-V Core/SoC

​	**Rocket Core**：顺序发射、顺序执行；五级流水线

![](E:\Lab\汇报&周报\22-3-6例会汇报\Rocket core.png)



​	**BOOM Core**：超标量、乱序发射、乱序执行；支持多核、二级Cache

![](E:\Lab\汇报&周报\22-3-6例会汇报\boom core.png)



<img src="E:\Lab\汇报&周报\22-3-6例会汇报\Rocket chip gen.png" style="zoom: 67%;" />



​	**Freedom E310 SoC**：Sifive开发

![](E:\Lab\汇报&周报\22-3-6例会汇报\freedom 310 SoC.png)

​	https://github.com/sifive/freedom

​	**HBird E200 SoC**：Based on Freedom E300 core

<img src="E:\Lab\汇报&周报\22-3-6例会汇报\HBird E203.png" style="zoom:150%;" />

​	https://github.com/riscv-mcu/e203_hbirdv2

​	**XiangShan SoC**: Yanqihu micro-arch 

![](E:\Lab\汇报&周报\22-3-6例会汇报\xiangshan.jpg)

​	https://github.com/OpenXiangShan/XiangShan

​	

​	**TinyRISCV**：RV32IM指令集；取指，译码，执行三级流水线 

<img src="E:\Lab\汇报&周报\22-3-6例会汇报\TinyRISCV-arch.jpg" style="zoom: 33%;" />

​	https://gitee.com/liangkangnan/tinyriscv



#### 5、Chisel基本语法

```scala
1.U                // 字面值为“1”的UInt对象

-8.S               // 字面值为“-8”的SInt对象

"b0101".U         // 字面值为“5”的UInt对象

true.B            // 字面值为“true”的Bool对象 
```

```scala
1.U              // 字面值为“1”、宽度为1bit的UInt对象

1.U(32.W)        // 字面值为“1”、宽度为32bit的UInt对象
```

```scala
val myVec = Wire(Vec(3, UInt(32.W)))

val myReg = myVec(0)
```

```scala
class MyModule extends Module {undefined
   val io = IO(new Bundle {undefined
       val in = Input(UInt(32.W))
       val out = Output(UInt(32.W))
   })
}
```



#### 6、Chisel数字电路设计实例

**and_gate**	

```scala
package test
 
import chisel3._
import chisel3.experimental._
 
class AND extends RawModule {
  val io = IO(new Bundle {
    val porta = Input(UInt(1.W))
    val portb = Input(UInt(1.W))
    val portc = Output(UInt(1.W))
  })
 
  io.c := io.a & io.b
}
```

```verilog
module AND(
     input   io_porta,
     input   io_portb,
     output  io_portc
);
     assign io_c = io_a & io_b;
endmodule 
```



**16bit LFSR**

```scala
package test
 
import chisel3._
import chisel3.util._
 
class LFSR extends Module {
  val io = IO(new Bundle {
    val en = Input(Bool())
    val out = Output(UInt(16.W))  
  })
 
  io.out := LFSR16(io.en)
}
```

```verilog
// LFSR.v
module LFSR(
  input         clock,
  input         reset,
  input         io_en,
  output [15:0] io_out
);
  reg [15:0] _T;
  wire  _T_1; 
  wire  _T_2; 
  wire  _T_3; 
  wire  _T_4; 
  wire  _T_5; 
  wire  _T_6; 
  wire  _T_7; 
  wire [14:0] _T_8; 
  wire [15:0] _T_9; 
  assign _T_1 = _T[0]; 
  assign _T_2 = _T[2]; 
  assign _T_3 = _T_1 ^ _T_2; 
  assign _T_4 = _T[3]; 
  assign _T_5 = _T_3 ^ _T_4; 
  assign _T_6 = _T[5]; 
  assign _T_7 = _T_5 ^ _T_6; 
  assign _T_8 = _T[15:1]; 
  assign _T_9 = {_T_7,_T_8}; 
  assign io_out = _T; 
 
  always @(posedge clock) begin
    if (reset) begin
      _T <= 16'h1;
    end else begin
      if (io_en) begin
        _T <= _T_9;
      end
    end
  end
endmodule
```



#### 7、Blackbox

​	提供了高度自主化的模块端口定义，用户可以根据需要自由拓展



#### 8、Reference

https://zhuanlan.zhihu.com/p/98097268

https://zhuanlan.zhihu.com/p/381391908

https://gitee.com/OpenXiangShan/XiangShan

https://blog.csdn.net/weixin_39684052/article/details/111365219
