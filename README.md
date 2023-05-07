Download Link: https://assignmentchef.com/product/solved-encm-369-lab-10
<br>



<h1>Exercise A: Tracing behaviour of an I-cache</h1>

<h2>Read This First</h2>

In learning about caches, it is useful to trace through all of the copying of bit patterns that occurs in a sequence of memory accesses.

<h2>What to Do</h2>

<strong>Figure 1: </strong>Computer with one level of cache, and no address translation.

The table in Figure 3 shows some of the main memory contents for a program running on a computer like the one shown in Figure 1, running the MIPS instruction set (except that this computer does <em>not </em>have delayed jumps and branches). Note that the first sequence of instructions is a complete procedure, but the second sequence is only part of a procedure. The second sequence includes a loop; within that loop there is a call to the procedure comprised of the first sequence of instructions. You will be asked to trace the interaction between the I-cache and the main memory starting with PC = 0x0040_27b8, at the moment in time just before the beq instruction is fetched.

The I-cache for this computer is direct-mapped with 1024 sets, and the block in each set contains one instruction. This structure exactly matches an example that has been presented in a lecture. For this cache, main memory addresses are split as shown in Figure 2.

At the moment in time mentioned above, the state of sets 494–499 of the cache is shown in Figure 4. Use 0x1000_1038 as the initial value for $s2 and 0x1000_1040 as the initial value for $s3. Trace all the instruction fetches until after the instruction at address 0x0040_27cc has been fetched. Record your answer in tabular form, using this trace of the first two instructions as a model:

<table width="451">

 <tbody>

  <tr>

   <td width="93">address</td>

   <td width="65">tag</td>

   <td width="36">set</td>

   <td width="256">action</td>

  </tr>

  <tr>

   <td width="93">0x0040_27b8</td>

   <td width="65">0x00402</td>

   <td width="36">494</td>

   <td width="256">I-cache hit—no I-cache update</td>

  </tr>

  <tr>

   <td width="93">0x0040_27bc</td>

   <td width="65">0x00402</td>

   <td width="36">495</td>

   <td width="256">I-cache miss—instruction 0x0240_2021 is copied into instruction field in set 495, Vbit in that set is changed to 1, tag to0x00402</td>

  </tr>

 </tbody>

</table>

<em>Hints: </em>(1) Including the two instruction fetches given as examples, there will be a total of 18 instruction fetches. (2) There is a useful C program in encm369w18lab10/exA.

<strong>Figure 2: </strong>How instruction addresses are split for access to the cache of Exercise A.

31                                                               1211                               21 0

byte offset

<strong>Figure 3: </strong>Small fragments of main memory contents for Exercise A.

<table width="447">

 <tbody>

  <tr>

   <td width="93">address</td>

   <td width="143">instruction at address</td>

   <td colspan="2" width="211">disassembly of instruction</td>

  </tr>

  <tr>

   <td width="93">0x0040_17c0</td>

   <td width="143">0x8c99_0000</td>

   <td width="99">P1: lw</td>

   <td width="113">$t9, ($a0)</td>

  </tr>

  <tr>

   <td width="93">0x0040_17c4</td>

   <td width="143">0x0019_c023</td>

   <td width="99">subu</td>

   <td width="113">$t8, $zero, $t9</td>

  </tr>

  <tr>

   <td width="93">0x0040_17c8</td>

   <td width="143">0xac98_0000</td>

   <td width="99">sw</td>

   <td width="113">$t8, ($a0)</td>

  </tr>

  <tr>

   <td width="93">0x0040_17cc</td>

   <td width="143">0x03e0_0008</td>

   <td width="99">jr</td>

   <td width="113">$ra</td>

  </tr>

  <tr>

   <td width="93">…</td>

   <td width="143">…</td>

   <td width="99">…</td>

   <td width="113"></td>

  </tr>

  <tr>

   <td width="93">0x0040_27b8</td>

   <td width="143">0x1253_0004</td>

   <td width="99">beq</td>

   <td width="113">$s2, $s3, L2</td>

  </tr>

  <tr>

   <td width="93">0x0040_27bc</td>

   <td width="143">0x0240_2021</td>

   <td width="99">L1: addu</td>

   <td width="113">$a0, $s2, $zero</td>

  </tr>

  <tr>

   <td width="93">0x0040_27c0</td>

   <td width="143">0x0c10_0f50</td>

   <td width="99">jal</td>

   <td width="113">P1</td>

  </tr>

  <tr>

   <td width="93">0x0040_27c4</td>

   <td width="143">0x2652_0004</td>

   <td width="99">addiu</td>

   <td width="113">$s2, $s2, 4</td>

  </tr>

  <tr>

   <td width="93">0x0040_27c8</td>

   <td width="143">0x1653_fffc</td>

   <td width="99">bne</td>

   <td width="113">$s2, $s3, L1</td>

  </tr>

  <tr>

   <td width="93">0x0040_27cc</td>

   <td width="143">0x2414_0000</td>

   <td width="99">L2: addiu</td>

   <td width="113">$s4, $zero, 0</td>

  </tr>

 </tbody>

</table>

<strong>Figure 4: </strong>Part of the initial state of the I-cache for Exercise A. (Only sets 494–499 in the cache are shown.)

<table width="238">

 <tbody>

  <tr>

   <td width="36">set</td>

   <td width="44">valid</td>

   <td width="65">tag</td>

   <td width="93">instruction</td>

  </tr>

  <tr>

   <td width="36">494</td>

   <td width="44">1</td>

   <td width="65">0x00402</td>

   <td width="93">0x1253_0004</td>

  </tr>

  <tr>

   <td width="36">495</td>

   <td width="44">0</td>

   <td width="65">0x00000</td>

   <td width="93">0x0000_0000</td>

  </tr>

  <tr>

   <td width="36">496</td>

   <td width="44">1</td>

   <td width="65">0x00401</td>

   <td width="93">0x8c99_0000</td>

  </tr>

  <tr>

   <td width="36">497</td>

   <td width="44">1</td>

   <td width="65">0x00401</td>

   <td width="93">0x0019_c023</td>

  </tr>

  <tr>

   <td width="36">498</td>

   <td width="44">1</td>

   <td width="65">0x00401</td>

   <td width="93">0xac98_0000</td>

  </tr>

  <tr>

   <td width="36">499</td>

   <td width="44">1</td>

   <td width="65">0x00401</td>

   <td width="93">0x03e0_0008</td>

  </tr>

 </tbody>

</table>

<strong>What to Hand In</strong>

Hand in your completed table.

<h1>Exercise B: Analysis of direct-mapped caches</h1>

<h2>Read This First</h2>

<h3>The base-two logarithm</h3>

The <em>base-two logarithm </em>is a simple and useful concept that has many useful applications in computer systems, one of which is describing dimensions in caches. The log<sub>2 </sub>function is simply the inverse of the function <em>f</em>(<em>x</em>) = 2<em><sup>x</sup></em>, in the same way that the ln function is the inverse of <em>f</em>(<em>x</em>) = <em>e<sup>x </sup></em>and the log<sub>10 </sub>function (often written as simply log) is the inverse of <em>f</em>(<em>x</em>) = 10<em><sup>x</sup></em>. For example, log<sub>2 </sub>1 = 0<em>, </em>log<sub>2 </sub>4 = 2<em>, </em>log<sub>2 </sub>32 = 5<em>, </em>and log<sub>2 </sub>65536 = 16<em>.</em>

<h3>Dimensions within direct-mapped caches</h3>

Direct-mapped lookup is the simplest practical way to organize a data or instruction cache. It is illustrated in Figures 8.7 and 8.12 in the course textbook. The general structure of all direct-mapped caches is shown in Figure 5.

To search for an instruction word or data word in a direct-mapped cache, the main memory address of that word is broken into three or four parts:

<ul>

 <li><em>tag: </em>used to distinguish a block address among a group of block addresses that all generate the same set bits;</li>

 <li><em>set bits: </em>used to select one set among the <em>S </em>sets in the cache;</li>

 <li><em>block offset: </em>used to select a single word within a multi-word block, so not necessary if the cache has one-word blocks;</li>

 <li><em>byte offset: </em>can be assumed to be zero when the cache access is to an entire data or instruction word, but would be important for access to indivdual bytes in instructions such as MIPS lb, lbu, and sb.</li>

</ul>

How wide are each of these fields? Let’s go right-to-left within an address. First,

byte offset width = log<sub>2</sub>(number of bytes per word)<em>.</em>

So with 4-byte words, as in textbook and lecture examples, the byte offset width is log<sub>2 </sub>4 = 2, but with 8-byte words, the byte offset width would be log<sub>2 </sub>8 = 3.

Next, block offset width = log<sub>2</sub>(number of words per block)<em>.</em>

For example, in textbook Figure 8.12, there are 4 words per block, so the block offset is log<sub>2 </sub>4 = 4 bits wide. Note that that gives you four different bit patterns to choose one of the four words within a block: 00, 01, 10, 11. Note also that log<sub>2 </sub>1 = 0, consistent with the idea that if the block size is one word, no bits from the address should be used as a block offset—that is what you see in textbook Figure 8.7. Moving on, let’s let <em>S </em>stand for the number of sets within the cache. Then

number of set bits = log<sub>2 </sub><em>S.</em>

I hope you can see a general pattern here: If <em>X </em>is a power of two, then log<sub>2 </sub><em>X </em>bits are needed to select one of <em>X </em>things.

<strong>Figure 5: </strong>General organization of a direct-mapped cache. Wiring and some logic components have been left out to reduce clutter.

.

.

.

for the whole cache.

Key to colouring of storage cells

status bit(s): 1 valid bit, plus, possibly, another bit to help with writes tag bits

block of data or instruction words

Note: Relative sizes are <em>not to scale</em>. A block might be as large as 64 bytes (512 bits), which is difficult to describe graphically in proportion to a single status bit.

Finally, the tag is everything in an address that hasn’t already been used:

tag width =

address width − number of set bits − block offset width − byte offset width

The <em>capacity </em>of a cache is usually defined as the maximum number of bytes of data or instructions that a cache can hold. Note that that definition <em>excludes </em>storage of status bits and tag bits. Let’s let Bpl (“bytes per line”) stand for the size of a block. (<em>Cache line </em>is a synonym for <em>cache block</em>, and unlike “block”, “line” does not confusingly start with the letter b.) From Figure 5 it should be clear that for a direct-mapped cache

<em>C </em>= <em>S </em>× Bpl<em>,</em>

and if we want to think of block size measured in words instead of bytes,

<em>C </em>= <em>S </em>× words per block × bytes per word<em>.</em>

<h3>Example calculations</h3>

<ol>

 <li><em>Suppose it has been decided that a direct-mapped cache should have 1024 entries, each with one 32-bit data word. How should addresses be split into parts? And what will the capacity of this cache be?</em></li>

</ol>

Byte offset: A 32-bit word is 4 bytes, so the width is log<sub>2 </sub>4 = 2.

Block offset: There is no block offset, because there is only one word per block.

Set bits: <em>S </em>= 1024, so we need log<sub>2 </sub>1024 = 10 set bits.

Tag: The tag is all the bits to the left of the set bits. So addresses should be split this way:

<ul>

 <li>1211 21 0</li>

</ul>

byte offset

Capacity is

word           bytes

<em>C </em>= 1024blocks × 1                 × 4

block           word

= 4096bytes = 4KB<em>.</em>

Remark: This has been a review of the organization of the cache used in Exercise A of this lab.

<ol start="2">

 <li><em>Suppose it has been decided to build a direct-mapped cache with a (very tiny) capacity of 32 bytes, in which each block holds 4 32-bit words. What is S, the number of sets? And how should addresses be split into parts?</em></li>

</ol>

To find <em>S</em>, solve for it in this equation:

32bytes = 25 bytes = <em>S </em>× 22 words × 22 bytes

block              word

That gives

25 bytes                      5−2−2                          1

<em>S </em>== 2                                        blocks = 2 blocks = 2blocks<em>.</em>

22 <u>words</u>block × 22 bytes<sub>word</sub>

(The equation gives <em>S </em>as a number of blocks rather than a number of sets, but that’s fine, because in a direct-mapped cache there is one block per set.)

The address split is: byte offset, log<sub>2 </sub>4 = 2 bits; block offset, log<sub>2 </sub>4 = 2 bits; set bits, log<sub>2 </sub>2 = 1 bit; tag, 32 − 1 − 2 − 2 = 27 bits. Graphically, that’s:

<ul>

 <li>543 21 0</li>

</ul>

<sup>set bit             </sup>byte offset block offset

Remark: This example has been a review of the organization of the cache in textbook Figure 8.12.

<h2>What to Do</h2>

Write well-organized solutions to the following problems.

<ol start="3">

 <li>Suppose the specification for the cache of textbook Figure 8.12 is changed. The block size is now supposed to be 8 words, and the capacity has been increased to a much more practical size of 32KB.

  <ul>

   <li>What is <em>S</em>, the number of sets?</li>

   <li>How should addresses be split into parts? Show this with a diagram like the previously given examples—include bit numbers marking the boundaries between parts.</li>

   <li>The cache will be built using SRAM cells, one SRAM cell for every V-bit, every bit within a tag, and every bit within a block of data or instruction words. How many SRAM cells are needed for the whole cache? Show your work carefully.</li>

  </ul></li>

 <li>The term “64-bit processsor” usually describes a processor in which generalpurpose registers are 64 bits wide, and memory addresses <em>within the processor core and in pointer variables </em>are managed as 64-bit patterns. However, 2<sup>64 </sup>bytes of DRAM is an enormously larger quantity of storage than can practically be connected to a single processor chip, so a typical 64-bit design might use only the least significant 44 bits of an address to access caches and main memory. This is illustrated in Figure 6.</li>

</ol>

Do the following calculations for the computer of Figure 6. We’ll assume direct-mapped design for all three caches, and we’ll consider the word size to be <em>64 bits</em>.

<ul>

 <li>The capacity of the L1 D-cache is 64KB. The block size is 64 <em>bytes</em>. Draw a diagram to show how a 44-bit address input to the cache would be split into these fields: tag, set bits, block offset, and byte offset. Indicate exactly how wide each field is.</li>

 <li>Repeat part (a) for the L2 cache, which has a capacity of 2MB. The block size is again 64 <em>bytes</em>.</li>

 <li>Use your results from (b) to determine how many one-bit SRAM cells are needed for all the V-bits, tags, and data/instruction blocks in the L2 cache.</li>

</ul>

<strong>Figure 6: </strong>Simplifed view of memory organization of a recent single-core 64-bit system. (The major simplification here is the omission of address translation.) The core can fetch two 32-bit instructions at once from from the Level 1 I-cache. The width of the data/instruction bus between the Level 1 and Level 2 caches is unspecified but should be much wider than 64 bits to support speedy transfers of large blocks.

<h1>Exercise C: Simulating a Cache</h1>

<h2>Read This First</h2>

In this exercise you will work with a C program to simulate some aspects of the behaviour of data caches. For two different sequences of memory accesses you will determine which accesses are cache hits and which accesses are cache misses. (This is relatively easy to do; a complete simulation that modeled write-through or writeback to main memory would be a much more complex problem.)

The sequences of memory accesses were generated by determining the data memory accesses that would be made in sorting an array of 3000 integers using two different sort algorithms on a machine similar to a 32-bit MIPS computer. Memory is stored in 32-bit words, and byte addresses are 32-bits in length. All accesses to data memory by the sort procedures are loads and stores of <em>words</em>, at addresses that are multiples of four.

These sequences are available in text files. Here are the first ten lines of one of the files:

r 804e6ac r 804fe1c w 804e6ac r 804e6a8 r 804fe14 r 804fe18 w 804e6a8 w 804fe18 r 804e6a4 r 804fe0c

r means read (load) and w means write (store). The addresses are in hexadecimal notation, even though there is no leading 0x.

Note that the actual data values are not included in the file, just the addresses used to access data. It turns out that to count cache hits and misses, the sequence of addresses used is all that really matters.

<h2>What to Do, Part I</h2>

Download the files from encm369w18lab10/exC. Note that two of the files in the directory are large—if you are close to using up your disk quota (or if the file server is having a bad day) your copy command might fail. To check that the copy was successful, use the Cygwin ls -l command (lower-case L, not number 1), to check the sizes of the large files—they should be

heapsort_trace.txt 1251240 bytes mergesort_trace.txt 1824492 bytes

(The files might get a little bigger if the Web browser downloading them converts them to the Microsoft Windows text file format.)

Read the C source file sim1.c carefully. The program does a simulation of a data cache with 1024 words in 1-word blocks. Build an executable and run it with both data files, following the instructions in a comment near the top of the source file.

Here is some information about two memory access traces:

<ul>

 <li>In txt all data memory accesses are to the array elements. Each of the 3000 elements is read at least once, and is likely to be read and written many more times.</li>

 <li>In txt the data memory accesses are to all of the array elements, to a 1500-word array of temporary storage needed by the mergesort algorithm, and to 72 words of stack used to manage a sequence of recursive function calls. So the total number of different words accessed is 4572.</li>

</ul>

In both cases the 1024-word cache is much too small to hold all of the different data memory words being accessed. If you na¨ıvely guess that access to memory words is truly random, you would expect very high miss rates, such as (3000−1024)<em>/</em>3000 = 65<em>.</em>9% or worse for the heapsort run, and (4572 − 1024)<em>/</em>4572 = 77<em>.</em>6% or worse for the mergesort run. However, you should see much lower miss rates due to <em>locality of reference </em>in the memory accesses.

<h2>What to Do, Part II</h2>

Let’s examine the effect of changing the block size of the cache of Part I, while maintaining capacity.

Make a copy of sim1.c called sim2.c, and edit it to simulate a direct-mapped cache with 256 four-word blocks. You will not have to edit many lines of the C code, but to do it correctly you will have to do some calculations like the ones in Exercise B, then think carefully about how to isolate the correct set and tag bits.

Run the program using the two given input files. Copy and paste records of your programs runs into a file and print that file along with your source file sim2.c. Also, answer this question:

Compare results obtained in this part with results from Part I. Do they suggest that there is significant <em>spatial </em>locality of reference in the memory accesses done by the heapsort and mergesort algorithms? Give a brief explanation.

<h2>What to Do, Part III</h2>

Now let’s consider a direct-mapped cache with the same 4KB capacity as in Part II, but with the block size quadrupled to sixteen words.

Make another copy of sim1.c; call this one sim3.c. Edit it to simulate a directmapped cache with the appropriate number of sixteen-word blocks.

Run the program using the two given input files. Copy and paste records of your programs runs into a file and print that file along with your source file sim3.c.

<h2>Final Note</h2>

<em>Cache-friendliness </em>(a tendency towards low miss rates) is an important factor in performance of algorithms on modern computer hardware.

But don’t use this exercise to draw any firm conclusions about which of the two sort algorithms is more cache-friendly. (My own suspicion is that mergesort may often be significantly more cache-friendly than heapsort.) The caches being simulated are unrealistically small, and using one run of each algorithm for a single array hardly constitutes enough input data for a good experiment.

Researchers doing simulation experiments to compare cache designs will use traces of trillions of memory accesses from many different programs in order to ensure that performance is being measured for many different patterns of memory access.

<h2>What to Hand In</h2>

Hand in the printouts from Parts II and III, and your answer to the question in Part II. Please label the printouts clearly so your TA’s don’t have to guess which printout is from which part.