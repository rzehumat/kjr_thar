# Úvod

## Obsah a cíle předmětu
- praktická aplikace výpočetních kódů v termohydraulice -- zejména CFD a subkanálová analýza


## Teorie k proudění a sdílení tepla (opakování)
- více info viz THNJ2, 3

### Proudění -- jednofázové
- chceme: {math}`p(x, t)`, {math}`w(x, t)`, {math}`h(x, t)` --> 5 neznámých

- tedy potřebujeme 5 rovnic (níže jsou rovnice kontinuity, Navier-Stokesovy rovnice -- ve formulaci pro stlačitelné Newtonovské tekutiny a zákon zachování energie)

```{math}
    \newcommand{\pder}[2]{
        \frac{\partial #1}{\partial #2}
    }
    \pder{\rho}{\tau} + \pder{\rho w_i}{x_i} &= 0 \\
    \pder{\rho w_i}{\tau} + \pder{w_i}{x_j}(\rho w_j) &= \rho K_i - \pder{p}{x_i} + \pder{\tau_{ij}}{x_j} \\
    \pder{(\rho h)}{\tau} + \pder{(\rho h w_j)}{x_j} &= \pder{p}{\tau} + w_j \pder{p}{x_j} + \pder{}{x_i}\left(\lambda \pder{T}{x_i}\right) + \tau_{ij} \pder{w_i}{x_j} + K_i \rho w_i + q_V - \pder{q_{r,i}}{x_j}

```
kde
```{math}
    \pder{\tau_{ij}}{x_j} &= \pder{}{x_j}\left[\eta\left(\pder{w_i}{x_j} + \pder{w_j}{x_i} - \frac{2}{3}\delta_{ij}\pder{w_k}{x_k}\right) + \xi \delta_{ij}\pder{w_k}{x_k}\right] \\
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
\pder{}{\tau}(\rho_\ell (1-<\alpha>)) + \pder{}{x_i}\left(\rho_\ell w_{\ell,i}(1-<\alpha>)\right) &= \Gamma_\ell \\
\pder{}{\tau}(\rho_v <\alpha>) + \pder{}{x_i}\left(\rho_v w_{v,i}<\alpha>\right) &= \Gamma_v \\
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
  - Př: [ANSYS Fluent](https://www.ansys.com/products/fluids/ansys-fluent), [Siemens StarCCM+](https://www.plm.automation.siemens.com/global/pl/products/simcenter/STAR-CCM.html), [OpenFOAM](https://www.openfoam.com/),...
- subkanálová analýza
  - předpoklad: proudění v axiálním směru je dominantní, ale existují příčné přetoky
    - rovnice se přepíší do 1D tvaru s členy pro příčné přetoky
    - "mezi 1D a 2D"
  - potřebuje více konstitutivních vztahů
  - dnes používané jen ve výpočtech aktivních zón
  - Př: Cobra, Altham, [Subchanflow](https://www.inr.kit.edu/english/1008.php)
- metoda náhradního média
  - původní složitá geometrie se nahradí jednodušší "náhradní" úlohou
- systémové (integrální) kódy
  - rovnice jsou integrované přes objem, výpočetní oblast se "nodalizuje" 
  - časté v havarijních analýzách
  - typicky vhodné i pro velké oblasti jako celá smyčka nebo celý primární okruh
  - při velkém množství nodů je srovnatelné se subkanálovou analýzou či dokonce s CFD
  - Př: [RELAP](https://relap7.inl.gov/SitePages/Overview.aspx), ATHLET, [MELCOR](https://energy.sandia.gov/programs/nuclear-energy/nuclear-energy-safety-security/melcor/), TRACE
- metoda izolovaného kanálu
- code coupling
  - spojování více různých kódů do složitějších celků
  - specifické pro daný typ úlohy
  - časté pro propojení termohydraulických a neutronických výpočtů
  - Př: RELAP + neutronika, ATHLET + neutronika, [DYN3D](https://www.hzdr.de/db/Cms?pOid=11771&pNid=542), [TRACE + PARCS](https://doi.org/10.1016/j.anucene.2008.12.022), [OpenFOAM + Serpent](https://publications.vtt.fi/julkaisut/muut/2016/OA-Coupling-serpent-and.pdf),...
