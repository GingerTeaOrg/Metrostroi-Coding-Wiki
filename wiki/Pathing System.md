# Metrostroi's Node Pathing System

Metrostroi keeps track of trains by registering a pathing coordinate system along the track. The coordinate system is essentially a one-dimensional linear graph, 
consisting of a chain of points, called "nodes", which can be recorded using metrostroi's track editor.

## Basics Of The Track Editor

In order to understand the pathing system, it's best to go to an existing Metrostroi map and open the track editor. To do this, you can type the command ``metrostroi_trackeditor`` into the console.
It's recommended to bind that command to a free key if you haven't already, for easy access.
Once you've opened the track editor, press "load" in oder to load the track definition file. You should now see a visual representation of the node network. If not, click "Hide/Show Nodes".

You'll now see a table populated in the window. There are the columns "ID" and "Nodes" for each row. The "ID" refers to a "path", which is a complete chain of connected nodes, while "Nodes" tells you how many nodes are in one path chain.

Under the hood, these paths are organised in a global table under ``Metrostroi.Paths``. The structure of that table is as follows:

```
Metrostroi.Paths = {
  [1] = { -- path id
          [1] = { vec = "0.117188 512.388184 0.202881",
                  dir = "0.007341 0.999973 -0.000060",
                  id = 1,
                  length = 1.908121030426,
                  next = --reference to the next node in the chain --
          [2] = { --and so on}
}
```


-- TO BE CONTINUED
