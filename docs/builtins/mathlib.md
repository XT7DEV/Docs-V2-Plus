---
title: Math Library
weight: 4
---

```
function math.abs(n: number): number
```

Returns the absolute value of `n`. Returns NaN if the input is NaN. 

```
function math.acos(n: number): number
```

Returns the arc cosine of `n`, expressed in radians. Returns a value in `[0, pi]` range. Returns NaN if the input is not in `[-1, +1]` range.

```
function math.asin(n: number): number
```

Returns the arc sine of `n`, expressed in radians. Returns a value in `[-pi/2, +pi/2]` range. Returns NaN if the input is not in `[-1, +1]` range.

```
function math.atan2(y: number, x: number): number
```

Returns the arc tangent of `y/x`, expressed in radians. The function takes into account the sign of both arguments in order to determine the quadrant. Returns a value in `[-pi, pi]` range.

```
function math.atan(n: number): number
```

Returns the arc tangent of `n`, expressed in radians. Returns a value in `[-pi/2, pi-2]` range.

```
function math.ceil(n: number): number
```

Rounds `n` upwards to the next integer boundary.

```
function math.cosh(n: number): number
```

Returns the hyperbolic cosine of `n`.

```
function math.cos(n: number): number
```

Returns the cosine of `n`, which is an angle in radians. Returns a value in `[0, 1]` range.

```
function math.deg(n: number): number
```

Converts `n` from radians to degrees and returns the result.

```
function math.exp(n: number): number
```

Returns the base-e exponent of `n`, that is `e^n`.

```
function math.floor(n: number): number
```

Rounds `n` downwards to previous integer boundary.

```
function math.fmod(x: number, y: number): number
```

Returns the remainder of `x` modulo `y`, rounded towards zero. Returns NaN if `y` is zero.

```
function math.frexp(n: number): (number, number)
```

Splits the number into a significand (a number in `[-1, +1]` range) and binary exponent such that `n = s * 2^e`, and returns `s, e`.

```
function math.ldexp(s: number, e: number): number
```

Given the significand and a binary exponent, returns a number `s * 2^e`.

```
function math.lerp(a: number, b: number, t: number): number
```

Linearly interpolated between number value `a` and `b` using factor `t`, generally returning the result of `a + (b - a) * t`.
When `t` is exactly `1`, the value of `b` will be returned instead to ensure that when `t` is on the interval `[0, 1]`, the result of `lerp` will be on the interval `[a, b]`.

```
math.map(x: number, inmin: number, inmax: number, outmin: number, outmax: number): number
```

Returns a value that represents `x` mapped linearly from the input range (`inmin` to `inmax`) to the output range (`outmin` to `outmax`).

```
function math.log10(n: number): number
```

Returns base-10 logarithm of the input number. Returns NaN if the input is negative, and negative infinity if the input is 0.
Equivalent to `math.log(n, 10)`.

```
function math.log(n: number, base: number?): number
```

Returns logarithm of the input number in the specified base; base defaults to `e`. Returns NaN if the input is negative, and negative infinity if the input is 0.

```
function math.max(list: ...number): number
```

Returns the maximum number of the input arguments. The function requires at least one input and will error if zero parameters are passed. If one of the inputs is a NaN, the result may or may not be a NaN.

```
function math.min(list: ...number): number
```

Returns the minimum number of the input arguments. The function requires at least one input and will error if zero parameters are passed. If one of the inputs is a NaN, the result may or may not be a NaN.

```
function math.modf(n: number): (number, number)
```

Returns the integer and fractional part of the input number. Both the integer and fractional part have the same sign as the input number, e.g. `math.modf(-1.5)` returns `-1, -0.5`.

```
function math.pow(x: number, y: number): number
```

Returns `x` raised to the power of `y`.

```
function math.rad(n: number): number
```

Converts `n` from degrees to radians and returns the result.

```
function math.random(): number
function math.random(n: number): number
function math.random(min: number, max: number): number
```

Returns a random number using the global random number generator. A zero-argument version returns a number in `[0, 1]` range. A one-argument version returns a number in `[1, n]` range. A two-argument version returns a number in `[min, max]` range. The input arguments are truncated to integers, so `math.random(1.5)` always returns 1.

```
function math.randomseed(seed: number)
```

Reseeds the global random number generator; subsequent calls to `math.random` will generate a deterministic sequence of numbers that only depends on `seed`.

```
function math.sinh(n: number): number
```

Returns a hyperbolic sine of `n`.

```
function math.sin(n: number): number
```

Returns the sine of `n`, which is an angle in radians. Returns a value in `[0, 1]` range.

```
function math.sqrt(n: number): number
```

Returns the square root of `n`. Returns NaN if the input is negative.

```
function math.tanh(n: number): number
```

Returns the hyperbolic tangent of `n`.

```
function math.tan(n: number): number
```

Returns the tangent of `n`, which is an angle in radians.

```
function math.noise(x: number, y: number?, z: number?): number
```

Returns 3D Perlin noise value for the point `(x, y, z)` (`y` and `z` default to zero if absent). Returns a value in `[-1, 1]` range.

```
function math.clamp(n: number, min: number, max: number): number
```

Returns `n` if the number is in `[min, max]` range; otherwise, returns `min` when `n < min`, and `max` otherwise. If `n` is NaN, may or may not return NaN.
The function errors if `min > max`.

```
function math.sign(n: number): number
```

Returns `-1` if `n` is negative, `1` if `n` is positive, and `0` if `n` is zero or NaN.

```
function math.round(n: number): number
```

Rounds `n` to the nearest integer boundary. If `n` is exactly halfway between two integers, rounds `n` away from 0.
