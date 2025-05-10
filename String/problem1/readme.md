# problem 1

![alt text](image.png)

Examples:
![alt text](image-1.png)

simple approch using internal function .split()

![alt text](image-2.png)

My approch:

ans array created
using flag ch or sp

iterate A from last. look for chr
update flag = ch and append chr to temp array.
once space is found flag = sp and update ans from temp + space.
look for chr and flag = ch and append chr into temp....

better:

![alt text](image-3.png)
![alt text](image-4.png)