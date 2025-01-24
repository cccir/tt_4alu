<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

Explain how your project works

# Longer description of how the project works. You can use standard markdown format.
  how_it_works: |
      Each clock cycles ALU performs one of the 8 possible operations and stores result in the 4-bit accumulator register.

      accumulator [4 bit] = accumulator [4 bit] (operation) operand [4 bit]

      Supported operations:
      lda imm   ::  imm -> accumulator
      neg imm   ::  0x0F - imm -> accumulator
      shr       ::  accumulator / 2 -> accumulator
      sub imm   ::  accumulator - imm -> accumulator
      and imm   ::  accumulator & imm -> accumulator
      xor imm   ::  accumulator ^ imm -> accumulator
      or  imm   ::  accumulator | imm -> accumulator
      add imm   ::  accumulator + imm -> accumulator

      Matrix mapping of operation opcode to internal control signals
               muxA muxB muxC AtoX negX setC outC invC
      000 lda   -    -    1    0    0    -    0    -
      001 neg   -    -    1    0    1    -    0    -
      010 shr   -    -    1    1    0    -    0    -
      011 sub   1    1    0    0    1    1    1    1
      100 and   0    0    0    0    0    -    0    -
      101 xor   0    1    0    0    0    -    0    -
      110 or    1    0    0    0    0    -    0    -
      111 add   1    1    0    0    0    0    1    0


# Instructions on how someone could test your project, include things like what buttons do what and how to set the clock if needed
  how_to_test:  |
    The following diagram shows a simple test setup that can be used to test ALU
    ```
      VCC
      |    __|__ pushbutton
      +----.   .-------------+
                            _|_
                 schmitt    \ /
                 trigger     O
                 inverter    |
                             +--> CLK   OUT0--> +-----------+
                   +--------+---> OP0   OUT1--> +  hex to   +
                   +        +---> OP1   OUT2--> + 7 segment +--->> 7 segment display
                   +        +---> OP2   OUT3--> +  decoder  +
                   +  DIP   +---> IMM0          +-----------+
                   + switch +---> IMM1          
                   +        +---> IMM2          
                   +        +---> IMM3 CARRY--> LED
                   +--------+--
    ```
    
    To reset ALU set all input pins to 0 which corresponds to ```lda 0``` operation
    loading Accumulator register with 0.

# A description of what the inputs do
  inputs:               
    - clock
    - opcode 0th bit
    - opcode 1st bit
    - opcode 2nd bit
    - operand 0th bit
    - operand 1st bit
    - operand 2nd bit
    - operand 3rd bit
# A description of what the outputs do
  outputs:
    - accumulator value 0th bit
    - accumulator value 1st bit
    - accumulator value 2nd bit
    - accumulator value 3rd bit
    - unused (TODO: negative flag)
    - unused (TODO: overflow flag)
    - unused (TODO: zero flag)
    - carry flag

## How to test

Explain how to use your project

## External hardware

List external hardware used in your project (e.g. PMOD, LED display, etc), if any
