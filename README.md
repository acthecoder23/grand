<div align=center><img src="docs/grand.png" width=400 /></div>

_Grand_ is a Rosetta Stone of graph technologies.

## Example use-cases

-   True-serverless graph databases using DynamoDB\*
-   Pretend NetworkX is Neo4j and use Cypher to query a graph in memory

> \* [Neptune is not true-serverless.](docs/What-About-Neptune.md)

## Why it's a big deal

_Grand_ is a Rosetta Stone of graph technologies. In short, a _Grand_ graph has a "Backend," which handles the nitty-gritty of talking to data on disk (or in the cloud), and an "Dialect", which is your preferred way of talking to a graph.

For example, here's how you make a graph that is persisted in DynamoDB (the "Backend") but that you can talk to as though it's a `networkx.DiGraph` (the "Dialect"):

```python
import grand

G = grand.Graph(backend=grand.DynamoDBBackend())

G.nx.add_node("Jordan", type="Person")
G.nx.add_node("DotMotif", type="Project")

G.nx.add_edge("Jordan", "DotMotif", type="Created")

assert len(G.nx.edges()) == 1
assert len(G.nx.nodes()) == 2
```

It doesn't stop there. If you like the way IGraph handles anonymous node insertion (ugh) but you want to handle the graph using regular NetworkX syntax, use a `IGraphDialect` and then switch to a `NetworkXDialect` halfway through:

```python
import grand

G = grand.Graph()

# Start in igraph:
G.igraph.add_vertices(6)

# And switch to networkx:
assert len(G.nx.nodes()) == 6

# And back to igraph!
assert len(G.igraph.vs) == 6
```

## Current Support

<table><tr>
<th>✅ = Fully Implemented</th>
<th>🤔 = In Progress</th>
</th>🔴 = Unsupported</th>
</tr></table>

| Dialect           | Description & Notes                            | Status |
| ----------------- | ---------------------------------------------- | ------ |
| `NetworkXDialect` | NetworkX-like interface for graph manipulation | ✅     |
| `IGraphDialect`   | Python-IGraph interface for graph manipulation | ✅     |
| `DotMotifDialect` | DotMotif subgraph isomorphisms                 | 🤔     |

| Backend           | Description & Notes                                 | Status |
| ----------------- | --------------------------------------------------- | ------ |
| `NetworkXBackend` | A NetworkX graph, in memory                         | ✅     |
| `DynamoDBBackend` | A graph stored in two sister tables in AWS DynamoDB | ✅     |
| `SQLBackend`      | A graph stored in two SQL-queryable sister tables   | ✅     |

```

```
