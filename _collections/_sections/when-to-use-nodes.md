---
title: When To Use Nodes
layout: main
collection: sections
---

## When To Use Nodes

This guide is written with some bias toward node-based applications.  As mentioned in the foreword section, I like nodes, they work in a way that my brain finds easy to understand and I enjoy their non-destructive properties.  Keep my personal preferences in mind while assessing the content of this section and considering if nodes are the best fit for your application.

As mentioned in previous sections, node-based software typically allows users to create complex results out of many simple and contained operations.  If this sounds like the type of software you're developing, a node-based interface may be for you!

If your application has any sort of one-dimensional layering system, consider the extra power for users that could be afforded by using a node-graph instead.  This also applies to any other hierarchical data structures within your application, if these data structures need to be represented and displayed to the user a node-graph may be the best way to do so.

### When Not To Use Nodes

Building on the point above, if having hierarchical data accessible in two dimensions is not useful, use a layering system instead!

[Node-based interfaces can get pretty dense!](https://scriptsofanotherdimension.tumblr.com/)  Due to their near-infinite workspace and the user-organized nature of most node-graphs, implementations of nodes typically allot a significant portion of screen real-estate to the node editor.  For this reason, I would recommend against the use of nodes for mobile applications focusing on simplicity.  There are undoubtably some great mobile node-based applications — [Nintendo's Game Builder Garage](https://www.youtube.com/watch?v=9obygTJVG_g) is one innovative example — however I don't believe nodes offer the same utility (non-destructive editing and display of complex operations) on phones that they do on the desktop or tablets.  In short, I don't believe that most people are trying to perform the types of tasks that nodes do best using their phones.

Node-based interfaces are uncommon in software today (2021).  Maybe all the kids that grow up with Game Builder Garage will be more familiar with them, but all of my experience and attempts to introduce nodes to my peers have resulted in some initial confusion.  If your target demographic doesn't require the power offered by nodes and your application wouldn't benefit from them, don't use them!  Like any UI element nodes are best implemented when required, and more specifically when they play a large role in the function of your application.  If your application requires this complexity know that its appeal will likely be limited to those who are willing to learn new tools knowing that it will help them produce better work.