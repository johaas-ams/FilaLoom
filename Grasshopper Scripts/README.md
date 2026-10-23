# Grasshopper Scripts

This document gives a short overview of the computational workflow for each of the Grasshopper scripts.

## Vertical woven objects

The Grasshopper script which generates GCode for printing vertical woven objects takes a lofted surface as the input geometry. It then generates vertical skeleton curves projected onto this surface, which define the warp pillars. Horizontal planes are constructed at each height where weaving occurs, these intersect the skeleton curves at a single point each, defining the anchor points. From these, the weaving toolpath is created as a curve which arcs between these anchor points, and the printing toolpath is created by generating horizontal circles at each layer height (0.4mm in our script) along the vertical skeleton curves. These toolpaths are then converted into GCode, sequenced in the correct printing order, and merged, outputting a ready-to-print GCode file.

## Planar semi-woven textiles

The script for fabricating planar semi-woven textiles takes two curve inputs: a closed planar curve defining the outline of the textile and a network of planar curves defining the warp layout, as well as a number input defining the spacing between adjacent yarns. The script then draws lines along the X axis with this defined spacing whose intersection with the outline curve define anchor points. The weaving toolpath is then created by generating a curve which arcs around these anchor points in a zigzag pattern. The printing toolpath is created by combining the outline and warp curves, as well as generating a stack of horizontal circles at each anchor point to print the anchors. Lastly, these toolpaths are converted into GCode, sequenced in the correct order, and combined into a complete printable GCode file.

## Loop-based spacer fabrics

The script to generate GCode for loop-based spacer fabrics uses a fixed linear layout for the weaving and printing toolpath, which matches up precisely with the weaver tool (this tool can be found in the script itself and downloaded to a printable STL). These toolpaths are converted to GCode and sequenced in the correct order. The user can determine the height of the loops by tuning the extrusion value.

## Yarn textures

The Grasshopper script to generate GCode for embedding yarn textures takes a geometry and a surface input. The surface input determines the textured area in the geometry. The script then generates the weaving path, and modifies the base geometry to include anchors for the yarn to weave through. The printing GCode is generated using a normal slicer, after which the weaving sequences should be manually inserted in a text editor. Note that this script is mainly used to develop demonstrators and show off the principle of embedding yarn textures. It is less robust than our other scripts.

## Cable-driven mechanisms

To fabricate cable-driven mechanisms with FilaLoom, one first models a cable-driven geometry, and models a curve running through this geometry. These are then inserted into a Grasshopper script. The curve defines the toolpath the yarn takes; the user should draw this curve so that it runs through the motion primitives and its ends are inside the fixed ends of the geometry. This curve is used to generate the weaving GCode. The script also modifies the geometry by cutting a channel through the motion primitives through which the yarn can be woven, and places anchors at the ends of the curve. The geometry is then exported and sliced, after which the weaving sequence should be manually inserted into the GCode.
