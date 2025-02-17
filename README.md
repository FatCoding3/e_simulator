# E-Simulator Package

 This is a small library designed to provide a useful tool for simulating the trajectories of a charged particle in an electromagnetic field. The motion of the particles is computed using the 4th-order Runge-Kutta method and relativistic physics, ensuring high accuracy in simulations at both low and high velocities.

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [Contribute](#contribute)

## Install

The package can be easily installed using pip.

```bash
pip install e-simulator
```

## Usage

For a more detailed explanation of the package and its usage, please refer to the [quick-guide](https://github.com/FatCoding3/e_simulator/blob/main/guide/quick_guide.ipynb).<br><br>
Below is a simple example. First, we need to import the package.

```python
import e_simulator as es
```

Then, we create a new `Project` object.
    
```python
project = es.Project(
    name = 'Sample Project',
)
```

Next, we set the project's system by adding boundary, particle, and electromagnetic regions.

```python
# Set polygon boundary
project.set_bounds(
    es.PolygonGeometry.simple_construct(
        tuples = [(0, 0), (0, 100), (100, 100), (100, 0)]
    )
)

# Set particle
project.set_particle(
    es.Particle(
        mass = 1,
        charge = 1,
        init_position = es.Coordinate(1, 1),
        init_velocity = es.Coordinate(2, 2)
    )
)

# Set electromagnetic regions
project.set_em_regions([
    es.EMRegion( 
        em_field = es.StaticEMField(electric=es.Vector(1, 0), magnetic=5),
        geometry = es.PolygonGeometry.simple_construct(
            tuples = [(10, 10), (10, 20), (20, 20), (20, 10)]
        )
    ), 
])
```

Finally, we can run the simulation and view the result.

```python
# Run simulation
project.simulate(
    max_s = 100,
    max_t = 50,
)

# View the result in a DataFrame
project.simulate_data_to_df()
```

We also can plot the orbit of the particle.

```python
import matplotlib.pyplot as plt

# Create a visualizer
visualizer = es.Visualizer(project)

fig, ax = plt.subplots()
visualizer.plot_simulation(ax)
plt.show()
```

## Contribute
If you've encountered a bug or want to contribute by helping fix one, your involvement is highly appreciated! You can contact me directly through [luongdoan000@gmail.com]().
