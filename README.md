Download Link: https://assignmentchef.com/product/solved-comp5112-assignment-3-cuda-version-of-the-smith-waterman-algorithm
<br>
The Smith-Waterman algorithm identifies the similar regions in two genome sequences. In this assignment, you will implement a CUDA version of the Smith-Waterman algorithm to measure the similarity between two strings.

The pseudocode of the Smith-Waterman algorithm is shown in Algorithm 1. Given string <em>A </em>= <em>a</em><sub>1</sub><em>,a</em><sub>2</sub><em>,…,a<sub>n </sub></em>and string <em>B </em>= <em>b</em><sub>1</sub><em>,b</em><sub>2</sub><em>,…,b<sub>m</sub></em>, we first construct a scoring matrix <em>H </em>of size (<em>n </em>+ 1) ∗ (<em>m</em>+1) and set the first row and column to zero. Then, we iteratively compute the scoring matrix using the following dynamic programming formula:

<table width="0">

 <tbody>

  <tr>

   <td width="218"><sup> </sup><em>H<sub>i</sub></em>−1<em>,j</em>−1 + <em>s</em>(<em>a<sub>i</sub>,b<sub>j</sub></em>) <sup> </sup><em>H<sub>i</sub></em>−1<em>,j </em>− <em>w</em><em>H<sub>ij </sub></em>= max<em>H</em><em>i,j</em>−1 − <em>w</em> 0</td>

   <td width="131">(1 ≤ <em>i </em>≤ <em>n,</em>1 ≤ <em>j </em>≤ <em>m</em>)</td>

  </tr>

 </tbody>

</table>

where <em>s </em>is the substitution matrix is the match score, <em>v </em>is the

mismatch score, and <em>w </em>is the gap penalty. The value of <em>u</em>, <em>v </em>and <em>w </em>are constant and are given as part of the input to the algorithm. Finally, we return the highest score in the scoring matrix as the similarity score between <em>A </em>and <em>B</em>.

<h1>Input and Output</h1>

The input file will be in the following format:

<ol>

 <li>The first line contains two integers <em>a</em>_<em>len </em>and <em>b</em>_<em>len </em>(1 ≤ <em>a</em>_<em>len </em>≤ 20000<em>,</em>1 ≤ <em>b</em>_<em>len </em>≤ 20000), separated by a space. They represent the length of string <em>a </em>and <em>b</em>, respectively.</li>

 <li>The second line is a string <em>a </em>of length <em>a</em>_<em>len</em>, consisting of four letters <em>A,T,G,C</em>.</li>

 <li>The third line is a string <em>b </em>of length <em>b</em>_<em>len</em>, consisting of four letters <em>A,T,G,C</em>.</li>

</ol>

Assignment 3                                                                                                                      COMP5112, 2020 Spring

Algorithm 1: The Smith-Waterman Algorithm

Input : string <em>A </em>= <em>a</em><sub>1</sub><em>,a</em><sub>2</sub><em>,…,a<sub>n </sub></em>and <em>B </em>= <em>b</em><sub>1</sub><em>,b</em><sub>2</sub><em>,…,b<sub>m</sub></em>, match score <em>u</em>, mismatch score <em>v</em>, gap penalty <em>w</em>

Output: the similarity score between <em>A </em>and <em>B</em>

<ul>

 <li>int <em>score</em>[|<em>A</em>| + 1][|<em>B</em>| + 1];</li>

 <li>for <em>i </em>← 0 to |<em>A</em>| do</li>

</ul>

3<em>score</em>[<em>i</em>][0] ← 0;

<ul>

 <li>end</li>

 <li>for <em>i </em>← 0 to |<em>B</em>| do</li>

</ul>

6<em>score</em>[0][<em>i</em>] ← 0;

<ul>

 <li>end</li>

 <li>int <em>max</em>_<em>score </em>← 0;</li>

 <li>for <em>i </em>← 1 to |<em>A</em>| do</li>

 <li>for <em>j </em>← 1 to |<em>B</em>| do</li>

</ul>

11<em>score</em>[<em>i</em>][<em>j</em>] ← max(0<em>,</em>

12<em>score</em>[<em>i </em>− 1][<em>j</em>] − <em>w,</em>

13<em>score</em>[<em>i</em>][<em>j </em>− 1] − <em>w,</em>

14<em>score</em>[<em>i </em>− 1][<em>j </em>− 1] + <em>sub</em>_<em>mat</em>(<em>a<sub>i</sub>,b<sub>j</sub></em>));

15<em>max</em>_<em>score </em>← max(<em>max</em>_<em>score,score</em>[<em>i</em>][<em>j</em>]);

<ul>

 <li>end</li>

 <li>end</li>

</ul>

The output of the program consists of three lines:

<ol>

 <li>The similarity score between <em>a </em>and <em>b</em>, i.e., the highest score in the scoring matrix.</li>

 <li>The elapsed time in seconds of the execution.</li>

 <li>The driver time in seconds of the execution.0</li>

</ol>

We assume that the match score is 3, the mismatch score is -3, and the gap penalty is 2.

Here is an example input/output for your reference:

Input:

9 8

GGTTGACTA TGTTACGG

Output:

Max socre: 13

Elapsed time: 0.00001 s

Driver time: 0.0000095 s