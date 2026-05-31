# PRD — Cozy Cup ☕

**Produkt:** Cozy Cup — relaxační webová hra o vedení kavárny
**Verze dokumentu:** 0.1 (draft)
**Datum:** 31. 5. 2026
**Autor / owner:** Petr
**Platforma:** webový prohlížeč (single-file HTML), hostováno na GitHub Pages
**Stav:** MVP hratelné, plánuje se rozšíření

---

## 1. Shrnutí (TL;DR)

Cozy Cup je odpočinková ("cozy") hra do prohlížeče, ve které hráč vede malou kavárnu.
Hráč **nakupuje suroviny**, **podle receptů z nich připravuje** nápoje a jídlo, **obsluhuje
zákazníky** a za utržené mince nakupuje další zásoby, později i dekorace a sazenice pro
**vlastní pěstování**. Cílová atmosféra je klidná, vřelá a vizuálně útulná — žádný stres,
měkké barvy, jemná hudba/animace.

Hra je postavená čistě na HTML/CSS/JS v jednom souboru, aby šla zadarmo publikovat přes
GitHub Pages a aby byla zvládnutelná pro tvůrce-začátečníka.

---

## 2. Cíle a non-cíle

### 2.1 Cíle
- **G1 — Hratelnost rychle:** mít v každé fázi něco, co si jde okamžitě zahrát (priorita č. 1).
- **G2 — Útulný pocit:** vizuál a tempo navozující klid a spokojenost (priorita č. 2).
- **G3 — Učení v praxi:** tvůrce postupně chápe, jak kód funguje, a umí dělat drobné změny sám (priorita č. 3).
- **G4 — Smysluplná ekonomika:** mince mají hodnotu díky smyčce nakup → vyrob → prodej → doplň.

### 2.2 Non-cíle (záměrně mimo rozsah)
- Žádný online multiplayer ani účty.
- Žádný backend / databáze — veškerý stav běží v prohlížeči.
- Žádné mikrotransakce, reklamy ani monetizace.
- Žádná tvrdá obtížnost ani "game over" — hra je odpočinková.

---

## 3. Cílová skupina

- **Primárně:** hráči, kteří hledají krátké, klidné herní chvilky (cozy / casual segment) —
  podobné publikum jako u Farm to Table, kávových a farmařících her.
- **Sekundárně:** sám tvůrce jako učební projekt a portfolio kousek.

Typická hrací relace: **3–10 minut**, ideálně "ještě jeden den a končím" pocit.

---

## 4. Herní smyčka (core loop)

Toto je srdce celé hry a vše ostatní na ni navazuje:

```
nákup surovin  →  příprava podle receptu  →  obsluha zákazníka  →  zisk mincí
      ↑                                                                  │
      └──────────── doplnění zásob / dekorace / sazenice ←───────────────┘
```

Sekundární smyčka (denní): **začátek dne → plnění denního cíle → konec dne → vyšší cíl zítra.**
Každý den se cíl mírně zvýší, takže hra přirozeně graduje bez tvrdých timerů.

---

## 5. Funkční požadavky

Priority dle MoSCoW: **Must / Should / Could / Won't (zatím).**
Stav: ✅ hotovo · 🟡 rozpracováno · ⬜ plánováno.

### 5.1 Must have (MVP) — ✅ hotovo
| ID | Požadavek | Popis | Stav |
|----|-----------|-------|------|
| F1 | Příchod zákazníka | Náhodný zákazník s náhodnou objednávkou z receptů. | ✅ |
| F2 | Zobrazení receptu | Karta "Recept" ukazuje, jaké suroviny nápoj potřebuje. | ✅ |
| F3 | Spižírna (inventory) | Hráč vidí počty surovin; klepnutím je přidává do kelímku. | ✅ |
| F4 | Příprava nápoje | Skládání surovin do kelímku, tlačítka Serve / Clear. | ✅ |
| F5 | Kontrola receptu | Porovnání kelímku s receptem (na pořadí nezáleží). | ✅ |
| F6 | Ekonomika | Prodej dává mince + malý tip za rychlost; suroviny se spotřebují. | ✅ |
| F7 | Trh (market) | Nákup surovin za mince, hlídání zůstatku. | ✅ |
| F8 | Denní cíl + progres | Ukazatel postupu k dennímu cíli, obrazovka konce dne. | ✅ |
| F9 | Trpělivost zákazníka | Jemný ubývající ukazatel (bez trestu, jen zákazník odejde). | ✅ |
| F10 | Útulný vizuál v0 | Teplá paleta, měkká typografie, emoji jako placeholder grafika. | ✅ |

### 5.2 Should have — ⬜ plánováno
| ID | Požadavek | Popis | Priorita |
|----|-----------|-------|----------|
| F11 | Pěstování surovin | Sazenice → růst v čase → sklizeň (např. zrnka, matcha). Snižuje nákup. | další na řadě |
| F12 | Uložení postupu | Uchování mincí, dne a spižírny mezi návštěvami (`localStorage`*). | vysoká |
| F13 | Více jídla | Rozšíření receptů o jídlo, které zákazníci chtějí. | střední |
| F14 | Zvuk | Jemné ambientní zvuky a " pozitivní" cinknutí při obsloužení. | střední |

\* Pozn.: `localStorage` nefunguje uvnitř náhledu na claude.ai, ale **funguje normálně**
v reálném nasazení na GitHub Pages. Implementujeme až mimo náhled.

### 5.3 Could have — ⬜ později
| ID | Požadavek | Popis |
|----|-----------|-------|
| F15 | Dekorace kavárny | Samostatná obrazovka, kde hráč utrácí úspory za útulnost (nábytek, rostliny, světla). |
| F16 | Preference zákazníků | Různí zákazníci mají oblíbené nápoje/jídlo → bonusy. |
| F17 | Upgrady vybavení | Lepší kávovar = rychlejší příprava nebo vyšší tip. |
| F18 | Denní/sezónní motivy | Ráno/večer, roční období, svátky. |

### 5.4 Won't have (zatím)
- Příběhové dialogy a postavy s linkou.
- Vlastní grafický editor uvnitř hry.
- Mobilní nativní aplikace (zůstáváme u webu, který na mobilu funguje).

---

## 6. Uživatelské příběhy (user stories)

- Jako hráč chci **vidět, co zákazník chce**, abych věděl, co připravit. *(F1, F2)*
- Jako hráč chci **klepáním skládat suroviny**, aby příprava byla rychlá a hmatatelná. *(F3, F4)*
- Jako hráč chci **vydělávat mince a nakupovat zásoby**, aby moje rozhodování mělo dopad. *(F6, F7)*
- Jako hráč chci **denní cíl**, abych měl pocit pokroku, ale bez stresu. *(F8)*
- Jako hráč chci **pěstovat vlastní suroviny**, abych byl míň závislý na nákupu. *(F11)*
- Jako hráč chci **zdobit kavárnu**, abych si vytvořil vlastní útulný prostor. *(F15)*
- Jako tvůrce chci **přehledný kód a komentáře**, abych uměl dělat malé úpravy sám. *(G3)*

---

## 7. Návrhové / UX principy

1. **Bez trestu.** Špatný recept nic nestojí — jen jemná nápověda. Zákazník nanejvýš odejde.
2. **Vždy čitelný cíl.** Hráč v každém okamžiku ví, co dělat dál.
3. **Měkké tempo.** Žádné agresivní timery; trpělivost ubývá pomalu.
4. **Teplá vizualita.** Krémové tóny, zaoblené tvary, jemné stíny a animace.
5. **Hmatatelná odezva.** Každá akce má mikro-animaci (poskočení, "+mince", lehké zatřesení).

---

## 8. Technická architektura

- **Stack:** čisté HTML + CSS + JavaScript, **jeden soubor `index.html`**.
- **Hosting:** GitHub Pages (repo → Settings → Pages → zapnout). Název `index.html` zajistí
  automatické publikování.
- **Bez závislostí na buildu** — žádný npm, žádný framework. Otevře se i dvojklikem lokálně.
- **Data-driven design:** suroviny i recepty jsou **datové objekty** (`INGREDIENTS`, `RECIPES`).
  Přidání nového nápoje/jídla = jeden nový řádek, ne zásah do logiky.
- **Grafika dnes:** emoji + CSS jako placeholder. Výměna za vlastní obrázky/pixel art je
  cílená změna na úrovni jednotlivých položek (pole `emoji` → `<img>`).
- **Perzistence (plán):** `localStorage` pro uložení stavu (mimo náhled claude.ai).

### Datové entity (zjednodušeně)
```
INGREDIENT = { name, emoji, price }        // co nakupuji a z čeho vařím
RECIPE     = { needs: [ingredientId...], sell }   // co zákazník chce a za kolik
STATE      = { coins, day, earned, goal, pantry{}, cup[], currentOrder }
```

---

## 9. Roadmapa / milníky

| Milník | Obsah | Stav |
|--------|-------|------|
| **M0 — Hratelné MVP** | Obsluha + recepty + ekonomika + trh + denní cíl | ✅ hotovo |
| **M1 — Trvalost & pěstování** | `localStorage` (F12) + pěstování surovin (F11) | ⬜ další |
| **M2 — Skutečná grafika** | Výměna emoji za vlastní obrázky / pixel art, zvuk (F14) | ⬜ |
| **M3 — Útulnost & hloubka** | Dekorace (F15), preference zákazníků (F16), upgrady (F17) | ⬜ |
| **M4 — Doladění** | Motivy, vyvážení ekonomiky, leštění UX | ⬜ |

**Doporučené pořadí** vychází z principu "stav v aktuální smyčce → pak nová vrstva":
nejdřív uložení a pěstování (navazuje na ekonomiku), pak grafika, pak dekorace (nejlépe
vypadá až s reálnými obrázky).

---

## 10. Metriky úspěchu

Protože jde o hobby/učební projekt, metriky jsou záměrně měkké:
- **M-ux:** hráč dohraje aspoň 3 dny v jedné relaci (pocit "ještě jeden den").
- **M-feel:** subjektivní hodnocení "je to útulné?" od testerů (přátelé, rodina).
- **M-learn:** tvůrce dokáže sám přidat nový recept a surovinu bez cizí pomoci.
- **M-ship:** hra je živá na veřejné GitHub Pages URL.

---

## 11. Otevřené otázky

1. **Vizuální směr:** emoji v0 → **pixel art** (doporučeno pro start) vs. ilustrovaný styl à la Farm to Table? *(rozhodnout před M2)*
2. **Pěstování:** růst v reálném čase, nebo "po dnech" (sklizeň při otevření dalšího dne)?
3. **Trvalost:** stačí jeden uložený stav, nebo víc slotů / reset?
4. **Zvuk:** vlastní stopa, nebo volně licencovaná knihovna ambientních zvuků?
5. **Rozsah jídla:** kolik položek jídla je "akorát", aby menu nebylo zahlcené?

---

## 12. Závislosti a rizika

- **Riziko — feature creep:** chuť dělat vše naráz. *Mitigace:* držet se milníků, jedna vrstva po druhé.
- **Riziko — grafika brzdí postup:** hledání assetů zdrží hru. *Mitigace:* emoji placeholdery, art až v M2.
- **Závislost — vlastní obrázky:** dekorace a finální vizuál čekají na výběr assetů (tvůrce dodá fotky/art).
- **Pozn. k náhledu:** `localStorage` a některé funkce nejdou otestovat v náhledu na claude.ai,
  ale fungují v reálném nasazení.

---

*Tento PRD je živý dokument — bude se upravovat, jak se hra vyvíjí. Verzovat společně s `index.html` ve stejném repu.*
