# Bit Hacks

Bit manipulation codes & hacks with C++

</br>

- [Arithmatic operations](#Arithmatic-operations)
  * [Check if integer is even or odd](#Check-if-integer-is-even-or-odd)
  * [Count Set bits in number](#Count-Set-bits-in-number)

- [Nth bit operations](#Nth-bit-operations)
  * [Set Nth bit in number](#Set-Nth-bit-in-number)
  * [Clear Nth bit in number](#Clear-Nth-bit-in-number)
  * [Toggle Nth bit in number](#Toggle-Nth-bit-in-number)
  * [Check Nth bit in number Set or Unset](#Check-Nth-bit-in-number-set-or-unset)
  * [Clear All bits from LSB till Nth bit in number](#Clear-All-bits-from-LSB-till-Nth-bit-in-number)
  * [Clear All bits from MSB till Nth bit in number](#Clear-All-bits-from-MSB-till-Nth-bit-in-number)
  
- [Bit manipulations](#Bit-manipulations)
  * [Rotate left by N bits](#Rotate-left-by-N-bits)
  * [Rotate right by N bits](#Rotate-right-by-N-bits)


<!-- toc -->

## Arithmatic operations
#### Check if integer is even or odd
```C++
void even_odd(int &num)
{
    if(num & 1)
	    cout<<"Odd";
    else
        cout<<"Even";
}
```

#### Count Set bits in number
```C++
int nibble_set_bits[16] = { 0, 1, 1, 2, 1, 2, 2, 3, 
                        1, 2, 2, 3, 2, 3, 3, 4 };

void count_set_bits(int &num)
{
    int nibble = 0;

    if (num == 0) 
        return nibble_set_bits[0]; 
  
    nibble = num & 0xf; 

    return nibble_set_bits[nibble] + count_set_bits(num >> 4);
}
```
num = 1010 1110  

Call 1:  
current call num = 1010 1110  
nibble = (num & 0xf) = (1010 **1110**) & (1111) = 1110 which is decimal "14"  
nibble_set_bits[14] = 3  


call 2:  
current call num = (previous call num >> 4) = (1010 1110 >> 4) = 0000 1010  
nibble = (num & 0xf) = (0000 **1010**) & (1111) = 1010 which is decimal "10"  
nibble_set_bits[10] = 2  

All call return sum = 3+2 = 5 which are total set bits in 1010 1110  






## Nth bit operations
#### Set Nth bit in number
```C++
void set_Nth_bit(int &num, int pos)
{
    num |= (1 << pos);
}
```
num = 10000  
pos = 2  

(1 << pos) &nbsp; => &nbsp; (1 << 2) &nbsp; => &nbsp; 00100  

&nbsp; &nbsp; &nbsp; 10**0**00  
OR &nbsp; 00**1**00  
&nbsp; &nbsp; &nbsp; ............  
&nbsp; &nbsp; &nbsp; 10**1**00  


#### Clear Nth bit in number
```C++
void clear_Nth_bit(int &num, int pos)
{
    num &= ~(1 << pos);
}
```
num = 10100  
pos = 2  

~(1 << pos) &nbsp; => &nbsp; ~(1 << 2) &nbsp; => &nbsp; ~00100 &nbsp; => &nbsp; 11011

10**1**00  
11**0**11 &nbsp; AND  
............  
10**0**00 


#### Toggle Nth bit in number
```C++
void toggle_Nth_bit(int &num, int pos)
{
    num ^= (1 << pos);
}
```
num = 10100  
pos = 2  

(1 << pos) &nbsp; => &nbsp; (1 << 2) &nbsp; => &nbsp; 00100  

10**1**00  
00**1**00 &nbsp; XOR  
............  
10**0**00  


#### Check Nth bit in number Set or Unset
```C++
void set_unset_Nth_bit(int &num, int pos)
{
    return num & (1 << pos);
}
```
num = 10100  
pos = 2  

(1 << pos) &nbsp; => &nbsp; (1 << 2) &nbsp; => &nbsp; 00100  

10**1**00  
00**1**00 &nbsp; AND  
............  
00**1**00  



#### Clear All bits from LSB till Nth bit in number
```C++
void clear_till_Nth_bit_from_LSB(int &num, int pos)
{
    int mask = ~((1 << pos+1) - 1);
    num &= mask;
}
```
num = 0011 1111    
pos = 2  

~((1 << pos+1) - 1) &nbsp; => &nbsp; ~((1 << 3) - 1) &nbsp; => &nbsp; ~(0000 1000 - 0000 0001) &nbsp; => &nbsp; ~(0000 0111) &nbsp; => &nbsp; ~(1111 1000)  

mask = 1111 1000  

0011 1111  
1111 1000 &nbsp; AND  
........................  
0011 1000  



#### Clear All bits from MSB till Nth bit in number
```C++
void clear_till_Nth_bit_from_MSB(int &num, int pos)
{
    int mask = (1 << pos) - 1;
    num &= mask;
}
```
num = 1111 1000  
pos = 6  

((1 << pos+1) - 1) &nbsp; => &nbsp; ((1 << 6) - 1) &nbsp; => &nbsp; (0100 0000 - 0000 0001) &nbsp; => &nbsp; (0011 1111)  

mask = 0011 1111  

1111 1000  
0011 1111 &nbsp; AND  
........................  
0011 1000  


## Bit manipulations
#### Rotate left by N bits
```C++
#define INT_BITS 8

void rotate_left(int &num, int pos)
{
    return (num << pos) | (num >> (INT_BITS - pos));  
}
```
num = 0100 0010  
pos = 2  
INT_BITS = 8  

(0100 0010 << 2) &nbsp; => &nbsp; 0000 1000  
(0100 0010 >> (8-2)) &nbsp; => &nbsp; 0000 0001  

0000 1000  
0000 0001 &nbsp; OR  
........................  
0000 1001  


#### Rotate left by N bits
```C++
#define INT_BITS 8

void rotate_right(int &num, int pos)
{
    return (num >> pos) | (num << (INT_BITS - pos));  
}
```
num = 0100 0010  
pos = 2  
INT_BITS = 8  

(0100 0010 >> 2) &nbsp; => &nbsp; 0001 0000  
(0100 0010 << (8-2)) &nbsp; => &nbsp; 1000 0000  

0001 0000  
1000 0000 &nbsp; OR  
........................  
1001 0000  