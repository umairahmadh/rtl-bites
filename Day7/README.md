## Course Note - Day 7: Designing State Machines

Welcome to Day 7 of our RTL Design course! In today's session, we will focus on designing state machines, which are essential components in digital systems that exhibit sequential behavior. We will explore the concept of state machines, their significance in digital design, and practical examples with implementation in Verilog. Here's an overview of the topics we will cover:

### 1. Introduction to State Machines

- Understand the concept of state machines and their role in digital design.
- Explore the basic components of a state machine: states, inputs, outputs, and transitions.
- Discuss the importance of state machines in modeling complex sequential behavior.

### 2. Moore and Mealy Machines

- Compare two common types of state machines: Moore machines and Mealy machines.
- Understand the differences in output generation and timing between these machine types.
- Analyze their advantages and use cases in different design scenarios.

### 3. State Diagrams and State Tables

- Learn how to represent state machines using state diagrams and state tables.
- Translate behavioral requirements into graphical and tabular representations.
- Discuss the benefits of using state diagrams and state tables for visualization and analysis.

### 4. State Encoding

- Explore various state encoding techniques, such as binary encoding and one-hot encoding.
- Understand the impact of state encoding on circuit complexity, timing, and design trade-offs.
- Analyze different scenarios and select suitable state encoding methods.

### 5. State Machine Design Process

- Walk through the step-by-step process of designing state machines.
- Identify states, inputs, outputs, and transitions based on system requirements.
- Define state diagrams and state tables to visualize the state machine behavior.

### Design Example: Traffic Light Controller

To illustrate the concepts covered in this session, let's design a state machine for a traffic light controller. The traffic light controller will have three states: "Green", "Yellow", and "Red". The inputs will include a "pedestrianRequest" signal, and the outputs will control the traffic light signals: "greenSignal", "yellowSignal", and "redSignal". Here's the Verilog code for the traffic light controller:

```verilog
module TrafficLightController(input pedestrianRequest, output reg greenSignal, yellowSignal, redSignal);
  reg [1:0] state;

  always @(posedge clk or posedge reset) begin
    if (reset)
      state <= 2'b00;
    else begin
      case (state)
        2'b00: if (pedestrianRequest) state <= 2'b01; else state <= 2'b00;
        2'b01: state <= 2'b10;
        2'b10: state <= 2'b11;
        2'b11: state <= 2'b00;
      endcase
    end
  end

  always @(state) begin
    case (state)
      2'b00: begin greenSignal = 1'b1; yellowSignal = 1'b0; redSignal = 1'b0; end
      2'b01: begin greenSignal = 1'b0; yellowSignal = 1'b1; redSignal = 1'b0; end
      2'b10: begin greenSignal = 1'b0; yellowSignal = 1'b0; redSignal = 1'b1; end
      2'b11: begin greenSignal = 1'b1; yellowSignal = 1'b0; redSignal = 1'b0; end
    endcase
  end
endmodule
```

This code implements the traffic light controller using a finite state machine (FSM) approach. The `state` variable represents the current state of the traffic light controller, and the output signals are assigned based on the current state. The FSM transitions are determined by the `pedestrianRequest` input signal.

By the end of this session, you will have a solid understanding of state machines and be able to design and implement them effectively using Verilog. The design example of the traffic light controller demonstrates how state machines can be used to model and control the sequential behavior of real-world systems.

**Note:** This is a condensed course note for Day 7. The full course material will provide more detailed explanations, examples, and exercises to reinforce your understanding of state machine design and implementation.



Certainly! Let's walk through a simple example of designing a state machine for a traffic light controller. The goal is to create a state machine that controls the sequence of traffic light signals: Green, Yellow, and Red. Here's the step-by-step process:

1. Identify States:
   - We can define three states: "Green", "Yellow", and "Red". Each state corresponds to a specific traffic light signal.

2. Define Inputs and Outputs:
   - Inputs: We can have an input called "pedestrianRequest" to indicate when a pedestrian wants to cross the road.
   - Outputs: We need three outputs to control the traffic light signals: "greenSignal", "yellowSignal", and "redSignal".

3. Create a State Diagram:
   - Using the identified states, we can create a state diagram that represents the transitions between states based on inputs and outputs.
   - Here's an example of a state diagram for our traffic light controller:

   ![State Diagram](state_diagram.png)

   In this diagram:
   - The arrows indicate the transitions between states based on specific conditions.
   - The conditions are shown near the arrows, indicating the triggering event for each transition.
   - The labels on the transitions represent the actions taken during the transition (e.g., activating or deactivating specific signals).

4. Create a State Table:
   - Translate the state diagram into a state table that defines the behavior of the state machine.
   - Here's an example of a state table for our traffic light controller:

   | Current State | Inputs             | Next State | Outputs                          |
   |---------------|--------------------|------------|----------------------------------|
   | Green         | pedestrianRequest  | Yellow     | greenSignal = 0, yellowSignal = 1 |
   | Green         | !pedestrianRequest | Green      | greenSignal = 1, yellowSignal = 0 |
   | Yellow        | -                  | Red        | yellowSignal = 0, redSignal = 1   |
   | Red           | -                  | Green      | yellowSignal = 0, redSignal = 0   |

   In this table:
   - The "Inputs" column represents the input conditions for each transition.
   - The "Next State" column indicates the state to transition to based on the inputs.
   - The "Outputs" column defines the values of the output signals for each state.

5. Implement the State Machine in Verilog:
   - Using the state table as a guide, implement the state machine in Verilog code.
   - Here's an example of how the Verilog code for the traffic light controller might look:

   ```verilog
   module traffic_light_controller(input pedestrianRequest, output reg greenSignal, yellowSignal, redSignal);
     reg [1:0] state;

     always @(posedge clk or posedge reset) begin
       if (reset)
         state <= 2'b00;
       else begin
         case (state)
           2'b00: if (pedestrianRequest) state <= 2'b01; else state <= 2'b00;
           2'b01: state <= 2'b10;
           2'b10: state <= 2'b11;
           2'b11: state <= 2'b00;
         endcase
       end
     end

     always @(state) begin
       case (state)
         2'b00: begin greenSignal = 1'b1; yellowSignal = 1'b0; redSignal = 1'b0; end
         2'b01: begin greenSignal = 1'b0; yellowSignal = 1'b1; redSignal = 1'b0; end
         2'b10: begin greenSignal = 1'b0; yellowSignal = 1'b0; redSignal = 1'b1; end
         2'b11: begin greenSignal = 1'b1; yellowSignal = 1'b0; redSignal = 1'b0; end
       endcase
     end
   endmodule
   ```

   Note: This is a simplified example and does not include the clock signal or reset functionality. In a real implementation, you would need to consider these aspects.

6. Simulate and Verify the State Machine:
   - Use a Verilog simulator or EDA Playground to simulate the behavior of the state machine and verify that it behaves as expected.
   - Write a testbench that provides inputs and monitors the outputs, ensuring they follow the expected state transitions and signal values.

By following these steps, you can design and implement a state machine for a traffic light controller. This example demonstrates the practical application of state machines in controlling sequential behavior in digital systems.
