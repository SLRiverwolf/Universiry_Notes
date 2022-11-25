![[multilevelIndex.jpg]]

Could reduce the size of the index until it fits into the memory.

Types of MultiLevel Indexes
- B Tree
- B<sup>+</sup> Tree

## B Tree And B<sup>+</sup> Tree
- M way search tree
	- node can have max (M-1) keys.
	- Key have the pointer to a record while the others have pointers to children nodes(blocks with child index)
	- right side only larger values and left side only smaller values
- B tree is A M way search tree with  some rules(M = number of max children)
	- Every leaf must be at same level
	- every node(except root) must at least have M/2 (rounded off to up) children
	- Root can have min of 2 children
	- creation process is bottum up
![[B tree_sketch.png]]

![[B tree.png]]


- B + tree
	- difference is that, keys doesn't have record pointer with them on upper levels. Copy of the key goes down from right side(right side becomes greater than or equal). Record pointers are only available in leaf nodes.
![[BPulsTree_sketch.png]]

![[indexes_BPulsTree3_level.png]]

	![[BPulsTree.png]]


- When inserting data, after maximum key limit exceeds take the median element(considering with the new element) to the upper level and split the older index
- We shouldn't repeat the data in the internal nodes in B<sup>+</sup> trees. Repeating in the leaf nodes is enough.