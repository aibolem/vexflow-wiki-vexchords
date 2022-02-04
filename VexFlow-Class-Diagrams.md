See `vexflow/tools/` for scripts to generate dependency diagrams.

```sh
brew install graphviz imagemagick ghostscript
cd vexflow/tools

# Make SVGs
./dependency_graph.rb --dependencies | dot -T svg -o graph_dependencies.svg 
./dependency_graph.rb --inheritance  | dot -T svg -o graph_inheritance.svg 

# Make PNGs
./dependency_graph.rb --dependencies | dot -T png -o graph_dependencies.png 
./dependency_graph.rb --inheritance  | dot -T png -o graph_inheritance.png 
```

The [dependency cruiser](https://github.com/sverweij/dependency-cruiser) package can generate graphs where edges highlight on hover:

```sh
npm install -g dependency-cruiser

cd vexflow/
depcruise -T dot entry/ | dot -T svg | depcruise-wrap-stream-in-html > dependency-graph.html
```


[Generated on 2022-01-03](https://imgur.com/a/gBR1RLj)


[Generated on 2020-04-08](https://imgur.com/a/gBR1RLj)

* [Class Hierarchy](https://i.imgur.com/MyUl5HN.png)

* [Imports](https://i.imgur.com/7gGkS5s.png)


[Generated on 2016-06-16](https://imgur.com/o3ADoE4.png)

Blue lines are **uses** relationships (class A imports / uses class B).

Brown lines signify inheritance (class X extends class Y).
