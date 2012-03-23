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
	a;u| banana$;1 | $;7 | na;z
	
In the third line, you have nodes with different parents: the description you will put at the
beginning of the line will refer to the leftmost node at the upper level (in this case *u*). We can change the parent node using
the symbol '@': the parent will become the next parent node on the right (in this case *v*). If the next parent node does not 
have child nodes, leave the description empty.
Third line will be: 
	$;6	|na;v @  @  @ $;5 | na$;3
	