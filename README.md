# Language Competition Dynamics

### Course: Physics of Complex Networks (2022-2023)
### Master's Degree: Physics of Data, University of Padova (IT)

## Overview

This project was developed as part of the final exam for the Physics of Complex Network course during the academic year 2022-2023. The work was carried out individually during my first year in the Master's degree program in Physics of Data at the University of Padova. The goal of the project was to study the dynamics of language competition that arise between languages in a bilingual community. We will simulate the competition between two languages and study how outcomes change with varying parameters and model topologies.

## Model Description

In today's interconnected world, languages no longer have the natural or political borders that once separated them. This has led to the spread of languages beyond their places of origin, giving rise to bilingual communities. Within these communities, the coexistence of languages leads to a dynamic in which they compete for dominance in everyday communication.

To simulate language competition, we use a lattice-like structure with $N = L \times L$ nodes, where each node represents an agent (speaker) in the bilingual community. Each node is initialized randomly with an equal probability of belonging to different linguistic communities.

Once the initial state is set, we iterate over a number of epochs, each consisting of selecting a random node $i$ from the lattice. We compute the local densities $\sigma_i$ of each linguistic community in the neighborhood of agent $i$. Based on these local densities, the agent's transition probabilities between linguistic communities are calculated. By sampling a random number using these probabilities, we determine the linguistic community of the agent.

We define two models for this task:

1. Abrams-Strogatz Model: This model assumes that agents belong to one of two languages (A or B). The transition probabilities are:

   $$ p_{i, A \rightarrow B} = \frac{1}{2} \sigma_i^B \qquad p_{i, B \rightarrow A} = \frac{1}{2} \sigma_i^A $$

3. Bilingual Model: This model assumes the existence of bilingual agents (AB). The transition probabilities are:

   $$ p_{i, A \rightarrow AB} = \frac{1}{2} \sigma_i^B \qquad p_{i, B \rightarrow AB} = \frac{1}{2} \sigma_i^A $$

   $$ p_{i, AB \rightarrow B} = \frac{1}{2} (1 - \sigma_i^A) \qquad p_{i, AB \rightarrow A} = \frac{1}{2} (1 - \sigma_i^B) $$

As observed, as the number of epochs increases, spatial domains of each monolingual community form and grow. Bilingual communities never form fully but exist as a narrow band between the two monolingual domains.

## Model Analysis

### Number of Nodes $N$

We analyze how increasing the lattice size affects the time to reach extinction. We find that the average interface density decays as a power law: $<\rho> \sim t^{-\gamma}$, and the decay slows as we increase the number of nodes.

### Changing the Topology

We introduce a small-world (Watts-Strogatz) topology to observe the effect of social structure. This introduces a rewiring probability $p$, determining how likely an edge endpoint changes.

In the Bilingual model, a small-world topology produces rapid extinction of one monolingual community. However, changing $p$ has a small effect in the Abrams-Strogatz model.

### Community Structure Topology

We also introduce a community structure topology. This structure is created by a process of random attachment and search for new contacts, repeated for multiple iterations. Below is the degree distribution depending on the number of iterations:

A community structure topology seems to make the model converge slower, except in the Bilingual case, where more connections lead to faster convergence due to network saturation.

### Prestige and Volatility

Prestige and volatility parameters can model changes in the status of competing languages and how quickly agents imitate their neighbors. We modify the Abrams-Strogatz model with new transition probabilities:

$$ p_{i, A \rightarrow B} = (1 - s)(\sigma_i^B)^a \qquad p_{i, B \rightarrow A} = s(\sigma_i^A)^a $$

Where $a$ represents volatility and $s$ represents prestige. As the prestige deviates further from $s = 0.5$, or volatility increases, the system converges faster to monolingualism.

## Modeling Language Death Dynamics

We use real-world data to model the dynamics of language death using the Abrams-Strogatz model. The evolution dynamics are governed by:

$$ \frac{dx}{dy} = \sigma_B p_{B \rightarrow A} -\sigma_A p_{A \rightarrow B} $$

We fit this model to data on Welsh in Wales, Irish in Ireland, and Gaelic Scottish in Scotland. The inferred prestige and volatility parameters are as follows:

| Language         | Prestige ($s$) | Volatility ($a$) |
|------------------|----------------|------------------|
| Welsh            | 0.453          | 1.245            |
| Irish            | 0.898          | 1.274            |
| Gaelic Scottish  | 0.296          | 0.950            |

### Evolution of Languages Over Time

## Conclusion

This project presents a detailed analysis of language competition dynamics in bilingual communities using both Abrams-Strogatz and Bilingual models. By varying the size, topology, and parameters like prestige and volatility, we have shown how these factors influence the outcome of language competition.
