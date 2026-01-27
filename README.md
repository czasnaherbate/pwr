## Overview

- This repository contains various engineering and programming challenges.
- This README introduces the `advanced/130` module.

## Grouping Challenge (Advanced/130)

- Located in `advanced/130/GroupingChallenge`, this project implements a **Genetic Algorithm** to solve a grouping optimization problem.
- The goal is to optimally group a set of points into a specified number of clusters using evolutionary computation techniques.

### Key Components

The solution is structured around several core classes:

- **CGeneticAlgorithm**: The higher-level controller that sets up the environment and parameters for the algorithm.
- **COptimizer**: The core engine that manages the population of solutions, executes the evolutionary cycle (selection, crossover, mutation), and tracks the best solution found so far.
- **CGroupingEvaluator**: A helper class responsible for calculating the fitness score of a specific grouping configuration.
- **CIndividual**: Represents a single candidate solution (chromosome) within the population.
- **GaussianGroupingEvaluatorFactory**: A utility for generating synthetic datasets with points distributed according to Gaussian distributions to test the algorithm.

### Compilation and Usage

You can compile and run the project using `g++`. Navigate to the project directory and execute the following commands:

```bash
cd advanced/130/GroupingChallenge
g++ -std=c++11 GaussianGroupingEvaluatorFactory.cpp GroupingEvaluator.cpp Optimizer.cpp GroupingChallenge.cpp Point.cpp -o GroupingChallenge
./GroupingChallenge
```
