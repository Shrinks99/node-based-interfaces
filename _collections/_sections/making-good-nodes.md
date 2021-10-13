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

### Node-Graph Interaction

Chances are if you're making a piece of node-based software your users will be adding, connecting, and removing nodes from the graph _a lot_.  Most node-based software implements a text-based search system where advanced users can hit a hotkey and start typing to search for the node or function they want to add or complete.  This is _great_ and allows users to rapidly add nodes to the graph.  New users may prefer to look through an organized menu of nodes based on their category, this is also valuable as command based search systems aren't always ideal for discovery—consider implementing both options.

How fast can I create, connect disconnect, and delete nodes from my application's graph?  Is it difficult to connect pipes?  Can these processes be made easier and faster?  Can I easily add and remove nodes from the middle of the graph?  All of these are good questions to ask yourself when designing and programming your node-graph and will pay dividends when other users are interacting with it.  

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

### Store graph data as plaintext!

Node-graphs allow users to create complex effects that can be applied to any input, it's especially useful to be able to share them effectively!  Blender has a large community of artists online however as of 2.92 whenever somebody creates something with nodes in the program they often share it with people _by posting an image of the node graph._  Blender users cannot copy and paste the graph data outside of the program or even between separate files.  Conversely, other node based applications (Nuke, Natron, Olive) _do_ store their graph data as plaintext, this has two key advantages for users.

1. Sharing project data! <br/> <br/> Plaintext data storage means that node-graph data can easily be copied and shared outside of the application, no need to save a new project file and import it every time you want to copy one node from another project (of course this should still be a way to import graphs). With plain text data storage users can easily share their projects — or parts of them — to the web or with other colleagues.  Moving data around inside your application is great, moving it around outside of your application with plaintext means that is easier for users to build their own tools and use your application as a platform instead of creating all graphs on a per-project-file basis.

2. Debugging! <br/> <br/> People aren't perfect, software isn't perfect, bugs are going to happen!  Saving project files as plaintext allows users to open the project in a text editor and begin the process of sorting out what node is breaking their project file.  Coupled with good logs this process shouldn't be terribly difficult for people to do!  Some node-based software has its own syntax for defining text-based file structure, others just use XML.  Whatever your application ends up using it shouldn't be terribly difficult to create a syntax that is relatively quick to parse as all node-graphs are just made up of smaller component parts and act with a hierarchy.

### Consider graph organization

Is a node-graph the primary way that users create content within your application?  If so users may need to maintain a mental model of what they have created and organize it in a way that makes sense to them.  Auto-layout systems may not work well for users if they are developing complex graphs that require hundreds of nodes to achieve desired effects.

Does your node-graph exist primarily to show data flow of content made with other parts of your interface and _isn't_ the primary way of interacting with your application?  You may be able to rely more heavily on an automatically laid-out graph, especially if interacting with the graph isn't the only way to manipulate data within your application.  If the node-graph is a secondary part of your application it may actually be advantageous to lay it out automatically, as taking the manual approach may lead to lower operations executed per second by the user.  If the scope of nodes in your application is limited and your users aren't going to be laying out hundreds or even tens of nodes, an auto-layout system can also make sense to speed up workflows.

Node graphs aren't bound by the same restrictions that other UI components have.  Because of the seemingly infinite workspace and ability to zoom the graph that users are typically afforded with other UI elements, hiding sections of the graph that are created by users as part of their process isn't really positive in most cases.  Graph components like node backdrops may be a helpful way of visually grouping nodes to serve the same function as a group would in a layer-based system.  Actual group nodes usually act as individual contained tools so users aren't required to constantly hide the main graph and jump in and out of them to do their work.

### General best practices

1. Expose low-level access to data transformation abilities to the user! <br/> <br/> This is an asset, it allows users to build complex effects!  When manipulating data with destructive workflows these low level abilities can be painful to use because of the amount of time they take to execute in order to achieve desired effects.  Because nodes can be constructed into more complex groups and copied separate from their inputs as mentioned previously, users can build out their own toolsets (or use community created and pre-packaged grouped effects) and create amazing things with your software.

2. Remember trackpad users!  <br/> <br/>  Lots of node-based software works really well with a mouse and relies on middle-mouse to move the graph around, middle mouse doesn't exist on trackpads!  Your application may be aimed at people that will be mostly working on desktops with mice or trackballs but it _will_ be used by somebody with a laptop at some point.  This advice is absolutely not limited to node-based software but it IS a personal gripe of mine.