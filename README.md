# neurofinder-python

> python module for testing neuron finding algorithms.

This repository contains a module and a CLI for working with neuron finding algorithm results. It is used by the [neurofinder](https://github.com/neurofinder) benchmarking challenge to compare ground truth results to results from submitted algorithms.

Assumes a standard format for spatial regions, in either `JSON` or `MAT`.

The `JSON` format is:

And the `MAT` format is:

## install

Install using pip

```
pip install neurofinder
```

## use as a command line tool

To evaluate a pair of results, just pass two `JSON` files as arguments

```
neurofinder evaluate neurons1.json neurons2.json
```

You can also pass `MAT` files as one or both arguments

```
neurofinder evaluate neurons1.mat neurons2.mat
```

## methods

#### `neurofinder.load(file)`

Load regions from either a `JSON` or `MAT` file.

#### `neurofinder.match(a, b, unique=True, min_distance=inf)`

Match regions from `a` to `b` based on distances between their centers. Returns a list of indicies specifying, for each region in `a`, what the index of the matching region in `b` is. If `unique` is true, will ensure uniqueness of matches. If `min_distance` is less than `inf`, will not allow matches that exceed this distance.

#### `neurofinder.centers(a, b, threshold=5)`

Compare centers between two sets of regions `a` and `b`. Returns two metrics, the `recall` and `precision`, which are defined as the total number of matching regions, according to the given distance `threshold`, dividing by the number of regions in `a`, or `b`, respectively.

#### `neurofinder.shapes(a, b, min_distance=inf)`

Compare shapes between regions in `a` and `b` after first finding matches. For each pair of matched regions, the `overlap` and `exactness` are computed as the number of intersecting pixels divided by the number of pixels in the first, or second, region, respectively.