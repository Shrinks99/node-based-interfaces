---
  title: Nodes in Maya
  layout: main
  collection: casestudies
---

## Maya 2019 (Hypershade Editor)

##### Multi In, Multi Out

Maya is a 3D DCC that serves a similar generalized use case comparable to Blender.  While Maya actually uses node-graphs for multiple different parts of the software this case study will focus on the Hypershade editor.  Each node in this editor represents an action that manipulates or creates shader material information that will be applied to a 3D object or volume.

### Anatomy of Maya's Hypershade Nodes

![Maya's hypershade node states](../img/casestudies/maya/Maya-node.png)

Maya's default Fractal Noise 2D texture will generate a fractal noise pattern that can be applied to materials which cover 3D objects.

Nodes in Maya are labelled with a unique identifier located directly atop the node in the graph.  Below this they display their identifying icon at the top left of the node.  Beside this on the right there are two controls, one marked with an 'S' allows users to "solo" the node and output its results directly rather than just outputting the full result of the graph.  The second control has three states, shown left to right they are as follows: recommended inputs & outputs, fully collapsed, connected inputs & outputs, and all inputs & outputs.  When this is set to either display connected only, or display all, a search box appears directly below the multi-state button allowing users to quickly find the parameter they are trying to connect.  Because these nodes expose every property as a socket, complex nodes can be very tall.

#### Sockets in Maya

![Maya's socket selection shortcut](../img/casestudies/maya/Maya-dropdown.png)

Like Blender, sockets in Maya are represented as coloured circles with the fill colour assigned by data type.  The larger white sockets present in the top section of each node allow users to select from a menu of inputs and outputs to quickly find and connect a parameter, even if it is not currently visible if the node is minimized.  Sockets are always displayed in alphabetical order when a node is fully expanded.

Sockets can also have multiple different grouped properties of the same data-type, this is commonly used for RGB colour data where users will only need to connect a single pipe between nodes and can expand to show the individual channels.  In this screenshot of the fractal node, we can see that both the "Out Alpha" and "Out Color" sockets both share the same data-type (a floating point number) but whereas "Out Alpha" is only composed of one channel, "Out Color" is composed of three.

### Maya's Hypershade Node-graph

![A typical node-graph in Maya](../img/casestudies/maya/Maya-graph.png)

Like Nodebox, pipes in Maya are curvy and automatically laid out by the software and are coloured according to their data-type.  Pipes in Maya also have directional indicators that appear when there is space to display them.

![Three states of pipe rendering in Maya](../img/casestudies/maya/Maya-pipe-rendering.png)

Unlike Nodebox, pipes are rendered behind the node unless that node is being moved or selected.  The above image displays these three states that a node or pipe can exist in, the leftmost group is already connected and the pipe is rendered behind the nodes, the middle group has the fractal2 node selected, any pipes that are connected to it will be rendered above the node to make their connections clear, the rightmost group is currently being connected and it's pipe is marked in yellow as it is dragged into place until the user has let go of the cursor.

Maya does not contain backdrops or a system of grouping Hypershsade nodes into sub-networks.

#### Editing properties in Maya

![Maya's properties panel](../img/casestudies/maya/Maya-properties.png)

Maya's properties panel allows users to set the values of unconnected parameters.  This window also allows users to change the node's name and view a larger version of the node icon to visually link the panel to the graph.  The checkered box beside each parameter also acts as a shortcut allowing users to quickly add a node and automatically connect it to the property the user clicked on.

### Other Points of Interest

Maya has an auto-layout button that will re-arrange a graph for the user, it does seem not optimize the graph for uncrossed pipes.

Maya's node-graph Can optionally have a grid with the ability to snap nodes to it.

![](../img/casestudies/maya/Maya-example-graph.png)

Node icons in Maya can be displayed as dynamic swatch images.  This graph represents a fractal noise pattern that has had its base colour manipulated by another node.  Note that the preview icon it uses as well as the icon of the colorConstant1 node are set to display the output of these nodes.
