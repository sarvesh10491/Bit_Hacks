# Bit Hacks

Bit manipulation codes & hacks with C++

</br>

- [Arithmatic operations](#Arithmatic-operations)
  * [Check if integer is even or odd](#Check-if-integer-is-even-or-odd)

- [Nth bit operations](#Nth-bit-operations)
  * [Set Nth bit in number](#Set-Nth-bit-in-number)
  
- [Bit manipulations](#Bit-manipulations)
  * [Sub-heading](#sub-heading-2)


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

1<<pos  =>  1<<2  =>  00100  

10000  
00100  
............  
10100  


#### Clear Nth bit in number
```C++
void clear_Nth_bit(int &num, int pos)
{
    num &= ~(1 << pos);
}
```
num = 10100  
pos = 2  

~(1<<pos) $~$ => $~$ ~(1<<2) $~$ => $~$ ~00100 $~$ => $~$ 11011

10100  
11011  
............  
10000 

## Bit manipulations
