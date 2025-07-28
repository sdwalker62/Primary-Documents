---
tags:
  - omscs
  - cs7641
  - optimization
link: https://gatech.instructure.com/courses/423062/assignments/1976800
---
# FAQ Review

* Must implement the following *discrete* algorithms:
	* Randomized Hill Climbing
	* Simulated Annealing
	* Genetic Algorithms
	* ==May implement a population based strategy for extra credit as a point of comparison for the neural network==
* Must include two sections in either order:
	* In section 1:
		* Create two optimization problems and run
			* RHC
			* SA
			* GA
		* You will need to experiment with various problems and choose the appropriate ones that highlight the properties of the respective algorithm
	* In section 2:
		* You will compare backprop to RHC, SA, and GA while reusing one data set from A1
		* To do this you will need to freeze your network architecture from A1 and use each of the RO algorithms as a backprop replace for weight updates
* We will need to understand the convergence criteria of the library we are using and explicitly pick a convergence criteria for our problems
* Include the following plots:
	* **Fitness/Iteration:** What is the fitness score at each iteration
	* **Fitness/Problem Size**: What is the end fitness per problem size? Or maybe they mean we could have a graph that shows $n$ line plots for each problem size on the same figure for size savings
	* **Function Evaluations**: 

## $N$-Queens

You have a standard chess board containing $n$ queens that are randomly placed. The goal is to move the queens such that we minimize the number of attacking queens. 

### Properties
* Start with a number of queens equal to the number of rows and columns (for instance with 20 queens we would have a `20x20` board)
	* This is because if we had `19x19` board, then minimizing the number of attacking queens would mean we need to have each queen occupy a different row/col and thus with a 19x19 board two would have to be in the same row/col and therefore be attacking
* The state `s=[1, 2, 0, 1]` means that there are queens at `(0,1)`, `(1,2)`, `(2,0)`, `(3,1)`. The index position indicates the row and the value indicates the column. The index position starts at the top left corner and works down.
* 