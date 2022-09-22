---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Sky22"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2022-09-20T19:32:42+01:00
lastmod: 2022-09-20T19:32:42+01:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
## Midland Sky 2022 Launch

```python
import numpy as np
from bokeh.plotting import figure, show, output_notebook
from bokeh.models import LinearAxis, Range1d
```

```python
data_file = "220918_midland_sky.csv"
output_notebook()
```

<div class="bk-root">
        <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="2337">Loading BokehJS ...</span>
    </div>

```python
d = np.loadtxt(data_file, delimiter=",", dtype=float)
x = d[:,0]
y = d[:,1]
v = d[:,2]

# create a new plot with a title and axis labels
p = figure(title="Flight data", x_axis_label='time', y_axis_label='altitude')

p.circle(x, y, legend_label="flight", color="red", line_width=.5)
p.extra_y_ranges = {"gee": Range1d(start=-7, end=7)}
p.line(x, v, legend_label="gforce", color="blue", line_width=1, y_range_name="gee")
p.add_layout(LinearAxis(y_range_name="gee"), 'left')
show(p)
```



<div class="bk-root" id="bd97cab6-c970-47c7-890a-e080d330b30e" data-root-id="6875"></div>






```python

```
