
Tracks and Switches, Patricia Trie based Map
--------------------------------------------
A flexible patricia trie implementation for Java offering rich features and prefix-related operations. It implements the [NavigableMap](http://docs.oracle.com/javase/6/docs/api/java/util/NavigableMap.html) interface and can use any kind of object for keys as long as they can be compared bitwise via a specialized `BitwiseComparator`. It has relative performance in comparison with [TreeMap](http://docs.oracle.com/javase/6/docs/api/java/util/TreeMap.html), has as good memory footprint, and can be used as a complete replacement.

This project was inspired by an existing patricia trie implementation by Roger Kapsi and Sam Berlin at <https://github.com/rkapsi/patricia-trie>; hence, there is a similar XOR metric nearness query operation.

Tree Design
===========
It uses a very different algorithm than most conventional Patricia Trie implementations, that I would like to originally call "**Tracks and Switches**", because nodes are treated as tracks with many alternative bit routes called switches:

	--=
	  0
	  0------=1
	  1       0
	  0--=1   0-------=1
	  0   0   0        0----=1
	          +-=--=   0     0
	            1  0   +-=   0
	            0  1     0
	            0  0     1

> Note that all middle switches are 1-bits (and appears only in the middle of the track). A 0-bit switch can only appear in the end of a switch list with an index set to the end of the track. Also, only 1 middle switch at a time can be assigned to an index, whereas the end of the track can have 2, a 1-bit and a 0-bit switch. The end switches are also referred to as edge switches in the source code. In comparison with a node in a basic patricia trie implementation, the 1-bit switch is the right child node and the 0-bit switch is the left.

A complete documentation of the algorithm, why the algorithm, and the source is not yet done, for now. Well I guess, you could study the diagram above with the source code to get an idea of how internal things works.

I am also working on a much efficient (re)implementation of everything, I'll make it available when it's ready as a new branch.