---
title: "Nose Cone Detail"
toc: true
type: book
date: "2021-05-05T00:00:00+01:00"
draft: false
url_code: "https://github.com/rlhatcher/rocketry_notebooks/blob/master/phoenix_nosecone.ipynb"
---

![Nose cone cut-away view](scale_nose_v14.png "cutaway")

## Define the nose cone shape

Comparing several different shapes with the original drawings of the nose cone, the Haack shape visually fit best. That choice would make sense from an engineering standpoint particularly with an L/D shape to minimize drag.

### Haack series

Wikipedia gives a [good description of the series](https://en.wikipedia.org/wiki/Nose_cone_design#Haack_series)

>Unlike many other nose cone shapes, the Haack Series are mathematically derived for the purpose of minimizing drag. While the series is a continuous set of shapes determined by the value of $C$ in the equations below, two values of $C$ have particular significance: when $C = 0$, the notation $LD$ signifies minimum drag for the given length and diameter, and when $C = {1 \over 3}$, $LV$ indicates minimum drag for a given length and volume. The Haack series nose cones are not perfectly tangent to the body at their base except for the case where $C = {2 \over 3}$. However, the discontinuity is usually so slight as to be imperceptible. For $C > {2 \over 3}$, Haack nose cones bulge to a maximum diameter greater than the base diameter. Haack nose tips do not come to a sharp point, but are slightly rounded.

Based on that, we're looking for a Von Kármán shape.

$\theta = \arccos \Bigl(1 - {2X \over L}\Bigr)$

$y = {R \over \sqrt{\pi}} \sqrt{\theta-{\sin({2\theta})\over2}+C \sin^3({\theta})}$

Where: $C = 0$ for LD-Haack (Von Kármán)

## Python and OpenSCAD

The [Jupyter Notebook](https://github.com/rlhatcher/rocketry_notebooks/blob/master/phoenix_nosecone.ipynb) shown here is available in my [notebooks repo](https://github.com/rlhatcher/rocketry_notebooks)

The notebook leverages several common packages such as matplotlib, numpy for data handling and 2D graphing and some less-common packages viewscad, solidpython and OpenSCAD for 3D rendering.

Our first step is to import these packages.

```python
import matplotlib.pyplot as plt
import numpy as np
import viewscad
from solid import *

L = 408 # length base to tip
R = 95  # radius at base
S = 94  # shoulder diameter
M = 50  # mount length

# define an x axis the same length as the nose cone
x = np.linspace(0, L, int(L))

C = 0

f = lambda x: (R/np.sqrt(np.pi))*np.sqrt((np.arccos(1 - (2*x)/L)) - (np.sin(2 * (np.arccos(1 - (2*x)/L))))/2 + C * np.sin((np.arccos(1 - (2*x)/L)))**3)
y = f(x)

zero = np.array([0])
xplt = np.concatenate((zero, x, zero))
yplt = np.concatenate((zero, y[::-1], zero))

plt.axes().set_aspect("equal")    
plt.plot(xplt, yplt)

points = np.vstack((yplt, xplt)).T
```

The smoothing factor defines the number of segments used to render objects. As is often the case, the larger the number the more processing is required. I find 100 provides enough detail for practical use.

```python
SMOOTH=100
```

We can pass the pints to OpenSCAD now to rotate around an axis as a solid.

```python
r = viewscad.Renderer()
p = rotate_extrude(360, segments=SMOOTH)(polygon(points))
if S != 0:
    p += translate([0, 0, -S])(cylinder(r=S, h=S, segments=SMOOTH))
        
if M != 0:
    p -= translate([0, 0, -S])(cylinder(r=M, h=S, segments=SMOOTH))

r.render(p, outfile='./phoenix_haak.stl')
```

```python

```
