# Metoda konečných diferencí (*finite difference method, FDM*)
- jednoduchá metoda založena na diferenciaci a převodu diferenciální rovnice na úlohu s pásovou maticí

**Příklad - uniformní síť:**

```{math}
    \newcommand{\pder}[2]{
        \frac{\partial #1}{\partial #2}
    }
    \newcommand{\ppder}[2]{
        \frac{\partial^2 #1}{\partial #2^2}
    }
    \pder{\rho}{\tau} + \pder{\rho w_i}{x_i} &= 0 \\
    \pder{\rho}{\tau} + \pder{\rho w_i}{x_i} &= 0 \\
    \left(\pder{f}{x}\right)_i = \frac{f_{i+1} - f_{i-1}}{2\Delta x} + \mathcal{O} \\
    \left(\ppder{f}{x}\right)_i \approx \frac{f_{i+1} - 2f_i + f_{i-1}}{\Delta x^2} + \mathcal{O}
```

**Příklad - jednoduchá rovnice vedení tepla:***
```{math}
    a\ppder{T}{x} = \pder{T}{\tau} \Rightarrow \frac{t_i^{n+1} - t_i^{n}}{\Delta \tau} = \frac{a}{\Delta x^2}\left(t_{i+1}^n - 2t_i^n + t_{i+1}^n \right)
```

**Výhody:**
- jednoduchá

**Nevýhody:**
- nepoužitelné pro nestrukturované sítě
- pomalá konvergence (v CFD)
