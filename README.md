# Robust Transductive Few-Shot Learning via Dual Conditional Transport and Prototype-Graph Synergy

This repository contains the implementation of **Graph-guided Dual Conditional Transport (GDCT)** for robust transductive few-shot learning under unknown and imbalanced query-class distributions.

## Overview

Few-shot learning methods often assume that query samples are uniformly distributed across classes. This assumption may not hold in practical applications, where query classes can be highly imbalanced.

GDCT combines:

- **Joint Message Passing (JMP)** for task-aware feature refinement;
- **Dual Conditional Transport (Dual-CT)** for global prototype-level and local anchor-level alignment;
- **KNN graph-based neighbor voting** for local structural reasoning;
- **Prototype-Graph Synergy (PGS)** for fusing prototype-based and graph-based posterior predictions.

The method improves query classification, pseudo-label selection, and progressive prototype refinement under both class-balanced and class-imbalanced settings.

## Benchmarks

Experiments are conducted on four few-shot learning benchmarks:

- miniImageNet
- tieredImageNet
- CUB-200-2011
- CIFAR-FS

We evaluate 5-way 1-shot and 5-way 5-shot tasks under both balanced and class-imbalanced query distributions.

## Main Results

Under class-imbalanced query distributions, GDCT achieves the best or tied-best:

- Classification accuracy in 7 out of 8 dataset--shot settings;
- F1 score in 7 out of 8 settings;
- AUC in all 8 settings.

For example, GDCT obtains the following classification accuracies under class imbalance:

| Dataset | 1-shot | 5-shot |
|---|---:|---:|
| miniImageNet | 75.0% | 86.7% |
| CUB | 87.6% | 92.6% |
| tieredImageNet | 82.1% | 90.8% |
| CIFAR-FS | 82.2% | 88.8% |

## Experimental Settings

- Backbone: pre-trained WideResNet-28-10;
- Backbone features are frozen during task adaptation;
- Task setting: 5-way 1-shot and 5-way 5-shot;
- Number of query samples: 75 per task;
- Imbalanced query distributions are sampled using a symmetric Dirichlet distribution with concentration parameter $\alpha_{\mathrm{dir}}=2$;
- JMP scaling factor: $\tau=10$;
- Number of graph neighbors: $K=9$;
- Conditional transport trade-off factor: $\rho=0.5$;
- Joint-objective weight: $\lambda=0.4$;
- Graph-posterior fusion weight: $\gamma=0.4$;
- Optimization: Adam with a learning rate of $10^{-3}$;
- Number of adaptation iterations: $T=30$.

## Method

GDCT contains three major components:

1. **Joint Message Passing**  
   Refines feature representations and constructs a task-specific graph.

2. **Dual Conditional Transport**  
   Performs prototype-to-query conditional transport for global class alignment and anchor-to-node conditional transport for local manifold modeling.

3. **Prototype-Graph Synergy**  
   Fuses prototype-based predictions with graph-based posterior estimates to improve prediction robustness and prototype refinement.

## Citation

```bibtex
@article{jiang2026gdct,
  title={Robust Transductive Few-Shot Learning via Dual Conditional Transport and Prototype-Graph Synergy},
  author={Jiang, Zhen and Li, Qiji and Yu, Haoran and Xing, Yuping},
  journal={Neurocomputing},
  note={Under review}
}