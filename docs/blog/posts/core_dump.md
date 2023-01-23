---
date: 2023-01-31
authors:
  - ezio
---
#What is dumped when "core dumped"?

Quote from **geekforgeeks**:

Core Dump/Segmentation fault is a specific kind of error caused by accessing memory that “does not belong to you.” In other words, when a piece of code tries to do write operation in a read only location in memory or freed block of memory, it is known as core dump.

here is an example.

```
int main()
{
char *str;

/* Stored in read only part of data segment */
str = "abc";	

/* Problem: trying to modify read only memory */
*(str+1) = 'n';
return 0;
}
```