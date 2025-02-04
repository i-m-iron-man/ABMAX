<div align="center">
    <img src="https://github.com/i-m-iron-man/abmax/blob/master/media/abmx_logo.png" width="250"/>
</div>
<div align="center">
    <img src="https://github.com/i-m-iron-man/abmax/blob/master/media/flocking.gif" width="250"/>
    <img src="https://github.com/i-m-iron-man/abmax/blob/master/media/sheep_wolf.gif" width="250"/>
    <img src="https://github.com/i-m-iron-man/abmax/blob/master/media/small_foragaing.gif" width="250"/>
</div>

Abmax is an agent-based modeling(ABM) framework in Jax, focused on dynamic population size.
It provides:
- Data structures and functions that can be used to define sets of agents and their manipulations.
    * Adding and removing an arbitrary number of agents.
    * Searching and sorting agents based on their attributes.
    * Updating an arbitrary number of agents to a specific state.
    * Stepping agents in a vectorized way.
    * Running multiple such simulations in parallel.
- Implementation of common algorithms used in ABM implemented in Vmap and Jit friendly way.

# Installation
```bash
pip install abmax
```
Dependencies:
- [Python >= 3.10](https://www.python.org/downloads/)
- [Jax >= 0.4.13](https://jax.readthedocs.io/en/latest/installation.html)
- [Flax >= 0.7.4](https://flax.readthedocs.io/en/latest/index.html)

# Benchmark
A comparison of the performance of Abmax with other ABM frameworks: [Agents.jl](https://juliadynamics.github.io/Agents.jl/stable/) and [Mesa](https://mesa.readthedocs.io/en/stable/) based on the [Wolf-Sheep (Grid space) and Bird-Flock (Continuous space) models](https://github.com/i-m-iron-man/ABMFrameworksComparison/tree/main). These simulations are run for 100 steps and the median time taken for 10 runs is logged. The benchmark is run on a [gcn GPU node](https://servicedesk.surf.nl/wiki/display/WIKI/Snellius+hardware)(Intel Xeon Platinum 8360Y + Nvidia A100) of the [Snelius cluster](https://www.surf.nl/en/services/snellius-the-national-supercomputer)
The number of initial agents for these simulations are as follows:
- Wolf-Sheep small: 1000 sheep, 500 wolves
- Wolf-Sheep large: 10000 sheep, 5000 wolves
- Bird-Flock small: 1000 birds
- Bird-Flock large: 10000 birds

| Model | Abmax | Agents.jl | Mesa |
| ----- | ----- | --------- | ---- |
| Wolf-Sheep small | 5X | X~140(ms) | 29X |
| Wolf-Sheep large | 60X | 60X~6420(ms) | >1hr |
| Bird-Flock small | 3Y | Y~126(ms) | 126Y |
| Bird-Flock large | 3Y | 17Y~2179(ms) | >1hr |

In Abmax, we can [run multiple simulations](https://github.com/i-m-iron-man/abmax/blob/master/benchmarks/wolf_sheep/benchmarks_vmap.py) in parallel because of automatic batching and vectorization. 
Here is a trend in running different numbers of wolf-sheep small models in parallel.

| Number of models | 10 | 20 | 50 | 100 | 200 | 500 |
| ----------------- | -- | -- | -- | --- | --- | --- |
| time taken (s) | 5.75 | 6.81 | 7.32 | 8.52 | 8.617 | 14.32 |

Note: All times that are reported, are excluding the model setup time.


# Tutorial
A basic tutorial on how to use Abmax is available [here](https://github.com/i-m-iron-man/abmax/blob/master/tutorials/getting_started.ipynb)


# Citation
If you use Abmax in your work, please consider citing it as follows:
```
@software{abmaxgithub,
  author = {Siddharth Chaturvedi and Ahmed EL-Gazzar and Marcel van Gerven},
  title = {{ABMAX}: An agent-based modeling framework in {Jax}},
  url = {https://github.com/i-m-iron-man/abmax},
  version = {0.0.1},
  year = {2025},
}



