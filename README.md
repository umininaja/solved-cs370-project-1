Download Link: https://assignmentchef.com/product/solved-cs370-project-1
<br>
The learning objective of this project is for students to get familiar with using secret-key encryption and one-way hash functions in the openssl library. After finishing the assignment, in addition to improving their understanding of secret-key encryption and one-way hash function concepts, you should be able to use tools and write programs to generate one-way hash value and encrypt/decrypt messages.

<h2>3   Lab Environment and Tasks</h2>

Installing OpenSSL. In this MP, you will use openssl commands and libraries. Please install the latest version of openssl compatible with your platform. It should be noted that if you want to use openssl libraries in your programs, you need to install several other things for the programming environment, including the header files, libraries, manuals, etc.




<h3>3.1  [10pts] Observation Task: Encryption using different ciphers and modes</h3>

In this exercise, you will play with various encryption algorithms and modes. You can use the following openssl enc command to encrypt/decrypt a file. To see the manuals, you can type man openssl and man enc







% openssl enc ciphertype -e -in plain.txt -out cipher.bin 

-K 00112233445566778889aabbccddeeff 




-iv 0102030405060708







Please replace the ciphertype with a specific cipher type, such as -aes-128-cbc, -aes-128-cfb, -bf-cbc, etc. Try at least 3 different ciphers and three different modes. You can find the meaning of the command-line options and all the supported cipher types by typing “man enc”. We include some common options for the openssl enc command in the following:







<table width="625">

 <tbody>

  <tr>

   <td width="136">-in &lt;file&gt;</td>

   <td width="489">input file</td>

  </tr>

  <tr>

   <td width="136">-out &lt;file&gt;</td>

   <td width="489">output file</td>

  </tr>

  <tr>

   <td width="136">-e</td>

   <td width="489">Encrypt</td>

  </tr>

  <tr>

   <td width="136">-d</td>

   <td width="489">Decrypt</td>

  </tr>

  <tr>

   <td width="136">-K/-iv</td>

   <td width="489">key/iv in hex is the next argument</td>

  </tr>

  <tr>

   <td width="136">-[pP]</td>

   <td width="489">print the iv/key (then exit if -P)</td>

  </tr>

  <tr>

   <td width="136"></td>

   <td width="489"></td>

  </tr>

 </tbody>

</table>




<strong>What to include in your submission for 3.1:</strong>

Include the plaintext used for encryption and the cipher test obtained using 3 different encryption modes/algorithms that you tried




<h3>3.2  [10pts] Observation Task: Encryption Mode – ECB vs. CBC</h3>

Obtain a simple picture in .bmp format. Encrypt this picture, so people without the encryption keys cannot know what is in the picture. Please encrypt the file using the ECB (Electronic Code Book) and CBC (Cipher Block Chaining) modes, and then do the following:




<ol>

 <li>Let us treat the encrypted picture as a picture, and use a picture viewing software to display it. However, for the .bmp file, the first 54 bytes contain the header information about the picture, you have to set it correctly, so the encrypted file can be treated as a legitimate .bmp file. Replace the header of the encrypted picture with that of the original picture. You can use a hex editor tool (e.g. ghex or Bless) to directly modify binary files.</li>

</ol>




<ol start="2">

 <li>Display the encrypted picture using any picture viewing software. Can you derive any useful infor-mation about the original picture from the encrypted picture? Record both encrypted pictures and the original picture for your report.</li>

</ol>




<strong>What to include in your submission for 3.2:</strong>

Include the encrypted pictures with CBC and ECB mode along with the original picture.




<h3>3.3  [10 pts] Observation Task: CBC Encryption using different IVs</h3>

IVs or initialization vectors act as a random seed to the block cipher modes of encryption

like CBC. In this task you will understand the role of IVs.

<ul>

 <li>Step 1: Create any file with one line of text and name it plain.txt, the content of the file doesn’t matter.</li>

 <li>Step 2: Now, using the command in the Q3.1, encrypt the file using aes-128-cbc scheme and write the output to the file ‘encrypt1.bin’. You are free to choose the Key and IV in this step, but note them down.</li>

 <li>Step 3: Now using the same Key and IV in the step 2, encrypt the file again and write the output to ‘encrypt2.bin’.</li>

 <li>Step 4: Now using the same Key in Step 2 and a different IV, encrypt the file again and write your output to ‘encrypt3.bin’.</li>

</ul>




<strong>What to include in your submission for 3.2:</strong>

Now based on your observations of the above steps and the 3 different files that you generated, answer the following questions:

<ol>

 <li>Does the contents of ‘encrypt1.bin’ match the contents of ‘encrypt2.bin’? Explain why or why not.</li>

 <li>Does the contents of ‘encrypt1.bin’ match the contents of ‘encrypt3.bin’? Explain why or why not.</li>

</ol>




<h3>3.4. [OPTIONAL] [80pts] Coding Task: Encrypting with OpenSSL</h3>

So far, we have learned how to use the tools provided by openssl to encrypt and decrypt messages. In this task, we will learn how to use openssl’s crypto library to encrypt/decrypt messages in programs.







OpenSSL provides an API called EVP, which is a high-level interface to cryptographic functions. Although OpenSSL also has direct interfaces for each individual encryption algorithm, the EVP library provides a common interface for various encryption algorithms. To ask EVP to use a specific algorithm, we simply need to pass our choice to the EVP interface. A sample C code is given in http://www.openssl. org/docs/crypto/EVP_EncryptInit.html. Please get yourself familiar with this program, and then do the following exercise.




You are given a plaintext and a ciphertext, and you know that aes-128-cbc is used to generate the ciphertext from the plaintext, and you also know that the numbers in the IV are all zeros (not the ASCII character ‘0’). Another clue that you have learned is that the key used to encrypt this plaintext is an English word shorter than 16 characters; the word that can be found from a typical English dictionary. Since the word has less than 16 characters (i.e. 128 bits), space characters (hexadecimal value 0x20) are appended to the end of the word to form a key of 128 bits. Your goal is to write a program to find out this key.




You can download an English word list from the Internet. We have also linked one here <a href="http://www.cis.syr.edu/~wedu/seed/Labs/Crypto/Crypto_Encryption/files/words.txt">http://www.cis.syr.edu/~wedu/seed/Labs/Crypto/Crypto_Encryption/files/words.txt</a>.

The plaintext and ciphertext are the following:

Plaintext (total 21 characters): This is a top secret.

Ciphertext (in hex format): 8d20e5056a8d24d0462ce74e4904c1b5




13e10d1df4a2ef2ad4540fae1ca0aaf9







Note 1: If you choose to store the plaintext message in a file, and feed the file to your program, you need to check whether the file length is 21. Some editors may add a special character to the end of the file. If that happens, you can use a hex editor tool to remove the special character.




Note 2: In this task, you are supposed to write your own program to invoke the crypto library. No credit will be given if you simply use the openssl commands to do this task.




Note 3: To compile your code, you may need to include the header files in openssl, and link to openssl libraries. To do that, you need to tell your compiler where those files are. In your Makefile, you may want to specify the following:

INC=/usr/local/ssl/include/ or the actual location in your system

LIB=/usr/local/ssl/lib/ or the actual location in your system




all:




gcc -I$(INC) -L$(LIB) -o enc yourcode.c -lcrypto –ldl




<h3>3.5 [10pts] Observation Task: Generating Message Digest and MAC</h3>

In this exercise, you will generate message digests using a few different one-way hash algorithms. You can use the following openssl dgst command to generate the hash value for a file. To see the manuals, you can type man openssl and man dgst.




% openssl dgst dgsttype filename







Please replace the dgsttype with a specific one-way hash algorithm, such as -sha1, -sha256, etc. In this exercise, you should try at least 3 different algorithms, and note your observations. You can find the supported one-way hash algorithms by typing “man openssl”.




<strong>What to include in your submission for 3.5:</strong>

Include the plaintext used and the hash digest obtained using 3 different hash algorithms that you tried.




<h3>3.6  [10pts] Observation Task: Keyed Hash and HMAC</h3>

In this exercise, you will generate a keyed hash (i.e. MAC) for a file. Please generate a keyed hash using HMAC-SHA256, and HMAC-SHA1 for any file that you choose. Please try several keys with different length.




<strong>What to include in your submission for 3.6:</strong>

Answer the following question. Do we have to use a key with a fixed size in HMAC? If so, what is the key size? If not, why?




You can use the -hmac option of openssl command line. The following example generates a keyed hash for a file using the HMAC-SHA256 algorithm. The string following the -hmac option is the key.




% openssl dgst –sha256 -hmac “abcdefg” filename




<table width="624">

 <tbody>

  <tr>

   <td width="389">OSU Computer Security</td>

   <td width="235">2</td>

  </tr>

 </tbody>

</table>

<h3> 3.7. [10pts] Observation Task: The Randomness of One-way Hash</h3>

To understand the properties of one-way hash functions, do the following exercise for SHA512 and SHA256:

<ol>

 <li>Create a text file with the following text — ‘The cow jumps over the moon’</li>

 <li>Generate the hash value H<sub>1</sub> for this file using SHA512 (SHA256).</li>

 <li>Flip one bit of the input file. You can achieve this modification using hex editors like ghex or Bless.</li>

 <li>Generate the hash value H<sub>2</sub> for the modified file.</li>

</ol>

<strong> </strong>

<strong>What to include in your submission for 3.7:</strong>

Please observe whether H<sub>1</sub> and H<sub>2</sub> are similar or not. How many bits are the same between H<sub>1</sub> and H<sub>2</sub>. Flip bits 1, 49, 73, and 113 and record the number of bits that are different between H<sub>1</sub> and H<sub>2</sub> when using SHA512 and SHA256 in a table. What trend do you see in table? Does this trend change if you flip different bits or flip multiple bits? What if you flipped two bits or all 4 bits at the same time?




<h3>3.8 [OPTIONAL] [120pts] Coding Task: Weak versus Strong Collision Resistance Property</h3>

In this task, we will investigate the difference between hash function’s two properties: weak collision resistance property versus strong collision-resistance property. You will use the brute-force method to see how long it takes to break each of these properties. Instead of using openssl’s command-line tools, you are required to write own programs to invoke the message digest functions in openssl’s crypto library.




A sample C code can be found from <a href="https://www.openssl.org/docs/crypto/EVP_DigestInit.html">http://www.openssl.org/docs/crypto/EVP_DigestInit.html</a>.

Please get familiar with this sample code.







Since most of the hash functions are quite strong against the brute-force attack on those two properties, it will take us years to break them using the brute-force method. To make the task feasible, we reduce the length of the hash value to 24 bits. We can use any one-way hash function, but we only use the first 24 bits of the hash value in this task. Namely, we are using a modified one-way hash function. Please design an experiment to find out the following:




<ol>

 <li>[50pts] How many trials it will take you to break the weak collison resistsance property using the brute-force method? You should repeat your experiment for multiple times (100 or more depending on how long each trial takes), and report your average number of trials.</li>

</ol>




<ol start="2">

 <li>[50pts] How many trials it will take you to break the collision-free property using the brute-force method? Similarly, you should report the average.</li>

</ol>




<ol start="3">

 <li>[10pts] Based on your observation, which property is easier to break using the brute-force method?</li>

</ol>




<ol start="4">

 <li>[10pts] Can you explain the difference in your observations?</li>

</ol>

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2022/04/625.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2022/04/625.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>





