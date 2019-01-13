---
title: Bitmap
date: 2018-12-06 18:06:11
categories:
tags:
---
输入：一个最多包含n个unsigned int型整数的数组，每个数都小于n，其中n=10,000,000。没有重复的整数，没有其他数据与该整数相关联。
输出： 按升序排列这些数。
约束：有 1MB多（不超过2MB） 的内存空间可用，有充足的硬盘空间。
```c
#include <stdio.h>
#include <limits.h>
#define BITSPERWORD 32           // bits_per_int
#define SHIFT       5            // 2 ^ 5 = 32
#define MASK        0x1F         // 1 1111
#define N           100000000   // n numbers to sort   
int bitmap[1 + N / BITSPERWORD];
unsigned int array[] = {23, 45, 54, 34, 123, 34534, 4, 99, 2, 78, 99999, 0};

// bitmap[i >> SHIFT]   i这个数字应该在第几个int上
// i & MASK             截取i这个数字对应二进制的后五位
// 1 << (i & MASK)      对应到某一个int上，特定位为1，其他位为0  000...0001000...000

/*  将i对应的特定位设置为1
*   bitmap              0101....0100100...000001
*   1 << (i & MASK)     0000...0000001000....000
*/
void set_bit(int i)
{
    bitmap[i >> SHIFT] |= (1 << (i & MASK));
}

/** 将i对应的特定位设置为0
 *  bitmap              0101....0100100...000001
 *  ~(1 << (i & MASK))  111111111101111111111111 
 */
void clear_bit(int i)
{
    bitmap[i >> SHIFT] &= ~(1 << (i & MASK));
}

/** 获取i对应的特定位的值
*   bitmap              0101....0100100...000001
*   1 << (i & MASK)     0000...0000001000....000
*/
int get_bit(int i)
{
    return bitmap[i >> SHIFT] & (1 << (i & MASK));
}

int main(int argc, char const *argv[])
{
    printf("INT_MAX: %d\n", INT_MAX);
    printf("UINT_MAX: %u\n", UINT_MAX);

    unsigned int i = 0;
    unsigned int length = 0;
    for (i = 0; i < N; i++)
    {
        clear_bit(i);
    }

    length = sizeof(array) / sizeof(array[0]);
    printf("length = %u\n", length);
    
    for (i = 0; i < length; i++)
    {
        set_bit(array[i]);
    }

    for (i = 0; i < N; i++)
    {
        if(get_bit(i))
        {
            printf("%d ", i);
        }
    }
    
    printf("\n");
    return 0;
}
```
```cmd
INT_MAX: 2147483647
UINT_MAX: 4294967295
length = 12
0 2 4 23 34 45 54 78 99 123 34534 99999
```

