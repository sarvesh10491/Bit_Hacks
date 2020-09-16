# Bit Hacks

Bit manipulation codes & hacks with C++

</br>

- [Arithmatic operations](#Arithmatic-operations)
  * [Check if integer is even or odd](#Check-if-integer-is-even-or-odd)

- [Nth bit operations](#Nth-bit-operations)
  * [Set Nth bit in number](#Set-Nth-bit-in-number)
  * [Clear Nth bit in number](#Clear-Nth-bit-in-number)
  * [Toggle Nth bit in number](#Toggle-Nth-bit-in-number)
  * [Check Nth bit in number Set or Unset](#Check-Nth-bit-in-number-set-or-unset)
  
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