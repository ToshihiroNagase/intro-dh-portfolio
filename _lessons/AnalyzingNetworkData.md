---
layout: page
title: Network Data
description: This lesson uses Python to analyze Network Data
---

## Analyzing Network Data with Pyton

By doing this project I was able to learn more about one of the Digital Humanity Project evaluations I did. The project that I evaluated was mapping the republic of letters. The republic of letters mapped communication across europe and america and showcased how people were connected to one another as well as how ideas transfered across the globe. Networkx allows us to work with this data and find information on the structure of the network, who the important people/hubs were, and if there were any subgroups.

Through this project I learned how to work with Network Data. The most important thing to look at before beginning a project like this is understanding the data you are working with. This allows you to determine what type informationy one can pull from the data. In the example we worked on this data had 119 nodes and 174 edges. Furthermore, because the Network data is undirected, which allows us to easily find sub communities and important people in those groups. One cool tool that I learned about in the project is Gephi or Palladio which allows you to visually map the network.

Even though this project shed light on the network of quakers. There are plenty of research questions that can follow. For example, our network analysis showed that the community is centered around a couple large hubs Margaret Fell, George Fox, and William Penn, but there are also many small communities on their own. Now as digital humanity researchers we can look into why there are small communities or what made people like Margaret Fell or George Gox the central hubs of these communities.

There are many different applications to working with Network Data. Especialy with the use of the internet, we can map more complex communities. For example, we could look into facebook friends and see if there are communities in facebook and where the central hubs are. This can help us understand for example, how politics shape communities and answer why there is such a disconnect in political views.

## Getting Started


```python
import csv
from operator import itemgetter
import networkx as nx
from networkx.algorithms import community #This part of networkx, for community detection, needs to be imported separately.
```


```python
with open('quakers_nodelist.csv', 'r') as nodecsv: # Open the file
    nodereader = csv.reader(nodecsv) # Read the csv
    nodes = [n for n in nodereader][1:]

node_names = [n[0] for n in nodes] # Get a list of only the node names

with open('quakers_edgelist.csv', 'r') as edgecsv: # Open the file
    edgereader = csv.reader(edgecsv) # Read the csv
    edges = [tuple(e) for e in edgereader][1:] # Retrieve the data
```


```python
print(len(node_names))
```

    119



```python
print(len(edges)) ## Note that there are no directions
```

    174


## Basics of NetworkX: Creating the Graph


```python
G = nx.Graph()
```


```python
G.add_nodes_from(node_names)
G.add_edges_from(edges)
```


```python
print(nx.info(G))
```

    Graph with 119 nodes and 174 edges


    /var/folders/6p/wc1ydx1s3vqdc2dk8jqgr1440000gn/T/ipykernel_52611/2606185536.py:1: DeprecationWarning: info is deprecated and will be removed in version 3.0.
    
      print(nx.info(G))


## Adding Attributes


```python
hist_sig_dict = {}
gender_dict = {}
birth_dict = {}
death_dict = {}
id_dict = {}
```


```python
for node in nodes: # Loop through the list
    hist_sig_dict[node[0]] = node[1]
    gender_dict[node[0]] = node[2]
    birth_dict[node[0]] = node[3]
    death_dict[node[0]] = node[4]
    id_dict[node[0]] = node[5]
```


```python
nx.set_node_attributes(G, hist_sig_dict, 'historical_significance')
nx.set_node_attributes(G, gender_dict, 'gender')
nx.set_node_attributes(G, birth_dict, 'birth_year')
nx.set_node_attributes(G, death_dict, 'death_year')
nx.set_node_attributes(G, id_dict, 'sdfb_id')
```


```python
for n in G.nodes(): # Loop through every node
    print(n, G.nodes[n]['birth_year']) # Access every node by its name, and then by the attribute birth_year
```

    Joseph Wyeth 1663
    Alexander Skene of Newtyle 1621
    James Logan 1674
    Dorcas Erbery 1656
    Lilias Skene 1626
    William Mucklow 1630
    Thomas Salthouse 1630
    William Dewsbury 1621
    John Audland 1630
    Richard Claridge 1649
    William Bradford 1663
    Fettiplace Bellers 1687
    John Bellers 1654
    Isabel Yeamans 1637
    George Fox the younger 1551
    George Fox 1624
    John Stubbs 1618
    Anne Camm 1627
    John Camm 1605
    Thomas Camm 1640
    Katharine Evans 1618
    Lydia Lancaster 1683
    Samuel Clarridge 1631
    Thomas Lower 1633
    Gervase Benson 1569
    Stephen Crisp 1628
    James Claypoole 1634
    Thomas Holme 1626
    John Freame 1665
    John Swinton 1620
    William Mead 1627
    Henry Pickworth 1673
    John Crook 1616
    Gilbert Latey 1626
    Ellis Hookes 1635
    Joseph Besse 1683
    James Nayler 1618
    Elizabeth Hooten 1562
    George Whitehead 1637
    John Whitehead 1630
    William Crouch 1628
    Benjamin Furly 1636
    Silvanus Bevan 1691
    Robert Rich 1607
    John Whiting 1656
    Christopher Taylor 1614
    Thomas Lawson 1630
    Richard Farnworth 1630
    William Coddington 1601
    Thomas Taylor 1617
    Richard Vickris 1590
    Robert Barclay 1648
    Jane Sowle 1631
    Tace Sowle 1666
    Leonard Fell 1624
    Margaret Fell 1614
    George Bishop 1558
    Elizabeth Leavens 1555
    Thomas Curtis 1602
    Alice Curwen 1619
    Alexander Parker 1628
    John Wilkinson 1652
    Thomas Aldam 1616
    David Barclay of Ury 1610
    David Barclay 1682
    Sir Charles Wager 1666
    George Keith 1638
    James Parnel 1636
    Peter Collinson 1694
    Franciscus Mercurius van Helmont 1614
    William Caton 1636
    Francis Howgill 1618
    Richard Hubberthorne 1628
    William Ames 1552
    William Rogers 1601
    Isaac Norris 1671
    Anthony Sharp 1643
    Mary Fisher 1623
    Anne Conway Viscountess Conway and Killultagh 1631
    Samuel Fisher 1604
    Francis Bugg 1640
    Sarah Gibbons 1634
    William Tomlinson 1650
    Humphrey Norton 1655
    William Gibson 1628
    Gideon Wanton 1693
    John Wanton 1672
    Grace Chamber 1676
    Mary Prince 1569
    John Bartram 1699
    Edward Haistwell 1658
    John ap John 1625
    John Rous 1585
    Anthony Pearson 1627
    Solomon Eccles 1617
    John Burnyeat 1631
    Edward Burrough 1633
    Rebecca Travers 1609
    William Edmundson 1627
    Sarah Cheevers 1608
    Edward Pyott 1560
    Daniel Quare 1648
    John Penington 1655
    Mary Penington 1623
    Charles Marshall 1637
    Humphrey Woolrich 1633
    William Penn 1644
    Mary Pennyman 1630
    Dorothy Waugh 1636
    David Lloyd 1656
    Lewis Morris 1671
    Martha Simmonds 1624
    John Story 1571
    Thomas Story 1670
    Thomas Ellwood 1639
    William Simpson 1627
    Samuel Bownas 1677
    John Perrot 1555
    Hannah Stranger 1656


## Metrics available in NetworkX


```python
density = nx.density(G)
print("Network density:", density)
```

    Network density: 0.02478279447372169



```python
fell_whitehead_path = nx.shortest_path(G, source="Margaret Fell", target="George Whitehead")

print("Shortest path between Fell and Whitehead:", fell_whitehead_path)
```

    Shortest path between Fell and Whitehead: ['Margaret Fell', 'George Fox', 'George Whitehead']



```python
print("Length of that path:", len(fell_whitehead_path)-1)
```

    Length of that path: 2



```python
# If your Graph has more than one component, this will return False:
print(nx.is_connected(G))
components = nx.connected_components(G)
largest_component = max(components, key=len)

# Create a subgraph of just the largest component
subgraph = G.subgraph(largest_component)
diameter = nx.diameter(subgraph)
print("Network diameter of largest component:", diameter)
```

    False
    Network diameter of largest component: 8



```python
triadic_closure = nx.transitivity(G)
print("Triadic closure:", triadic_closure)
```

    Triadic closure: 0.16937799043062202


## Centrality


```python
degree_dict = dict(G.degree(G.nodes()))
nx.set_node_attributes(G, degree_dict, 'degree')
```


```python
print(G.nodes['William Penn'])
```

    {'historical_significance': 'Quaker leader and founder of Pennsylvania', 'gender': 'male', 'birth_year': '1644', 'death_year': '1718', 'sdfb_id': '10009531', 'degree': 18}



```python
sorted_degree = sorted(degree_dict.items(), key=itemgetter(1), reverse=True)
```


```python
print("Top 20 nodes by degree:")
for d in sorted_degree[:20]:
    print(d)
```

    Top 20 nodes by degree:
    ('George Fox', 22)
    ('William Penn', 18)
    ('James Nayler', 16)
    ('George Whitehead', 13)
    ('Margaret Fell', 13)
    ('Benjamin Furly', 10)
    ('Edward Burrough', 9)
    ('George Keith', 8)
    ('Thomas Ellwood', 8)
    ('Francis Howgill', 7)
    ('John Perrot', 7)
    ('John Audland', 6)
    ('Richard Farnworth', 6)
    ('Alexander Parker', 6)
    ('John Story', 6)
    ('John Stubbs', 5)
    ('Thomas Curtis', 5)
    ('John Wilkinson', 5)
    ('William Caton', 5)
    ('Anthony Pearson', 5)



```python
betweenness_dict = nx.betweenness_centrality(G) # Run betweenness centrality
eigenvector_dict = nx.eigenvector_centrality(G) # Run eigenvector centrality

# Assign each to an attribute in your network
nx.set_node_attributes(G, betweenness_dict, 'betweenness')
nx.set_node_attributes(G, eigenvector_dict, 'eigenvector')
```


```python
sorted_betweenness = sorted(betweenness_dict.items(), key=itemgetter(1), reverse=True)

print("Top 20 nodes by betweenness centrality:")
for b in sorted_betweenness[:20]:
    print(b)
```

    Top 20 nodes by betweenness centrality:
    ('William Penn', 0.23999456006192205)
    ('George Fox', 0.23683257726065216)
    ('George Whitehead', 0.12632024847366005)
    ('Margaret Fell', 0.12106792237170329)
    ('James Nayler', 0.10446026280446098)
    ('Benjamin Furly', 0.06419626175167242)
    ('Thomas Ellwood', 0.046190623885104545)
    ('George Keith', 0.045006564009171565)
    ('John Audland', 0.04164936340077581)
    ('Alexander Parker', 0.03893676140525336)
    ('John Story', 0.028990098622866983)
    ('John Burnyeat', 0.028974117533439564)
    ('John Perrot', 0.02829566854990583)
    ('James Logan', 0.026944806605823553)
    ('Richard Claridge', 0.026944806605823553)
    ('Robert Barclay', 0.026944806605823553)
    ('Elizabeth Leavens', 0.026944806605823553)
    ('Thomas Curtis', 0.026729751729751724)
    ('John Stubbs', 0.024316593960227152)
    ('Mary Penington', 0.02420824624214454)



```python
#First get the top 20 nodes by betweenness as a list
top_betweenness = sorted_betweenness[:20]

#Then find and print their degree
for tb in top_betweenness: # Loop through top_betweenness
    degree = degree_dict[tb[0]] # Use degree_dict to access a node's degree, see footnote 2
    print("Name:", tb[0], "| Betweenness Centrality:", tb[1], "| Degree:", degree)
```

    Name: William Penn | Betweenness Centrality: 0.23999456006192205 | Degree: 18
    Name: George Fox | Betweenness Centrality: 0.23683257726065216 | Degree: 22
    Name: George Whitehead | Betweenness Centrality: 0.12632024847366005 | Degree: 13
    Name: Margaret Fell | Betweenness Centrality: 0.12106792237170329 | Degree: 13
    Name: James Nayler | Betweenness Centrality: 0.10446026280446098 | Degree: 16
    Name: Benjamin Furly | Betweenness Centrality: 0.06419626175167242 | Degree: 10
    Name: Thomas Ellwood | Betweenness Centrality: 0.046190623885104545 | Degree: 8
    Name: George Keith | Betweenness Centrality: 0.045006564009171565 | Degree: 8
    Name: John Audland | Betweenness Centrality: 0.04164936340077581 | Degree: 6
    Name: Alexander Parker | Betweenness Centrality: 0.03893676140525336 | Degree: 6
    Name: John Story | Betweenness Centrality: 0.028990098622866983 | Degree: 6
    Name: John Burnyeat | Betweenness Centrality: 0.028974117533439564 | Degree: 4
    Name: John Perrot | Betweenness Centrality: 0.02829566854990583 | Degree: 7
    Name: James Logan | Betweenness Centrality: 0.026944806605823553 | Degree: 4
    Name: Richard Claridge | Betweenness Centrality: 0.026944806605823553 | Degree: 2
    Name: Robert Barclay | Betweenness Centrality: 0.026944806605823553 | Degree: 3
    Name: Elizabeth Leavens | Betweenness Centrality: 0.026944806605823553 | Degree: 2
    Name: Thomas Curtis | Betweenness Centrality: 0.026729751729751724 | Degree: 5
    Name: John Stubbs | Betweenness Centrality: 0.024316593960227152 | Degree: 5
    Name: Mary Penington | Betweenness Centrality: 0.02420824624214454 | Degree: 4


## Advanced NetworkX: Community detection with modularity


```python
communities = community.greedy_modularity_communities(G)
```


```python
modularity_dict = {} # Create a blank dictionary
for i,c in enumerate(communities): # Loop through the list of communities, keeping track of the number for the community
    for name in c: # Loop through each person in a community
        modularity_dict[name] = i # Create an entry in the dictionary for the person, where the value is which group they belong to.

# Now you can add modularity information like we did the other metrics
nx.set_node_attributes(G, modularity_dict, 'modularity')
```


```python
# First get a list of just the nodes in that class
class0 = [n for n in G.nodes() if G.nodes[n]['modularity'] == 0]

# Then create a dictionary of the eigenvector centralities of those nodes
class0_eigenvector = {n:G.nodes[n]['eigenvector'] for n in class0}

# Then sort that dictionary and print the first 5 results
class0_sorted_by_eigenvector = sorted(class0_eigenvector.items(), key=itemgetter(1), reverse=True)

print("Modularity Class 0 Sorted by Eigenvector Centrality:")
for node in class0_sorted_by_eigenvector[:5]:
    print("Name:", node[0], "| Eigenvector Centrality:", node[1])
```

    Modularity Class 0 Sorted by Eigenvector Centrality:
    Name: James Nayler | Eigenvector Centrality: 0.3352974100447867
    Name: Margaret Fell | Eigenvector Centrality: 0.253170949905681
    Name: Francis Howgill | Eigenvector Centrality: 0.19095393782681047
    Name: Richard Farnworth | Eigenvector Centrality: 0.15368535029296412
    Name: Anthony Pearson | Eigenvector Centrality: 0.11120476725256782



```python
for i,c in enumerate(communities): # Loop through the list of communities
    if len(c) > 2: # Filter out modularity classes with 2 or fewer nodes
        print('Class '+str(i)+':', list(c)) # Print out the classes and their members
```

    Class 0: ['Elizabeth Leavens', 'Margaret Fell', 'Thomas Aldam', 'Robert Rich', 'Francis Howgill', 'William Gibson', 'Gervase Benson', 'William Tomlinson', 'Richard Farnworth', 'Thomas Lower', 'Martha Simmonds', 'James Nayler', 'Dorcas Erbery', 'George Fox the younger', 'Anthony Pearson', 'Hannah Stranger', 'Thomas Holme']
    Class 1: ['Peter Collinson', 'William Penn', 'Isaac Norris', 'Tace Sowle', 'David Lloyd', 'Joseph Besse', 'John Bartram', 'Jane Sowle', 'Samuel Bownas', 'Isabel Yeamans', 'George Keith', 'Thomas Story', 'Edward Haistwell', 'William Bradford', 'Anne Conway Viscountess Conway and Killultagh', 'Richard Claridge', 'James Logan']
    Class 2: ['Leonard Fell', 'John Perrot', 'Edward Burrough', 'George Fox', 'Ellis Hookes', 'Mary Prince', 'Mary Fisher', 'Thomas Salthouse', 'William Coddington', 'William Dewsbury', 'William Mucklow', 'William Crouch', 'Elizabeth Hooten', 'William Mead', 'John Crook']
    Class 3: ['Gilbert Latey', 'Alice Curwen', 'Thomas Lawson', 'Daniel Quare', 'Francis Bugg', 'Alexander Parker', 'Rebecca Travers', 'Henry Pickworth', 'John Whitehead', 'Richard Hubberthorne', 'Silvanus Bevan', 'Sir Charles Wager', 'Lewis Morris', 'George Whitehead']
    Class 4: ['William Rogers', 'Samuel Clarridge', 'Mary Penington', 'John Burnyeat', 'Thomas Ellwood', 'John Penington', 'John ap John', 'Thomas Curtis', 'James Claypoole', 'Anthony Sharp', 'Joseph Wyeth', 'William Simpson', 'William Edmundson']
    Class 5: ['John Swinton', 'Franciscus Mercurius van Helmont', 'Benjamin Furly', 'William Caton', 'John Stubbs', 'Samuel Fisher', 'James Parnel', 'Robert Barclay', 'William Ames', 'Stephen Crisp', 'David Barclay of Ury']
    Class 6: ['Thomas Camm', 'Anne Camm', 'John Audland', 'Solomon Eccles', 'Charles Marshall', 'John Story', 'John Camm', 'Edward Pyott', 'John Wilkinson']
    Class 7: ['Thomas Taylor', 'John Whiting', 'Christopher Taylor']


## Export Information


```python
nx.write_gexf(G, 'quaker_network.gexf')
```


```python

```
