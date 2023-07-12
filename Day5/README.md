## Course Note - Day 5: Combinational Circuits - Multiplexers, Decoders, and Encoders

In this session, we will continue our exploration of combinational circuits by focusing on multiplexers, decoders, and encoders. We will provide examples of Verilog code and testbenches using EDA Playground. Here's an overview of the topics we will cover:

### 1. Multiplexers (MUX)

- We will dive into the functionality and applications of multiplexers.
- Understanding how multiplexers select and route data based on control signals will be our main focus.
- We will provide an example of a 4-to-1 multiplexer implemented in Verilog, along with a corresponding testbench to simulate its behavior using EDA Playground.

```verilog
module mux_4to1(input [3:0] data, input [1:0] select, output out);
  assign out = select[0] ? data[1] : data[0];
endmodule
```

```verilog
module mux_4to1_tb;
  reg [3:0] data;
  reg [1:0] select;
  wire out;

  mux_4to1 dut (.data(data), .select(select), .out(out));

  initial begin
    data = 4'b0000;
    select = 2'b00;

    #10;
    data = 4'b0101;
    select = 2'b01;

    #10;
    // Add more test cases as needed

    $finish;
  end
endmodule
```

### 2. Decoders

- We will study the purpose and operation of decoders in digital circuits.
- Understanding how decoders convert encoded data into a set of output signals will be emphasized.
- We will provide an example of a 3-to-8 decoder implemented in Verilog, along with a testbench to verify its functionality on EDA Playground.

```verilog
module decoder_3to8(input [2:0] address, output [7:0] data);
  assign data = (address == 3'b000) ? 8'b00000001 :
               (address == 3'b001) ? 8'b00000010 :
               (address == 3'b010) ? 8'b00000100 :
               (address == 3'b011) ? 8'b00001000 :
               (address == 3'b100) ? 8'b00010000 :
               (address == 3'b101) ? 8'b00100000 :
               (address == 3'b110) ? 8'b01000000 :
                                    8'b10000000 ;
endmodule
```

```verilog
module decoder_3to8_tb;
  reg [2:0] address;
  wire [7:0] data;

  decoder_3to8 dut (.address(address), .data(data));

  initial begin
    address = 3'b000;
    #10;
    address = 3'b010;
    #10;
    // Add more test cases as needed

    $finish;
  end
endmodule
```

### 3. Encoders

- We will explore the role of encoders in digital systems.
- Understanding how encoders convert multiple input signals into a smaller set of output signals will be our primary objective.
- We will provide an example of an 8-to-3 priority encoder implemented in Verilog, along with a testbench to validate its functionality using EDA Playground.

```verilog
module encoder_8to3(input [7:0] data, output [2:0] encoded);
  wire [7:0] inverted_data;

  assign inverted_data = ~data;
  assign encoded = (inverted_data[7]) ? 3'b111 :
                  (inverted_data[6]) ? 3'b110 :
                  (inverted_data[5]) ? 3'b101 :
                  (inverted_data[4]) ? 3'b100 :
                  (inverted_data[3]) ? 3'b011 :
                  (inverted_data[2]) ? 3'b010 :
                  (inverted_data[1]) ? 3'b001 :
                                      3'b000 ;
endmodule
```

```verilog
module encoder_8to3_tb;
  reg [7:0] data;
  wire [2:0] encoded;

  encoder_8to3 dut (.data(data), .encoded(encoded));

  initial begin
    data = 8'b00000001;
    #10;
    data = 8'b00000100;
    #10;
    // Add more test cases as needed

    $finish;
  end
endmodule
```

By using the provided Verilog code and testbenches, you can simulate and verify the behavior of multiplexers, decoders, and encoders on EDA Playground. Feel free to modify the test cases or add additional ones to further explore their functionality.

**Note:** The examples provided are simplified and intended for educational purposes. In practical applications, you may need to consider additional factors such as timing, edge cases, and optimizations for real-world circuit designs.
