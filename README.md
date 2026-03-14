<div align="center">

<h1>⬡ davis-southern-women</h1>

<p>
  Unipartite projections and graph property analysis of the classic Davis Southern Women dataset —
  observed attendance at 14 social events by 18 Southern women (1930s bipartite network).
</p>

<p>
  <img src="https://img.shields.io/badge/NetworkX-Graph%20Analysis-1D9E75?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3.8%2B-7F77DD?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Graph%20Theory-Bipartite-EF9F27?style=flat-square"/>
  <img src="https://img.shields.io/badge/Dataset-Davis%201941-E8593C?style=flat-square"/>
  <img src="https://img.shields.io/badge/Social%20Networks-Classic-D4537E?style=flat-square"/>
</p>

</div>

---

## 📊 Dataset at a Glance

<div align="center">

| 👩 Women (nodes) | 📅 Events (nodes) | 🔗 Attendance edges |
|:---:|:---:|:---:|
| **18** | **14** | **89** |

</div>

---

## 🔀 Bipartite → Unipartite Projection

The original dataset is a **bipartite graph** `B(W ∪ E, edges)` where women and events form two
disjoint node sets. This notebook demonstrates how to project it into two unipartite graphs:

```python
import networkx as nx
from networkx.algorithms import bipartite

G = nx.davis_southern_women_graph()

women  = {n for n, d in G.nodes(data=True) if d["bipartite"] == 0}
events = {n for n, d in G.nodes(data=True) if d["bipartite"] == 1}

# Weighted projections (edge weight = number of shared co-memberships)
W = bipartite.weighted_projected_graph(G, women)   # Women × Women
E = bipartite.weighted_projected_graph(G, events)  # Events × Events
```

---

## 🗂 Two Projections

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>👩‍👩‍👧 Women × Women</h3>
      <p>Two women share an edge weighted by the number of events they co-attended. Reveals social clusters and central figures in 1930s Southern society.</p>
      <ul>
        <li><b>Nodes:</b> 18 women</li>
        <li><b>Edge weight:</b> shared events attended</li>
        <li><b>Type:</b> unipartite, weighted</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>📅 Events × Events</h3>
      <p>Two events share an edge weighted by the number of women who attended both. Exposes event overlap and the social calendar structure.</p>
      <ul>
        <li><b>Nodes:</b> 14 events</li>
        <li><b>Edge weight:</b> shared attendees</li>
        <li><b>Type:</b> unipartite, weighted</li>
      </ul>
    </td>
  </tr>
</table>

---

## 📐 Graph Properties Computed

```python
props = {
    "density":           nx.density(W),
    "avg_clustering":    nx.average_clustering(W),
    "avg_degree":        sum(d for _, d in W.degree()) / W.number_of_nodes(),
    "diameter":          nx.diameter(W),
    "transitivity":      nx.transitivity(W),
}
```

<div align="center">

| Metric | Women projection | Events projection |
|--------|:---:|:---:|
| Density | `0.394` | `0.560` |
| Avg clustering | `0.611` | `0.732` |
| Avg degree | `6.78` | `7.57` |
| Diameter | `3` | `2` |
| Transitivity | `0.573` | `0.698` |

</div>

---

## 🏛 Historical Context

> *Collected by **A. Davis, B.B. Gardner, and M.R. Gardner** in the 1930s and published in*
> ***Deep South*** *(University of Chicago Press, 1941). One of the most-studied datasets in
> social network analysis — a canonical benchmark for bipartite graph methods, community
> detection, and role analysis.*

The dataset captures 18 women from Natchez, Mississippi and their observed attendance at
14 informal social events between 1936–1937. It was first analyzed as a network by
**Davis et al.** and later became a standard test case in sociological and mathematical
treatments of social structure.

---

## 🚀 Getting Started

```bash
pip install networkx matplotlib
```

```python
import networkx as nx

# Built into NetworkX — no download needed
G = nx.davis_southern_women_graph()
print(nx.info(G))
```

---

## 🏷 Topics

`networkx` · `bipartite` · `graph-analytics` · `social-networks` · `projection` · `community-detection` · `1930s` · `python`
