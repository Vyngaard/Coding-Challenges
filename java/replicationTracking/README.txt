Here we have three stages of implementation of a solution to a coding challenge. Given two numbers X and Y as strings, with a given starting point of 1 and 1. 
What is the smallest number of generations needed to occur from the set 1, 1 to reach X, Y. X can only increase by Y. Conversely Y can only increase by X. 
X and Y will never be greater than 10^50. If 1, 1 can never be reached we return "impossible".

Attempt #1: Depth First Search
You'll find the first implementation of a solution based on a depth first style search which produces all of the possible combinations of addition starting by adding adding
	to X. Then to Y. This implementation was found to have flaws. Primarily in that while finding either the answer or the inverse should be an equal number of steps.
	The number of steps to reach that point is unnecessarily large, especially when dealing in large numbers. When using recursion the stack grows to an excessive
	size compounded by a large number of unnecessary steps to reach a final answer.

Thus it was abandoned in favor of attempt #2.

Attempt #2:Linear Backtracking
What I have called linear backtracking is a recursive solution that starts from X and Y. Using the knowledge that either one can only ever be increased by the other I have
	implemented a simple mathematics based solution that recursively subtracts the smaller from the greater for every step. This solution dramatically reduces the number of
	recursive calls necessary to reach a final solution. However, when dealing in arbitrarily large numbers the stack will eventually overflow. This is especially true
	on numerical situations where an arbitarily small number is subtracted repetatively from an arbitarily large number. It was also noted in this particular implementation
	that we had yet to adjust the algorithm implementation for truly large numbers that an int was unable to hold.

So on to attempt #3.

Attempt #3:Linear Backtracking without Recursion
With attempt #3 we start our implementation by accounting for those excessively large numbers up to 10^50 by using BigInteger from java.math.BigInteger to store those values
	larger than int. This means utilizing functions built into BigInteger for comparisions, mathematical operations, and string conversion. Many of the comparisons
	in attempt 3 are done with compareTo which returns a basic integer value of -1, 0, 1 based on whether the values are less than, equal to, or greater than another value.
	Attempt 3 is also dramatically different from 2 in that rather than simple repetative subtraction we divide the larger by the smaller, the resulting output is automatically
	reduced similar to floor so we can simply multiply this output by our smaller number. This new number is then subtracted from the larger of X and Y to gain a new number.
	This reduces what could be several steps into one set of mathematical operations. Allowing us to rapidly deal in those arbitrarily large numbers of 10^50.