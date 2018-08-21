<h1 align="center">Conic Sections Plotter</h1>
<p align="center"><img src="https://feen.us/5jqafv.png" alt=""></p>

## What is this?
Short story: I was bored in Maths, I started writing this plotter thingie to better understand these things.

It's not perfect. It's just a learning tool for me and anyone else who wants to look at this mess of code. It was done in only a few maths classes.

## How to use
Edit formulas by editing the characters marked in a reddish-yellowish background colour. If you don't have anything, the variable name will be shown instead.

You can also choose between formulas by selecting the tabs above.

## Known Issues/Feature Wishlist
* Graph doesn't change on input
* Additional information on the graph

## Design
I've decided to keep the equations seperate from the code (as in kept the in their own objects rather than intertwine them).

They are stored in the `modes` objects and called up when needed.

They all have their `title`, the `equation` visiable and editable by the user, a function which calculates `y`, whether it needs to be `dualSided` since `Math.sqrt()` only returns the positive result, required `parameters` and an unused `properties` object.

```js
line: {
    title: "Line",
    equation: "y = $mx + $c",
    y: function(x)
    {
        var m = eval(equVars["m"])
        var c = eval(equVars["c"])

        // y = mx + c
        return (m * x) + c
    },
    dualSided: false,
    parameters: [ "m", "c" ],
    properties: { ... },  // Unused
}
```

# Conic Sections
## Straight Line
Equation: ![y = mx + c](https://latex.codecogs.com/gif.latex?y%3Dmx&plus;c)

```js
return (m * x) + c
```

## Circle
Equation: ![r^2 = (x - h)^2 + (y - k)^2](https://latex.codecogs.com/gif.latex?r%5E2%3D%28x-h%29%5E2&plus;%28y-k%29%5E2)

Rearranged into: ![\sqrt{r^2 - (x-h)^2} + k](https://latex.codecogs.com/gif.latex?%5Csqrt%7Br%5E2%20-%20%28x-h%29%5E2%7D%20&plus;%20k)

```js
return Math.sqrt(Math.pow(r, 2) - Math.pow(x - h, 2)) + k
```

## Ellipse
Equation: ![1 = \frac{(x-h)^2}{a^2}+\frac{(y-k)^2}{b^2}](https://latex.codecogs.com/gif.latex?1%20%3D%20%5Cfrac%7B%28x-h%29%5E2%7D%7Ba%5E2%7D&plus;%5Cfrac%7B%28y-k%29%5E2%7D%7Bb%5E2%7D)

Rearranged into: ![\sqrt{b^2 \left(1 - \frac{(x-h)^2}{a^2}\right)} + k](https://latex.codecogs.com/gif.latex?%5Csqrt%7Bb%5E2%20%5Cleft%281%20-%20%5Cfrac%7B%28x-h%29%5E2%7D%7Ba%5E2%7D%5Cright%29%7D%20&plus;%20k)

```js
return Math.sqrt(Math.pow(b, 2) * (1 - (Math.pow(x - h, 2) / Math.pow(a, 2)))) + k
```

## Parabola (Horizontal)
Equation: ![(y-k)^2 = 4a(x-h)](https://latex.codecogs.com/gif.latex?%28y-k%29%5E2%20%3D%204a%28x-h%29)

Rearranged into: ![\sqrt{4a(x-h)} + k](https://latex.codecogs.com/gif.latex?%5Csqrt%7B4a%28x-h%29%7D%20&plus;%20k)

```js
return Math.sqrt(4 * a * (x - h)) + k
```

## Parabola (Vertical)
Equation: ![y - k = 4a(x - h)^2](https://latex.codecogs.com/gif.latex?y%20-%20k%20%3D%204a%28x%20-%20h%29%5E2)

Rearranged into: ![4a(x-h^2) + k](https://latex.codecogs.com/gif.latex?4a%28x-h%5E2%29%20&plus;%20k)

```js
return 4 * a * Math.pow(x - h, 2) + k
```

## Hyperbola
Equation: ![1 = \frac{(x-h)^2}{a^2} - \frac{(y-k)^2}{b^2}](https://latex.codecogs.com/gif.latex?1%20%3D%20%5Cfrac%7B%28x-h%29%5E2%7D%7Ba%5E2%7D%20-%20%5Cfrac%7B%28y-k%29%5E2%7D%7Bb%5E2%7D)

Rearranged into: ![\sqrt{ b^2\left(\frac{ (x - k)^2 }{a^2} \right) - 1} + k](https://latex.codecogs.com/gif.latex?%5Csqrt%7B%20b%5E2%5Cleft%28%5Cfrac%7B%20%28x%20-%20k%29%5E2%20%7D%7Ba%5E2%7D%20%5Cright%29%20-%201%7D%20&plus;%20k)

```js
return Math.sqrt(Math.pow(b, 2) * ((Math.pow(x - h, 2) / Math.pow(a, 2))) - 1) + k
```
