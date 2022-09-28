# CFD 

## Principy modelování
*CFD = Computational Fluid Dynamics*
- řešení diferenciálních rovnic (ZZ hmoty - rovnice kontinuity, hybnosti - Navier-Stokesovy rovnice, energie)

Obecně výpočet probíhá ve 2 krocích:
1. Diskretizace definičního oboru ({math}`\vec{x}, t`)
    - různé metody (FVM, FEM, ...)
2. Iterační řešení systému algebraických rovnic

## Postup
1. Pre-processing
    - definice geometrie
    - generace výpočetní sítě (mesh) - prostorová, časová
    - volba modelů (turbulence, fyzikální a chemické procesy,...)
        - záleží na požadované přesnosti (a dostupném hardwaru)
        - další faktory - počt fází, přenos energie,...
    - termofyzikální vlastnosti materiálů (hustota, viskozita,...)
        - zadané jako konstanty, tabulka hodnot nebo funkce
    - hraniční (popř. i počáteční) podmínky
        - vstup, výstup, stěny,...
        - v případě nestacionárních úloh se často používá řešení stacionární úlohy jako počáteční podmínka
2. Výpočet
    - nejsnažší část - pracuje počítač
    - vyplatí se sledovat konvergenci -- např. zkontrolovat, že residua klesají
3. Post-processing
    - kontrola, že výsledky dávají smysl
    - analýza konvergence
        - zkontrolovat, že další iterace už nemění výsledek
        - ověřit vliv sítě (meshe) na výsledek
            - provést výpočet na jemnějším meshi a porovnat výsledky
    - zpracování výsledků do požadovaného formátu


## Chyby
1. **Numerické**
    1. Diskretizační

    Souvisí s náhradou derivace diferenčním schématem:
    ```{math}
    \frac{\partial u}{\partial x} &\approx \frac{u(x+h) - u(x)}{h} + \mathcal{O}(h) \\
    \frac{\partial u}{\partial x} &\approx \frac{u(x) - u(x-h)}{h} + \mathcal{O}(h) \\
    \frac{\partial u}{\partial x} &\approx \frac{u(x+0.5h) - u(x-0.5h)}{h} + \mathcal{O}(h^2)
    ```

    Odhad velikosti diskretizační chyby -- porovnat výpočty na různých sítích.

    2. Zaokrouhlovací

       Souvisí s reprezentací reálných čísel v počítači (`float`, `double`). 

       Diskretizační a zaokrouhlovací chyby jdou proti sobě:
       - snížení diskretizační chyby vede k většímu počtu výpočtů, což může vést k větší zaokrouhlovací chybě (záleží však na typu úlohy, stabilitě schématu,...)

    3. Chyba konvergence
    - výpočet různých veličin (rychlosti, teploty,...) konverguje různě rychle 
    - pro kontrolu stačí sledovat např. velikost residua v závislosti na iteraci
    - souvisí s iteračním schématem (typem a hyperparametry) pro řešení maticové úlohy

    4. Chyba diskretizace fyzikálního modelu
    - souvisí se zadáním a modelovacími chybami
    - TODO

2. **Modelovací**
    1. Příliš zjednodušená geometrie
    - např. špatné použití symetrie nebo zanedbání malé oblasti
    2. Fyzikální modely
    - souvisí s modelováním fyzikálních procesů
    - např. volba modelu turbulence
        - RANS je rychlé, ale dělá značná zjednodušení
        - LES řeší některé struktury v proudění, malé struktury pak modeluje; více náročné na HW než RANS, méně než LES
        - DNS řeší přímo Navier-Stokesovy rovnice, ale je vysoce náročné na HW

        | ![Obrázek - Srovnání RANS, LES a DNS](./img/rans_les_dns.png) |
        |:--:|
        | Vlevo: Srovnání DNS (a), LES (b) a RANS (c) simulace proudění z trysky (Italian Agency For New Energy Technologies 2006). Vpravo: Schematické znázornění rozdílu mezi RANS, LES and DNS modelováním (Deck et al. 2014). Převzato z ResearchGate, příspěvek uživatele Alwin Hopf, přeloženo. Originál viz https://www.researchgate.net/figure/Left-Comparison-of-a-DNS-a-LES-b-and-RANS-c-simulation-of-a-jet-flow-Italian_fig1_330765625 |

       - stlačitelnost tekutin -- často se aproximují jako nestlačitelné - ale to není použitelné vždy
       - potřeba předem odhadnout, co je použitelné (např. {math}`v \ll c`, kde {math}`c` je rychlost zvuku, pak aproximace nestlačitelné tekutiny lze použít)

    3. Termofyzikální vlastnosti
    - často aproximujeme konstantami, ale někdy je potřeba poskytnout závislost {math}`x(\rho)` nebo {math}`x(T)` 
    - např. přirozená konvekce

    4. Hraniční podmínky
    5. Počáteční podmínky
    6. Uživatelské funkce
    7. Fázové přechody


## Tvorba geometrie

foo
