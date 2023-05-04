Download Link: https://assignmentchef.com/product/solved-cs6500-network-security-assignment-1-cryptanalysis-of-rc4-encryption-algorithm
<br>
The objective of this assignment is to do some simple cryptanalysis of the RC4 encryption algorithm. RC4 is a stream cipher, internally generating a stream of random bits which is then <strong>XOR-ed </strong>with the <strong>plaintext</strong>. The secret key initializes the random number generator. However, on observation there appears to be a weakness in RC4. Perhaps two keys that are very similar will result in similar random numbers coming out of RC4. In this assignment you will implement RC4, make some differential measurements of randomness for related keys, and you will graph your results. For details about RC4 you can refer <a href="https://en.wikipedia.org/wiki/RC4">wiki RC4</a><a href="https://en.wikipedia.org/wiki/RC4">.</a>

CreditsCourtesy –

<a href="https://www.cs.rice.edu/~dwallach/courses/comp527_s99/ass4.html">https://www.cs.rice.edu/ dwallach/courses/comp527</a> <a href="https://www.cs.rice.edu/~dwallach/courses/comp527_s99/ass4.html">s99/ass4.html</a>

<h2>1       Assignment Details</h2>

<h3>1.1     The Basics</h3>

You are going to first implement the RC4 algorithm. You can find some code at the RC4 in three lines of <a href="https://pi4.informatik.uni-mannheim.de/pi4.data/content/projects/cryptography/rgp/rc4/rc4c.html">Perl </a><a href="https://pi4.informatik.uni-mannheim.de/pi4.data/content/projects/cryptography/rgp/rc4/rc4c.html">site</a> (which also includes a full, readable C version). This assignment is a form of related-key cryptanalysis. With a stream cipher like RC4, it should be the case that, if you toggle exactly one bit in the key, 50% of output bits should toggle. If you look closely at the key setup, it doesn’t look like this is the case. It appears that single-bit differences in the key will result in fairly small differences in the internal state of RC4. After a sufficient amount of output, this small change will eventually propagate and then you would expect 50% of the output bits to toggle.

<h3>1.2      Implement the cipher</h3>

Don’t worry about XOR-ing the output bits with a message you’re going to keep secret. We’re only going to study the random bits. Make sure you can accept keys of length up to 2048 bits.

<h3>1.3        Capture the output bits from two runs and XOR them</h3>

Generate a random key of 2048 bits (Unix’s <strong>random(3C) </strong>is good enough for now). Collect some output from RC4. Toggle one or more of the key bits. Reinitialize RC4 and collect the output again. XOR them together. This gives you the <strong>difference </strong>of the two streams. If RC4 were ”perfect”, this difference stream would be ”perfectly” random.

<h3>1.4        Analyze the differential output bits for randomness</h3>

There are many tests for randomness of numbers. You’re going to implement a simple frequency counting test. Create an array of counters of length equal to a power of two (say, 256). Now, say the test data is a sequence of bits (<em>b</em><sub>0</sub><em>,b</em><sub>1</sub><em>,b</em><sub>2</sub><em>,b</em><sub>3</sub><em>…b<sub>N</sub></em>). You can look at each sequence of 8 bits (<em>b</em><sub>0</sub><em>,b</em><sub>1</sub><em>,b</em><sub>2</sub><em>,b</em><sub>3</sub><em>…b</em><sub>9</sub>) as a number and increment the appropriate counter in the array. When you’re done you would expect that the counters would be approximately equal. If the two original bit streams were very similar, you would expect the counters for lots of zeros to have higher values than the counters for lots of ones.

You can compute a numerical measure of the randomness like so:

<ul>

 <li>N = number of samples.</li>

 <li>C = number of counters.</li>

 <li>D = standard deviation of counter values.</li>

 <li>R =(<em>D </em>∗ <em>C</em>)/N;</li>

</ul>

The closer the randomness (<em>R</em>) is to zero, the more random the data. You might consider using different numbers of counters and see if your randomness measure changes very much

<h3>1.5        Run this randomness test lots of times and collect the results</h3>

Measure the randomness on outputs ranging from short through long (i.e., 2 bytes, 4 bytes, 8 bytes, 32 bytes, 128 bytes, 1024 bytes). For each of these, you need to consider the effect of toggling one bit in the key, two bits in the key, and so forth through 32 bits. For each of these pairs, you should make at least 20 measurements of the randomness and average the results. Your results will be more accurate if you make several thousand measurements for each pair.

<h3>1.6     Graph the results</h3>

You should produce a graph with one line for each output length. The Y axis is the randomness (higher values imply less randomness). The X axis is the number of bits you toggled. You would expect each line to start somewhere above zero and, as you toggle more bits, approach zero quickly. You would also expect to see higher values for the lines corresponding to shorter runs of data.

You can either use Unix tools like gnuplot or a spreadsheet like Excel to generate your graph.

<h2>2      What to Submit</h2>

Create a tar-gz file with name: Assignment1-RollNo1.tgz (e.g. Assignment1-CS17B099.tgz) that will contain a directory named Assignment1-RollNo1 with all relevant files.

The directory should contain the following files:

<ul>

 <li>Source Files</li>

 <li>A Makefile which generates all your executables</li>

 <li>A technical REPORT (in PDF format) with help of screen shots showing the working of your implementation (Graphs). Report your observations and analyze the results, in 1-2 paragraphs. The report should include your name, roll number, assignments.</li>

</ul>

Also, give a brief summary as to what you learnt in this experiment and how much beneficial you feel the experiment was.

<ul>

 <li>a README file containing instructions to compile, run and test your program. README file should be written such that a TA must be able to run your code without your presence/help.</li>

</ul>