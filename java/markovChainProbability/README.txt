Here we have an attempted implementation at a problem I found much more challenging. The current code is incomplete and therefore does not return a correct value but
the underlying groundwork for a solution as well as an explanation for the problem can be found in the code as well as additional information files.

This problem was to find the probability of reaching all of the terminal states in a given matrix up to 10x10. The output should be returned as an array of numerators with
the final bucket of the array as the denominator. The final output should be in its simplest form. For this we find that we can break down the problem by looking at it as a
Markov Chain system. Each value in the given array is a numerator with the total sum of each state as a denominator. So for the array:

int[][]   m2 = 	     {{0, 1, 0, 0, 0, 1}, 
                      {4, 0, 0, 3, 2, 0}, 
                      {0, 0, 0, 0, 0, 0}, 
                      {0, 0, 0, 0, 0, 0}, 
                      {0, 0, 0, 0, 0, 0}, 
                      {0, 0, 0, 0, 0, 0}};
            //OUTPUT:       [0, 3, 2, 9, 14]

We can see each bucket in a state represents the probablity of reaching the state represented by that bucket. Here state0 (s0) has equal probability of going to s1 or s5. 
When calculating this probability we can represent this probablity as (1/2). And the probablity of reaching s0 from s1 is (4/9). For calculation purposes we must always
evaluate each full state in our mathematical operations. So our full mathematical operation for the probablity of s0 reaching s5 will look like.

s0 = (1/2) * s1 + (1/2) * s5

We multiply the probablity of reaching s5 in s1 to the probablity of reaching s1 in s0. Likewise we multiply the probablity of s5 to the probablity of reaching s5 in s0.
Our goal state being the goal can be compared to an absorbing state in a standard Markov Chain system and thus be represented by a 1 in these mathematical operations. Other
terminal states that are not the goal state will be represented by 0 since once you enter those states you cannot escape. With this in mind we can expand the above operation.

Substituting state 1 and 5

s0 = (1/2) * ((4/9 * s0) + (3/9 * s3) + (2/9 * s4)) + (1/2) * 1

Substituting for the other two states we can simplify the overall equation.

s0 = (1/2) * (4/9 * s0) + (1/2)

Continuing....

s0 = 4/18 s0 + 1/2

Solving for s0

18/18s0 = 4/18s0 + 1/2
14/18s0 = 1/2
s0 = (14/18)/(1/2)

s0 = 18/28

s0 = 9/14

Given the above information. With hindsight on my previous attempt to solve this challenge. 

I believe my previous attempt to be a bit off the mark. While it likely would work the code ultimately becomes confusing and unnecessarily bloated with an excessive number of
arrays and duplicate operations. In the event that I were to attempt this challenge again I might create a rational object that stores a numerator and denominator and then break
the given matrix into a matrix of the rational objects. This would simply many of the operations necessary to reach the correct final output.