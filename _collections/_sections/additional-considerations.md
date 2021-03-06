---
  title: Additional Considerations
  layout: main
  collection: sections
---

## Additional Considerations

### Node-Graph Interaction

Chances are if you're making a piece of node-based software your users will be adding, connecting, and removing nodes from the graph _a lot_.  Most node-based software implements a text-based search system where advanced users can hit a hotkey and start typing to search for the node or function they want to add or complete.  This is _great_ and allows users to rapidly add nodes to the graph.  New users may prefer to look through an organized menu of nodes based on their category, this is also valuable as command based search systems aren't always ideal for discovery—consider implementing both options.

How fast can I create, connect disconnect, and delete nodes from my application's graph?  Is it difficult to connect pipes?  Can these processes be made easier and faster?  Can I easily add and remove nodes from the middle of the graph?  All of these are good questions to ask yourself when designing and programming your node-graph and will pay dividends when other users are interacting with it.  

Don't let interacting with the node graph be the bottleneck of operations per minute that an advanced user can achieve within your software!

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