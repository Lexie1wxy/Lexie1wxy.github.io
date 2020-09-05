---
tags: 
- cpu
categories: 
- 硬件
- cpu
typora-root-url: ../_posts
---

# 32位单周期MIPS CPU设计报告

## 一、设计说明

根据课程设计要求,设计一个单周期32位MIPS CPU。

所谓单周期CPU指的是一条指令的执行在一个时钟周期内完成，然后开始下一条指令的执行，即一条指令用一个时钟周期完成。电平从低到高变化的瞬间称为时钟上升沿，两个相邻时钟上升沿之间的时间间隔称为一个时钟周期。时钟周期一般也称振荡周期（如果晶振的输出没有经过分频就直接作为CPU的工作时钟，则时钟周期就等于振荡周期。若振荡周期经二分频后形成时钟脉冲信号作为CPU的工作时钟，这样，时钟周期就是振荡周期的两倍。）

CPU在处理指令时，一般需要经过以下几个步骤：

(1) 取指令(IF)：根据程序计数器PC中的指令地址，从存储器中取出一条指令，同时，PC根据指令字长度自动递增产生下一条指令所需要的指令地址，但遇到“地址转移”指令时，则控制器把“转移地址”送入PC，当然得到的“地址”需要做些变换才送入PC。 

(2) 指令译码(ID)：对取指令操作中得到的指令进行分析并译码，确定这条指令需要完成的操作，从而产生相应的操作控制信号，用于驱动执行状态中的各种操作。 

(3) 指令执行(EXE)：根据指令译码得到的操作控制信号，具体地执行指令动作，然后转移到结果写回状态。 

(4) 存储器访问(MEM)：所有需要访问存储器的操作都将在这个步骤中执行，该步骤给出存储器的数据地址，把数据写入到存储器中数据地址所指定的存储单元或者从存储器中得到数据地址单元中的数据。 

(5) 结果写回(WB)：指令执行的结果或者访问存储器中得到的数据写回相应的目的寄存器中。 
单周期CPU，是在一个时钟周期内完成这五个阶段的处理。

本设计中各个底层模块采用Verilog语言编写，顶层模块完成各模块之间的连接，采用RTL原理图进行设计。

## 二、指令系统及指令功能说明：

## 三、指令格式

其中，

**op：**为操作码；

**rs：**为第1个源操作数寄存器，寄存器地址（编号）是00000~11111，00~1F；

**rt：**为第2个源操作数寄存器，或目的操作数寄存器，寄存器地址（同上）；

**rd：**为目的操作数寄存器，寄存器地址（同上）；

**sa：**为位移量（shift amt），移位指令用于指定移多少位；

**func：**为功能码，在寄存器类型指令中（R类型）用来指定指令的功能；

**immediate：**为16位立即数，用作无符号的逻辑操作数、有符号的算术操作数、数据加载（Laod）/数据保存（Store）指令的数据地址字节偏移量和分支指令中相对程序计数器（PC）的有符号偏移量；

**address：**为地址。

## 三、整体框架图

![image-20200901154501834](../../source/images/917106840408%E5%90%B4%E5%B8%8C%E9%A2%96%E7%A1%AC%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%8A%A5%E5%91%8A/image-20200901154501834.png)

## 四、数据通路图

![image-20200903215848789](../../source/images/917106840408%E5%90%B4%E5%B8%8C%E9%A2%96%E7%A1%AC%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%8A%A5%E5%91%8A/image-20200903215848789.png)

## 六、各模块的程序

### 1、控制单元ControlUnit

**设计思路**

根据数据通路图可以知道，控制单元的功能是接收一个6位的操作码（opCode）和一个标志符（zero）作为输入，输出PCWre、ALUSrcB等控制信号

各控制信号的作用见（表1），从而达到控制各指令的目的。

**程序代码：**

```verilog
`timescale 1ns / 1ps
module ControlUnit(
    input [5:0] op,         // op操作符
    input zero,             // ALU的zero输出

    output reg PCSrc,           // 多路选择器
    output reg PCWre,           // (PC)PC是否更改，如果为0，PC不更改
    output reg ALUSrcB,         // 多路选择器
    output reg ALUM2Reg,        // 多路选择器
    output reg RegWre,          // (RF)写使能信号，为1时，在时钟上升沿写入
    output reg InsMemRW,        // (IM)读写控制信号，1为写，0位读
    output reg DataMemRW,       // (DM)数据存储器读写控制信号，为1写，为0读
    output reg ExtSel,          // (EXT)控制补位，如果为1，进行符号扩展，如果为0，全补0
    output reg RegOut,          // 多路选择器
    output reg [2:0] ALUOp      // (ALU)ALU操作控制 
    );

    initial 
     begin
        ExtSel = 0;
        PCWre = 1;
        InsMemRW = 1;
        RegOut = 1;
        RegWre = 0;
        ALUOp = 0;
        PCSrc = 0;
        ALUSrcB = 0;
        DataMemRW = 0;
        ALUM2Reg = 0;
    end

    always@(op or zero)
    begin  
      case(op) 
            // add
            6'b000000:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 000;
             end
            // addi
            6'b000001:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 1;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 000;
             end
            // sub
            6'b000010:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 001;
             end
             
           // subi
            6'b000011:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 001;
             end
            // ori
            6'b010000:
             begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 011;
          end
           // and
         6'b010001:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 100;
          end
            // or
            6'b010010:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 011;
             end
            // andi
            6'b010011:
          begin   //以下都是控制单元产生的控制 new
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 100;
             end
           // xor
            6'b010100:
          begin   //以下都是控制单元产生的控制 new
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 110;
             end
                // not
            6'b010101:
          begin   //以下都是控制单元产生的控制 new
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 010;
             end
             // leftmovei
            6'b011001:
          begin   //以下都是控制单元产生的控制 new
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 111;
             end
              // righttmovei
            6'b011010:
          begin   
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 101;
             end
           // move
         6'b100000:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 1;
                ALUOp = 000;
          end
           // movei
         6'b100001:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 000;
          end
            // sw
            6'b100110:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 0;
                RegWre = 0;
                InsMemRW = 1;
                DataMemRW = 1;
                ExtSel = 1;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 000;
          end
         // lw
            6'b100111:
          begin   //以下都是控制单元产生的控制信号
                PCWre = 1;
                ALUSrcB = 1;
                ALUM2Reg = 1;
                RegWre = 1;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 1;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 000;
          end
         // beq
           6'b110000:
          begin   //以下都是控制单元产生的控制信号
                if (zero) begin
                    PCSrc = 1;
                end else begin
                    PCSrc = 0;
                end
            ALUM2Reg = 0;
                PCWre = 1;
                ALUSrcB = 0;
                RegWre = 0;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 1;
                RegOut = 0;
                ALUOp = 001;
          end
          // bne
           6'b110001:
          begin   //以下都是控制单元产生的控制信号
                if (zero) begin
                    PCSrc = 0;
                end else begin
                    PCSrc = 1;
                end
            ALUM2Reg = 0;
                PCWre = 1;
                ALUSrcB = 0;
                RegWre = 0;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 1;
                RegOut = 0;
                ALUOp = 001;
          end
  
          // j
           6'b110010:
          begin   //以下都是控制单元产生的控制信号
    
                PCWre = 1;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 0;
                InsMemRW = 1;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 1;
                RegOut = 0;
                ALUOp = 000;
          end
           // halt
           6'b111111:
             begin   //以下都是控制单元产生的控制信号
                PCWre = 0;
                ALUSrcB = 0;
                ALUM2Reg = 0;
                RegWre = 0;
                InsMemRW = 0;
                DataMemRW = 0;
                ExtSel = 0;
                PCSrc = 0;
                RegOut = 0;
                ALUOp = 000;
             end
        endcase
     end

endmodule
```

### 2、算术运算单元（ALU）

**设计思路：**

模块ALU接收寄存器的数据和控制信号作为输入，执行相应的计算，然后将结果输出:

**程序代码**

````verilog
module ALU(
     input [2:0] ALUOp,          
    input [31:0] A,             
    input [31:0] B,             
    output reg zero,             // 运算结果result的标志，result为0输出1，否则输出0
    output reg [31:0] result   
    );

    // 进行ALU计算
    always@(*)
     begin
        case (ALUOp)
            3'b000 : result = A + B; 
            3'b001 : result = A - B; 
            3'b010 : result = ~ A; 
            3'b011 : result = A | B; 
            3'b100 : result = A & B; 
            3'b101 : result = A >> B; 
            3'b110 : result = A ^ B; 
            3'b111 : result = A << B; 
            default : result = 0;
        endcase
        if (result)  zero = 0;
        else  zero = 1;
     end

endmodule

````

### 3、**PC单元（PC）**

**设计思路：**

PC单元以时钟信号clk、重置标志Reset、立即数、PCWreck信号控制和newAddress新指令为输入，根据输入决定是否修改当前地址并输出。

**程序代码**

```verilog
module PC(
    input CLK,                         
    input Reset,                     
    input PCWre,                       
    input [31:0] newAddress,          
    output reg[31:0] currentAddress  
    );

    initial begin
        currentAddress <= 0;  // 初始化赋值
    end

    always@(posedge CLK or posedge Reset)
     begin
        if (Reset == 1)  currentAddress <= 0;  // 重置，赋值为0
        else 
         begin
             if (PCWre)  currentAddress <= newAddress;
             // PCWre决定PC是否更改，如果为1，PC更改为新指令当前地址
            else  currentAddress <= currentAddress;
         end
     end
endmodule
```

### 4、 扩展单元（signZeroExtend）

**设计思想**

比较简单的一个模块，用于立即数的扩展。ExtSel 为控制补位信号。判断后，将 extendImmediate 的前 16 位全补 1 或 0 即可。

**程序代码**

```verilog
module SignZeroExtend(
    input [15:0] immediate,        // 16位立即数
    input ExtSel,                  // 控制补位，如果为1，进行符号扩展，如果为0，全补0
    output [31:0] extendImmediate   // 输出的32位立即数
    );

    assign extendImmediate[15:0] = immediate;
    assign extendImmediate[31:16] = ExtSel ? (immediate[15] ? 16'hffff : 16'h0000) : 16'h0000;

endmodule

```

### 5、数据存储单元（DataMemory)

**设计思想**

数据存储单元的功能是读取数据

**程序代码**

```verilog
//`timescale 1ns / 1ps
module DataMemory(
    input [31:0] DAddr,         // 地址输入端口
    input [31:0] DataIn,        // 数据输入端口
    input DataMemRW,            // 读写控制信号，为1写，为0读
    output reg [31:0] DataOut  
    );

    //以8位为一字节存储
    reg [7:0] memory[0:15];

    integer i;
    initial
     begin
        for (i = 0; i < 16; i = i + 1) 
            memory[i] <= 0;
     end

    // 读写内存
    always@(DAddr)
     begin

     end

    always@(DAddr or DataIn)
     begin
        // 写
        if (DataMemRW)
         begin
           memory[DAddr] <= DataIn[31:24];
            memory[DAddr + 1] <= DataIn[23:16];
            memory[DAddr + 2] <= DataIn[15:8];
            memory[DAddr + 3] <= DataIn[7:0];
         end
        // 读
        else
         begin
            DataOut[31:24] <= memory[DAddr];
            DataOut[23:16] <= memory[DAddr + 1];
            DataOut[15:8] <= memory[DAddr + 2];
            DataOut[7:0] <= memory[DAddr + 3];
         end
     end
endmodule
```

### 6、指令存储单元（instructionMemory）

**设计思想**

根据当前的PC地址得到对应的op，rs，rt，rd以及immediate.内部实现：将需要测试的汇编指令程序转化为指令代码，每个人都可以有自己的测试指令

其次，为了存储这些指令代码，可以申请一个32位的二进制数组来存储它们，最后根据PC地址得到对应的op,rs,rt,immediate

**程序代码:**

```verilog
module InstructionMemory(
    input InsMemRW,            // 读写控制信号，1为写，0位读
    input [31:0] IAddr,        // 指令地址输入入口

    output [5:0] op,
    output [4:0] rs,
    output [4:0] rt,
    output [4:0] rd,
    output [15:0] immediate    // 指令代码分时段输出
    );

    reg[7:0] mem[0:63];

    initial 
     begin
        $readmemb("test1.txt", mem);  //读取指令
     end

    // 从地址取值
    assign op = mem[IAddr][7:2];
    assign rs[4:3] = mem[IAddr][1:0];
    assign rs[2:0] = mem[IAddr + 1][7:5];
    assign rt = mem[IAddr + 1][4:0];
    assign rd = mem[IAddr + 2][7:3];
    assign immediate[15:8] = mem[IAddr + 2];
    assign immediate[7:0] = mem[IAddr + 3];

endmodule

```

### 7、寄存器文件单元（registerFile）

**设计思想**

寄存器文件单元的功能是接收instructionMemory中的rs，rt，rd作为输入，输出对应寄存器的数据，从而达到取寄存器里的数据的目的。在其内部实现的过程中，为了防止0号寄存器写入数据需要在writeReg的时候多加入一个判断条件，即writeReg不等于0时写入数据。

**程序代码**

```verilog
//`timescale 1ns / 1ps
module RegisterFile(
    input CLK,                 // 时钟
    input RegWre,              // 写使能信号，为1时，在时钟上升沿写入
    input [4:0] rs,            // rs寄存器地址输入端口
    input [4:0] rt,            // rt寄存器地址输入端口
    input [31:0] WriteData,    // 写入寄存器的数据输入端口
    input [4:0] WriteReg,      // 将数据写入的寄存器端口，其地址来源rt或rd字段,
    //为了防止0号寄存器写入数据需要在writeReg的时候多加入一个判断条件，即writeReg不等于0时写入数据
    output [31:0] ReadData1,   // rs寄存器数据输出端口
    output [31:0] ReadData2    // rt寄存器数据输出端口
    );
   
    reg [31:0] register[0:15];  // 新建16个寄存器，用于操作
 
    // 初始时，将16个寄存器全部赋值为0
    integer i;
    initial 
     begin
        for(i = 0; i < 16; i = i + 1)  register[i] <= 0;
     end

    // 读寄存器
    assign ReadData1 = register[rs];
    assign ReadData2 = register[rt];

    // 写寄存器
    always@(negedge CLK)
     begin
        // 如果寄存器不为0，并且RegWre写使能信号为真，写入数据
        if (RegWre && WriteReg != 0)  register[WriteReg] = WriteData;
     end 
endmodule

```

**8、顶层模块（CPU）**

**设计思想**

顶层模块（CPU）是整个CPU的控制模块，通过连接各个子模块来达到运行CPU的目的，整个模块设计可以如下：

**程序代码**

````verilog
//`timescale 1ns / 1ps
module cpu(
    input CLK,
    input Reset,
    output [5:0] op,
    output [4:0] rs,
    output [4:0] rt,
    output [4:0] rd,
    output [15:0] immediate,
    output [31:0] ReadData1,
    output [31:0] ReadData2,
    output [31:0] WriteData,
    output [31:0] currentAddress,
    output [31:0] result
    );

    // 各种临时变量
   wire [2:0] ALUOp; 
   wire [31:0] B, newAddress;
   wire [31:0] currentAddress_4, extendImmediate, currentAddress_immediate;   
   wire [4:0] WriteReg;  
   wire zero, PCSrc, PCWre, ALUSrcB, ALUM2Reg, RegWre, InsMemRW, DataMemRW, ExtSel, RegOut;

    ControlUnit cu(op, zero, PCSrc, PCWre, ALUSrcB, ALUM2Reg, RegWre, InsMemRW, DataMemRW, ExtSel, RegOut, ALUOp);

    PC pc(CLK, Reset, PCWre, newAddress, currentAddress);

    InstructionMemory im(InsMemRW, currentAddress, op, rs, rt, rd, immediate);
    RegisterFile rf(CLK, RegWre, rs, rt, WriteReg, WriteData, ReadData1, ReadData2);
    ALU alu(ALUOp, ReadData1, B, zero, result);
    SignZeroExtend sze(ExtSel, immediate, extendImmediate);
    DataMemory dm(DataMemRW, result, ReadData2, DataOut);

    assign currentAddress_4 = currentAddress + 4;
    assign currentAddress_immediate = currentAddress_4 + (extendImmediate << 2);

    Multiplexer5 m5(RegOut, rd, rt, WriteReg);
    Multiplexer32 m321(ALUSrcB, extendImmediate, ReadData2, B);
    Multiplexer32 m322(ALUM2Reg, DataOut, result, WriteData);
    Multiplexer32 m323(PCSrc, currentAddress_immediate, currentAddress_4, newAddress);
endmodule

````

## 8、顶层原理图

![image-20200903220616586](../../source/images/917106840408%E5%90%B4%E5%B8%8C%E9%A2%96%E7%A1%AC%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%8A%A5%E5%91%8A/image-20200903220616586.png)

## 9、各条指令运行的仿真波形图



![image-20200903214958963](../../source/images/917106840408%E5%90%B4%E5%B8%8C%E9%A2%96%E7%A1%AC%E4%BB%B6%E8%AE%BE%E8%AE%A1%E6%8A%A5%E5%91%8A/image-20200903214958963.png)



