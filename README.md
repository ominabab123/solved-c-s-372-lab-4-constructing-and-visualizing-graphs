Download Link: https://assignmentchef.com/product/solved-c-s-372-lab-4-constructing-and-visualizing-graphs
<br>



C S 372 Data Structures and Algorithms




In this lab, you will design data structures to represent graphs using adjacency lists, read and write text files that encode a graph, and visualize the graphs in R.

<h1>1        Data structure for graphs</h1>

The node class is provided to you and contains: class Node {

private :

s t r i n g   m_name;       / /         a          s t r i n g         that     labels the      node i n t       m_id ; / /         a          unique           integer            from    0          to         n−1,

/ /        where   n   i s    the   t o t a l   number    of    nodes

public :

Node ( )   { } ;

Node( const   s t r i n g   &amp; name,    i n t    id )

{m_name = name, m_id = id ; } ; i n t id ( ) const { return m_id ; } ;

const   s t r i n g  &amp; name ( )    const    {     return   m_name ; } ;

} ;

Design a graph class using adjacency list, it must contain the following members and functions:

class Graph { private : vector &lt; Node &gt; m_nodes ; vector &lt; l i s t &lt;Node&gt; &gt; m_adjList ; public :

/ /   Construct       the      graph  from    a          f i l e    of         edges Graph ( const       s t r i n g         &amp;         f i l e ) ;

/ / I n s e r t a edge (a , b ) to m_adjList void addEdge ( const Node &amp; a , const Node &amp; b ) ;

/ / I n s e r t a node a to m_nodes void addNode( const Node &amp; a) { m_nodes [ a . id ( ) ] = a ; } ;

/ / Return node with id equal to i const Node &amp; getNode ( size_t i ) const { return m_nodes [ i ] ; }

/ / Return reference of the adjacency l i s t of node a l i s t &lt;Node&gt; &amp; getAdjNodes ( const Node &amp; a)

{     return      m_adjList [ a . id ( ) ] ; }

/ / Return constant reference to adjacency l i s t of node a const l i s t &lt;Node&gt; &amp; getAdjNodes ( const Node &amp; a) const

{     return      m_adjList [ a . id ( ) ] ; }

/ / Return the t o t a l number of nodes in the graph size_t num_nodes ( ) const { return m_nodes . size ( ) ; }

/ /    Create    a   graph    from    a     tab−separated     t e x t   edge    l i s t      f i l e

/ / to adjacency l i s t s void scan ( const s t r i n g &amp; f i l e ) ;

/ /    Save a    graph    from     adjacency     l i s t s    to   a     tab−separated

/ / t e x t edge l i s t f i l e void save ( const s t r i n g &amp; f i l e ) const ;

} ;

The overloaded i/o operator “«” is also provided as follows

std : : ostream&amp;          operator &lt;&lt;( std : : ostream&amp; out ,        const         Graph &amp; g )

{

out &lt;&lt; ”Nodesinthegraph : ” &lt;&lt; endl ; f o r ( unsigned i =0; i &lt;g . num_nodes ( ) ; i ++) {

out   &lt;&lt; g . getNode ( i ) . name ( )   &lt;&lt;   ” , ” ;

}

out    &lt;&lt;    endl ;

out &lt;&lt; ” Adjacency l i s t ofthegraph : ” &lt;&lt; endl ; f o r ( unsigned i =0; i &lt;g . num_nodes ( ) ; i ++) {

out &lt;&lt; ”Node” &lt;&lt; g . getNode ( i ) . name ( ) &lt;&lt; ” : ” ; const l i s t &lt;Node&gt; neighbors = g . getAdjNodes (g . getNode ( i ) ) ;

f o r ( l i s t &lt;Node &gt; : : c o n s t _ i t e r a t o r i t r   =     neighbors . begin ( ) ;

i t r    !=     neighbors . end ( ) ;     ++ i t r )    {

out   &lt;&lt;     i t r −&gt; name ( )    &lt;&lt;   ” , ” ;

}

out   &lt;&lt;    endl ;

}

return     out ;

}

You must utilize the classes to generate all the required tests. If your code deviates from the given template, please explain in your lab report why your choice may be better in terms of time and space complexity.

<h1>2        File input and output for graphs</h1>

The graph file format is <em>tab separated </em>text file containing a list of edges in the graph, specified by the source and destination nodes of each edge, one on each row:

a    d a  b c  b d  c

This graph is visualized in the next section.

<h1>3        Visualization graphs in R</h1>

The interface between R and C++ code will be via graph text files, as the graph class cannot be easily passed between R and C++.

You can easily visualize your graph in R with the R package igraph. Please install the package first. If you want to use it on home computer, you will need to install it by callinginstall.packages(”igraph”). R will install a few other R packages that igraph requires.

require ( ” igraph ” )

l i n k s &lt;− data . frame ( from=c ( ” a ” , ” a ” , ” c ” , ” d ” , ” e ” ) , to=c ( ” d ” , ” b ” , ” b ” , ” c ” , ” a ” ) )

net &lt;− graph_from_data_frame (d=links , directed=T) p l o t ( net , vertex . size =30, vertex . label . cex=2)

net &lt;− graph_from_data_frame (d=links ,                      directed=F)

p l o t ( net ,      vertex . size =30,         vertex . label . cex=2)

When the graph is large, you will use read.table() function in R to load the edges instead of typing them in your program.

You can read the online tutorial “Network visualization with R” by Katya Ognyanova for how to generate a variety of graph visualizations in R at

http://kateto.net/network-visualization

An R script file random_graph.R was provided to plot graphs from files and generate random graphs.

<h1>4        Test the classes</h1>

You will generate five graph text files containing a list of edges each. You must generate some large graphs containing at least 1,000,000 edges and 10,000 nodes, which can be randomly generated in R. Call you C++ program to scan and save it.

For small graphs, compare the visualization of the graph from the initial file and the one that was read from the saved file by your graph class. The graphs may not look identical due to the rearranged edge order, but must be identical in structure.

For large graphs, compare the text file and confirm they contain the same set of edges regardless of the order.

Your C++ program must include a main() function that calls the testall() function. When the program is compiled by a C++ compiler it generates a binary executable file that will run when invoked from the command line.


