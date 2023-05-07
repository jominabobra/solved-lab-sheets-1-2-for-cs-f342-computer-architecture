Download Link: https://assignmentchef.com/product/solved-lab-sheets-1-2-for-cs-f342-computer-architecture
<br>
<strong style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;"><u>Goals for Lab 1 &amp; 2</u></strong><u style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">:</u><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;"> </span>

<strong><u>Goal 1</u></strong>: Installing and launching QTSPIM – this tool will be used for major part of the lab work.

<strong><u>Installing and launching QTSPIM</u></strong>

Open a terminal to run the following commands.

<ol>

 <li>Check the OS and the processor support on your Linux machine – verify whether it is</li>

</ol>

32 bit or 64 bit. [Try commands like uname –p ; uname –a ; man uname]

<ol>

 <li>Download the       appropriate      QTSPIM         binary from    Internet</li>

</ol>

<a href="https://sourceforge.net/projects/spimsimulator/files/">(</a><a href="https://sourceforge.net/projects/spimsimulator/files/">https://sourceforge.net/projects/spimsimulator/files/</a><a href="https://sourceforge.net/projects/spimsimulator/files/">)</a> or from <a href="http://172.16.103.147/CA">http://172.16.103.147/CA</a>

<ol>

 <li>Install using dpkg tool. Do not forget to get “super user privilege” using sudo. $ sudo dpkg -i &lt;qtspim package&gt;</li>

 <li>Launch QTSPIM</li>

</ol>




Note: Please refer to the following: (i) HP_AppA.pdf (ii) Chapter 2 Hennessey &amp; Patterson Book (iii) <strong>MIPS Reference Data Card (“Green sheet”)</strong>

<strong><u>Goal 2</u></strong>: To get introduced to QTSPIM and implement some code related to – System Calls and User Input. Further, we will do basic integer Add/Sub/And/Or and their immediate flavours

(e.g. ori).

<u>Reference for MIPS assembly</u> – refer to the <strong>MIPS Reference Data Card (“Green sheet”)</strong> uploaded in CMS. Further, some of the QTSPIM assembly instructions are beyond this data card (e.g. the pseudo instruction <strong><em><u>la</u></em></strong>).

Additionally use Appendix A (HP_AppA.pdf) from Patterson and Hennessey “Assemblers, Linkers and the SPIM Simulator” for gaining background knowledge of SPIM.

In this lab we focus on reversing only integer based instructions (add, or, subi etc.).

<strong><u>Reference for Registers:</u></strong>




System calls as well as functions (in later part of the semester) should take care of using the registers in proper sequence. Especially take note of V0, V1 [R2, R3 in QTSPIM] and        a0-a3 [R4-R7 in QTSPIM] registers.

<strong><u>Reference for System Calls:</u></strong><strong>  </strong>




<strong> </strong>

<strong><u>Reference for Data directives:</u></strong><strong>  </strong>

<strong>.word w1, …, wn</strong>

-store n 32-bit quantities in successive memory words

<strong> </strong>

<strong>.half h1, …, hn</strong>

-store n 16-bit quantities in successive memory half words

<strong>.byte b1, …, bn</strong>

-store n 8-bit quantities in successive memory bytes

<strong>.ascii str</strong>

-store the string in memory but do not null-terminate it

-strings are represented in double-quotes “str”

-special characters, eg. 
, t, follow C convention




<strong>.asciiz str</strong>

-store the string in memory and null-terminate it

<strong> </strong>

<strong>.float f1, …, fn</strong>

-store n floating point single precision numbers in successive memory locations

<strong> </strong>

<strong>.double d1, …, dn</strong>

-store n floating point double precision numbers in successive memory locations

<strong> </strong>

<strong>.space n </strong>

-reserves n successive bytes of space

<strong><u>Layout of Code in QTSPIM:</u></strong> Typical code layout (*.asm file edited externally)

# objective of the program

.data #variable declaration follows this line  .text #instructions follow this line  main: # the starting block label

…

xxx yyy zzz

…..

li $v0,10 #System call- 10 =&gt; Exit;

syscall   # Tells QTSPIM to properly terminate the run

#end of program




<strong><u>Exercise 0:</u></strong> Understanding Pseudo instruction.

Not all instructions used in the lab will directly map to MIPS assembly instructions. Pseudoinstructions are instructions not implemented in hardware. E.g. using $0 or $r0 we can load constants or move values across registers using add instruction.

<strong>E.g.</strong><strong> li $v0, 10 </strong><strong>actually gets implemented by assembler as</strong><strong> ori $v0, $r0, 10 </strong>




In subsequent exercises, identify the pseudo instruction by looking at the actual code used by QTSPIM.

<strong><u>Exercise 1:</u></strong> Integer input and output and stepping through the code.

Invoking system calls <u>to output (print) strings and </u> and <u>input (read) integers</u>.

<strong>The following code snippet prints the number 10 on console. Modify it to read any number and print it back. </strong>

Hint: To copy it from $v0 to $a0, you can use add or addi with 0 or similar options.

Edit the code in your editor of choice and then load it in QtSpim. Single Step [] through the code and look at the register values as you execute various instructions. The demo code is given below:




# demo code to print the <strong>integer value 10 </strong>




<strong>.data </strong>#variable declaration follow this line

# sample string variable declaration – not used in first exercise.  myMsg: .asciiz “Hello Enter a number.” # string declaration

# .asciiz directive makes string null terminated




<strong>.text </strong>#instructions follow this line  main:  li $a0,10 li $v0,1 syscall

li $v0,10 #System call – Exit – QTSPIM to properly terminate the run syscall

#end of program




<strong><u>Exercise2:</u></strong> Modify the above code to output “myMsg” along with the input integer. You will use load address MIPS instruction (la $a0, myMsg)

<strong><u>Exercise 3:</u></strong> Take 2 integers as input, perform addition and subtraction between them and display the outputs. The result of addition is to be displayed as “The sum is =”  and that of subtraction is to be displayed as “The difference is =”. Check if negative integers can be handled.

<em>Observations: List all the pseudoinstructions used in this exercise and discuss. </em>

<strong> </strong>

<strong><u>Exercise 4:</u></strong> Disassemble the binary / hex code to MIPS assembly code. Note that pseudoinstructions cannot be identified using this. For your information, a brief discussion for a sample instruction follows below.







For code at address 0x0040 0038 – which is having a value of 0x2048 0000 when we break into opcode etc. we get:

Binary representation: 0010 0000 0100 1000 0000 0000 0000 0000

OpCode value is: 0010 00  (8 decimal)

As per green card, OpCode 8 decimal is for <strong>addi </strong><strong>(</strong>type <strong>I) </strong>




rs value is: 00 010 =&gt; 2 decimal- register v0 rt value is: 01 000 =&gt; 8 decimal – register t0 immediate value is: 0000 0000 0000 0000 =&gt; 0

Hence the instruction is <strong>addi $t0, $v0, 0 </strong>




In groups, write different assembly instructions and ask your group members to reverse from hexnotation.

Also as an exercise reverse the following three values:

<ol>

 <li>00a64020</li>

 <li>00a64822</li>

 <li>34020005</li>

</ol>


