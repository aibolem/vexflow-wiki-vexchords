See `vexflow/tools/` for scripts to generate dependency diagrams.

# Interactive Graphs
We use [dependency cruiser](https://github.com/sverweij/dependency-cruiser) to generate interactive graphs. Mouse over an edge to highlight &amp; show the dependency in a tooltip. Click a node to see the source file on GitHub:

```sh
cd vexflow/

./tools/dependency_graph.js
```

The HTML pages are saved to the `vexflow/graphs/` directory. The following graphs were generated on Feb 4, 2022:
* [src/](https://vexflow-dependency-graphs.surge.sh/src.html)
* [entry/](https://vexflow-dependency-graphs.surge.sh/entry.html)
* [tests/](https://vexflow-dependency-graphs.surge.sh/tests.html)

You can also call the dependency cruiser on the command line:

```sh
cd vexflow/

mkdir -p graphs

depcruise -T dot src/ | dot -T svg | depcruise-wrap-stream-in-html > graphs/src.html
```


# Static Graphs

```sh
brew install graphviz imagemagick ghostscript
cd vexflow/tools

# SVG graph of the class hierarchy.
./dependency_graph.rb --inheritance  | dot -T svg -o graph_inheritance.svg 

# SVG graph of the imports / chain of dependencies.
./dependency_graph.rb --dependencies | dot -T svg -o graph_dependencies.svg

# To make PNGs, replace svg with png in the above commands.
./dependency_graph.rb --dependencies | dot -T png -o graph_dependencies.png
./dependency_graph.rb --inheritance  | dot -T png -o graph_inheritance.png

# To make PDFs, replace use the pdf extension.
./dependency_graph.rb --dependencies | dot -T pdf -o graph_dependencies.pdf
./dependency_graph.rb --inheritance  | dot -T pdf -o graph_inheritance.pdf
```

Blue lines are **uses** relationships (class A imports / uses / depends on class B).

Brown lines signify **inheritance** (class X extends class Y).


[Generated on 2022-02-04](https://imgur.com/a/o3Gim3b) with VexFlow 4.


[Generated on 2020-04-08](https://imgur.com/a/gBR1RLj) | [Class Hierarchy](https://i.imgur.com/MyUl5HN.png) | [Imports & Dependencies](https://i.imgur.com/7gGkS5s.png)


[Generated on 2016-06-16](https://imgur.com/o3ADoE4.png)
