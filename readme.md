# Treepy #

Treepy is a python script compiling a simple text representation of a tree in a 
pretty latex figure.

Let's say you want to draw this tree:


![Banana tree](https://github.com/diegoceccarelli/treepy/raw/master/examples/banana.png)

Then you should create a txt file where each line describes a level of the tree, starting 
from the root:

	line 1: v

in the second line you want to describe 4 nodes. Each node description is separated by the others
with the symbol '|' and contains the label of the incoming edge (if any) and the label of the node,
encoded with this syntax: 
	
	[label of the incoming edge] ; [label of the node]

then the second will be: 
	
	line 2: a;u| banana$;1 | $;7 | na;z
	
In the third line, you have nodes with different parents: the description you will put at the
beginning of the line will refer to the leftmost node at the upper level (in this case *u*). You can change the parent node using
the symbol '@': the parent will become the next parent node on the right (in this case *1*). If the next parent node does not 
have child nodes, leave the description empty.
Third line will be: 
	
	line 3: $;6	|na;v @  @  @ $;5 | na$;3

Same for the fourth level/line, you have to specify the parent for each description, considering the node that you 
created in the previous level: the previous level contains four nodes and only the second has child, then:

	line 4: @ $;4| na$;2 @ @ 

## Producing the latex ##

The final txt describing the tree will be: 

	v
	a;u| banana$;1 | $;7 | na;z
	$;6	|na;v @  @  @ $;5 | na$;3 
	@ $;4| na$;2 @ @ 

(you can find it in [example/banana.dat](https://github.com/diegoceccarelli/treepy/raw/master/examples/banana.dat) ). 
In order to produce the latex simply exec:

	./treepy.py banana.dat

Treepy will print the latex on the standard output. The output can be directly compiled with pdflatex, 
or you can copy the snippet with the tree in your latex file:

	%start from here
	\begin{tikzpicture}[
	grow=down,
	level 1/.style={sibling distance=5cm,level distance=4cm},
	level 2/.style={sibling distance=3cm, level distance=2cm},
	level 3/.style={sibling distance=2cm, level distance=2.5cm},
	kant/.style={text width=2cm, text centered, sloped},
	every node/.style={text ragged, inner sep=2mm},
	punkt/.style={circle, shade, top color=white,
	bottom color=white, draw=black, very
	thick }
	]
	\node[punkt] {v} 
	[...]
	\end{tikzpicture}
	%end here
	
The tree is drawn using the [tikz package](http://www.texample.net/tikz/). 
You will have to import the package *tikz*.
As you can see the preamble of tikzpicture allows you to personalize your tree
(e.g., changing the distance between siblings and levels). Please refer to the tikz 
manual for more informations. 

[Diego Ceccarelli](http://www.di.unipi.it/~ceccarel) 2012


	