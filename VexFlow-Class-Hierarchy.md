### To Generate

    $ brew install graphviz imagemagick ghostscript
    $ cd tools; ./graph.rb | dot -Tpdf -o graph.pdf
    $ convert -density 300 graph.pdf -resize 25% graph.png

![image](https://i.imgur.com/IrSxyBD.png)