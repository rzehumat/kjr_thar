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
        - Souvisí s reprezentací reálných čísel v počítači
    3. Chyba konvergence
    4. Chyba diskretizace fyzikálního modelu
2. **Modelovací**
    1. Příliš zjednodušená geometrie
    2. Fyzikální modely
    3. Termofyzikální vlastnosti
    4. Hraniční podmínky
    5. Počáteční podmínky
    6. Uživatelské funkce
    7. Fázové přechody
