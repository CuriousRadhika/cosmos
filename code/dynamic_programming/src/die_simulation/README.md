## Description

There is a dice simulator which generates random numbers from 0 to 5. You are given an array `constraints` where `constraints[i]` denotes the 
maximum number of consecutive times the ith number can be rolled. You are also given `n`, the number of times the dice is to be rolled ie. the number of simulations. Find the total number of distinct sequences of length `n` which can be generated by the simulator. 
Two sequences are considered different if at least one element differs from each other.

## Thought Process

This question is tough, no doubt. So, I suggest you start with a paper and pen. Take the example `n = 3, constraints = [1,1,1,2,2,3]`. Draw three dashes for the 3 simulations (a roll of the die),  \_ \_ \_ and start building the sequence in an algorithmic (repetitive steps) manner.

<details> 
  <summary>How to fill the dashes?</summary>
  </br>
  You start filling in increasing order. <br/>
  1=> You fill 0 _ _ . <br/>
  2=> For the second dash, you notice that 0 can occur only 1 consecutive time. Hence you can't fill a 0 again. So you fill, 0 1 _ . <br/>
  3=> For third blank we can choose 0. Hence 0, 1, 0. That's one sequence. <br/>
  4=> Now, 1 can't occur more than 1 consecutive time. So you fill 2. 0 1 2. That's one sequence. <br/>
  5=> Now you put 3 inplace of 2. So now your sequence is 0 1 3. That's another valid sequence. <br/>
  6=> Similarly you put 4 and 5 to form 0 1 4 and 0 1 5. <br/>
  7=> Now, you come back to 2nd place and put in 2 (recall we already considered 0). 0 2 _ . <br/>
  8=> Can't put 2 again. Hence, we put 0, 1, 3, 4 and 5 to form 0 2 0, 0 2 1, 0 2 3, 0 2 4, 0 2 5. <br/>
  9=> For 3, 4, 5 in 2nd place, we repeat the steps.  <br/>
  10=> Come back to 1st place. Put in 1. Now the sequence is 1 _ _ . <br/>
  11=> In the second place, we can't put in 1. So we put 0. Do the same as above. <br/>
  12=> After that consider 1 2 _ . But wait! Have we seen this <b>subproblem</b> somewhere before? <br/>The subproblem of 2 in the second place has occurred before.
  We found that 2 0, 2 1, 2 3, 2 4, and 2 5 (but not 2 2) were the allowed sequences after it. Since we only need the count of total sequences, it would be good 
  if we record it. Hence let's assume we recorded (and we would btw) that with 2 in the 2nd place, we could form 5 distinct sequences after it. Thus while 
  forming 1 _ _ , for 1 2 _ , we need not calculate further. We know that 5 sequences are on their way. <br/>
  13=> So we try 1 3 _ . But again! We've encountered even this subsequence before in step 9! Similarly for 1 4, 1 5. <br/> 
  
</details>


<details> 
  <summary>Solution</summary>
  </br>
  We'll recurse over each dash(simulation) and do dp with memoization
</details>

<details>
  <summary>What's the time complexity?</summary>
  </br>
  Filling each cell takes O(1) time (Filling some cell require us to recurse but we can view that as filling other cells).
  There are a total of n*m*p cells where n is number of simulations, m is the length of constraint array (6 in our case) and p is the maximum constraint value,
  it takes O(6 * np) = O(np) time. 
</details>

