# Election-With-C-Console-With-Encrypted-Storage-
"Election With C" is a small C-based project that uses the console to create an intuitive voting program that comes with a free encryption system that stores results and names safely. The encryption system has an anti-tamper system employed to disable data tampering. 

ENCRYPTION ALGORITHM README
// ENCRYPTION ALGORITHM //

-The length of the encypted message is 10+length*5
-there are five universal arrays, all of which are for use in generating random characters
	
	universal arrays for the random function:
	random[] - lists all letters, uppercase and lowercase, numbers for 0 to 9 (responsible for generating nuisance)
	index1[] - lists all letters, all lowercase (responsible for the tamper key)
	index2[] - lists all letters, all uppercase (responsible for the tamper key)
	secondaryShift[] - lists numbers 1, 2, 3 (responsible for generating the shift key)
	thirdShift[] - lists numbers 4, 5, 6 (responsible for generating shift key)

-the encryption algorithm's result changes every time it is used due to it having shifting keys
-the encrypt() function has two parameters, char string [MAX] (string to be encrypted) and char * result (resulting encrypted string)

-the first five indexes for result[] contain the following:
	result[0] - random char from random[]
	result[1] - random char from index1[], holds the first tamper key
	result[2] - random char from index2[], holds the second tamper key
	result[3] - random char from secondaryShift[], holds the shift key
	result[4] - random char from thirdShift[], holds the second shift key

the tamper key is generated by subtracting result[1] from result[2].
the shift key is generated by subtracting from result[4] from result[3].
the enc key is generated using the rand() function, and can be 4, 5, or 6.

//THE TAMPER KEY//

the tamper key is revealed at result[(length*5)+8] and result[(length*5)+10]
the tamper key at result[(length*5)+8] is the original tamper key + 62
the tamper key at result[(length*5)+10] is the original tamper key + 34
another security feature for determining possible data tampering is stored at result[(length*5)+1]...
...where result[(length*5)+6] = string[0]+50+enc

//THE SHIFT KEY//

the shift key can be decrypted by subtracting result[4] from result[3].
the shift key determines the location of where the original string's character is in the encrypted string.
the shift key can take in the form of integers 1 to 5.
if the shift key is 3, then the original characters of the string is found at result[5+3*(stringINDEX+1)].

//THE ENC KEY//

the enc key determines how much we will add to the original string to further lock out the information.
the enc key can be found at result[(length*5)+9].
the encrypted character is found using the following algorithm:
	-result[(length*5)+9] = tamper + ENC key + 50

security features:

	1. the tamper key is essential as it will not decrypt the string WITHOUT the correct tamper key
	2. the shift key is to discern which of the random characters in the encrypted string is part of the original string
	3. the enc key is to decrypt the located characters
	4. every time one wants to encrypt a string, the result will ALMOST always be different, even if the same string is used
	5. this variable encryption method makes it hard to decode the encrypted string, as well as decode the algorithm.
	6. the TAMPER, SHIFT, and ENC key variates every time the algorithm is run.


the length of the original string is found at result[(length*5)+7] = length + tamper + 25;
