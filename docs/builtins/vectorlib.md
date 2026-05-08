---
title: Vector Library
weight: 11
---

This library implements functionality for the vector type in addition to the built-in primitive operator support. 
Default configuration uses vectors with 3 components (`x`, `y`, and `z`). 

Individual vector components can be accessed using the fields `x` or `X`, `y` or `Y`, `z` or `Z`
Since vector values are immutable, writes to individual components are not supported.

```
vector.zero
vector.one
```

Constant vectors with all components set to 0 and 1 respectively.

```
vector.create(x: number, y: number, z: number): vector
```

Creates a new vector with the given component values.

```
vector.magnitude(vec: vector): number
```

Calculates the magnitude of a given vector.

```
vector.normalize(vec: vector): vector
```

Computes the normalized version (unit vector) of a given vector.

```
vector.cross(vec1: vector, vec2: vector): vector
```

Computes the cross product of two vectors.

```
vector.dot(vec1: vector, vec2: vector): number
```

Computes the dot product of two vectors.

```
vector.angle(vec1: vector, vec2: vector, axis: vector?): number
```

Computes the angle between two vectors in radians. The axis, if specified, is used to determine the sign of the angle.

```
vector.floor(vec: vector): vector
```

Applies `math.floor` to every component of the input vector.
```
vector.ceil(vec: vector): vector
```

Applies `math.ceil` to every component of the input vector.

```
vector.abs(vec: vector): vector
```

Applies `math.abs` to every component of the input vector.

```
vector.sign(vec: vector): vector
```

Applies `math.sign` to every component of the input vector.

```
vector.clamp(vec: vector, min: vector, max: vector): vector
```

Applies `math.clamp` to every component of the input vector.

```
vector.max(...: vector): vector
```

Applies `math.max` to the corresponding components of the input vectors. Equivalent to `vector.create(math.max((...).x), math.max((...).y), math.max((...).z))`.

```
vector.min(...: vector): vector
```

Applies `math.min` to the corresponding components of the input vectors. Equivalent to `vector.create(math.min((...).x), math.min((...).y), math.min((...).z))`.
