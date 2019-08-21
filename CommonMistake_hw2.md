# vg101: Common mistakes in Homework 2

## ex1

1. Some students fail to deal with invalid input, or deal it in wrong way.
eg. write **if** statement to judge invalid input rather than **while** statement
2. Some students faill to deal with 100 and 400 correctly
```matlab
(mod(year,100)~=0 && mod(year, 4)==0) || (mod(year,400)==0)
```

## ex2

### Fatal mistakes

1. Some students find that primes with $p=4n+1$ can always be represented as the $a^2+b^2$, and they write in README like this.

	```Since a prime for which p=4n+1 can absolutely be the sum of two squares, we don't need to check if this number is a prime, we just need to check the other two conditions if p=4n+1 and if p=a^2+b^2.```

	We can see that this is a logical fallacy. 

	$$(A\land B\Rightarrow C)\Rightarrow(C\land B \Rightarrow A)$$

### Hints
1. MatLab function to determine the next prime:
	`nextprime()`.
Note that this function works differently if you are using old version of MatLab.

2. Method to check whether $n=a^2+b^2$
	* enumerate $a$ from 1 to $\sqrt{\frac{n}{2}}$
	* check whether $\lfloor\sqrt{n-a^2}\rfloor^2$ is equal to $n$

## ex3
### Fatal test cases
	100000001
	1001001
	100100100
	%

### Hints
1. Cut the number in to 3-digit partitions.  
Read each 3-digit correctly, add the thousand/ million correspondingly. 
2. The position of `and`
* Process 3 digits in a roll, represent them as `ABC`
* `and` is needed when
  * $B\neq 0$ or $C\neq 0$
  * It is not the most significant 3 bits
	
## ex4
### Fatal mistakes
1. At first, $x_1>x_0$, but this may not be true later on. Thus when we are checking the precision, the function `abs()` is necessary.
2. Some student cannot correctly understand the meaning of **precision**. (It is more similar to uncertianty rather than precision).   
    1. Some regard it as the number of digits it needs to preserve in the final result
    2. Others regard it as the ending case should have abs(f(x_new))<10^(-precision).

# while abs(x_{n-1}-x_{n-2}< 10^{-precision})
# recursion => if abs(x_{n-1}-x_{n-2}< 10^{-precision}) else recursively call this function

## ex5
### Fatal mistakes
1. There is no armstrong number in the region `[10,99]`, thus if you fixed the length of number in the beginning, something wrong will happen.

## ex6
1. Some student cannot understand the meaning of `Assign January and February to previous year`   
In this case, we need to have
```matlab
year=year-1;
```
and then calculate year and century correspondingly. 

