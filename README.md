# Bit Hacks

Bit manipulation codes & hacks with C++

</br>

- [Arithmatic operations](#Arithmatic-operations)
  * [Check if integer is even or odd](#Check-if-integer-is-even-or-odd)
  * [Count Set bits in number](#Count-Set-bits-in-number)
  * [Swap two numbers without using extra variable](#Swap-two-numbers-without-using-extra-variable)
  * [Check if number is power of 2](#Check-if-number-is-power-of-2)
  * [Convert uppercase character to lowercase](#Convert-uppercase-character-to-lowercase)
  * [Convert lowercase character to uppercase](#Convert-lowercase-character-to-uppercase)
  * [Invert character case in string](#Invert-character-case-in-string)

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

</br>

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


Call 2:  
current call num = (previous call num >> 4) = (1010 1110 >> 4) = 0000 1010  
nibble = (num & 0xf) = (0000 **1010**) & (1111) = 1010 which is decimal "10"  
nibble_set_bits[10] = 2  

All call return sum = 3+2 = 5 which are total set bits in 1010 1110  

</br>

#### Swap two numbers without using extra variable
```C++
void swap_numbers(int &x, int &y)
{
    if(x != y){
        x = x ^ y;
        y = x ^ y;
        x = x ^ y;
    }
}
```
x = 3 = 0011  
y = 4 = 0100  

x = x ^ y = 0011 ^ 0100 = 0111  
y = x ^ y = 0111 ^ 0100 = 0011  
x = x ^ y = 0111 ^ 0011 = 0100  

x = 0100 = 4  
y = 0011 = 3  

</br>

#### Check if number is power of 2
```C++
void check_power_of_2(int &num)
{
    return (num && !(num & (num - 1)));
}
```
If num==0, first condition fails & we return **False**  


num = 0100  

(num - 1) &nbsp; => &nbsp; (0100 - 0001) &nbsp; => &nbsp; 0011  
num & (num - 1) &nbsp; => &nbsp; (0100 & 0011) &nbsp; => &nbsp; 0000  
(num && !(num & (num - 1))) &nbsp; => &nbsp; **True** &nbsp; => Is power of 2  



num = 0110  

(num - 1) &nbsp; => &nbsp; (0110 - 0001) &nbsp; => &nbsp; 0101  
num & (num - 1) &nbsp; => &nbsp; (0110 & 0101) &nbsp; => &nbsp; 0100  
(num && !(num & (num - 1))) &nbsp; => &nbsp; **False** &nbsp; => Is not power of 2  

</br>

#### Convert uppercase character to lowercase
```C++
char * upper_to_lower(char *str) 
{ 
    for(int i=0; str[i]!='\0'; i++) 
        str[i] = str[i] | ' '; 
  
    return str; 
} 
```

We OR the character with ' ', which is ASCII 32, since lowercase characters ASCII value is 32 more than uppercase.  

'A' &nbsp; => &nbsp; (65)<sub>d</sub> &nbsp; => &nbsp; (0100 0001)<sub>b</sub>  
' ' &nbsp; => &nbsp; (32)<sub>d</sub> &nbsp; => &nbsp; (0010 0000)<sub>b</sub>  

0100 0001  
0010 0000 &nbsp; OR  
........................  
0110 0001  


(0110 0001)<sub>b</sub> &nbsp; => &nbsp; (97)<sub>d</sub> &nbsp; => &nbsp; 'a'  


</br>

#### Convert lowercase character to uppercase
```C++
char * lower_to_upper(char *str) 
{ 
    for(int i=0; str[i]!='\0'; i++) 
        str[i] = str[i] & ~' '; 
  
    return str; 
} 
```

We AND the character with ~' ', which is negation of ASCII 32, since uppercase characters ASCII value is 32 less than lowercase.  

'a' &nbsp; => &nbsp; (97)<sub>d</sub> &nbsp; => &nbsp; (0110 0001)<sub>b</sub>  
~' ' &nbsp; => &nbsp; ~(32)<sub>d</sub> &nbsp; => &nbsp; ~(0010 0000)<sub>b</sub> &nbsp; => &nbsp; (1101 1111)<sub>b</sub>  

0110 0001  
1101 1111 &nbsp; AND  
........................  
0100 0001  


(0100 0001)<sub>b</sub> &nbsp; => &nbsp; (65)<sub>d</sub> &nbsp; => &nbsp; 'A'  

</br>



#### Invert character case in string
```C++
char * invert_case(char *str) 
{ 
    for(int i=0; str[i]!='\0'; i++)
    {
        if(str[i]>=65 && str[i]<=90)
            str[i] = str[i] | ' ';
        else if(str[i]>=97 && str[i]<=122)
            str[i] = str[i] & ~' ';
    }
  
    return str; 
}
```

</br>


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

</br>

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

</br>

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

</br>

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

</br>

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

</br>

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

</br>

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

</br>

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