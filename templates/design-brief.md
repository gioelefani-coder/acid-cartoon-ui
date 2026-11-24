# Annex stile — [NOME PLUGIN]

> Solo il layer visivo, da allegare al brief prodotto dalla skill di processo (`plugin-visual-design`),
> che possiede ancore, tre direzioni, layout, asset e consegna. Compila tutte le righe; se un dato non
> esiste, dichiaralo invece di inventarlo.
> Esempio compilato: `examples/delay-stereo/design-brief.md`.

## 1. Scheda stile

- **Pack palette**: [A MAGENTA MELTDOWN / B CYAN STICKER RIOT / C TOXIC LEMON / D XEROX ZINE]
- **Contorni**: ink `#0B0B0B`, [3/4/5–6] px per tipo di elemento, giunzioni tonde, jitter [±0.5 px / no]
- **Riempimenti**: piatto + 1 lucentezza bianca [25/28/30]% + 1 ombra dura offset [(4,5)]
- **Texture dominante**: [halftone 10% / grana xerox 12% / scanline 10%] + [goo / fulmini / stelle]
- **Forme**: radius [10–18] px, pillole su pulsanti e badge, rotazioni [pulsanti −2° / tag −6°]
- **Anatomia cartoon**: [quale controllo eroe, quale mascotte, dove finisce]
- **Tipografia**: display [font + licenza] · etichette [font + licenza] · scala [titolo / sezione / etichetta / valore]

## 2. Palette

| Ruolo | Hex | Uso | Contrasto su |
|---|---|---|---|
| ink | `#0B0B0B` | | |
| bg | | | |
| panel | | | |
| a1 | | | |
| a2 | | | |
| a3 | | | |
| extra | | | |
| alert | | | |

Proporzione 60% bg / 30% panel / 10% accenti · etichette e valori ≥ 4.5:1 · nessun bianco su giallo o ciano.

## 3. Componenti

| Componente | Dimensione @1x | Riempimento | Contorno | Ombra | Stati |
|---|---|---|---|---|---|
| Manopola hero | 96 px | | | | |
| Manopola standard | 64 px | | | | |
| Manopola mini | 40 px | | | | |
| Pulsante sticker | 44 px h | | | | |
| Toggle/LED | 40×40 | | | | |
| Slider | 128 px | | | | |
| Pannello | | | | | |
| Combo | 36 px h | | | | |
| Display | | | | | |
| Badge/wordmark | | | | | |

Dettagli comuni: arco valore doppio (ink 10 px sotto, `a2` 6 px sopra) da −135° a +135° con cappucci
tondi · indicatore a cuneo ink base 7 px · etichette 11 px uppercase ink, valori 10 px tabellari ·
hit target ≥ 40×40 px anche sui controlli mini.

## 4. Vincoli estetici rispettati

- [ ] un solo fondo shock, un solo pannello chiaro, ≤ 2 accenti dominanti
- [ ] ogni forma ha contorno ink ≥ 3 px; ogni ombra è dura, nessun blur
- [ ] texture solo sotto etichette e numeri, opacità ≤ 15%
- [ ] anatomia cartoon su ≤ 2 controlli; icone disegnate, nessuna emoji
- [ ] nessun logo, badge o personaggio esistente copiato
