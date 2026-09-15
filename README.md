# Mixture Discriminant Analysis (MDA) — Built from Scratch via EM

Developed together with Stephanny Frasser Sanchez.

Hand-built implementation (no MDA library) of a mixture-of-Gaussians classifier trained via EM, compared against standard LDA, on a synthetic classification problem with a non-linear decision boundary.

## Result

| Model | Log-loss (test) | AUC (test) |
|---|---|---|
| LDA (linear boundary) | 0.683 | 0.651 |
| MDA — manual EM, 2 sub-classes per class | 0.578 | 0.780 |

## Why MDA wins here

The data was generated with a non-linear decision boundary (sin(a*x1/10) + sin(b*x2/10)). LDA can only draw a straight line between classes — with a boundary this curved, it loses real information. MDA models each class as a mixture of 2 sub-Gaussians (via EM, with a shared covariance matrix within each class but different between classes, similar to QDA), letting it approximate curved boundaries. The result: 13 extra points of AUC just from using a model with the right flexibility for the actual geometry of the problem.

## Methodology

500 synthetic observations (350 train / 150 test). LDA via MASS::lda. MDA implemented by hand: EM for 2 sub-classes per class, with likelihood computed via Cholesky decomposition (no dependency on mvtnorm).

## Stack

R, MASS (LDA), pROC — EM and multivariate density implemented from scratch
