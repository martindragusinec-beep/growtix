# Growtix Design System

**Verze:** 1.0 · **Kontext:** performance marketing, B2B, konverzní weby  
**Stack:** CSS custom properties (`growtix/css/growtix.css`), Bootstrap 5.3 jako layout grid  
**Font:** Plus Jakarta Sans  

Tento dokument je **implementovatelný referenční rámec**: pojmenování škál odpovídá běžnému design-token modelu; v kódu dnes často najdeš aliasy `--gx-*` — mapování je u každé sekce.

---

## 0. Shrnutí cíle

| Cíl | Jak ho DS drží |
|-----|----------------|
| **Konverze** | Jasný primární akcent, jedna dominantní CTA na sekci, vizuální hierarchie bez šumu |
| **Důvěra (agency-grade)** | Stabilní rytmus, tlumené dekorace, konzistentní motion |
| **Škálovatelnost** | Tokeny → komponenty → šablony; škály 50–900 místo ad-hoc hexů |
| **Přístupnost** | Kontrast textu a interaktivních prvků, focus viditelný, motion respektuje `prefers-reduced-motion` |

---

## 1. Color system

### 1.1 Pojmenování

- **Primární škála:** `primary-{50|100|…|900}` — značkový mint / growth green  
- **Sekundární škála:** `secondary-{50|…|900}` — námořní teal (podpora, info, druhotné plochy)  
- **Neutrální škála (dark UI):** `neutral-{50|…|900}` — „modro-břidlicová“ pro pozadí, text a okraje na tmavém podkladu  
- **Sémantické barvy:** `success`, `warning`, `error`, `info` — každá má `DEFAULT`, `-foreground` (text na výplni), `-muted` (pozadí/badge)

### 1.2 Primární (Primary) — mint / growth

**Role:** CTA, odkazy v akci, aktivní stavy, zvýraznění metrik, „doporučeno“ kickery.

| Token | HEX | Poznámka / použití |
|-------|-----|---------------------|
| primary-50 | `#e9fff4` | Světlý highlight (light mode / dokumenty); na dark UI zřídka |
| primary-100 | `#c6ffe3` | Jemné pozadí badge |
| primary-200 | `#8ef5c8` | Hover pozadí světlých variant |
| primary-300 | `#4ee0a3` | Ikony, dekorace |
| primary-400 | `#1fd67f` | Hover na tlačítku (světlejší než 500) |
| **primary-500** | **`#0bd96d`** | **Hlavní akcent — mapuje na `--gx-accent`** |
| primary-600 | `#09b35a` | Active / stisk |
| primary-700 | `#078d48` | Text na velmi světlém pozadí (málo u nás) |
| primary-800 | `#065c32` | — |
| primary-900 | `#043d22` | — |

**Kontrast (WCAG 2.1):**

- `primary-500` na `--gx-bg-deep` (#051824): **> 4.5:1** pro velké texty; pro **běžný body text** používej primární spíš jako **akcent na prvku** (tlačítko, border), ne dlouhé odstavce mint barvou.
- Primární **CTA tlačítko**: výplň `primary-500` / `primary-600` + text **bílý** nebo **neutral-950** podle náhledu — vždy ověř **min. 4.5:1** pro text na výplni.

**Mapování v kódu:** `--gx-accent`, `--gx-accent-bright`, `--gx-accent-dim`, `--gx-accent-border`, `--gx-accent-hairline`, `--gx-accent-glow`.

---

### 1.3 Sekundární (Secondary) — námořní teal

**Role:** Informační panely, sekundární tlačítka, „info“ stavy, ilustrace hran panelů, druhá vrstva značky vedle mintu.

| Token | HEX | Poznámka |
|-------|-----|----------|
| secondary-50 | `#e8f7fb` | — |
| secondary-100 | `#c5eaf3` | — |
| secondary-200 | `#8fd6e6` | — |
| secondary-300 | `#52b8cf` | — |
| secondary-400 | `#289ab5` | — |
| secondary-500 | `#1a7a92` | **Sekundární akční plocha** |
| secondary-600 | `#156278` | Active |
| secondary-700 | `#114d5f` | Text na světlém |
| secondary-800 | `#0d3c4a` | — |
| secondary-900 | `#0a2f3a` | Blíží se panelům |

**Použití:** Podpora primární CTA (outline, ghost), sekundární odkazy v patičce, diagramy. **Nenahrazuje** primary u hlavní konverze.

---

### 1.4 Neutrální (Neutral) — dark slate (pro tmavý UI)

Growtix je **dark-first**. Neutrální škála je od **nejtmavšího pozadí** po **nejvyšší zvednutí karty**.

| Token | HEX | Role |
|-------|-----|------|
| neutral-950 | `#030d14` | Nejnižší vrstva (optional „black hole“) |
| neutral-900 | `#051824` | **Page deep** — `--gx-bg-deep` |
| neutral-850 | `#061a27` | — |
| neutral-800 | `#071c2a` | **Mid** — `--gx-bg-mid` |
| neutral-750 | `#081f2e` | **Základ stránky** — `--gx-bg` |
| neutral-700 | `#0b2736` | `--gx-elev-1` |
| neutral-650 | `#0c2839` | `--gx-surface` |
| neutral-600 | `#0d2f3f` | `--gx-surface-panel` |
| neutral-550 | `#0e3345` | `--gx-elev-2` |
| neutral-500 | `#0f3449` | `--gx-surface-2` |
| neutral-450 | `#0f3a4c` | `--gx-surface-elevated` |
| neutral-400 | `rgba(255,255,255,0.45)` | **Muted secondary text** — `--gx-muted-2` |
| neutral-300 | `rgba(255,255,255,0.65)` | **Muted text** — `--gx-muted` |
| neutral-200 | `rgba(255,255,255,0.10)` | **Border default** — `--gx-border` |
| neutral-100 | `rgba(255,255,255,0.14)` | **Border strong** — `--gx-border-strong` |
| neutral-50 | `#ffffff` | **Primární text** — `--gx-text` |

**Pravidla:**

- **Pozadí:** mezi sekcemi max. **1–2 kroky** škály (např. `neutral-900` → `neutral-750`), ne chaotické skoky.
- **Text:** `neutral-50` nadpisy / body; `neutral-300` doprovod; `neutral-400` legal / meta.
- **Okraje:** `neutral-200` standard; `neutral-100` pro karty a mega menu, kde má být čitelnější oddělení.

---

### 1.5 Sémantické barvy (states)

| Role | Barva výplně (dark UI) | Text / ikona | Poznámka |
|------|------------------------|--------------|----------|
| **success** | `primary-500` / `rgba(11,217,109,0.14)` | `neutral-50` nebo `primary-100` | Úspěch = značkově sladěný s primary |
| **warning** | `#f5a623` / `rgba(245,166,35,0.15)` | `#1a1204` na výplni | Varování — nepoužívat jako druhý „brand“ |
| **error** | `#ff5470` / `rgba(255,84,112,0.14)` | `#fff` nebo `#2a0a10` | Formuláře, validace |
| **info** | `secondary-500` / `rgba(26,122,146,0.18)` | `neutral-50` | Neutrální informace |

**Pravidlo:** Sémantika **nesmí** konkurovat primary CTA v jedné oblasti — chybová hláška ano, ale globální banner ve warning žluté nesmí přebít hlavní tlačítko.

---

### 1.6 Pokyny k použití (shrnutí)

| Kategorie | Co sem patří | Co sem nepatří |
|-----------|--------------|----------------|
| **Primary** | Primární tlačítko, klíčový odkaz, aktivní nav, focus ring akcent | Celé odstavce textu, velké plochy bez důvodu |
| **Secondary** | Outline tlačítka, info karty, sekundární linky | Primární konverzní akce |
| **Neutral** | Všechna pozadí, text, dělicí čáry | „Akční“ výzva bez další vrstvy (primary/secondary) |
| **States** | Feedback po akci, formulář, systémové hlášky | Dekorativní sekce |

---

## 2. Typography system

### 2.1 Font family

| Role | Hodnota |
|------|---------|
| **Primary** | `"Plus Jakarta Sans", system-ui, sans-serif` — `--gx-font` |
| **Fallback** | `system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` |

**Pravidlo:** Jedna rodina napříč produktem. Pro **čísla v dashboardech** (budoucí) zvažte tabulkové číslice (`font-variant-numeric: tabular-nums`).

---

### 2.2 Type scale

Velikosti jsou **fluidní** tam, kde už to Growtix používá (`clamp`), jinak **rem** pro konzistenci.

| Token | Použití | Size | Line height | Weight | Letter-spacing |
|-------|---------|------|-------------|--------|----------------|
| **display** | Hero H1 | `clamp(2.25rem, 5vw, 4.25rem)` | 1.08–1.12 | 600–700 | -0.03em |
| **h1** | Stránkový titulek | `clamp(1.75rem, 3.5vw, 3rem)` | 1.15 | 600 | -0.02em |
| **h2** | Sekce | `clamp(1.75rem, 3.8vw, 2.65rem)` | 1.2 | 600 | -0.02em |
| **h3** | Podsekce, karty | `clamp(1.15rem, 2vw, 1.45rem)` | 1.25 | 600 | -0.02em |
| **h4** | Kompaktní nadpisy | `1.0625rem` – `1.1875rem` | 1.35 | 600 | -0.01em |
| **body-lg** | Úvodní odstavce, lead | `1.0625rem` – `1.125rem` | 1.6 | 400–500 | 0 |
| **body** | Běžný text | `1rem` | 1.65 | 400 | 0 |
| **body-sm** | Sekundární copy | `0.875rem` – `0.9375rem` | 1.5 | 400 | 0 |
| **caption** | Meta, timestamp | `0.75rem` – `0.8125rem` | 1.45 | 400–500 | 0.01em |
| **label** | Formuláře, ALL CAPS kickery | `0.625rem` – `0.6875rem` | 1.2 | 700 | **0.12em – 0.14em** (uppercase) |

**Barvy textu:**

- Nadpisy: `neutral-50`
- Body: `neutral-50` nebo `neutral-300` podle vrstvy
- Zákulisní: `neutral-400`

---

### 2.3 Hierachie — praktické pravidlo

1. Na obrazovku max. **jedna úroveň „display“**.  
2. V sekci: **jeden h2**, pak h3/h4 podle potřeby, ne skok z h2 na body-lg bez meziúrovně.  
3. **Line length:** ideálně **38–68 znaků** pro čtení (`max-width` ~ `42rem` — `--gx-prose-width`).

---

## 3. Spacing & layout

### 3.1 Spacing scale (4px base)

| Token | rem | px | Použití |
|-------|-----|-----|---------|
| `space-0` | 0 | 0 | — |
| `space-1` | 0.25rem | 4 | Tight inline gap |
| `space-2` | 0.5rem | 8 | Ikona + text, badge padding |
| `space-3` | 0.75rem | 12 | Kompaktní stack |
| `space-4` | 1rem | 16 | Default mezi souvisejícími prvky |
| `space-5` | 1.25rem | 20 | Karty vnitřek (min.) |
| `space-6` | 1.5rem | 24 | Sekce uvnitř boxu |
| `space-8` | 2rem | 32 | Mezi bloky v sekci |
| `space-10` | 2.5rem | 40 | — |
| `space-12` | 3rem | 48 | Mezi podsekcemi |
| `space-16` | 4rem | 64 | Sekce vertikální oddech |
| `space-20` | 5rem | 80 | Hero / velké sekce |

**Growtix často používá** `clamp()` pro sekce — to je v pořádku; škála výše je **minimální jazyk** pro nové komponenty.

---

### 3.2 Kontejner a grid

| Prvek | Hodnota |
|-------|---------|
| **Max šířka obsahu** | Bootstrap `container-xxl` (~ `1320px` s paddingem) |
| **Horizontální padding** | `px-3` mobil, `px-lg-4` desktop — konzistentně s `growtix` |
| **Grid** | 12 sloupců Bootstrap; **sekční layouty** typicky `col-lg-6` / `col-xl-4` pro karty |
| **Prose šířka** | `min(42rem, 100%)` |

**Sekční vertikální rytmus:**

- Standardní sekce: `padding-block: clamp(3rem, 6vw, 5rem)` (indikativně — sladit s `.gx-section` v CSS).
- Těsnější: `clamp(2.75rem, 5vw, 4.25rem)`.
- Hero: větší horní padding kvůli fixní navigaci (`padding-top` zohledňující `--gx-header-height`).

---

## 4. Component system

Níže: **varianty, stavy, spacing, pravidla**. Implementace: třídy v `growtix.css` + Bootstrap utility.

### 4.1 Buttons

| Varianta | Vzhled | Použití |
|----------|--------|---------|
| **Primary** | Výplň `primary-500`, text kontrastní | Jedna hlavní akce na viewport / sekci |
| **Secondary** | Outline `neutral-100` nebo `primary` border | Druhotná akce |
| **Ghost** | Transparentní, text `neutral-300`, hover zvedne kontrast | Terciární, v navigaci |
| **Disabled** | Snížená opacity 0.45–0.55, `pointer-events: none` | Jen po validaci / oprávnění |

**Stavy:** `hover` (světlejší/tmavší výplň nebo border), `active` (stisk — posun o 1px nebo sytost `primary-600`), `focus-visible` (ring `primary` / `--gx-focus-ring`, ne jen outline 0).

**Spacing:** horizontální min. `1.25rem`, vertikální `0.65rem`–`0.85rem` (standard); velké CTA větší padding a `font-size` 1rem.

**Pravidla:** Neskladovat dvě primary vedle sebe bez hierarchie — jedna dominantní.

---

### 4.2 Inputs

| Stav | Chování |
|------|---------|
| **Default** | Pozadí `neutral` vstupní plocha (`--gx-surface-input`), border `neutral-200`, text `neutral-50` |
| **Focus** | Ring nebo border `primary-500` / `--gx-accent`, žádné skokové animace |
| **Error** | Border + podpis `error` barvou; `aria-invalid="true"` |
| **Success** | Border nebo ikona `success`; ne duplicitně s error |
| **Disabled** | Snížená opacity, žádný focus |

**Spacing:** label `margin-bottom: space-2`; mezi poli `space-4`–`space-6`.

---

### 4.3 Cards

| Typ | Účel | Vizuál |
|-----|------|--------|
| **Content** | Články, citace | `neutral-650`–`600` pozadí, border `neutral-200`, radius `1rem`–`1.5rem` |
| **Product / pricing** | Nabídky | Silnější stín `--gx-shadow-card`, výraznější nadpis |
| **Feature** | Ikona + titulek + text | Jednotná výška řádků, ikona v `primary` nebo `secondary` |

**Stavy:** hover mírný lift `translateY(-2px)` + silnější stín (viz mega dlaždice). **Reduced motion:** bez transform.

---

### 4.4 Navigation

| Část | Pravidla |
|------|----------|
| **Header** | Sticky, značková výška `--gx-header-height`, pozadí poloprůhledné tmavé + blur |
| **Mega menu** | Plná šířka, povrch `--gx-mega-surface`, vnitřní karty menší radius než vnější panel |
| **Mobile** | Collapse; po kliku na odkaz zavřít menu (již implementováno skriptem) |

---

### 4.5 Modals / dialogs

- Overlay: `rgba(3, 13, 20, 0.72)` + `backdrop-filter` pokud je výkon OK.
- Panel: `neutral-700` pozadí, radius `1rem`, padding `space-8`.
- Primární akce vpravo dole (RTL-aware do budoucna).
- Focus trap + návrat fokusu na trigger.

---

### 4.6 Forms

- Jedna sloupec na mobilu; na širších dvě pole vedle sebe jen pokud jsou **související** (jméno + příjmení).
- Chybové hlášky pod polem, ne jen barva.
- Tlačítko odeslání = jedna **primary**.

---

### 4.7 Badges / tags

- Velikost: `caption` + `padding: space-1 space-2`.
- Barva: `primary` dim pozadí + `primary` text, nebo `neutral` outline.
- Max. **jeden** vizuální „badge“ styl na řádek vedle nadpisu.

---

### 4.8 Alerts / notifications

| Typ | Ikona + barva | Umístění |
|-----|---------------|----------|
| Inline | Pod polem / nad formulářem | Nevyhazovat toast pro každou drobnost |
| Toast | Krátký, pravý horní roh | Max. stack 2–3 |
| Banner | Celá šířka pod nav | Pouze důležité (cookies, outage) |

---

## 5. Interaction & UX rules

### 5.1 Hover, active, focus

- **Hover:** barva nebo stín; **ne** měnit layout o více než 2px bez důvodu.
- **Active:** sytější odstín nebo lehký stisk (scale max. 0.98 u tlačítek).
- **Focus-visible:** vždy viditelný ring pro klávesnici; **ne** skrývat `:focus` pro myš tak, že zablokuješ přístupnost.

### 5.2 Motion

| Parametr | Hodnota |
|----------|---------|
| **Easing (premium)** | `cubic-bezier(0.23, 1, 0.32, 1)` — `--gx-ease-premium` |
| **Délka UI** | 180–280 ms pro hover/fade; **> 400 ms** jen pro hero animace |
| **Reduced motion** | `@media (prefers-reduced-motion: reduce)` — vypnout translate, zkrátit fade |

### 5.3 Mikrointerakce

- Tlačítko: hover → active → focus jasný sled.
- Karta: lehký lift + šipka posun o 1–2 px (jak mega dlaždice).
- Odkaz v textu: podtržení nebo podbarvení `primary`, ne obojí přehnaně.

---

## 6. Design principles

1. **Clarity over decoration** — mesh a gradienty slouží hloubce, ne chaosu; každý vizuální prvek má důvod.  
2. **Consistency over one-off creativity** — jedna škála spacingu, jeden typový řád, jeden akcent.  
3. **Hierarchy first** — uživatel ví, co je nadpis, co akce, co doplňkový text.  
4. **Accessibility always** — kontrast, focus, sémantické HTML, chybové stavy čitelné i bez barvy.  
5. **Conversion with calm** — urgentnost ve copy, ne v pěti blikajících prvcích.  
6. **Performance is UX** — těžké blur a stíny jen tam, kde přidaná hodnota převáží.  
7. **Dark-first coherence** — světlý režim (pokud přijde) musí mít stejnou logiku tokenů, ne přepsané hex „od oka“.

---

## 7. Do / Don’t

| Do | Don’t |
|----|-------|
| Používat tokeny a škály (`primary-500`, `neutral-750`) | Vymýšlet nové hex barvy mimo škálu pro běžné UI |
| Jedna primární CTA na logický blok | Dvě „plné zelené“ tlačítka vedle sebe bez priority |
| `space-*` násobky 4px | Náhodné marginy `13px` / `19px` |
| Ověřit kontrast CTA a textu | Spoléhat, že „mint je vždy OK“ na každém pozadí |
| Focus ring u interaktivních prvků | `outline: none` bez náhrady |
| Kicker label uppercase + letter-spacing | Tři různé styly kickrů na jedné stránce |
| Zjednodušit animace pro `prefers-reduced-motion` | Parallax na každé sekci |

---

## 8. Implementace pro vývojáře

### 8.1 Kde co je

| Co | Kde |
|----|-----|
| Globální tokeny | `growtix/css/growtix.css` → `:root` |
| Živý přehled barev / základů | `growtix/design-system.html` |
| Komponenty (nav, hero, karty, CTA) | stejný CSS soubor + Bootstrap |

### 8.2 Doporučený další krok (tokenizace)

Postupně přidávat aliasy, např.:

```css
:root {
  --gx-primary-500: #0bd96d;
  --gx-neutral-900: #051824;
  /* … */
}
```

a mapovat existující `--gx-accent` → `--gx-primary-500`, aby dokumentace a kód **mluvily stejným jazykem**.

### 8.3 Kontrolní seznam před merge (UI)

- [ ] Kontrast textu a tlačítka (WebAIM / DevTools)  
- [ ] Focus viditelný na klávesnicovém průchodu  
- [ ] Jedna dominantní akce v sekci  
- [ ] Spacing z škály, ne náhodné hodnoty  
- [ ] Žádné nové font weights bez důvodu (Plus Jakarta má 400–700)

---

*Tento dokument je živý: při změně `:root` tokenů aktualizuj mapování v sekci 1 a 2.*
