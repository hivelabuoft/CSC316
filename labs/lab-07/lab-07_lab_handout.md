<!---
layout: labold
exclude: true
--->


&nbsp;

# Lab 7 Handout

### Pre-Reading Quiz
On Quercus!

### Learning Objectives

- Know how to create custom visualizations with D3
	- Set up a completely new project without templates
	- Consolidate the official documentation and external materials
	- Apply the learned web development skills and your deep understanding of D3 to realize your own ideas and to
	implement unique visualizations (apart from bar and area charts)


***Important Note:***
In this lab we want to guide you through creating a highly customized visualization in D3, without using typical building blocks like bar charts or line charts. That means that in this lab you will have to deal not just with writing correct D3 syntax, but also with figuring out *in what way* you can implement a certain feature.

We give you pointers, but part of this lab is figuring these things out on your own. Do not hesitate to ask for help if you are stuck!


## Visualization Goal: Padgett's Florentines Families

In this problem set you will work primarily with network data. The data sources about marriage and business ties among Renaissance Florentine families were originally collected by Padgett [1] and then made available to the public.
  The dataset includes important families that were involved in a struggle for political control in Florence around 1430. With the collected data, researchers can analyze the influence of individual families and, in addition, can get a better understanding of the impact of these different kinds of relationships.

Each network consists of 16 families of the city of Florence in the early 15th century. In the graph, a family is represented as a node and marriages or business ties are the relations (edges) between these nodes. All the relations we consider are non-directional (symmetrical).



[1] Padgett, J.F. (1994): Marriage and Elite Structure in Renaissance Florence, 1282-1500. ([http://home.uchicago.edu/~jpadgett/papers/unpublished/maelite.pdf](http://home.uchicago.edu/~jpadgett/papers/unpublished/maelite.pdf))



### Data

Network data is made up of two main components: the structure of the graph itself (topology) and attributes of the nodes and edges. The topology of the graph is captured via its edges, which connect the nodes in the network.  
Storing the topology is usually done in one of two ways: a matrix or an edgelist.  
Storing attributes/metadata for the nodes cannot be stored in a matrix nor an edgelist. This must be stored in a separate csv file.  
Storing attributes/metadata for the edges can only be stored in an edgelist, and not in a matrix.

- Edgelist: This is a simple way to represent a network as a basic list (e.g. csv file). Each row contains 2 IDs, each ID representing 1 node/vertex that link to each other via an edge. If edges have weights/magnitude, you can add a third column with the individual values. With this format, you can add more metadata for each edge, simply by adding a new column for each edge attribute. Alternatively, you can add the edge attributes in a separate csv file.

- Adjacency matrix: If a graph has *n* vertices we can store the data in an n × n matrix. Data stored in this format is in many cases very convenient for the further processing in JS and D3. For example, we can query it easily with ```graph[i][j]```. The disadvantage of matrices is that they use a lot of space to represent only a few edges.

For this lab, the structure of the network is stored in two adjacency matrices (one containing edges for marriages, another for business ties), while the attributes are stored in an external csv file:

1. Dataset: Meta data **[```florentine-family-attributes.csv```](florentine-family-attributes.csv)**

	- Family
	- Wealth (each family's net wealth in thousands of lira; in 1427)
	- Priorates (seats on the civic council)

	```csv
	"Family","Wealth","Priorates"
	"Acciaiuoli",10,53
	"Albizzi",36,65
	"Barbadori",55,NA
	"Bischeri",44,12
	...
	```

	*You will use the above dataset as a meta information for the networks. The family in the first row in the above dataset corresponds to the family in the first row and column of the adjacency matrices. The family in second row corresponds to the second row/column of the adjacency matrix, etc.*

2. Adjacency matrix: **Marriages**
<a name="adjacency_matrices"></a>
```
let dataMarriages = [
	[0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0],
	[0,0,0,0,0,1,1,0,1,0,0,0,0,0,0,0],
	[0,0,0,0,1,0,0,0,1,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,1,0,0,0,1,0,0,0,1,0],
	[0,0,1,0,0,0,0,0,0,0,1,0,0,0,1,0],
	[0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,1,0,1,0,0,0,1,0,0,0,0,0,0,0,1],
	[0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0],
	[1,1,1,0,0,0,0,0,0,0,0,0,1,1,0,1],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0],
	[0,0,0,1,1,0,0,0,0,0,0,0,0,0,1,0],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,1],
	[0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0],
	[0,0,0,1,1,0,0,0,0,0,1,0,1,0,0,0],
	[0,0,0,0,0,0,1,0,1,0,0,0,1,0,0,0]
];
```


3. Adjacency matrix: **Business Ties**

```
let dataBusiness = [
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,1,1,0,0,1,0,1,0,0,0,0,0],
	[0,0,0,0,0,0,1,1,0,0,1,0,0,0,0,0],
	[0,0,1,0,0,0,0,1,0,0,1,0,0,0,0,0],
	[0,0,1,0,0,0,0,0,1,0,0,0,0,0,0,0],
	[0,0,0,1,0,0,0,1,0,0,0,0,0,0,0,0],
	[0,0,0,1,1,0,1,0,0,0,1,0,0,0,0,0],
	[0,0,1,0,0,1,0,0,0,1,0,0,0,1,0,1],
	[0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0],
	[0,0,1,1,1,0,0,1,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
	[0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0]
];
```


[//]: # (Source: [http://svitsrv25.epfl.ch/R-doc/library/ergm/html/flomarriage.html](http://svitsrv25.epfl.ch/R-doc/library/ergm/html/flomarriage.html)


### Network Visualization

Networks can be visualized in several different ways, the two most common of which are node-link diagrams and adjacency matrices. Notices that the term `adjacency matrix` can refer to both the data structure that stores the graph, as described in the Data section above, and the visualization approach (which you will be implementing in this lab).

Node-link diagrams are the most common way of visualizing graphs, but they have a few key limitations:  
(1) they do not scale well to large networks,  
(2) they can quickly become cluttered for dense networks with several edge crossings (where edges start crossing over each other),  
(3) they are limited in the amount of attributes that can be encoded for the nodes and particuarly edges.

Adjacency Matrices are an alternative visualization approach for networks that address some of these limitations. They are particuarly well suited for dense graphs since every possible edge in a network is allotted a cell in the matrix, ensuring that there are no edge crossings. Additionally, they are well suited for encoding edge attributes directly in the matrix cell.

[You can read all about visualizing multivariate networks here!](https://vdl.sci.utah.edu/publications/2019_eurovis_mvn/)



### Preview & Problem Description

In this lab you will build a custom visualization with D3 that will look like this one:

![Lab 7 - Preview](assets/cs171-lab8-preview.gif?raw=true "Lab 7 - Preview")


Matrix visualizations are especially appropriate for dense networks, i.e. those that have many edges connecting the nodes in the network. This is because every edge is given its own cell in the matrix, and there is never any occlusion/overlap of edges, as is common in a node-link representation.

In the sortable matrix visualization you will be implementing in this lab, you will encode two types of edges simultaneously in the matrix cells.

*We suggest that you go through the following four iterations:*
1) **Matrix** - Set up a Matrix class where you pass all the necessary data to the constructor and wrangle the data by creating a JS object for each family with sub-arrays for marriages and business ties. 

2) **Labelled Matrix** - Using the JS objects for each family, load it in as labels for the matrix.

3) **Encode both relations** - Draw triangles to show the relationship for each family. 

4) **Sortable matrix** - Add a sorting function that's activated by a dropdown menu. Add transitions between the sorting. 


![Lab 7 - Iterations](assets/cs171-lab8-iterations.png?raw=true "Lab 7 - Iterations")






-----

**Resources**

- Custom visualizations with D3: [http://jsdatav.is/chap07.html#creating-a-unique-visualization](http://jsdatav.is/chap07.html#creating-a-unique-visualization)
- D3 object constancy: [https://bost.ocks.org/mike/constancy/](https://bost.ocks.org/mike/constancy/)
- Padgett Florentines Families: [http://home.uchicago.edu/~jpadgett/papers/unpublished/maelite.pdf](http://home.uchicago.edu/~jpadgett/papers/unpublished/maelite.pdf)
