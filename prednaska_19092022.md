# Úvod

## Obsah a cíle předmětu
- praktická aplikace výpočetních kódů v termohydraulice -- zejména CFD a subkanálová analýza


## Teorie k proudění a sdílení tepla (opakování)
- více info viz THNJ2, 3

### Proudění -- jednofázové
- chceme: {math}`p(x, t)`, {math}`w(x, t)`, {math}`h(x, t)` --> 5 neznámých

- tedy potřebujeme 5 rovnic (níže jsou rovnice kontinuity, Navier-Stokesovy rovnice -- ve formulaci pro stlačitelné Newtonovské tekutiny a zákon zachování energie)

```{math}
    \frac{\partial \rho}{\partial \tau} + \frac{\partial (\rho w_i)}{\partial x_i} &= 0 \\
    \frac{\partial (\rho w_i)}{\partial \tau} + \frac{\partial w_i}{\partial x_j}(\rho w_j) &= \rho K_i - \frac{\partial p}{\partial x_i} + \frac{\tau_{ij}}{\partial x_j} \\
    \frac{\partial (\rho h)}{\partial \tau} + \frac{\partial (\rho h w_j)}{\partial x_j} &= \frac{\partial p}{\partial \tau} + w_j \frac{\partial p}{\partial x_j} + \frac{\partial}{\partial x_i}\left(\lambda \frac{\partial T}{\partial x_i}\right) + \tau_{ij} \frac{\partial w_i}{\partial x_j} + K_i \rho w_i + q_V - \frac{\partial q_{r,i}}{\partial x_j}

```
kde
```{math}
    \frac{\partial \tau_{ij}}{\partial x_j} &= \frac{\partial}{\partial x_j}\left[\eta\left(\frac{\partial w_i}{\partial x_j} + \frac{\partial w_j}{\partial x_i} - \frac{2}{3}\delta_{ij}\frac{\partial w_k}{\partial x_k}\right) + \xi \delta_{ij}\frac{\partial w_k}{\partial x_k}\right] \\
```

Dále je potřeba dodat 
- vztahy pro transportní veličiny
  - stavové rovnice
  - další vztahy
- konstitutivní vztahy - popisují specifické situace, např.
  - proudění z povrchu (vztahy s Nu)
  - ...
- okrajové podmínky
  - v případě nestacionárních dějů se počáteční stav může určit např. stacionárním výpočtem


### Dvoufázové proudění

```{math}
\frac{\partial}{\partial \tau}(\rho_\ell (1-<\alpha>)) + \frac{\partial}{\partial x_i}

```
