## Course Note - Day 6: Sequential Logic Design - Flip-Flops and Latches

In this session, we will shift our focus to sequential logic design, which involves the use of flip-flops and latches. We will provide examples of Verilog code and testbenches using EDA Playground. Here's an overview of the topics we will cover:

### 1. Introduction to Sequential Logic

- We will discuss the importance of sequential logic in building memory elements and storing state information.
- Understanding the distinction between sequential and combinational logic will be emphasized.

### 2. Latches

- We will explore the working principles and behavior of latches, which are basic memory elements in sequential circuits.
- We will provide an example of an SR latch implemented in Verilog, along with a corresponding testbench to simulate its behavior using EDA Playground.

```verilog
module sr_latch(input s, r, output q, q_bar);
  reg q, q_bar;

  always @(s, r)
    case ({s, r})
      2'b01: begin q = 1'b0; q_bar = 1'b1; end
      2'b10: begin q = 1'b1; q_bar = 1'b0; end
      default: begin q = q; q_bar = q_bar; end
    endcase
endmodule
```

```verilog
module sr_latch_tb;
  reg s, r;
  wire q, q_bar;

  sr_latch dut (.s(s), .r(r), .q(q), .q_bar(q_bar));

  initial begin
    s = 0; r = 0;
    #10;
    s = 0; r = 1;
    #10;
    // Add more test cases as needed

    $finish;
  end
endmodule
```

### 3. Flip-Flops

- We will study flip-flops as synchronous memory elements that provide better control and synchronization in sequential circuits.
- We will provide an example of a D flip-flop implemented in Verilog, along with a testbench to verify its functionality on EDA Playground.

```verilog
module d_flip_flop(input d, clk, reset, output q, q_bar);
  reg q, q_bar;

  always @(posedge clk, posedge reset)
    if (reset)
      begin
        q <= 1'b0;
        q_bar <= 1'b1;
      end
    else
      begin
        q <= d;
        q_bar <= ~d;
      end
endmodule
```

```verilog
module d_flip_flop_tb;
  reg d, clk, reset;
  wire q, q_bar;

  d_flip_flop dut (.d(d), .clk(clk), .reset(reset), .q(q), .q_bar(q_bar));

  initial begin
    d = 0; clk = 0; reset = 0;
    #10;
    d = 1; clk = 0; reset = 0;
    #10;
    // Add more test cases as needed

    $finish;
  end
endmodule
```

### 4. Timing and Clock Signals

- We will delve into the importance of timing in sequential circuits and the role of clock signals.
- Understanding setup time, hold time, and clock frequency will be crucial for reliable circuit operation.
- We will discuss timing constraints and the impact of clock skew on circuit performance.

By using the provided Verilog code and testbenches, you can simulate and verify the behavior of latches and flip-flops on EDA Playground. Feel free to modify the test cases or add additional ones to further explore their functionality.

**Note:** The examples provided are simplified and intended for educational purposes. In practical applications, you may need to consider additional factors such as clock domains, metastability, and synchronization techniques for robust sequential circuit designs.
