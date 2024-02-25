I think this is a good enough project to display the addition of vectors with matrix and spans involved

`seedVectorIntro()` is used to initialise sketch (from the p5.js library)
`basis()` uses `i` and `j` as it's vectors. i.e. `R2`
`epoch` defines the millisecond response required (more like specified)

the radius of the vector is restricted to '200' with vectorRadius()
vector variable initialises the `vec2()` function through the math library
`followMouse(sketch, vector, maxVectorLen, 10, zeroThreshold)` updates through the mouse location with the specified parameters.
`vecNorm(vector)` calculates the magnitude of the vector
`normRounded` just rounds up the value calculated
direction computes the angle through `Math.atan2()` function [in radians]

```
dirArrow.style.transform = rotate(${direction}rad)

```

helps rotate the vector directly


vectorPositions stores the locations of multiple vectors
numberVectors defines the number of vectors (count)
`vectorPositions = generateVectorsCircle(150, numberVectors)` arranges the vectors generated in a circular position

```
vectorPositions.forEach(pos => {
    drawVectorOrZero(sketch, vector, isZero, COL_PINK, pos, font_, "v", "0")
})

``` 

loops through each vecor positions with

`drawVectorOrZero()` telling to draw multiple vectors if possible

`sketch.preload()` loads the `canvas dimensions, screen center, fonts, and epoch time` in advance
`sketch.setup()` initiates the two vectors v1 and v2 with random angles and lengths

```let p5vectorAddition = new p5(seedAddition, "vectorAddition")``` 

joins the drawing to the html id "vectorAddition"

Vector Scaling Logic:

Mouse coordinates are used to determine the target position for the vectors.
The vectors are scaled using linear interpolation (`sketch.lerp`) towards the target position.
Vectors are clamped to a maximum length (`maxVectorLen`).
A regular vector is calculated using a fixed length (`regularLen`).

Vector Coordinates Logic:

The vector's position is adjusted based on the mouse position using the followMouse function.
The rounded coordinates of the vector are calculated for display.
Drawing Functions:

Functions like:
 
`drawVectorOrZero()`, 
`drawColumnVector()`, and 
`drawGrid()` 

are used to draw vectors, matrix columns, and a grid on the canvas.

Drawing Functions:

The `drawVectorText()` is used to draw vectors along with text labels.

Vector Visualization:

The canvas background is cleared, and translations are applied.
Unit vector i (î) is drawn in red, and unit vector j (ĵ) is drawn in green.
The vectors are labeled with "î" and "ĵ" respectively.

```
sketch.preload = () => {
    // Set canvas dimensions and center
    sketch.canvasWidth = 550;
    sketch.canvasHeigth = 570;
    sketch.screenOx = sketch.canvasWidth/2;
    sketch.screenOy = sketch.canvasHeigth/2;
    normalFont = sketch.loadFont("assets/lexend-regular.ttf");
    boldFont = sketch.loadFont("assets/lexend-bold.ttf");
    epochTime = sketch.millis();
}

```

The preload function sets canvas dimensions, loads fonts, and initializes the epochTime.


```
let basis = {
    i: vec2(1, 0),
    j: vec2(0, -1)
}

```

```
let vectorsRadius = 200
let epochTime
let normalFont
let boldFont
let vec
let vectorBasisCoords
let spanVectors
let iVec = 6
let lerpSpeed = 10
let animSpeed = 0.7
let t = 0
let timeBetweenVectors = 1.5
const maxVectorLen = 200;
```

Variables for basis vectors, radius, fonts, vectors, and animation-related parameters are declared.



In the span.js file

```vec = vec2((Math.random()-0.5)*200, (Math.random()-0.5)*200);```

generate a random vector

```let det = basis.i.x*basis.j.y - basis.j.x*basis.i.y
vectorBasisCoords = vec2(
    ( basis.j.y*vec.x - basis.j.x*vec.y)/det,
    (-basis.i.y*vec.x + basis.i.x*vec.y)/det
)
```

The determinant (det) of the basis is calculated to be used in the transformation of the vector into the new basis (vectorBasisCoords). This step involves applying the inverse of the basis matrix to the vector.

