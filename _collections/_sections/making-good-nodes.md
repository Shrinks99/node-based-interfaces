---
  title: Making Good Nodes
  layout: main
  collection: sections
---

## Making Good Nodes

### Consider your data type(s)

If you're using nodes we can reasonably assume that users have reason to manipulate data in your application in order to achieve a certain result, the question now becomes what _kind(s)_ of data are users manipulating?  If there aren't many different kinds of data to be manipulated or if this data shares similar characteristics it is definitely preferable to choose multi-in-single-out nodes where the entire dataset is passed through the graph and operated on when selected by the user.  As an example, in Nuke users create node-graphs to modify image data composed of different channels.  We can reasonably assume that most of the time they will be operating on the RGBA colour and alpha channels and that nodes will usually manipulate these by default, when they manipulate other data it is denoted by an input label.  For instances where users do not want to operate on RGBA data they can select other channels through a dropdown inside the node properties panel.

If users are constantly using many different data types to perform operations you may be forced to represent them as multi-in-multi-out nodes.  These nodes usually display their connections with sockets that denote the data type being passed between them, when data types correspond those nodes can be connected to each-other through those sockets.  As of version 2.92, [Blender's nodes can deal with 11 different colour coded data types](https://docs.blender.org/manual/en/2.92/interface/controls/nodes/parts.html#sockets), therefore Blender has chosen a multi-in-multi-out node system to allow nodes to deal with many different data types without forcing the user to constantly use dropdown menus or other methods after connecting a node to determine what values should be operated upon.

The issue with multi-in-multi-out nodes is that they are typically harder for users to arrange and it is more difficult to create a clear node graph because there is a greater chance of pipes crossing.  Multi-in-single-out nodes — while advantageous for node-graph organization and showcasing data flow — can also slow users if they constantly need to select data types in order to control nodes effectively.

If you can assume a single data type that users will be operating on most of the time _use multi-in-single-out nodes!_  If this would result in constantly selecting many different data types post-connection _use multi-in-multi-out nodes!_

Don't let interacting with the node graph be the bottleneck of operations per minute that an advanced user can achieve within your software!

### Sockets VS Pre-Extended Pipes

![A node with two pipe arrows protruding from the top and a node with 3 socketed inputs and one output socket.  Both nodes are not connected to others.](../img/sockets-vs-extended.svg)

Some node-based programs use sockets to define input connections, others extend existing pipes from the node to display unconnected inputs instead.  If your program uses multi-in, multi-out nodes you will likely be connecting pipes to different operators.  In most cases, this requires a socketed system to ensure that users are able to visually determine where the data they want to connect will go.

If your program uses multi-in, single-out nodes that pass along all data through the pipe it may be advantageous to avoid sockets all-together.  Sockets are typically quite small and have less clickable area than pre-extended pipes, pre-extended pipes with labels can make the experience of connecting nodes together quicker due to their larger clickable area.

Both sockets and pre-extended pipes can run into similar issues when complex nodes demand many inputs, especially in a multi-in, single-out system where the size of nodes is typically more uniform both vertically and horizontally.

### Displaying data on nodes

While node-graphs contain an infinite (or at least _very_ large) amount of space, a user's screen does not have an infinite amount of resolution.  This means that there will be a scale that most users will find to be the most comfortable when working with nodes in your application.  At this scale it should be clear what each node does—displayed by colour, shape, or otherwise—and probably what each node is named.  Some node based applications may display other indicators on the node such as using coloured outline to denote their stage of processing, or a badge to display types of data flowing through the node.

Because nodes are typically of a fixed or semi-fixed size it can be tricky to balance information density and user customization with aesthetics.  Some applications typeset text so it overflows the node's body, others will constrain it or change its shape in order to conform to the content.  If you are creating a multi-in-single-out system your nodes should more or less be the same size, at least in one dimension.  Depending on how graph organization is intended this dimension could be either the X or Y dimension though typically multi-in-single-out systems organize vertically.  If you are creating a multi-in-multi-out system you may be comfortable with expanding the node's shape more because it already needs to expand to multiple different height values depending on the amount of inputs and outputs.

For multi-in-multi-out nodes create a clear way of displaying data types to the user on each node, this is typically done with colour, shapes, or a mix of both.  If your application has a properties panel and does not display the controls on the node, consider extending this display system to your properties panel to link the property to the graph's IO system in addition to labeling it.

Pay attention to the sizes at which information is visible, focus on your typesetting, and optimize for clarity and function.

### Displaying controls on nodes in multi-in-multi-out systems

![An example multi-in-single-out node graph with three nodes simply connected in sequence.](../img/controls-on-nodes.svg)

Displaying controls on nodes instead just a label _can_ reduce the friction between hooking up nodes and editing properties, especially when there are many different inputs.  Be warned that as your property editor interfaces become larger and more complex, the sizes of your nodes in the graph will become less uniform, which will likely present another organizational hurdle for users.