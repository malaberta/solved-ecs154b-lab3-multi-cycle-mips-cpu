Download Link: https://assignmentchef.com/product/solved-ecs154b-lab3-multi-cycle-mips-cpu
<br>
<ul>

 <li>Build and test a multi-cycle MIPS CPU that implements a subset of the MIPS instruction set.</li>

 <li>Design a microcode control unit.</li>

</ul>

<h1>Description</h1>

In this lab, you will use Logisim to build a multi-cycle CPU, to further increase your knowledge of MIPS and as an introduction to microcode control. To test your CPU, you will run assembly language programs and simulate them in Logisim. You will be provided with a base project as a starting point. Appendix D of <em>Computer Organization and Design</em>, available online at <a href="http://booksite.elsevier.com/9780124077263/downloads/advance_contents_and_appendices/appendix_D.pdf">http://booksite.elsevier.com/9780124077263/ </a><a href="http://booksite.elsevier.com/9780124077263/downloads/advance_contents_and_appendices/appendix_D.pdf">downloads/advance_contents_and_appendices/appendix_D.pdf</a><a href="http://booksite.elsevier.com/9780124077263/downloads/advance_contents_and_appendices/appendix_D.pdf">,</a> will be very useful for this lab. You can find it along with a sample program that you will be tested against in the Lab 3 assignment on SmartSite. You must implement the CPU control using microcode. The microcode implementation that you pick is up to you.

<h1>Details</h1>

In this lab, you will have a single RAM acting as both instruction and data memory. Just like Lab 2, you will have a 256 word-deep memory. You can logically reserve the first 128 words for instructions and the next 128 for data. This means that, in the programs you write and you will be tested on, <strong>the PC should not go beyond the 128th word’s address. Likewise, all memory locations accessed by </strong>LW <strong>and </strong>SW <strong>should be between the 129th and 256th words of memory. </strong>As in Lab 2, the PC is incremented by 4, so, in your instruction memory, the first instruction will be at 0x00000000, the second at 0x00000004, the third at 0x00000008, and so on.

You will be given an empty project to start your lab that includes an implementation of an ALU and a Register File. The file <strong>Lab 3 Given.circ </strong>contains these sub-circuits.

<h1>Instructions to Implement</h1>

Your CPU must execute the following instructions:

<ul>

 <li>All previous instructions from Lab 2.</li>

</ul>

<strong>– </strong>AND, ANDI, ADD, ADDI, OR, ORI, SUB, SLT, SLTU*, XOR, LW, SW, BEQ, J, JAL, JR

<ul>

 <li>SLL</li>

 <li>SRL</li>

</ul>

<strong>As with the previous lab, the instructions for SLTU are incorrect in the given MIPS PDF. </strong>The instructions should read:

If rs <em>&lt; </em>rt with an unsigned comparison, put 1 into rd. Otherwise put 0 into rd.

For this lab, you must use microcode to implement the main control unit. The exact microcode implementation is up to you. All control signals must come from a ROM.

<h1>Subcircuits</h1>

<strong>Register File</strong>

<ul>

 <li>The register file is the same as in Lab 2.</li>

</ul>

<strong>ALU</strong>

<ul>

 <li>The ALU will now support SLL and SRL, and there is now a Shamt[4..0] (shift amount) input.</li>

 <li>When performing shift operations, the B input is shifted by the amount specified by Shamt.</li>

 <li>The control signal <strong>ALUCtl </strong>is described below:</li>

</ul>

<table width="352">

 <tbody>

  <tr>

   <td width="75">Operation</td>

   <td width="69">ALUCtl3</td>

   <td width="69">ALUCtl2</td>

   <td width="69">ALUCtl1</td>

   <td width="69">ALUCtl0</td>

  </tr>

  <tr>

   <td width="75">OR</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="75">SLTU</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="75">SLT</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="75">ADD</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="75">SUB</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="75">XOR</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="75">AND</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="75"></td>

   <td width="69"></td>

   <td width="69">…</td>

   <td width="69"></td>

   <td width="69"></td>

  </tr>

  <tr>

   <td width="75">SLR</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="75">SLL</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">1</td>

  </tr>

 </tbody>

</table>