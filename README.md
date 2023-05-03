Download Link: https://assignmentchef.com/product/solved-cpsc418-math318-introduction-to-cryptography-assignment-3
<br>
<h1><strong style="font-size: 16px;">Problem 1 </strong><span style="font-size: 16px;">— Flawed MAC designs, 13 marks</span></h1>

<h1>Written Problems for CPSC 418 and MATH 318</h1>

For this problem, you need to carefully trace through the given MAC algorithms to understand the given attacks and explain how computation resistance is defeated.

Recall that iterated hash functions employ a <em>compression function f </em>in multiple rounds; SHA-1 is an example of such a hash function. Here, <em>f </em>takes as input pairs of <em>n</em>-bit blocks and outputs <em>n</em>-bit blocks, for some <em>n </em>∈ N. The compression function <em>f </em>is assumed to be public, i.e. anyone can compute values of <em>f</em>. As a result, the hash function is also public, so any one can compute hash values. For simplicity, we assume that the bit length of any message to be hashed is a multiple of <em>n</em>, i.e. messages have been padded appropriately prior to hashing. Then the input to an iterated hash function is a message <em>M </em>consisting of <em>L </em>blocks <em>P</em><sub>1</sub><em>,P</em><sub>2</sub><em>,…,P<sub>L</sub></em>, each of length <em>n</em>. An algorithmic description of an <em>n</em>-bit iterated hash function is given as follows (as usual. “k” denotes concatenation of strings).

<strong>Algorithm </strong>ItHash

Input: A message <em>M </em>= <em>P</em><sub>1</sub>k<em>P</em><sub>2</sub>k···k<em>P<sub>L</sub></em>

Output: An <em>n</em>-bit hash of <em>M</em>

1: Initialize <em>H </em>:= 0<em><sup>n </sup></em>(<em>n </em>zeros)

2: for <em>i </em>= 1 to <em>L </em>do

3:               <em>H </em>:= <em>f</em>(<em>H,P<sub>i</sub></em>)

4: end for

5: Output <em>H</em>

The following attacks show that the two “obvious” designs for using an iterated hash function as the basis for a MAC — prepending or appending the key to the message and then hashing — are not computation resistant. These attacks were informally discussed in class by Randy on March 4; in this question, you are asked to present a formal argument for the defeat of computation resistance. For simplicity, assume that keys also have length<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> <em>n</em>.

<ul>

 <li>(5 marks) Define a message authentication function PHMAC (“Prepend Hash MAC”) via PHMAC<em><sub>K</sub></em>(<em>M</em>) := ItHash(<em>K</em>k<em>M</em>) = ItHash(<em>K</em>k<em>P</em><sub>1</sub>k<em>P</em><sub>2</sub>k···k<em>P<sub>L</sub></em>)</li>

</ul>

for any message <em>M </em>= <em>P</em><sub>1</sub>k<em>P</em><sub>2</sub>k···k<em>P<sub>L</sub></em>.

Suppose an attacker knows a message/PHMAC pair (<em>M</em><sub>1</sub><em>,</em>PHMAC<em><sub>K</sub></em>(<em>M</em><sub>1</sub>)).            Let <em>X </em>be an arbitrary <em>n</em>-bit block and put <em>M</em><sub>2 </sub>= <em>M</em><sub>1</sub>k<em>X</em>.             Show how an attacker can compute PHMAC<em><sub>K</sub></em>(<em>M</em><sub>2</sub>) without knowledge of <em>K</em>, thereby defeating computation resistance for PHMAC.

<em>Hint: </em>Suppose <em>M</em><sub>1 </sub>consists of <em>L </em>blocks. Tracing through the ItHash algorithm, compare the outputs of the first <em>L </em>+ 1 rounds of PHMAC<em><sub>K</sub></em>(<em>M</em><sub>1</sub>) and PHMAC<em><sub>K</sub></em>(<em>M</em><sub>2</sub>).

<ul>

 <li>(8 marks) Define a message authentication function AHMAC<em><sub>K </sub></em>(“Append Hash MAC”) via</li>

</ul>

AHMAC<em><sub>K</sub></em>(<em>M</em>) := ItHash(<em>M</em>k<em>K</em>) = ItHash(<em>P</em><sub>1</sub>k<em>P</em><sub>2</sub>k···k<em>P<sub>L</sub></em>k<em>K</em>)

for any message <em>M </em>= <em>P</em><sub>1</sub>k<em>P</em><sub>2</sub>k···k<em>P<sub>L</sub></em>.

Assume that ItHash is not weakly collision resistant, and suppose an attacker knows a message/AHMAC pair (<em>M</em><sub>1</sub><em>,</em>AHMAC<em><sub>K</sub></em>(<em>M</em><sub>1</sub>)). Show how she can find (without knowledge of <em>K</em>) a second message/AHMAC pair (<em>M</em><sub>2</sub><em>,</em>AHMAC<em><sub>K</sub></em>(<em>M</em><sub>2</sub>)), thereby defeating computation resistance.

<em>Hint: </em>Note that on input any <em>L</em>-bit message, the first <em>L </em>rounds of the computation of AHMAC<em><sub>K</sub></em>(<em>M</em>) do not depend on <em>K</em>, just on <em>M</em>.

<strong>Problem 2 </strong>— Fast RSA decryption using Chinese remaindering, 8 marks)

In this problem, as usual, a user Alice has an RSA public key (<em>e,n</em>) with corresponding private key <em>d</em>. Here, <em>n </em>= <em>pq </em>for distinct large primes <em>p </em>and <em>q</em>.

If Alice does not discard <em>p </em>and <em>q </em>after computing <em>n </em>and <em>φ</em>(<em>n</em>), she can employ an alternative decryption procedure as described below (based on the <em>Chinese Remainder Theorem </em>which some of you may have seen before). For a given ciphertext <em>C </em>(1 ≤ <em>C </em>≤ <em>n </em>− 1<em>,</em>gcd(<em>C,n</em>) = 1), she proceeds as follows:

Step 1. Compute

<table width="389">

 <tbody>

  <tr>

   <td width="149"><em>d<sub>p</sub></em></td>

   <td width="25">≡</td>

   <td width="107"><em>d </em>(mod <em>p </em>− 1)<em>,</em></td>

   <td width="108">0 ≤ <em>d<sub>p </sub></em>≤ <em>p </em>− 2 <em>,</em></td>

  </tr>

  <tr>

   <td width="149"><em>d<sub>q</sub></em>Step 2. Compute</td>

   <td width="25">≡</td>

   <td width="107"><em>d </em>(mod <em>q </em>− 1)<em>,</em></td>

   <td width="108">0 ≤ <em>d<sub>q </sub></em>≤ <em>q </em>− 2<em>.</em></td>

  </tr>

  <tr>

   <td width="149"><em>M<sub>p</sub></em></td>

   <td width="25">≡</td>

   <td width="107"><em>C<sup>d</sup></em><em><sup>p </sup></em>(mod <em>p</em>)<em>,</em></td>

   <td width="108">1 ≤ <em>M<sub>p </sub></em>≤ <em>p </em>− 1 <em>,</em></td>

  </tr>

  <tr>

   <td width="149"><em>M<sub>q</sub></em></td>

   <td width="25">≡</td>

   <td width="107"><em>C<sup>d</sup></em><em><sup>q </sup></em>(mod <em>q</em>)<em>,</em></td>

   <td width="108">1 ≤ <em>M<sub>q </sub></em>≤ <em>q </em>− 1 <em>.</em></td>

  </tr>

 </tbody>

</table>

Step 3. Use the Extended Euclidean Algorithm to find integers <em>x</em>, <em>y </em>such that

<em>px </em>+ <em>qy </em>= 1 <em>.</em>

(Such integers exist because gcd(<em>p,q</em>) = 1.)

Step 4. Set <em>M </em>≡ <em>pxM<sub>q </sub></em>+ <em>qyM<sub>p </sub></em>(mod <em>n</em>), 0 ≤ <em>M </em>≤ <em>n </em>− 1.

Prove that if the above procedure decrypts correctly. That is, if <em>C </em>≡ <em>M<sup>e </sup></em>(mod <em>n</em>) is a ciphertext obtained by encrypting a message <em>M </em>the “normal” RSA way, and <em>M</em><sup>0 </sup>is the result of applying the procedure above to <em>C</em>, prove that <em>M</em><sup>0 </sup>= <em>M</em>.

<em>Remark: </em>It can be shown that this method is generally twice as fast as ordinary RSA decryption since it performs arithmetic with respect to moduli of half-size. So this is what is generally used in practice.

<strong>Problem 3 </strong>— RSA primes too close together, 18 marks)

This problem explores a <em>difference of squares </em>approach to factoring an RSA modulus due to Fermat, and hence also known as <em>Fermat factorization</em>. Fermat’s idea was to attempt to find a representation of an integer <em>n </em>as a difference of squares <em>n </em>= <em>x</em><sup>2 </sup>−<em>y</em><sup>2 </sup>where 0 <em>&lt; y &lt; x &lt; n</em>, which would lead to a factorization <em>n </em>= (<em>x</em>+<em>y</em>)(<em>x</em>−<em>y</em>). Of course if <em>x</em>+<em>y </em>= <em>n </em>and <em>x</em>−<em>y </em>= 1, then this doesn’t help. But if <em>n </em>= <em>pq </em>is an RSA modulus for example, the hope is that

<em>x </em>+ <em>y </em>= <em>p ,              x </em>− <em>y </em>= <em>q</em>

or vice versa; in which case

<em> .</em>

When <em>p </em>and <em>q </em>are close together, the quantity <em>y </em>is very small compared to <em>x </em>and we will see that this represents a serious attack on RSA.

Let <em>n </em>= <em>pq </em>with odd primes <em>p</em>, <em>q</em>, and assume without loss of generality that <em>p &gt; q </em>(so <em>y &gt; </em>0). In

√

this problem, all square roots are assumed to be positive, i.e. when we write <em>z </em>for some <em>z &gt; </em>0, we mean the positive square root of <em>z</em>.

√

<ul>

 <li>(3 marks) Prove that <em>p &gt; x &gt; n</em>.</li>

 <li>(8 marks) Consider the following algorithm:</li>

</ul>

<strong>Algorithm </strong>Fermat Factorization Input: <em>n </em>= <em>pq </em>with <em>p &gt; q</em>

Output: <em>q</em>

1: Putrounded up to the nearest integer)

2: <em>b </em>:=        <em>a</em><sup>2 </sup>− <em>n</em>

3: while <em>b </em>is not an integer do√

4:              <em>a </em>:= <em>a </em>+ 1; <em>b </em>:=         <em>a</em><sup>2 </sup>− <em>n</em>

5: end while 6: Output <em>a </em>− <em>b</em>.

Prove that this algorithm terminates when <em>a </em>= <em>x </em>and outputs <em>q</em>. Note that there are three items to show here:

<ul>

 <li>The “while” clause is satisfied when <em>a </em>= <em>x</em>;</li>

 <li>The algorithm does not terminate sooner, i.e. it does not terminate for any value <em>a &lt; x</em>;</li>

 <li>When the algorithm terminates with <em>a </em>= <em>x</em>, it outputs <em>q</em>.</li>

</ul>

√

<ul>

 <li>(2 marks) Show that the number of loop iterations executed by the algorithm is <em>x</em>−d <em>n</em>e+1.</li>

 <li>(3 marks) Prove that.</li>

</ul>

√            √

(<em>Hint: </em>Consider (<em>x </em>−        <em>n</em>)(<em>x </em>+      <em>n</em>).)

√

<ul>

 <li>(2 marks) Finally, the coup-de-grˆace. Suppose <em>p </em>− <em>q &lt; </em>2<em>B </em><sup>4 </sup><em>n </em>for some integer <em>B </em>that is very small compared to <em>n</em>; e.g. <em>B </em>could be on the order of a power of log<sub>2</sub>(<em>n</em>). In other words, <em>p </em>and <em>q </em>are very close together; they agree in nearly half of their most significant bits. Prove that the above algorithm factors <em>n </em>after at most</li>

</ul>

loop iterations.

<strong>Problem 4 </strong>– The El Gamal public key cryptosystem is not semantically secure, 12 marks

This problems requires typesetting Legendre symbols. To facilitate this, include at the beginning of your assignment file, right after the line documentclass{assignment} the two lines

usepackage{amsmath}

providecommand{Leg}[2]{genfrac{(}{)}{}{}{#1}{#2}}

Be sure that you copy these <em>verbatim</em>; the easiest is to copy and paste them right from this PDF file. The assignment template provided on the course website already includes these lines. The command $Leg{a}{n}$ will produce the typeset output , which is much easier than producing a fraction with large parentheses around it.

Recall that for the El Gamal public key cryptosystem, a user Alice produces her public and private keys as follows:

Step 1. Selects a large prime <em>p </em>and a primitive root <em>g </em>of <em>p</em>.

Step 2. Randomly selects <em>x </em>such that 0 <em>&lt; x &lt; p </em>− 1 and computes <em>y </em>≡ <em>g<sup>x </sup></em>(mod <em>p</em>)<em>.</em>

Alice’s public key: {<em>p,g,y</em>}

Alice’s private key: {<em>x</em>}

To encrypt a message  intended for Alice, Bob selects a random integer <em>k </em>∈ Z<em>p</em><sub>−1</sub>, computes <em>C</em><sub>1 </sub>≡ <em>g<sup>k </sup></em>(mod <em>p</em>) and <em>C</em><sub>2 </sub>≡ <em>My<sup>k </sup></em>(mod <em>p</em>), and sends <em>C </em>= (<em>C</em><sub>1</sub><em>,C</em><sub>2</sub>) to Alice. Alice decrypts the ciphertext <em>C </em>= (<em>C</em><sub>1</sub><em>,C</em><sub>2</sub>) by computing

In this problem, you will prove that the El Gamal PKC is not polynomially secure, and hence not semantically secure. This is because an attacker Mallory can distinguish messages according to whether they are quadratic residues or quadratic nonresidues modulo <em>p</em>.

Mallory mounts her attack with the following procedure:

Step 1. Selects two messages <em>M</em><sub>1 </sub>and <em>M</em><sub>2 </sub>such that <em>M</em><sub>1 </sub>∈ <em>QR<sub>p </sub></em>and <em>M</em><sub>2 </sub>∈ <em>QN<sub>p</sub></em>, and obtains ciphertext <em>C </em>= (<em>C</em><sub>1</sub><em>,C</em><sub>2</sub>) = <em>E</em>(<em>M<sub>i</sub></em>) where <em>i </em>= 1 or 2

(Mallory’s task is precisely to ascertain whether <em>i </em>= 1 or <em>i </em>= 2).

Step 2. Computes the Legendre symbols  and .

Step 3. If     = 1 and         = 1, she asserts that <em>C </em>= <em>E</em>(<em>M</em><sub>1</sub>).

If    = 1 and         1, she asserts that <em>C </em>= <em>E</em>(<em>M</em><sub>2</sub>).

If    = 1 and         = 1, she asserts that <em>C </em>= <em>E</em>(<em>M</em><sub>1</sub>).

If    = 1 and        1, she asserts that = <em>E</em>(<em>M</em><sub>2</sub>).

If    1 and        = 1, she asserts that <em>C </em>= <em>E</em>(<em>M</em><sub>2</sub>).

If    1 and        1, she asserts that <em>C </em>= <em>E</em>(<em>M</em><sub>1</sub>).

Note that this procedure requires three Legendre symbol computations — which can be done with modular exponentiation by Euler’s Criterion — and hence always takes polynomial time. Note also that Mallory states her assertions with certainty, i.e. probability 1.

Prove that Mallory’s assertions are correct, so the El Gamal system is not semantically secure.

<strong>Problem 5 </strong>— An IND-CPA, but not IND-CCA secure version of RSA, 12 marks Consider the following semantically secure variant of the RSA public key cryptosystem:

Parameters:

<ul>

 <li><em>m </em>— length of plaintext messages to encrypt (in bits)</li>

 <li>(<em>n,e</em>) — Alice’s RSA public key (<em>n </em>has <em>k </em>bits)</li>

 <li><em>d </em>— Alice’s RSA private key</li>

 <li><em>H </em>: {0<em>,</em>1}<em><sup>k </sup></em>7→ {0<em>,</em>1}<em><sup>m </sup></em>a public random function Encryption of an <em>m</em>-bit message <em>M</em>:</li>

</ul>

Step 1. Generate a random <em>k</em>-bit number <em>r &lt; n.</em>

Step 2. Compute <em>C </em>= (<em>s</em>k<em>t</em>) where <em>s </em>≡ <em>r<sup>e </sup></em>(mod <em>n</em>) and <em>t </em>= <em>H</em>(<em>r</em>) ⊕ <em>M.</em>

Decryption of ciphertext <em>C</em>:

Compute <em>M </em>≡ <em>H</em>(<em>s<sup>d </sup></em>(mod <em>n</em>)) ⊕ <em>t.</em>

Prove that this cryptosystem is not IND-CCA secure.

<em>Hint</em>: To mount her CCA, Mallory gets to choose two plaintexts and submit one ciphertext for encryption. Almost any two plaintexts <em>M</em><sub>1</sub>, <em>M</em><sub>2 </sub>will do. Let

<em>C </em>= (<em>s</em>k<em>t</em>) = (<em>r<sup>e </sup></em>(mod <em>n</em>) k <em>H</em>(<em>r</em>) ⊕ <em>M<sub>i</sub></em>)           where <em>i </em>= 1 or 2

be the encryption of one them; Mallory needs to ascertain whether <em>i </em>= 1 or <em>i </em>= 2. Mallory now chooses as her ciphertext <em>C</em><sup>0 </sup>= (<em>s</em>k<em>t</em>⊕<em>M</em><sub>1</sub>) and obtains its decryption (be sure to chose <em>M</em><sub>1 </sub>such that <em>C</em><sup>0 </sup>6= <em>C</em>; that’s the only restriction on the plaintexts). Prove that Mallory can with <em>certainty </em>(i.e. probability 1) and in polynomial time detect whether <em>C </em>is an encryption of <em>M</em><sub>1 </sub>or <em>M</em><sub>2</sub>.

<h1>Written Problems for MATH 318 only</h1>

<strong>Problem 6 </strong>— An attack on RSA with small decryption exponent, 25 marks This problem explores an attack on RSA with small <em>d </em>due to Wiener.

<strong>Preliminaries. </strong>Let <em>r </em>be a positive rational number and write <em>r </em>= <em>a/b </em>with <em>a,b </em>∈ N. Let <em>q</em><sub>0</sub><em>,q</em><sub>1</sub><em>,…q<sub>m </sub></em>∈ N be the sequence of quotients produced by applying the Euclidean Algorithm to the numerator and denominator of <em>r</em>:

<em>a  </em>= <em>q</em><sub>0</sub><em>b </em>+ <em>r</em><sub>0 </sub><em>,          </em>0 <em>&lt; r</em><sub>0 </sub><em>&lt; b, b      </em>= <em>q</em><sub>1</sub><em>r</em><sub>0 </sub>+ <em>r</em><sub>1 </sub><em>,          </em>0 <em>&lt; r</em><sub>1 </sub><em>&lt; r</em><sub>0 </sub><em>, r</em><sub>0        </sub>= <em>q</em><sub>2</sub><em>r</em><sub>1 </sub>+ <em>r</em><sub>2 </sub><em>,          </em>0 <em>&lt; r</em><sub>2 </sub><em>&lt; r</em><sub>1 </sub><em>,</em>

…

<em>r</em><em>m</em>−3     = <em>q</em><em>m</em>−1<em>r</em><em>m</em>−2 + <em>r</em><em>m</em>−1 <em>,          r</em><em>m</em>−1 = gcd(<em>a,b</em>)<em>, r</em><em>m</em>−2     = <em>q</em><em>mr</em><em>m</em>−1 + <em>r</em><em>m ,   r</em><em>m </em>= 0<em>.</em>

Recall the familiar sequences

<em>A</em>−<sub>2            </sub>=             0<em>,            A</em>−<sub>1            </sub>=             1<em>,            A<sub>i               </sub></em>= <em>q<sub>i</sub>A<sub>i</sub></em>−<sub>1 </sub>+ <em>A<sub>i</sub></em>−<sub>2            </sub>for 0 ≤ <em>i </em>≤ <em>m, B</em>−<sub>2                  </sub>=             1<em>,            B</em>−<sub>1 </sub>=             0<em>,            B<sub>i               </sub></em>=             <em>q<sub>i</sub>B<sub>i</sub></em>−<sub>1 </sub>+ <em>B<sub>i</sub></em>−<sub>2           </sub>for 0 ≤ <em>i </em>≤ <em>m.</em>

The quotients <em>A<sub>i</sub>/B<sub>i </sub></em>(0 ≤ <em>i </em>≤ <em>m</em>) are called the <em>convergents </em>of <em>r </em>because they oscillate around and converge toward <em>r</em>, with <em>A<sub>m </sub></em>= <em>a</em>, <em>B<sub>m </sub></em>= <em>b</em>, and hence <em>A<sub>m</sub>/B<sub>m </sub></em>= <em>r</em>. In fact, the following theorem (which you may use without proof) asserts that any rational number sufficiently close to <em>r </em>must occur as one of the convergents:

Now back to RSA. Let <em>n </em>= <em>pq </em>where <em>p,q </em>are odd primes satisfying <em>q &lt; p &lt; </em>2<em>q </em>(these inequalities are reasonable as <em>p </em>and <em>q </em>are usually assumed to have the same bit size). Let <em>e,d </em>be integers with 1 <em>&lt; e,d &lt; φ</em>(<em>n</em>) and <em>ed </em>≡ 1 (mod <em>φ</em>(<em>n</em>)). Let <em>k </em>∈ Z satisfy <em>ed </em>= 1 + <em>kφ</em>(<em>n</em>) and suppose that <em>d </em>is small compared to <em>n</em>; specifically,

<em>.</em>

<ul>

 <li>(5 marks) Prove that 1 ≤ <em>k &lt; d </em>and gcd(<em>d,k</em>) = 1.</li>

</ul>

√

<ul>

 <li>(3 marks) Prove that 2 ≤ <em>n </em>− <em>φ</em>(<em>n</em>) <em>&lt; </em>3 <em>n</em>.</li>

</ul>

√

<ul>

 <li>(4 marks) Use parts (a) and (b) to prove that 0 <em>&lt; kn </em>− <em>ed &lt; </em>3<em>d n</em>.</li>

 <li>(4 marks) Conclude from part (c) that 0 .</li>

 <li>(3 marks) Let <em>q</em><sub>0</sub><em>,q</em><sub>1</sub><em>,…,q<sub>m </sub></em>be the quotients obtained when applying the Euclidean algorithm to <em>e </em>and <em>n</em>, and let <em>A<sub>i</sub>,B<sub>i </sub></em>be the associated sequences as defined above. Use the theorem from above to prove that <em>k </em>= <em>A<sub>i </sub></em>and <em>d </em>= <em>B<sub>i </sub></em>for some <em>i </em>∈ {1<em>,</em>2<em>,…,m</em>}.</li>

</ul>

(Note that <em>i </em>= 0 is impossible here even though the theorem allows it in principle. This is because <em>e &lt; n </em>forces <em>q</em><sub>0 </sub>= 0, so <em>A</em><sub>0 </sub>= 0 and <em>B</em><sub>0 </sub>= 1. Since <em>k &gt; </em>0 by part (a), we cannot have <em>k/d </em>= <em>A</em><sub>0</sub><em>/B</em><sub>0</sub>.)

<ul>

 <li>(6 marks) Use part (e) to devise a procedure for finding <em>d </em>and factoring <em>n </em> Explain why your procedure works and why it is efficient, i.e. argue that the number of computation steps performed by your procedure is small.</li>

</ul>

<strong>Problem 7 </strong>— Universal forgery attack on the El Gamal signature scheme, 12 marks)

Recall that for the El Gamal signature scheme, a user Alice produces her public and private keys as follows:

Step 1. Selects a large prime <em>p </em>and a primitive root <em>g </em>of <em>p</em>.

Step 2. Randomly selects <em>x </em>such that 0 <em>&lt; x &lt; p </em>− 1 and computes <em>y </em>≡ <em>g<sup>x </sup></em>(mod <em>p</em>)<em>.</em>

Alice’s public key: {<em>p,g,y</em>}

Alice’s private key: {<em>x</em>}

Alice also fixes a public cryptographic hash function <em>H </em>: {0<em>,</em>1}<sup>∗ </sup>7→ Z<em>p</em><sub>−1</sub>.

Alice signs a message <em>M </em>∈ {0<em>,</em>1}<sup>∗ </sup>intended for Bob as follows:

Step 1. Selects a random integer.

Step 2. Computes <em>r </em>≡ <em>g<sup>k </sup></em>(mod <em>p</em>), 0 ≤ <em>r &lt; p</em>.

Step 3. Solves.

Step 4. Signs the message <em>M </em>with the pair (<em>r,s</em>)<em>.</em>

Bob verifies Alice’s signature (<em>r,s</em>) to the message <em>M </em>as follows:

Step 1. Obtains Alice’s authentic public key {<em>p,g,y</em>}<em>.</em>

Step 2. Verifies that 1 ≤ <em>r &lt; p</em>; if not, reject.

Step 3. Computes <em>v</em><sub>1 </sub>≡ <em>y<sup>r</sup>r<sup>s </sup></em>(mod <em>p</em>) and <em>v</em><sub>2 </sub>≡ <em>g<sup>H</sup></em><sup>(<em>M</em>k<em>r</em>) </sup>(mod <em>p</em>).

Step 4. Accepts the signature if and only if <em>v</em><sub>1 </sub>= <em>v</em><sub>2</sub><em>.</em>

The following is a universal forgery attack against a variant of this scheme that hashes only the message <em>M</em>, but does not include the random number <em>r </em>in the argument of the hash function in step 3 of the signature generation. More specifically, the second component of a signature is generated as a solution <em>k </em>to

<em>ks </em>≡ <em>H</em>(<em>M</em>) − <em>xr </em>(mod <em>p </em>− 1) <em>,</em>

and a signature (<em>r,s</em>) to a message <em>M </em>is accepted if and only if

<em>y</em><em>rr</em><em>s </em>≡ <em>g</em><em>H</em>(<em>M</em>) (mod <em>p</em>) <em>.</em>

Suppose Eve has intercepted a signature (<em>r,s</em>) to a message <em>M </em>generated by Alice, such that gcd(<em>H</em>(<em>M</em>)<em>,p </em>− 1) = 1. Eve proceeds as follows:

Step 1. Chooses any <em>M</em><sup>0 </sup>∈ {0<em>,</em>1}<sup>∗</sup>.

Step 2. Computes <em>H</em>(<em>M</em>) and <em>H</em>(<em>M</em><sup>0</sup>).

Step 3. Solves <em>H</em>(<em>M</em>)<em>u </em>≡ <em>H</em>(<em>M</em><sup>0</sup>) (mod <em>p </em>− 1) for <em>u </em>via the Extended Euclidean

Algorithm.

Step 4. Computes <em>S </em>≡ <em>su </em>(mod <em>p </em>− 1).

Step 5. Computes <em>R </em>≡ <em>rup </em>− <em>r</em>(<em>p </em>− 1) (mod <em>p</em>(<em>p </em>− 1)).

<ul>

 <li>(4 marks) Prove that <em>R </em>≡ <em>ru </em>(mod <em>p </em>− 1), and conclude that <em>y<sup>R </sup></em>≡ <em>y<sup>ru </sup></em>(mod <em>p</em>).</li>

 <li>(4 marks) Prove that <em>R<sup>S </sup></em>≡ <em>r<sup>su </sup></em>(mod <em>p</em>).</li>

 <li>(4 marks) Prove that (<em>R,S</em>) is a valid signature to the message <em>M</em><sup>0</sup>. In other words, given <em>r,s </em>and <em>M</em>, Eve can generate a a valid signature (<em>R,S</em>) to <em>any </em>message <em>M</em><sup>0 </sup>that will be accepted as coming from Alice.</li>

</ul>

<em>Remark: </em>The quantity <em>R </em>will almost certainly exceed <em>p</em>, so this attack can be foiled if a verifier checks that <em>r &lt; p </em>and rejects signatures for which <em>r </em>exceeds <em>p</em>. A better fix is to include <em>r </em>in the argument of the hash function as presented in class (Pointcheval 1996).

<h1>Programming Problem for CPSC 418 only</h1>

<strong>Problem 8 </strong>— Secure file transfer with prior key agreement, 37 marks

<em>Don’t be daunted by the long description of this problem! </em>Most of it is very clear specifications, including those for the autograder, to make your life easier.

<strong>Overview. </strong>Transport Layer Security (TLS) is a security protocol which aims to provide endto-end communication security over networks. It provides both privacy and data integrity. While TLS has many steps, our focus will be on the <em>cipher suite</em>, a set of algorithms that add cryptographic security to a network connection. There are typically four components to a cipher suite:

<ul>

 <li>Key Exchange Algorithm</li>

 <li>Authentication algorithm (signature)</li>

 <li>Bulk Encryption Algorithm (block cipher and mode of operation)</li>

 <li>Message Authentication Algorithm</li>

</ul>

Cipher suites are specified in shorthand by a string such as

<strong>SRP-SHA3-256-RSA-AES-256-CBC-SHA3-256</strong>.

<ul>

 <li>This implies SRP-SHA3-256 as the key exchange algorithm, RSA signatures for authentication, AES-256-CBC for encryption and SHA3-256 as the MAC (used as HMAC).</li>

 <li>SRP is the protocol implemented in Assignment 2. Please replace the former hash algorithm SHA-256 with SHA3-256 (see cryptography library).</li>

 <li>Using SHA3-256 as the MAC implies the use of HMAC with SHA3-256 (see cryptography library).</li>

</ul>

In a <em>TLS handshake</em>, upon connection two parties automatically negotiate TLS settings, including the cipher suite to use. Through an exchange of messages the two parties verify each other and establish a session key. In this assignment, the two parties will be a server and client. The server will authenticate itself to the client by means of a <em>certificate</em>, and if successful, will derive a shared session key. The two parties are then able to use the session key to exchange encrypted and authenticated messages.

In reality, a certificate is an electronic document which contains a public key and information about the owner of the key. The certificate must be signed by a <em>trusted authority </em>to verify the contents of the certificate. For us, the certificate will merely be a <em>name </em>concatenated with a <em>public key</em>, concatenated with the signature of a <em>trusted third party </em>(TTP).

<strong>Problem specifications. </strong>For this assignment, assume that the Client and Server have negotiated SRP-SHA3-256-RSA-AES-256-CBC-SHA3-256 as the TLS cipher suite.<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> At a high-level, your task is to implement a toy version of the TLS handshake using the cipher suite specified above. The protocol will have two parties a Client and Server, each run by the commands python3 Client.py filename1 python3 Server.py filename2

where filename1 is the name of a file that will be encrypted and sent to the server and filename2 is the name of the server’s decrypted output file. For testing purposes, we will assume the sent file is <strong>small</strong>, i.e. less than 1 MB. Our simplified version of the TLS handshake proceeds as follows:

<ul>

 <li>The Client first registers itself to the server as in Assignment 2 (see registration step).</li>

 <li>The Client sends its username <em>I </em>to the Server.

  <ul>

   <li>First encode <em>I </em>as a byte array in ’utf-8’ format, <em>I<sub>bytes</sub></em>. Then encode the length of <em>I<sub>bytes</sub></em>, denoted <em>len</em>(<em>I</em>) into a 4-byte array in big-endian. Send the concatenation <em>len</em>(<em>I</em>)||<em>I<sub>bytes</sub></em>.</li>

  </ul></li>

 <li>The Server sends a <em>certificate </em>consisting of the server’s name and public key as well as a signature of these two values by a Trusted Third Party (details are described in the next section).

  <ul>

   <li>The server encodes its name in a byte array <em>S </em>in ‘utf-8’ format.</li>

   <li>Encode the length of <em>S </em>in a 4-byte array <em>len</em>(<em>S</em>) and concatenate it along with the server’s public key Server PK. Note that the Server’s public key should consist of the modulus <em>N </em>concatenated with the public exponent <em>e</em>, each encoded as 128-byte bigendian numbers.</li>

   <li>Finally, append the TTP’s <em>signature </em>TTP SIG (obtained at an earlier time) to this byte array. The signature TTP SIG will be encoded in 128-bytes big-endian. The Server’s certificate should be of the form <em>len</em>(<em>S</em>)||<em>S </em>||Server PK|| TTP SIG.</li>

   <li>Upon receiving the certificate, the Client should verify the signature of the TTP.</li>

  </ul></li>

 <li>Initiate the SRP protocol from Assignment 2 (the protocol, not the registration) with the following modifications:

  <ul>

   <li>Instead of the client sending <em>A </em>as plaintext, they will send <em>Enc</em>(<em>A</em>), the RSA encryption of <em>A </em>under the Server’s public key.</li>

   <li>Upon receiving <em>Enc</em>(<em>A</em>) the server will decrypt to obtain <em>A</em>.</li>

   <li>In case you did not implement the following check in Assignment 2: the server should ensure that the value <em>A </em>is not congruent to 0 under the SRP modulus and abort otherwise (it may be fun to think about why).</li>

   <li>The remainder of the protocol proceeds as n Assignment 2 (derive the shared key and verify).</li>

  </ul></li>

 <li>With the shared key derived, the client encrypts and authenticates the file using the shared key and the symmetric algorithms specified in the suite (Note, Bob’s protocol from Assignment 1 will help with this).</li>

 <li>Have the server decrypt and verify the tag, creating a new file called PTXT that contains the decrypted message.</li>

</ul>

<strong>Requirements.</strong>

<ul>

 <li>You must implement your own version of the RSA parameter/key generation, encryption, decryption, signature generation and verification. <em>You should have a separate function for each, 5 in total</em>. For efficiency we have chosen relatively small parameter sizes: The server and TTP will pick separate RSA primes <em>p </em>and <em>q </em>to be 512 bit safe primes (see Assignment 2 for how to generate these). This means that the modulus <em>N </em>will be 1024 bits (128 bytes). See the course notes for the specifics of the RSA encryption and signature schemes.</li>

 <li>All other primitives should make use of the <em>cryptography library</em>.</li>

 <li>Alongside the Client and Server, you will need a TTP, which should be run via the command</li>

</ul>

python3 TTP.py

<ul>

 <li>Upon execution, the TTP should first obtain RSA primes <em>p </em>and <em>q </em>of size 512-bits and calculate <em>N </em>= <em>pq</em>. It should then create an RSA key pair for itself.</li>

 <li>Afterwards, the TTP should open a socket with specified port 31802 and IPV4 address 127.0.4.18 and listen.</li>

 <li>Upon a connection, the TTP should wait to receive one of two messages: ”REQUEST SIGN” or ”REQUEST KEY”.</li>

 <li>Upon receipt of ”REQUEST SIGN”, the TTP should next receive a byte array consisting of 3 (concatenated) pieces of information: a 4-byte encoding of the length of <em>name</em>, a utf-8 encoded <em>name</em>, and an RSA public key <em>PK </em>encoded as a 256-byte array.

  <ul>

   <li>The TTP should proceed to hash the byte array (name || PK) using <strong>SHA-512 </strong>to obtain a 512 bit value <em>t</em>, store it, and then hash <em>t </em>a second time, to produce <em>t</em><sup>0</sup>. Interpret the byte array <em>t</em>||<em>t</em><sup>0 </sup>as big-endian integer, and reduce it by the TTP’s RSA modulus. The purpose of this is to make full use of the RSA message space.</li>

   <li>Finally, compute the RSA signature on this value, then send <em>N </em>concatenated with the signature to the requester.</li>

   <li>Note that <em>N </em>and the TTP-signature should each be encoded as 128-byte numbers in big endian.</li>

   <li>When receiving ”REQUEST KEY”, the TTP should simply send its modulus <em>N </em>concatenated to its public key. For simplicity, have the TTP close the socket connection after this communication.</li>

  </ul></li>

 <li>When your server script is run, prompt the user for a <em>server name</em>, then create an RSA key pair for the server. The server should connect to the TTP and send the message ”REQUEST SIGN”.</li>

 <li>Upon receiving the signature from the TTP, the Server can now create a socket connection on port 31803, IPV4 address 127.0.4.18 and begin listening for a client.</li>

 <li>When the Client program is executed, it should connect to the TTP and send ”REQUEST KEY”. Upon receiving the public key, store it, and connect to the Server and proceed with the derivation of a shared key.</li>

</ul>

<strong>Autograder requirements. </strong>For the purposes of the autograder, <em>whenever </em>a value is computed please print out a statement with the following format:

<ul>

 <li>“Server: Server PK = 1234…”</li>

</ul>

here the word ‘Server’ is replaced by the relevant party (Client or TTP), ‘Server PK’ is replaced by the relevant variable, and 1234.. is replaced by the corresponding value. This <em>includes </em>secret values (just think of them as debug statements).

<ul>

 <li><strong>When sending a value through a socket</strong>, please print a statement with the following format:</li>

</ul>

Server: Sending Server N = <em>&lt;hex value of N&gt;</em>

<strong>When receiving a value via socket</strong>, please interpret the value first, then print a statement with the format

Client: Receiving Server N = 1234 …

<ul>

 <li><strong>Naming conventions: </strong>For printing names, please use the naming convention Client name, Server name and len(Client name), len(Server name). Do not use a different name for byte encodings. For RSA parameters <em>p,q,N</em>, use Server N, TTP N, Server q etc. SRP parameters are the same as in Assignment 2. For the public and private keys, please use the notation Server PK, Server SK, where PK stands for public key, and SK stands for secret key. Denote the TTP signature by TTP SIG. For the encrypted version of A, use Enc(A).</li>

</ul>

<strong>Example: </strong>For the TTP we would expect a print statement for the following values:

<ul>

 <li>Each of <em>p </em>and <em>q </em>as well as the value <em>N</em>.</li>

 <li>Each of the public and private RSA signature values <em>e </em>and <em>d</em>.</li>

 <li>The signature of the server information after it has been computed.</li>

 <li>The received message from any connections (“REQUEST SIGN” or “REQUEST KEY”).</li>

 <li>Any values received and sent, interpreted as described above.</li>

</ul>

<strong>Submission</strong>:

Please submit a separate README file in text format.            Your description must include the following:

<ul>

 <li>A list of files you have submitted that pertain to the problem and a short description of each file.</li>

 <li>A list of what is implemented in the event that you are submitting a partial solution or a statement that the problem is fully solved.</li>

 <li>A list of what is not implemented in the event that you are submitting a partial solution, (d) A list of known bugs or a statement that there are no known bugs.</li>

</ul>

You may use your own code from previous assignments as part of your solution, or make use of the solution files from Assignments 1 and 2.

<h1>Bonus Problem for Everyone</h1>

<strong>Problem 9 </strong>— Columnar transposition cryptanalysis, 10 marks

Decrypt the following ciphertext that was encrypted using a <em>columnar transposition </em>cipher. Show all your work; this includes source code if you used programming. Answers without satisfactory explanation and documentation of how they were obtained will receive no credit. Neither will answers obtained by simply running columnar transposition decryption from an online crypto applet website on the ciphertext.

A text file containing the ciphertext can be downloaded from the “assignments” page.

EPAHR ELNFO CPOIO ASROS MWIWA SOTAV TIOES INDED DXTAT

YTNTU OMEPC ASFCR LTORN MOGRA SAORO SLLAH AMGAB OGTEW

DOSME ILOOO DRFTA TVABT RHDER DEXPH NOYIP WIITO CEDON

WIRTU LMRNX LWAIN OVTUH LIONN XARLU SOTSS RNNMI EGERH AATCE FRMOS NS

<em>Hint: </em>The word “cavalry” appears in the plaintext.

<a href="#_ftnref1" name="_ftn1">[1]</a> The attack in part (a) will in fact work for any key length, but for part (b), this key length restriction is required.

<a href="#_ftnref2" name="_ftn2">[2]</a> With TLS 1.3, there has been a move towards using <em>authenticated encryption schemes </em>such as AES-GCM. For pedagogical reasons, we will look at a more classic cipher-suite.