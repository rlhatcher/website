---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Open Source Rover"
date: 2021-10-03T20:41:59+01:00
summary: ""
authors: []
tags: []
categories: []
type: book

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/ronald_hatcher
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

The [JPL](https://www.jpl.nasa.gov/) Open Source rover is an open source, build it yourself, scaled down version of the 6 wheel rover design that JPL uses to explore the surface of Mars. I have recently completed the build of this rover, which was rally a challenge! Interestingly, the software was one of the more challenging aspects of the build, which was unexpected since I've been working with software for more than 30 years!

The build is pretty well [documented](https://github.com/nasa-jpl/open-source-rover) but I did run across a few bumps in the road.

{{< youtube Vp9dJ5upceo >}}

For convenience, the table here provides the overall specifications

| Attribute              |Value [imp] | Value [SI] |
| ----------             |-----      | -------------  |
| Weight                 | 25 [lbs]    | 11.34[kg]        |
| Footprint              | 24x14 [in]  | 60.96x30.48 [cm] |
| Battery Capacity       | 5200 [mAh]  | 5200 [mAh]       |
| Battery Discharge Rate | 8 [A]       | 8 [A]            |
| Nominal Current Draw   | 1.2 [A]     | 1.2 [A]          |
| Operating time (continual use)        | 5 [hrs]   | 5 [hrs] |
| Approximate Max speed  | 9.7 [in/s]  | 24.6 [cm/s]      |
| Max 90 deg vertical scale | 12 [in]   | 30.48 [cm]      |
| Max height differential between sides | 14 [in] | 35.56 [cm] |
| Communication (in this guide) | Bluetooth app (Android only) and Xbox Controller| |
| Cost                   | ~ $2,500     |                 |

## Building the source

Building the ROS source on the Pi3 is a **giant** pain in the neck. The [software steps](https://github.com/nasa-jpl/open-source-rover/blob/master/Software/Software%20Steps.pdf) provide links for:

* [Direct downloadable Raspbian Stretch image](https://downloads.raspberrypi.org/raspbian/images/raspbian-2019-04-09/2019-04-08-raspbian-stretch.zip)
* [Custom JPL image with both Raspbian Stretch and ROS pre-built](https://drive.google.com/drive/folders/1RbYWDRthpcktqkPEHb7qVqDiy27EiAc1)

Downloading the pre-built image is **much** easier but also fat less of a challenge. I found that going through the [build process](http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi) was really helpful in understanding the whole structure of the software elements and greatly helped in subsequent troubleshooting.

As noted in the build process docs, you **absolutely** need to add swap to the Pi and using an external drive is the best option. I had to add swap on the main SD card it the whole build took about 20 hours to complete!
