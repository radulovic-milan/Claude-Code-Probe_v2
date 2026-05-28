# Kalkulator brzine putovanja čestice vode
**Groundwater Travel Time Calculator**

Web aplikacija za izračun vremena putovanja čestice vode kroz zasićenu poroznu sredinu, zasnovana na Darcyjevom zakonu.

---

## Teorijska osnova

Kalkulator koristi trostepeni pristup:

### 1. Darcyjeva specifična brzina filtracije (Darcy flux)
```
q = K × i
```

### 2. Efektivna (porska) brzina čestice
```
vₑ = q / nₑ = (K × i) / nₑ
```
> Darcyjeva brzina `q` predstavlja prosječnu brzinu kroz cijeli poprečni presjek (uključujući čvrstu fazu). Stvarna brzina čestice kroz pore je veća i dijeli se sa efektivnom poroznošću.

### 3. Vrijeme putovanja
```
t = L / vₑ = (L × nₑ) / (K × i)     [dani]
```

---

## Ulazni parametri

| Simbol | Naziv | Jedinice | Tipičan opseg |
|--------|-------|----------|---------------|
| **K** | Hidraulička provodljivost *(Hydraulic Conductivity)* | m/dan, m/s, cm/s, ft/dan | 10⁻⁶ – 10³ m/dan |
| **i** | Hidraulički gradijent *(Hydraulic Gradient)* | bezdimenziono | 0.0001 – 0.1 |
| **nₑ** | Efektivna poroznost *(Effective Porosity)* | bezdimenziono (0–1) | 0.05 – 0.40 |
| **L** | Rastojanje *(Travel Distance)* | m, km, ft | — |

### Tipične vrijednosti K po tipu sedimenta

| Materijal | K (m/dan) |
|-----------|-----------|
| Glina | < 0.001 |
| Silt / prašinasti pijesak | 0.001 – 0.1 |
| Fini pijesak | 0.1 – 10 |
| Srednji/krupni pijesak | 10 – 100 |
| Šljunak | 100 – 1 000 |
| Karstifikovani krečnjak | 100 – 10 000 |

### Tipične vrijednosti efektivne poroznosti

| Materijal | nₑ |
|-----------|----|
| Glina | 0.01 – 0.10 |
| Silt | 0.05 – 0.20 |
| Fini pijesak | 0.15 – 0.30 |
| Krupni pijesak | 0.20 – 0.35 |
| Šljunak | 0.15 – 0.25 |
| Pukotinski stijena | 0.001 – 0.10 |

---

## Izlazni rezultati

| Rezultat | Opis |
|----------|------|
| **Darcyjeva brzina** `q` | Specifična brzina filtracije (m/dan) |
| **Efektivna brzina** `vₑ` | Stvarna brzina čestice kroz pore (m/dan) |
| **Vrijeme putovanja** `t` | Ukupno vrijeme od izvora do cilja (dani, sa pregledom u godinama/mjesecima) |

---

## Konverzija jedinica (interno)

Aplikacija sve vrijednosti interno pretvara u **m/dan** i **metre** prije računanja:

| Unijeta jedinica | Faktor konverzije u m/dan |
|------------------|--------------------------|
| m/dan | × 1 |
| m/s | × 86 400 |
| cm/s | × 864 |
| ft/dan | × 0.3048 |

---

## Pokretanje aplikacije

Aplikacija je čista HTML/CSS/JS datoteka bez vanjskih zavisnosti — radi direktno u pretraživaču:

```bash
# Klonirati repozitorij
git clone https://github.com/radulovic-milan/Claude-Code-Probe_v2.git
cd Claude-Code-Probe_v2

# Otvoriti u pretraživaču (macOS)
open index.html

# ili pokrenuti lokalni server
python3 -m http.server 8080
# → http://localhost:8080
```

---

## Napomene i ograničenja

- Kalkulator pretpostavlja **zasićenu, homogenu i izotropnu poroznu sredinu**.
- **Darcyjev zakon važi** za laminarno strujanje (Re < 1–10); nije primjenjiv za kavernirani karst ili krupnozrni šljunak pri visokim brzinama.
- Za procjenu transporta **zagađivača** potrebno je uvesti **retardacijski faktor R**:
  ```
  t_zagađivač = R × (L × nₑ) / (K × i)
  ```
  gdje `R = 1 + (ρb × Kd) / nₑ` (bulk density × distribution coefficient).
- Rezultati su **1D aproksimacija** duž smjera toka; disperzija, difuzija i heterogenost nisu uzeti u obzir.

---

## Primjer izračuna

**Scenario:** Procjena vremena putovanja podzemne vode od deponije do bunara.

| Parametar | Vrijednost |
|-----------|-----------|
| K | 15 m/dan |
| i | 0.005 |
| nₑ | 0.25 |
| L | 300 m |

**Izračun:**
```
q  = 15 × 0.005 = 0.075 m/dan
vₑ = 0.075 / 0.25 = 0.30 m/dan
t  = 300 / 0.30 = 1 000 dana ≈ 2.74 godine
```

---

## Reference

- Darcy, H. (1856). *Les fontaines publiques de la ville de Dijon.* Dalmont, Paris.
- Bear, J. (1972). *Dynamics of Fluids in Porous Media.* Elsevier.
- Freeze, R.A. & Cherry, J.A. (1979). *Groundwater.* Prentice-Hall.
- Domenico, P.A. & Schwartz, F.W. (1990). *Physical and Chemical Hydrogeology.* Wiley.

---

## Razvoj

Napravljeno uz pomoć [Claude Code](https://claude.ai/code) (Anthropic).  
Repozitorij: [radulovic-milan/Claude-Code-Probe_v2](https://github.com/radulovic-milan/Claude-Code-Probe_v2)
