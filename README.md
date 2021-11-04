# Graph theory extension for Numbas

This extension provides some functions for working with and drawing graphs in Numbas.

## JME functions

Many of these functions take an adjacency matrix as an argument.
A value of 0 in position `[i][j]` means that there is no edge from vertex `i` to `j`; a positive value means that there is an edge, with any value less than 1 being drawn as a dashed line, and a value of 1 being drawn as a solid line.

### `adjacency_matrix(edges)`

Given a list of edges, in the form `[v1,v2]`, where `v1` and `v2` are indices of vertices, produce an adjacency matrix for the graph with those edges and no extra vertices.

### `draw_graph_from_adjacency(adjacency, labels)`

Given an adjacency matrix and an optional list of string labels for the vertices, produce a drawing of a graph.

### `draw_graph(adjacency, vertices, labels)`

Given an adjacency matrix, a list of vectors giving the positions of the vertices, and an optional list of string labels for the vertices, produce a drawing of a graph.

### `layout_graph(adjacency)`

Given an adjacency matrix, lay the graph out, trying to separate vertices reasonably and avoid crossing edges.

Returns a list of vectors giving the positions of the vertices.

### `vertex_degrees(adjacency)`

Given an adjacency matrix, return a list giving the degree of each vertex.

### `graph_union(a,b)`

Given adjacency matrices `a` and `b`, return an adjacency matrix representing the union of the two graphs.

### `cartesian_product(a,b)`

Given adjacency matrices `a` and `b`, return an adjacency matrix representing the cartesian product of the two graphs.

### `direct_product(a,b)`

Given adjacency matrices `a` and `b`, return an adjacency matrix representing the direct product of the two graphs.

### `adjacency_permutation(p,m)`

Given a permutation `p` (produced by the permutations extension) and an adjacency matrix `m`, return an adjacency matrix representing the graph with the vertices permuted according to `p`.

### `is_graph_isomorphism(p,m)`

Given a permutation `p` (produced by the permutations extension) and an adjacency matrix `m`, return `true` if `p` is an isomorphism of the graph represented by `m`, and `false` otherwise.

## JavaScript functions

All JavaScript functions are available under `Numbas.extensions['graph-theory']`.

Many of these functions take an adjacency matrix as an argument.
An adjacency matrix is a 2D array (an array of arrays), with added integer properties `rows` and `columns` giving the number.
A value of 0 in position `[i][j]` means that there is no edge from vertex `i` to `j`; a positive value means that there is an edge, with any value less than 1 being drawn as a dashed line, and a value of 1 being drawn as a solid line.

### `connected_components(adjacency)`

Given an adjacency matrix, find the connected components.
Returns a list of components, each represented as a list of the indices of the vertices in that component.

### `is_connected(adjacency)`

Return `true` if the graph represented by the given adjacency matrix has a single connected component.

### `subgraph(adjacency,vertices)`

Given a graph represented by an adjacency matrix, and a list of indices of vertices, return the adjacency matrix of the subgraph containing only those vertices.

### `largest_connected_component(adjacency, labels)`

Given a graph represented as an adjacency matrix, and a list of labels for the vertices, return the largest connected component of the graph and the labels of its vertices.

Returns an object `{adjacency, labels}`.

*(I'm not sure if this function is needed)*

### `adjacency_matrix_from_edges(edges,directed)`

Given a list of edges, produce the corresponding adjacency matrix.

`edges` is a list of values `[v1,v2]`, where `v1` and `v2` are indices of vertices.

If `directed` is true, then the adjacency matrix will be made symmetric about its diagonal. 
So for an undirected edge between vertices `i` and `j`, you only need to include `[i,j]` in `edges`.

If `directed` is false, then `[i,j]` and `[j,i]` are different directed edges.

### `from_adjacency_matrix(adjacency)`

Given an adjacency matrix, return lists of vertices and edges, to be used by the cola layout engine.

Returns an object `{vertices, edges}`.

### `draw_graph(graph)`

`graph` is an object `{vertices, adjacency, labels}`.

* `vertices` is a list of objects `{x,y}`.
* `adjacency` is an adjacency matrix: 0 means no edge; 1 means an edge; and any number between 0 and 1 means a dashed edge. If there are edges `i` to `j` and `j` to `i`, the edge is drawn as undirected; otherwise if there is just an edge `i` to `j` it is drawn as directed with an arrow.
* `labels` is a list of string labels for the vertices.

Returns an SVG element containing a drawing of the graph.

### `layout_graph(graph)`

`graph` is an object `{vertices, edges}`.

* `vertices` is a list of objects `{x,y}`.
* `edges` is a list of objects `{source, target, weight}`, where `source` and `target` are indices of vertices, and `weight` is a scalar controlling how long the edge should be.

Returns a list of positions for the vertices, as objects `{x,y}`.

### `vertex_degrees(adjacency)`

Given a graph represented as an adjacency matrix, return a list giving the degree of each vertex.

### `graph_union(m1, m2, ...)`

Given arbitrarily many adjacency matrices representing graphs, return an adjacency matrix representing the union of those graphs.

### `cartesian_product(m1, m2, ...)`

Given arbitrarily many adjacency matrices representing graphs, return an adjacency matrix representing the cartesian product of those graphs.

### `direct_product(m1, m2, ...)`

Given arbitrarily many adjacency matrices representing graphs, return an adjacency matrix representing the direct product of those graphs.

### `adjacency permutation(p,m)`

Apply the given permutation `p`, represented as a list where `p[i]` gives the image of `i` under `p`, to the vertices of the graph represented by the adjacency matrix `m`.

Returns an adjacency matrix.

### `is_graph_isomorphism(p,m)`

Returns `true` if the permutation `p` is an isomorphism of the graph represented by the adjacency matrix `m`.

### `edges_from_weight_matrix(weights)`

`weights` is a 2D array, where `weights[i][j]` gives the weight of the edge between vertices `i` and `j`, or `-1` if there's no edge.

Returns a list of edges represented as objects `{from, to, weight}`.

### `kruskals_algorithm(weights)`

Find a minimum spanning forest of the graph represented by `weights`, using Kruskal's algorithm.

`weights` is a 2D array representing the weights of edges in a graph, which will be passed to `edges_from_weight_matrix` to produce a list of edges.

Returns a list of edges, each represented by an object `{from, to, weight}`.

### `prims_algorithm(weights)`

Find a minimum spanning tree of the graph represented by `weights`, using Prim's algorithm.
The graph must be connected.

`weights` is a 2D array representing the weights of edges in a graph, which will be passed to `edges_from_weight_matrix` to produce a list of edges.

Returns a list of edges, each represented by an object `{from, to, weight}`.
