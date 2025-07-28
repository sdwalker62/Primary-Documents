The $n$-Queens Problem is a common optimization problem where there are $n$ queens to place on an $n \times n$ chessboard. The fitness function calculates how many of the queens are attacking each other.

## Values

The *maximum* fitness value is calculated by, assuming $n$ is the number of queens, the following formula:

$$
\frac{n!}{(n-2)!2!}
$$
For $n=8$, this would be $8!/(6!2!)=28$.

## Notes

* One approach that you can try is start with the queen that is being attacked the most, moving it to a position where there are no attacking queens.
	* This is similar to most constrained variable heuristic in constrained satisfaction problems
* A local minima for this problem is when no moves (for any of the queens) reduces the overall number of attacks. 
