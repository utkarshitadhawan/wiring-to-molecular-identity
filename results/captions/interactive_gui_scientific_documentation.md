# Drosophila Olfactory Neurotransmitter Predictor

## Purpose

This interactive tool demonstrates whether connectivity architecture
contains predictive information about neurotransmitter identity in
the examined Drosophila olfactory neuron population.

The predictor uses 16 connectivity-derived features describing
outgoing, incoming, total, and directional connectivity architecture.

## Model

The interactive demonstration uses a Logistic Regression model with
standardized connectivity features.

The model was trained on the final audited dataset of:

- 165 olfactory neurons
- 65 canonical cell types
- 16 connectivity features
- Acetylcholine (ACh) and GABA neurotransmitter classes

## Interpretation

The output represents the model's predicted neurotransmitter class
and its estimated class probabilities.

These probabilities are model outputs and should not be interpreted
as experimentally measured neurotransmitter concentrations or as
biological certainty.

## Validation

Model generalization was assessed separately using cell-type-grouped
five-fold cross-validation.

The full-dataset model used by this interactive interface is a
demonstration model and its predictions must not be interpreted as
independent held-out test performance.

## Scientific limitation

This analysis demonstrates an associative predictive relationship
between connectivity architecture and neurotransmitter identity
within the examined olfactory neuron population.

It does not establish that connectivity mechanistically determines
neurotransmitter identity, nor does it establish universal
generalization across other neurons, brain regions, or species.

## Input

Enter the 16 connectivity features of an olfactory neuron:

1. Outgoing edges
2. Outgoing synapses
3. Outgoing mean synaptic strength
4. Outgoing median synaptic strength
5. Outgoing maximum synaptic strength
6. Outgoing synaptic strength SD
7. Incoming edges
8. Incoming synapses
9. Incoming mean synaptic strength
10. Incoming median synaptic strength
11. Incoming maximum synaptic strength
12. Incoming synaptic strength SD
13. Total edges
14. Total synapses
15. Outgoing/incoming edge ratio
16. Outgoing/incoming synapse ratio

## Important

Predictions from this interface are intended for demonstration and
research exploration. They should not be treated as experimental
confirmation of neurotransmitter identity.