# General
Use *clearvars, clc* in the first line of every script, good convention.

## Ex 1 & readme
write everyone's name and id  

no chinese, especially punctuations.



## Ex 2
better to write y=x.^y rather than y=[x.^y] <= this is unnecessary
### task 2
write sth like y(5,1)=sum(x) is not good. Since it visits the places not belongs to you. 



## Ex 4

**When the number of laps is not an integer also return the number of meters
remaining in order to complete one more lap.**  

In this case, use if statement to judge mod(input, 400). If it is 0, disp(floor(input/400)), else disp lap and reminder.  

How to display  lap and reminder?  

1. easiest way to display: fprintf/sprintf  

fprintf("%d and %d", lap, remain)  

2. use disp  

disp(num2str(a)+" and "+num2str(b));



## Ex 6
1. input a list if values: use input('') to obtain the list directly
2. input('..','s') can input a string from command window
3. can use strcmp to compare string input and the desired input. If they are same return 1. / can also directly compare them


## Ex 7
### task1
Print the number of primes (how many primes), not the value of all the primes.  

Use sum(isprime(1:100000))    
OR  
length(primes(100000))  
OR
numel(primes(100000))  --- number of elements in an array

### task2
1. use randi -- discrete uniform distribution, including 1 and 10
use unifrnd function -- returns an array of random numbers chosen from the
    continuous uniform distribution on the interval from A to B, including 1 and 10
2. unifrnd(1,10,5,1) -- 5*1 array 
3. rand -- uniform distribution on (0,1)
