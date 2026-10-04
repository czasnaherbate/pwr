# Grouping Challenge

A C++ project that uses a Genetic Algorithm to split points in n-dimensional space into groups.
The goal is to find the group assignment that minimizes the sum of distances between points in the same group.

## Problem Definition

- **Input**: points randomly generated from several clusters that follow Gaussian distributions
- **Solution (genotype)**: an integer array whose length equals the number of points. The `i`-th value is the group number (`1` to `nGroups`) of the `i`-th point
- **Fitness**: the sum of Euclidean distances over every pair of points in the same group, multiplied by 2. **Lower is better.**

## Algorithm

`COptimizer` performs the following steps for each generation.

1. **Initialization** — create `nPopulation` individuals with random genotypes
2. **Mutation** — replace each gene with a random group number with probability `pMutate`
3. **Selection** — tournament selection (size 2): pick two random individuals and keep the better one as a parent
4. **Crossover** — with probability `pCrossover`, perform one-point crossover to produce 2 children
5. **Elitism** — always carry the current best solution into the next generation, and insert an extra copy with 10% probability
6. **Best solution update** — update the best solution if the new generation contains a better one

## Structure

| File                                      | Role                                                                           |
| ----------------------------------------- | ------------------------------------------------------------------------------ |
| `GroupingChallenge.cpp`                   | `main` and `CGeneticAlgorithm` (parameter setup, execution, saving results)    |
| `Optimizer.h/.cpp`                        | `CIndividual` (genotype, mutation, crossover), `COptimizer` (runs generations) |
| `GroupingEvaluator.h/.cpp`                | `CGroupingEvaluator` — computes the fitness of a solution                      |
| `GaussianGroupingEvaluatorFactory.h/.cpp` | Factory that generates points from Gaussian clusters and builds the evaluator  |
| `Point.h/.cpp`                            | `CPoint` — an n-dimensional point and distance calculation                     |
| `result.txt`                              | Run output (point coordinates, best fitness, group assignment)                 |

## Build and Run

Run from the `GroupingChallenge/` directory.

```bash
g++ -std=c++11 GaussianGroupingEvaluatorFactory.cpp GroupingEvaluator.cpp Optimizer.cpp GroupingChallenge.cpp Point.cpp -o GroupingChallenge && ./GroupingChallenge
```

On Windows, you can open `GroupingChallenge.sln` in Visual Studio and build it there.

When the run finishes, the best solution is printed to the console and saved to `result.txt`.

## Parameters

Edit the values in `main` in `GroupingChallenge.cpp`.

| Variable                  | Default | Description                                         |
| ------------------------- | ------- | --------------------------------------------------- |
| `nGroups`                 | 5       | Number of groups to split into                      |
| `nPoints`                 | 10      | Number of points                                    |
| `nMultivalueDistribution` | 5       | Number of Gaussian clusters used to generate points |
| `nDimension`              | 3       | Number of dimensions                                |
| `nPopulation`             | 1000    | Individuals per generation                          |
| `terminateCriterion`      | 100     | Number of generations to run                        |
| `pMutate`                 | 0.1     | Per-gene mutation probability                       |
| `pCrossover`              | 0.6     | Crossover probability                               |

The point-generation seed is fixed at `0`, so every run generates the same points. Each dimension's mean is drawn from the range `-100` to `100`, and the standard deviation is `1.0`.
