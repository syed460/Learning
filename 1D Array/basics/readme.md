# Notes on 1D array problems

![alt text](image-1.png)

![alt text](image.png)

![alt text](image-2.png)

Edge Case:

![alt text](image-3.png)

psudo code:

![alt text](image-4.png)

TC: worst case, best case

![alt text](image-5.png)

## Consecutive once, varient 1 
![alt text](image-6.png)

![alt text](image-7.png)
![alt text](image-8.png)

![alt text](image-9.png)

My approch:
count total ones t
total 1s == lenth of array return t
for every 0 finding, count l and r
l + r + 1 <= t
    ans = max(ans, l+r+1)
else:
    ans = max(ans, t)
