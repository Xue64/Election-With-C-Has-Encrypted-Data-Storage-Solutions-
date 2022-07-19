# Election-With-C
"Election With C" is a small C-based project that uses the console to create an intuitive voting program that comes with a free encryption system that stores results and names safely. The encryption system has an anti-tamper system employed to disable data tampering. 

crypt.h
- has four functions:
function guide for crpyt.h :
crypt.h is a header file made specifically for ELECTION program created by Rufelle Pactol, 2022.
as of version 1.0, crypt.h has four functions:

- void rnewline (char*)
	loops through a string and removes new line characters and turns them into "eoS" i.e.,'\0'

- int tamper(char*)
	it is a function for checking possible tampering with encrypted strings. It can detect if a string is a legitimate string encrypted using
	crypt.h or not. It returns 1 if the string is safe.

- void encrypt(char*)
	it is an encryption alogrithm, with variating results every time it is used. This is to limit security breaches.
	
- void decrypt(char*)
	it is a decryption algorithm and utilizes tamper() to check if a string is a legitimate string or not. 


as of version 1.0, these are the current weaknesses of crypt.h:
- does not encrypt special character properly
- it has a security vulnerability concerning the "string corrupted" if the hacker can time
