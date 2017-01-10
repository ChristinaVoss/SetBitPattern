# SetBitPattern
Solved exercise 8 Chapter 11 from Programming in C by Kochan - Bitwise operators

	/* Program to change a set of bits inside a number */

	#include <stdio.h>

	void bitpat_set(unsigned int *number, unsigned int setTo, int n, int numBits);
	int int_size(unsigned int num);

	int main(void)
	{
    	unsigned int x = 0x3bff;
	
    	printf(" Number x before setting bits: \n\n Decimal value = %i\n Hex value     = %x\n\n", x, x);
	
    	bitpat_set(&x, 0, 6, 4);
	
    	printf(" Number x after setting bits: \n\n Decimal value = %i\n Hex value     = %x\n", x, x);
	
    	return 0;
	}

	void bitpat_set(unsigned int *number, unsigned int setTo, int n, int numBits)
	{
    	int sizeNum = int_size(*number); // Find size of number
	
    	// set "ones" to have as many 1s as numBits (so 4 numBits = 1111) by calculating to power and subtracting one
    	int ones = (1 << numBits) -1;
	
    	// Move the "ones" bits to the position you want to swap numbers in "number" and XOR with number (will remove all unwanted 1s)
    	*number ^= (ones <<= (sizeNum -(n+numBits)));
	
    	// move the setTo bits to the correct position, and OR number with setTo to add setTo to number.
    	*number |= (setTo <<= (sizeNum -(n+numBits)));
	
	}

	int int_size(unsigned int num)
	{
    	int size = 0;
	
    	while (num)
    	{
        	size++;
        	num >>= 1;
    	}
	
    	return size;
	}

