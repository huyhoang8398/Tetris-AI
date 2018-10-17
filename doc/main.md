---
title:
- Tetris AI with Genetic Algorithm
subtitle: 
- Machine Learning and Data Mining 
author: 
- Group 8
date: \today{}
institute: 
- University of Science And Technology of Hanoi
- ICT Department
theme:
- CambridgeUS
---

# Introduction 

## Tetris
![Classic Tetris World Championship](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/1.png){width=360px }

## Tetris 
* Tetris is one of the most amazing games since 1984 so far.
* Tetris is an interesting
game to play with because it combines both luck and skill.
* Tetris is hard, even to approximate
* Additionally, Tetris has been a common topic in artificial intelligence.\
\

### &rarr; Our team want to create an AI to play tetris using genetic algorithm.

## Goal 
*  Make as many moves as possible without losing.\
\
* Efficiently score points by making more tetrises.

# Tetris 
## Tetris 

::: columns
:::: column

* Grid: 22x10 cells.\
\
* There are 7  Tetrominoes: “I”, “O”, “J”, “L”, “S”, “Z”,“T”.\
\
* The Rotation System is used for all rotations.
::::

:::: column

![All rotation states of all seven tetrominoes](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/2.png){width=150px }
::::
:::

## Heuristics
* The score for each move is computed by assessing the grid the move would result in. 
* 4 heuristics which will estimate the utility of a given Tetris board:
	1. Aggregate Height.
	2. Complete Lines.
	3. Holes.
	4. Bumpiness.

## Aggregate height
* This heuristic tells us how “high” a grid is.

![Aggregate Height = 48](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/3.png){width=300px }

## Complete lines
* It is simply the the number of complete lines in a grid.

![Complete lines = 2](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/4.png){width=300px }

## Holes 
* A hole is defined as an empty space such that there is at least one tile in the same column above it.

![Number of holes = 2](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/5.png){width=200px }

## Bumpiness
* The bumpiness of a grid tells us the variation of its column heights. It is computed by summing up the absolute differences between all two adjacent columns.

![Bumpiness = 6](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/6.png){ width=155px}

* bumpiness = 6 = |3 - 5| + |5 - 5| +...+|4 - 4| + |4 - 5|

## Score Function
```
Score = A * Aggregate height
		+ B * Complete lines
		+ C * Number of Holes
		+ D * Number of Bumpiness
```
Where A, B, C, and D are weights that we decide.\
Check better move: if move 1 better than move 2 (Score1 > Score2).

# Genetic Algorithms
## Genetic Algorithms
* A search technique.
* Use techniques inspired by evolutionary.
* Decide how important each heuristic is, and whether each measures a positive or negative aspect of the board. 
* Find true or approximate solutions to optimization problems.

## Genetic Algorithms
* Population\
\
* Chromosomes.\
\
* Fitness.\
\
* Selection.\
\
* Crossover.\
\
* Mutation.

## Chromosomes
* Subset of solutions in the current generation(set of Chromosome).
* Each "chromosome" is a dictionary of heuristics and their weights.
* How much each chromosome can influence the direction of the search is based on how long they survive, and how many offspring they produce.

```python
def utility(self, board):
return sum([fun(board)*weight for (fun, weight) 
	in self.heuristics.items()])
```

## Population
* Subset of solutions in the current generation(set of Chromosome).

## Fitness
* Indicates how well the solution to the problem

## Selection
* Method of selecting an individual from a population.

## Crossover 
* Analogous to reproduction and biological crossover.
* This program currently defines two crossover methods:
	* Random attributes: Randomly take all required attributes from either parent.
	* Average attributes: Average each of the attributes of each parent.

## Mutation 
* Small random tweak in the chromosome, to get a new solution.

# Domain model

## Domain model 
* A chromosome is simply a set of heuristics and their weights.
* A genetic algorithms class will generate many random chromosomes to create an initial population, and simulate many games of Tetris by swapping new chromosomes into the AI.
* Using the final score as a "fitness function".\
\
&rarr; Determine which chromosomes were the most successful and create new chromosomes based off those chromosomes

## Domain model
![](/Users/huyhoang8398/Desktop/genetic-tetris-ai/doc/domain_model.png){width=350px }

## Algorithm 
The genetic algorithm starts by creating a population of random chromosomes.

```python
def __init__(self):
  self.population = [self.random_chromosome() 
  	for _ in range(POPULATION_SIZE)]

def random_chromosome(self):
  return Chromosome({fun: randrange(-1000, 1000) 
  	for fun, weight in self.ai.heuristics.items()})

```

## Algorithm 
* The size of the population heavily influences the performance of the program.
* Populations that are too small won't cover as much of the search space, and are more likely to get stuck in local minimums.

## Genetic Algorithm 
* Step 1: **Initialize** population\
\
* Step 2: **Selection**\
\
* Step 3: Reproduction:
	* Pick 2 parents
	* Crossover
	* Mutation\
\
* Step 4: New population

# Summary 

## Summary 
* The AI was implemented in Python and tested with both Linux/Windown
*  Make as many moves as possible without losing.
* Efficiently score points by making more tetrises.\
**Problem**
* A "tetris" is when you clear four lines at once. The easiest way to do this is to build up four solid lines, and leave a one-block column clear on one side.
* But the AI always tries to make a best possible move (highest score).


