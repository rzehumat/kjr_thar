# Úvod

## Obsah a cíle předmětu
- praktická aplikace výpočetních kódů v termohydraulice -- zejména CFD a subkanálová analýza


## Teorie k proudění a sdílení tepla (opakování)
- více info viz THNJ2, 3

### Proudění
- chceme: {math}`p(x, t)`, {math}`w(x, t)`, {math}`h(x, t)` --> 5 neznámých

- tedy potřebujeme 5 rovnic

```{math}
    \frac{\partial \rho}{\partial \tau} + \frac{\partial (\rho w_i)}{\partial x_i} &= 0 \\
    \frac{\partial (\rho w_i)}{\partial \tau} + \frac{\partial w_i}{\partial x_j}(\rho w_j) &= \rho K_i - \frac{\partial p}{\partial x_i} + \frac{\tau_{ij}}{\partial x_j} \\
    \frac{\partial \tau_{ij}}{\partial x_j} &= \frac{\partial}{\partial x_j}\left[\eta(\frac{\partial w_i}{\partial x_j})\right]
```
