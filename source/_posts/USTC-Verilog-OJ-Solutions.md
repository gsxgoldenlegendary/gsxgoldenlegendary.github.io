---
title: USTC Verilog OJ Solutions
date: 2021-10-19 19:30:00
tags: Digital Circuit
categories: Computer Science
---

[USTC Verilog OJ链接](https://verilogoj.ustc.edu.cn)

## 输出1

```verilog
module top_module(
      output one
  );
  assign one = 1;
endmodule
```

## 输出0

```verilog
module top_module(
  output out
);
  assign out=1'b0;
endmodule
```

<!--more-->

## wire

```verilog
module top_module(
  input in,
  output out
);
  assign out=in;
endmodule
```

## 多个端口的模块

```verilog
module top_module( 
    input a,b,c,
    output w,x,y,z );
	assign w=a,x=b,y=b,z=c;
endmodule
```

## 非门

```verilog
module top_module(
    input in, 
    output out );
  	assign out=!in;
endmodule
```

## 与门

```verilog
module top_module(
  input a, 
  input b,
  output out );
	assign out=a&b;
endmodule
```

## 或非门

```verilog
module top_module( 
    input a, 
    input b, 
    output out );
  	assign out=!(a|b);
endmodule
```

## 同或门

```verilog
module top_module( 
    input a, 
    input b, 
    output out );
  	xnor(out,a,b);
endmodule
```

## 线网型中间变量

```verilog
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out,
    output out_n   
); 
	wire ab,cd,abcd;
  	and(ab,a,b);
  	and(cd,c,d);
  	or(abcd,ab,cd);
  	assign out=abcd;
  	assign out_n=!abcd;
endmodule

```

## 向量

```verilog
module top_module ( 
    input wire [2:0] vec,
    output wire [2:0] outv,
    output wire o2,
    output wire o1,
    output wire o0);
  assign outv=vec;
  assign o0=vec[0];
  assign o1=vec[1];
  assign o2=vec[2];
endmodule
```

## 向量\_续1

```verilog
`default_nettype none     // Disable implicit nets. Reduces some types of bugs.
module top_module( 
    input	wire	[15:0]	in,
    output	wire	[7:0]	out_hi,
    output	wire	[7:0]	out_lo 
);
  assign out_lo=in[7:0];
  assign out_hi=in[15:8];
endmodule
```

## 向量\_续2

```verilog
module top_module(
  input [31:0] in,
  output [31:0] out
);
  assign out[31:24] =in[7:0];
  assign out[23:16]=in[15:8];
  assign out[15:8]=in[23:16];
  assign out[7:0]=in[31:24];
endmodule
```

## 位操作

```verilog
module top_module( 
    input [2:0] a,
    input [2:0] b,
    output [2:0] out_or_bitwise,
    output out_or_logical,
    output [5:0] out_not
);
  assign out_or_bitwise=a|b;
  or(out_or_logical,|a,|b);
  assign out_not[5]=!b[2];
  assign out_not[4]=!b[1];
  assign out_not[3]=!b[0];
  assign out_not[2]=!a[2];
  assign out_not[1]=!a[1];
  assign out_not[0]=!a[0];
endmodule
```

## 位操作

```verilog
module top_module( 
    input [3:0] in,
    output out_and,
    output out_or,
    output out_xor
);
assign out_and=&in;
  assign out_or=|in;
  assign out_xor=^in;
endmodule
```

## 向量拼接

```verilog
module top_module (
    input [4:0] a, b, c, d, e, f,
    output [7:0] w, x, y, z );
  assign w ={a[4:0],b[4:2]} ;
  assign x={b[1:0],c[4:0],d[4]};
  assign y={d[3:0],e[4:1]};
  assign z={e[0],f[4:0],2'b11};
endmodule
```

## 向量翻转

```verilog
module top_module( 
    input [7:0] in,
    output [7:0] out
);
  assign out[0]=in[7];
  assign out[1]=in[6];
  assign out[2]=in[5];
  assign out[3]=in[4];
  assign out[4]=in[3];
  assign out[5]=in[2];
  assign out[6]=in[1];
  assign out[7]=in[0];
endmodule
```

## 复制算子

```verilog
module top_module (
    input [7:0] in,
    output [31:0] out );
  assign out = { {24{in[7]}},in[7:0] };
endmodule
```

## 复制算子\_2

```verilog
module top_module (
    input a, b, c, d, e,
    output [24:0] out );
    // The output is XNOR of two vectors created by 
    // concatenating and replicating the five inputs.
  assign out = ~{ {5{a}},{5{b}},{5{c}},{5{d}},{5{e}}} ^ { {5{a,b,c,d,e}} };
endmodule
```

## 模块例化

```verilog
module top_module(
  input 	a,
  input 	b,
  output 	out
);
  mod_a inst_name1(
    .out	(out),
    .in1	(a),
    .in2	(b));
endmodule

module mod_a ( 
  input 	in1, 
  input 	in2, 
  output 	out 
);
assign out = in1 & in2;
endmodule
```

## 基于端口位置的实例化

```verilog
module mod_a (
    output   out1	,
    output   out2	,
    input    in1	,
    input    in2	,
    input    in3	,
    input    in4
);
    assign out1 = in1 & in2 & in3 & in4;    
    assign out2 = in1 | in2 | in3 | in4;   
endmodule

module top_module ( 
	input	a	,
    input	b	,
    input	c	,
    input	d	,
    output	out1,
    output	out2
);
  mod_a mod_a(out1,out2,a,b,c,d);
endmodule
```



## 基于端口名称的实例化

```verilog
module mod_a(
	output out1, out2,
	input in1,in2,in3,in4);
	assign out1 = in1 & in2 & in3 & in4; 	
	assign out2 = in1 | in2 | in3 | in4;	
endmodule

module top_module( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
  mod_a mod_a(
    .out1	(out1),
    .out2	(out2),
    .in1	(a),
    .in2	(b),
    .in3	(c),
    .in4	(d));
endmodule
```

## 多个模块的例化

```verilog
module my_dff(input clk,input d,output reg q);
	always@(posedge clk)
    	q <= d;
endmodule

module top_module ( input clk, input d, output q );
  wire w1,w2;
  my_dff my_dff1(clk,d,w1);
  my_dff my_dff2(clk,w1,w2);
  my_dff my_dff3(clk,w2,q);
endmodule
```

## 模块与向量信号

```verilog
module my_dff8(
  input clk,
  input [7:0] d,
  output reg [7:0] q
);
	always@(posedge clk)
    	q <= d;
endmodule

module top_module(
  input clk,
  input [7:0] d,
  input [1:0] sel,
  output reg [7:0] q
);
  wire[7:0]w1;
  wire[7:0]w2;
  wire[7:0]w3;
  my_dff8 my_dff81(clk,d,w1);
  my_dff8 my_dff82(clk,w1,w2);
  my_dff8 my_dff83(clk,w2,w3);
  always @*
    begin case(sel)
      2'b00:	q=d;
      2'b01:	q=w1;
      2'b10:	q=w2;
      default :	q=w3;
    endcase
    end
endmodule
```

## 加法器

```verilog
module add16 ( input[15:0] a, input[15:0] b, input cin, output[15:0] sum, output cout );
	assign {cout,sum} = a + b + cin;
endmodule

module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
  wire w1,w2;
  wire[15:0] s1;
  wire[15:0] s2;
  add16 add161(a[15:0],b[15:0],1'b0,s1,w1);
  add16 add162(a[31:16],b[31:16],w1,s2,w2);
  assign sum={s2,s1};
endmodule
```

## 多层次例化加法器

```verilog
module top_module (input [31:0] a,
                   input [31:0] b,
                   output [31:0] sum);
wire w1,w4;
wire[15:0]w2;
wire[15:0]w3;
	add16 inst_0(a[15:0],b[15:0],1'b0,w2,w1);
  	add16 inst_1(a[31:16],b[31:16],w1,w3,w4);
assign sum = {w3,w2};
endmodule

module add1 (input a, input b, input cin,   output sum, output cout);
    // Full adder module here
    assign {cout,sum} = cin+a+b;
endmodule
```

## 进位选择加法器

```verilog
module add16 (input[15:0] a,
              input[15:0] b,
              input cin,
              output[15:0] sum,
              output cout);
assign {cout,sum} = a + b + cin;
endmodule

module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
    );
    wire[15:0]w1,w2,w3,w4;
    wire w5,w6,w7;
    add16 add16_1(a[15:0],b[15:0],1'b0,w1,w5);
    add16 add16_2(a[31:16],b[31:16],1'b0,w2,w6);
  add16 add16_3(a[31:16],b[31:16],1'b1,w3,w7);
  assign sum={{w5?w3:w2},w1};
endmodule

```

## 加法减法器

```verilog
module add16 (input[15:0] a,
              input[15:0] b,
              input cin,
              output[15:0] sum,
              output cout);
    assign {cout,sum} = a + b + cin;
endmodule
    module top_module(
        input [31:0] a,
        input [31:0] b,
        input sub,
        output [31:0] sum
        );
        wire[31:0]b1;
        wire w1,w2;
        assign b1 = b^{32{sub}};
      add16 add16_0(a[15:0],b1[15:0],sub,sum[15:0],w1);
      add16 add16_1(a[31:16],b1[31:16],w1,sum[31:16],w2);
    endmodule
```

## always过程块\_组合逻辑

```verilog
module top_module(
    input a, 
    input b,
    output wire out_assign,
    output reg out_alwaysblock
);
assign out_assign=a&b;
  always@(*)out_alwaysblock=a&b;
endmodule
```

## always过程快\_时序逻辑

```verilog
module top_module(
    input clk,
    input a,
    input b,
    output wire out_assign,
    output reg out_always_comb,
    output reg out_always_ff   
);
assign out_assign=a^b;
  always@(*)out_always_comb=a^b;
  always@(posedge clk)out_always_ff<=a^b;
endmodule
```

## if…else…语句

```verilog
module top_module(
    input a,
    input b,
    input sel_b1,
    input sel_b2,
    output wire out_assign,
    output reg out_always); 
assign out_assign=sel_b1&&sel_b2?b:a;
  always@(*)
    begin
      if(sel_b1&&sel_b2)out_always=b;
      else out_always=a;
    end
endmodule
```

## if语句与锁存器

```verilog
module top_module (
    input		cpu_overheated		,
    output	reg	shut_off_computer	,
    input      	arrived				,
    input      	gas_tank_empty		,
    output 	reg keep_driving
);
  	// Edit the code below
	always @(*) begin
    	if (cpu_overheated)
        	shut_off_computer = 1'b1;
      else 
        shut_off_computer=1'b0;
    end
    always @(*) begin
    	if (~arrived)
        	keep_driving = ~gas_tank_empty;
      else
        keep_driving=1'b0;
    end
endmodule
```

## case语句

```verilog
module top_module ( 
    input [2:0] sel, 
    input [3:0] data0,
    input [3:0] data1,
    input [3:0] data2,
    input [3:0] data3,
    input [3:0] data4,
    input [3:0] data5,
    output reg [3:0] out   );
    always@(*) begin  // This is a combinational circuit
      case(sel)
        3'b000:out=data0;
        3'b001:out=data1;
        3'b010:out=data2;
        3'b011:out=data3;
        3'b100:out=data4;
        3'b101:out=data5;
        default:out=3'b000;
      endcase
    end
endmodule
```

## 优先编码器

```verilog
module top_module(input [3:0] in,
                  output reg [1:0] pos);
    always @(*) begin
        if(in[0])
            pos = 2'd0;
        else if (in[1])
            pos = 2'd1;
        else if (in[2])
            pos = 2'd2;
        else if (in[3])
            pos = 2'd3;
        else
            pos = 2'd0;
    end
endmodule
```

## casez语句

```verilog
module top_module (input [7:0] in,
                   output reg [2:0] pos);
    always @(*) begin
        casez(in[7:0])
            8'bzzzzzzz1:pos = 0;
            8'bzzzzzz1z:pos = 1;
            8'bzzzzz1zz:pos = 2;
            8'bzzzz1zzz:pos = 3;
            8'bzzz1zzzz:pos = 4;
            8'bzz1zzzzz:pos = 5;
            8'bz1zzzzzz:pos = 6;
            8'b1zzzzzzz:pos = 7;
            default:pos     = 0;
        endcase
    end
endmodule
```

## 避免锁存器

```verilog
module top_module (input [15:0] scancode,
                   output reg left,
                   output reg down,
                   output reg right,
                   output reg up);
    always @(*) begin
        left  = 1'b0;
        down  = 1'b0;
        right = 1'b0;
        up    = 1'b0;
        case (scancode)
            16'he06b:left  = 1;
            16'he072:down  = 1;
            16'he074:right = 1;
            16'he075:up    = 1;
        endcase
    end
endmodule
```

## 条件运算符

```verilog
module top_module (input [7:0] a,
                   b,
                   c,
                   d,
                   output [7:0] min);
    wire[7:0] min1,min2;
    assign min1 = a<b?a:b;
    assign min2 = c<d?c:d;
    assign min  = min1<min2?min1:min2;
endmodule
```

## 归约运算符

```verilog
module top_module (input [7:0] in,
                   output parity);
    assign parity = ^in;
endmodule
```

## D触发器

```verilog
module top_module (input clk,     // Clocks are used in sequential circuits
                   input d,
                   output reg q);
    // Use a clocked always block
    //   copy d to q at every positive edge of clk
    //   Clocked always blocks should use non-blocking assignments
    always @(posedge clk) begin
        q <= d;
    end
endmodule
```

## 寄存器

```verilog
module top_module (input clk,
                   input [7:0] d,
                   output reg [7:0] q);
    always @(posedge clk) begin
        q <= d;
    end
endmodule

```

## 有复位功能的寄存器

```verilog
module top_module (input clk,
                   input reset,         // Synchronous reset
                   input [7:0] d,
                   output reg [7:0] q);
    always @(posedge clk) begin
        if (reset)
            q <= 8'd0;
        else
            q <= d;
    end
endmodule
```

## 下降沿触发的寄存器

```verilog
module top_module (input clk,
                   input reset,         // Synchronous reset
                   input [7:0] d,
                   output reg [7:0] q);
    always @(negedge clk) begin
        if (reset)
            q <= 8'h34;
        else
            q <= d;
    end
endmodule
```

## 异步复位的寄存器

```verilog
module top_module (input clk,
                   input areset,         // Synchronous reset
                   input [7:0] d,
                   output reg [7:0] q);
  	always @(posedge clk or posedge areset) begin
      if (areset)
            q <= 8'h0;
        else
            q <= d;
    end
endmodule
```

## 带使能的寄存器

```verilog
module top_module(input clk,
                  input resetn,
                  input [1:0] byteena,
                  input [15:0] d,
                  output reg [15:0] q);
    always @(posedge clk) begin
        if (~resetn)
            q <= 8'd0;
        else if (byteena[0]&&byteena[1])
            q <= d;
        else if (byteena[0])
            q[7:0] <= d[7:0];
        else 
            q[15:8] <= d[15:8];
    end
endmodule
```

## 触发器+逻辑门

```verilog
module top_module (input clk,
                   input in,
                   output reg out);
    always @(posedge clk) begin
        out <= in^out;
    end
endmodule
```

## 寄存器+逻辑门

```verilog
module top_module (input clk,
                   input x,
                   output z);
    reg q1,q2,q3;
    always @(posedge clk) begin
        q1 <= q1^x;
        q2 <= ~q2&x;
        q3 <= ~q3|x;
    end
    assign z = ~(q1|q2|q3);
endmodule
```

## 上升沿检测

```verilog
module top_module (input clk,
                   input in,
                   output out);
    reg in_delay,out_r;
    initial begin
        in_delay = 0;
        out_r    = 0;
    end
    assign out = out_r;
    always @(posedge clk) begin
        in_delay <= in;
    end
    always @(posedge clk) begin
        if (in&&!in_delay)
            out_r <= 1;
        else
            out_r <= 0;
    end
endmodule
```

## 双边沿检测

```verilog
module top_module (input clk,
                   input in,
                   output out);
    reg in_delay,out_r;
    initial begin
        in_delay = 0;
        //#3 out_r    = 0;
    end
    assign out = out_r;
    always @(posedge clk) begin
        in_delay <= in;
    end
    always @(posedge clk) begin
        if (in&&!in_delay||!in&&in_delay)
            out_r <= 1;
        else if(out_r==1)
            out_r <= 0;
    end
endmodule

```



## 计数器

```verilog
module top_module (input clk,
                   input reset,         
                   output reg [3:0] q);
    always @(posedge clk or posedge reset) begin
        if (reset||q == 4'b1111)
            q <= 0;
        else
            q <= q+4'b0001;
    end
endmodule
```

## 十进制计数器

```verilog
module top_module (input clk,
                   input reset,         
                   output reg [3:0] q);
    always @(posedge clk) begin
        if (reset||q == 4'd10)
            q <= 4'd1;
        else
            q <= q+4'b0001;
    end
endmodule
```

## 带使能的计数器

```verilog
module top_module(input clk,
                  input reset,
                  input en,
                  output reg [3:0]q);
    always @(posedge clk) begin
        if (en&&reset)
            q <= 4'd5;
        else if (en&&q != 4'd5)
            q <= q-4'd1;
        else if (en&&q == 4'd5)
            q <= 4'd15;
    end
endmodule
```



## 秒表

```verilog
module top_module(input 			clk		,   //4Hz
                  input 			reset	,
                  output	[7:0]	ss);
    reg [7:0]temp1,temp2,s;
    initial begin
        temp1 = 0;
        temp2 = 0;
    end
    assign ss=s;
    always @(posedge clk) begin
        if (reset)
            s <= 0;
        if(reset)
            temp1<=0;
        if(reset)
            temp2<=0;
        else if (temp1 == 7'd3)
            s[3:0] <= s[3:0]+4'd1;
        else
           temp1 <= temp1+7'd1;
        if (reset)
            s <= 0;
        else if (temp2 == 7'd39)
            s[7:4] <= s[7:4]+4'd1;
        else
            temp2 <= temp2+7'd1;
            if(temp1==7'd3)
            temp1<=0;
            if(temp2==7'd39)
            temp2<=0;
        if (s[3:0] == 4'd10)
            s[3:0] <= 4'd0;
        if (s[7:4] == 4'd6)
            s[7:4] <= 4'd0;
    end
endmodule
```



## 移位寄存器

```verilog
module top_module(input clk,
                  input areset,        
                  input load,
                  input ena,
                  input [3:0] data,
                  output reg [3:0] q);
    always @(posedge clk or posedge areset) begin
        if (areset)
            q <= 0;
        else if (load)
            q <= data;
        else if (ena)
            q <= q>>1;
    end
endmodule
```

## 查找表

```verilog
module top_module(
  input clk,
  input enable,
  input S,
  input A, B, C,
  output reg Z 
);
  reg[7:0]q;
  always@(*)
    z<=q[{A,B,C}];
  always@(posedge clk)
    if(enable)
    q<={q[6:0],S};
endmodule
```



## ROM

```verilog
module top_module(input	[2:0] addr,
                  output	[3:0]	q);
reg  [3:0] mem [7:0];
initial begin
    mem[0] = 8'h00;
    mem[1] = 8'h01;
    mem[2] = 8'h02;
    mem[3] = 8'h03;
    mem[4] = 8'h04;
    mem[5] = 8'h05;
    mem[6] = 8'h06;
    mem[7] = 8'h07;
end
assign q = mem[addr];
endmodule
```

## RAM

```verilog
module ram_one_port(input 		 clk,
                    input		 wr_en,
                    input 	[2:0] wr_addr,
                    input	[15:0] wr_data,
                    input	[2:0] rd_addr,
                    output	[15:0] rd_data);
                    reg[15:0] mem[7:0];
    initial begin
        $readmemh("memfile.dat",mem);
    end
    assign rd_data = mem[rd_addr];
    always@(posedge clk)
    begin
        if (wr_en)
            mem[wr_addr] <= wr_data;
    end
endmodule
```

## 有限状态机

```verilog
module top_module(input clk,
                  input areset, // Asynchronous reset to state B
                  input in,
                  output out);
    
    parameter A = 0, B = 1;
    reg state, next_state;
    always @(*) begin    //有限状态机第一段
        // State transition logic
        case (in)
            1'b1:next_state     <= state;
            default: next_state <= ~state;
        endcase
    end
    always @(posedge clk, posedge areset) begin    //有限状态机第二段
        // State flip-flops with asynchronous reset
        if (areset)
            state <= B;
        else if(clk)
            state <= next_state;
    end
    //有限状态机第三段，信号输出逻辑
    assign out = (state == A)?0:1;
endmodule

```



## 读代码找错误

```verilog
module top_module (
    input sel,
    input [7:0] a,
    input [7:0] b,
  	output[7:0] out  );
  assign out = sel?b:a;
endmodule
```

## 编写仿真文件

```verilog
module tb();
    reg a,b;
    initial begin
        a     = 1'b1;
        b     = 1'b0;
        #10 b = 1'b1;
        #10 a = 1'b0;
        #10 b = 1'b0;
        #10 a = 1'b1;
        #20 $finish;
    end
endmodule
```

## 组合逻辑模块仿真

```verilog
module tb();
    reg a,b;
    wire q;
    //对ab信号进行初始化
    initial begin
        a    = 0;b    = 0;
        #15 b = 1;
        #10 b = 0;a    = 1;
        #10 b = 1;
        #10 a = 0;b    = 0;
        #10 b = 1;
        #10 b = 0;a    = 1;
        #10 b = 1;
        #10 b = 0;a    = 0;
        #2 $finish;
    end
    //例化mymodule模块
    mymodule mymodule(a,b,q);
endmodule
    
module mymodule(
    input a,b,
    output q
);
    assign q = a & b;
endmodule
```



## 生成时钟信号

```verilog
module tb();
    wire [2:0]out;
    reg clk;
    initial begin
        clk    = 0;
        #5 clk = 1;
        #5 clk = 0;
        #5 clk = 1;
        #5 clk = 0;
        #5 clk = 1;
        #5 clk = 0;
        #5 clk = 1;
        #5 clk = 0;
        #5 clk = 1;
        #5 clk = 0;
        #5 $finish;
    end
    dut dut(clk,out);
endmodule
    
    module dut(input clk, output reg [2:0]out);
        //测试模块
        always @(posedge clk)
            out <= out + 1'b1;
    endmodule

```


## 单端口RAM仿真

```verilog
module ram_one_port(
	input 	clk,
	input	[1:0] addr,
	input	wr_en,
	input	[7:0] wr_data,
	output	[7:0] rd_data
);
	reg		[7:0] mem[3:0];
	initial
	begin
      mem[0] = 8'b0;
      mem[1] = 8'b0;
      mem[2] = 8'b0;
      mem[3] = 8'b0;
	end
	assign rd_data = mem[addr];
	always@(posedge clk)
	begin
		if(wr_en)
			mem[addr] <= wr_data;
	end
endmodule


module tb(
);
	//信号定义
	reg				clk,wr_en;
	reg		[1:0] 	addr;
	reg		[7:0] 	wr_data;
	wire	[7:0] 	rd_data;
	//信号生成
    initial begin
    clk = 0;
    forever #5 clk = ~clk; //生成周期为10的一个时钟信号，forever为verilog的关键字
end
initial begin
    addr = 2'b0;
    repeat(4) begin 			//repeat为verilog关键字，表示重复操作
	@(posedge clk);		//等待clk信号的上升沿到来
	#1 addr = addr + 1;	//clk上升沿1个时间单位后，addr加一
    end
end
initial begin
	wr_en = 0;
	#501;			//延时一段时间，
	@(posedge clk);
	#1 wr_en = 1;
	@(posedge clk);
	@(posedge clk);
	@(posedge clk);
	@(posedge clk);	//等待4个clk上升沿
	#1 wr_en = 0;
end
initial begin
    wr_data = 8'h0;
    repeat(4) begin
    	wait(wr_en==1'b1);
	#1 wr_data = $random%256;
    	@(posedge clk);
    end
end
	//例化被测模块
endmodule

```

