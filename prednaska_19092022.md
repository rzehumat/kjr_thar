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
\frac{\partial}{\partial \tau}(\rho_\ell (1-<\alpha>)) + \frac{\partial}{\partial x_i}\left(\rho_\ell w_{\ell,i}(1-<\alpha>)\right) &= \Gamma_\ell \\
\frac{\partial}{\partial \tau}(\rho_v <\alpha>) + \frac{\partial}{\partial x_i}\left(\rho_v w_{v,i}<\alpha>\right) &= \Gamma_v \\
TODO

```

- je potřeba více vztahů -- např. konstitutivní vztahy pro výpočet členů {math}`\Gamma`

## Problémy s řešením proudění v praxi
- výpočetní prostředky jsou omezené
  - vztahy je potřeba zjednodušovat (k dosažení rozumné výpočetní náročnosti)
  - typicky se balancuje rychlost výpočtu proti přesnosti (a realističnosti)
- je potřeba zvolit vhodnou metodu

### Aspekty ovlivňující výběr výpočetní metody
- geometrie problému
- probíhající fyzikální jevy
  - proudění - jednofázové x vícefázové
  - fázové přeměny
  - chemické reakce
  - rychlost změn - velikost časového kroku musí být dostatečně malá
- požadovaná přesnost
- nároky na HW a rychlost výpočtu
  - souvisí s aplikací 
    - můžeme si dovolit čekat (např. bezpečnostní analýzy), nebo ne (on-line modelování)
    - počet opakování - jen 1 výpočet, nebo více (např. při optimalizaci)
<!-- (What is the correct word for 'předpoklady') -->
- předpoklady výpočtu
  - konzervativní nebo best-estimate?

### Příklady metod -- výpočet aktivní zóny
- kanálová zóna -- k příčnému mísení nedochází (RBMK, GCR,...) - lze aproximovat 1D výpočtem
- kazetové palivové soubory s obálkou (např. BWR, VVER-440,...) - přetoky mezi PS nejsou, ale chceme uvažovat přenos energie
  - subkanálová analýza funguje dobře
- příčné přetoky existují (např. VVER-1000) - složitější

## Metody řešení 
- CFD
  - univerzální, široce rozšířené v praxi
  - nejblíže skutečnému řešení, ale typicky používá zjednodušené modely (např. RANS, LES v modelování turbulence)
  - velká náročnost na výpočetní prostředky
  - Př: ANSYS Fluent, Siemens StarCCM+, OpenFOAM,...
- subkanálová analýza
  - předpoklad: proudění v axiálním směru je dominantní, ale existují příčné přetoky
    - rovnice se přepíší do 1D tvaru s členy pro příčné přetoky
    - "mezi 1D a 2D"
  - potřebuje více konstitutivních vztahů
  - dnes používané jen ve výpočtech aktivních zón
  - Př: Cobra, Altham, Subchanflow
- metoda náhradního média
  - původní složitá geometrie se nahradí jednodušší "náhradní" úlohou
- systémové (integrální) kódy
  - rovnice jsou integrované přes objem, výpočetní oblast se "nodalizuje" 
  - časté v havarijních analýzách
  - typicky vhodné i pro velké oblasti jako celá smyčka nebo celý primární okruh
  - při velkém množství nodů je srovnatelné se subkanálovou analýzou či dokonce s CFD
  - Př: RELAP, ATHLET, MELCOR, TRACE
- metoda izolovaného kanálu
- code coupling
  - spojování více různých kódů do složitějších celků
  - specifické pro daný typ úlohy
  - časté pro propojení termohydraulických a neutronických výpočtů
  - Př: RELAP + neutronika, ATHLET + neutronika, DYN3D, TRACE + PARCS, OpenFOAM + Serpent,...