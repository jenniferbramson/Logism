Jennifer Bramson
jib41@pitt.edu

This logism file creates a single-cycle processor to implement a subset of MIPS instructions.

I tried to use the same general layout as the datapath we covered in class. So,
for example, all of the arithmetic and logical operations (and, nor, add, sub,
addi, addui, mult, div, along with the comparisons necessary for branches) all
occur within the ALU. The decoder computes a 3-bit value called ALUOp that
controls which of the operations' results is output. There are three outputs
total from the ALU: Branch (1 when the comparison done would lead to branching
and 0 when the the comparison was incorrect), result, and HI. HI is used
primarily for multiply and divide, but it holds the carryout or carryin for
the add and subtract calls. Result feeds to $LO for multiply and divide.

Moving on to the Register File, there are eight registers ($r0-$r7) and
ReadRegister1 input and ReadRegister2 input control which registers are read.
The values for those two inputs comes directly from the instruction. The
decoder's RegWrite controls whether a register should be written to or not.
The clock from the main circuit is used as the clock in this subcircuit by
passing it in as an input labeled 'clock'.

The data that is written to a register depends on the input that the WriteData
MUX choses, which also comes from the decoder. There are 6 possibilities here:
the result directly from the ALU, an immediate value, PC+1, data from memory
from lw instructions (this input uses a tunnel called MemData), $LO, and $HI.

The decoder is a subcircuit comprised of 6 subcircuits to keep everything
visually clear. The first controls writing to the registers and which
data should be chosen from the WriteData MUX to be written. The second controls
the ALU operation, the third halt and put. The fourth is for enabling the
$HI and $LO registers. The fifth is for enabling writing to the memory. Finally,
the sixth is for changing the PC to a branch (BR) or jump (JR) immediate when
necessary. This results in the decoder having nine control outputs.

There are no known bugs. All of the instructions that were listed in the
project assignment are implemented.
