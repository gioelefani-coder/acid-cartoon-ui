# Design brief — ECHO GUM

> Prova della skill `acid-cartoon-ui` su un caso reale: delay stereo, 820×500, 8 parametri principali.
> Struttura del brief: quella della skill di processo; scheda stile, palette e componenti: token
> `acid-cartoon-ui`, pack B.

## 1. Ancore

| Ancora | Valore |
|---|---|
| Prodotto | ECHO GUM — delay stereo creativo, VST3 |
| Tipo di suono | ripetizioni gommose, code che si allungano e si stordiscono, ping-pong largo |
| 3 aggettivi | gommoso, ripetuto, stordito |
| Riferimenti | sticker da skate, cartoni anni '90, gomme masticate sotto la suola, fanzine fotocopiate |
| Vincoli duri | finestra 820×500 fissa, 8 parametri principali, nessun logo di marca, UI solo in inglese |
| Deve sembrare / NON deve sembrare | un adesivo appiccicato su un amplificatore / un delay "vintage tape" con legno e VU meter |

_(assunzione: nessun colore di marca, fondo shock libero → ciano, perché il delay deve sembrare "aria" moscia.)_

## 2. Direzioni proposte e scelta

| | Nome | Colore dominante | Forma | Mascotte | Verdetto |
|---|---|---|---|---|---|
| A | **Bubble Echo** | ciano `#14CFE0` | gomme tonde, pillole | blob con un occhio solo + 3 fantasmi eco | **scelta** |
| B | Tape Rot | senape + nero | bobine quadrate | nastro con la faccia | scartata: troppo "vintage", va contro il "NON deve sembrare" |
| C | Neon Well | magenta su nero | pozzo circolare | occhio nel pozzo | scartata: il fondo nero uccide l'idea di "sticker bomb" |

**Scelta: A** — il ciano regge un fondo grande senza mangiarsi i pannelli crema, e i "fantasmi eco" sono
già la metafora del feedback: si leggono senza etichette.

## 3. Scheda stile

- **Pack palette**: B — CYAN STICKER RIOT (`references/PALETTES.md`)
- **Contorni**: ink `#0B0B0B` 4 px su manopole e pulsanti, 3 px su etichette/pillole, 6 px sul bordo
  esterno dei pannelli; giunzioni tonde; jitter ±0.5 px sulle curve grandi
- **Riempimenti**: piatto + 1 lucentezza bianca 28% in alto a sinistra + 1 ombra dura (4,5)
- **Texture dominante**: halftone 10% in un angolo per pannello, grana xerox 8% sul fondo,
  scanline 10% dentro il display
- **Forme**: radius 14 sui pannelli, pillole su pulsanti/badge, tag sezione ruotati −6°, pulsante PING-PONG −2°
- **Anatomia**: un occhio solo sulla manopola TIME (eroe); 3 fantasmi-eco nel display; goo arancio
  sul bordo inferiore del pannello SPACE
- **Tipografia**: display *Bungee* (SIL OFL) per wordmark e titoli · etichette *Archivo Bold* (SIL OFL)

## 4. Palette

| Ruolo | Hex | Uso qui | Contrasto |
|---|---|---|---|
| ink | `#0B0B0B` | contorni, testo, ombre dure | su panel 17.1:1 |
| bg | `#14CFE0` | fondo finestra, fascia top bar scurita 10% | — |
| panel | `#FFF6E0` | 4 pannelli, top bar, footer | ink 17.1:1 |
| a1 | `#FF2E97` | TIME (eroe), manopole attive, riempimento PING-PONG | ink 4.9:1 |
| a2 | `#FFE20A` | archi valore, tacche, wordmark underline | ink 15.4:1 |
| a3 | `#6BE01A` | hover, anelli, fulmini dei meter | ink 13.4:1 |
| extra | `#FF6A1A` | goo, fantasmi-eco nel display | — |
| alert | `#D81228` | clip, feedback al 95% | ink 4.9:1 |

60% bg · 30% panel · 10% accenti. Nessun bianco su giallo o ciano: le etichette sono sempre ink.

## 5. Componenti

| Componente | @1x (x,y,w,h) | Riempimento | Contorno | Ombra | Stati |
|---|---|---|---|---|---|
| Manopola TIME (hero) | 97,86,96,96 | `a1` corpo, anello `a3` | ink 4 | (4,5) | idle; hover alone `a3` 20% r+6; drag scala 1.03 e ombra (2,3); sync-led `a2` |
| Manopola FEEDBACK | 320,100,64,64 | `a1` | ink 4 | (4,5) | a ≥ 95% anello diventa `alert` e il fulmine pulsa |
| Manopola TONE | 446,100,64,64 | `a1` | ink 4 | (4,5) | come sopra, senza allarme |
| Manopola MOD | 580,92,56,56 | `panel` + anello `a3` | ink 4 | (3,4) | off: riempimento `panel`, tratteggio ink 25% |
| Manopola WIDTH | 684,92,56,56 | `a1` | ink 4 | (3,4) | 100% = anello `a2` pieno |
| Manopola MIX | 644,156,72,72 | `extra` dal 50% in su, altrimenti `panel` | ink 4 | (4,5) | 100% wet: badge "WET" `a2` |
| Combo DIVISION | 40,206,170,32 | `panel` | ink 3 | (3,4) | popup 26 px, hover `a3` 35%, selezionata `a1` ink text |
| LED SYNC (indicatore, non parametro) | 226,206,40,40 | gemma `a1` accesa se DIVISION segue il BPM host | ink 3 | (2,3) | acceso: fulmine `a2` 10 px; spento: ink 40% + tratteggio; non cliccabile |
| Pulsante PING-PONG | 580,310,180,44 (−2°) | `panel`, on → `a1` | bianco 3 + ink 3 | (3,4) | hover (4,5); premuto trasla (2,2); on: badge "L↔R" |
| Pannello ×4 | vedi §6 | `panel` | ink 3, r14 | (5,6) | tag `a3` −6°, halftone 10% angolo alto-dx |
| Display tap | 20,290,520,150 | ink | panel 3 + ink 2, r12 | nessuna | scanline 10%, tracce L/R, fantasmi `extra` |
| Meter fulmini | 580,370,28,50 ×2 | `a3` che si riempie | ink 3 | (2,3) | clip → `alert`, 2 Hz |
| LED clip | 736,370,40,40 | `panel` | ink 3 | (2,3) | off ✕ 40%; on `alert` + fulmine |
| Wordmark | 20,8,190,28 | — | ink | (3,4) | underline `a2` 6 px a −1° |

Dettagli comuni: arco valore doppio (ink 10 px sotto, `a2` 6 px sopra) da −135° a +135° con cappucci
tondi; indicatore a cuneo ink base 7 px; etichette 11 px uppercase ink, valori 10 px tabellari.

## 6. Layout (820×500, coordinate assolute)

| Elemento | x | y | w | h | Note |
|---|---|---|---|---|---|
| Top bar | 0 | 0 | 820 | 44 | panel, bordo ink 6 in basso; wordmark a sinistra, "STEREO DELAY" 10 px a destra |
| Pannello TIME | 20 | 60 | 250 | 210 | tag "TIME" −6° sul bordo alto-sx |
| Pannello REPEAT | 290 | 60 | 250 | 210 | tag "REPEAT" |
| Pannello SPACE | 560 | 60 | 240 | 210 | tag "SPACE", goo `extra` sul bordo inferiore |
| Display tap | 20 | 290 | 520 | 150 | tracce L/R, posizioni dei tap, fantasmi-eco |
| Pannello OUT | 560 | 290 | 240 | 150 | PING-PONG, 2 meter, LED clip |
| Footer | 20 | 455 | 780 | 24 | "v1.0" 10 px ink 70% + 4 stelle `extra` a destra |

Gerarchia: TIME è l'eroe (96 px, occhio), FEEDBACK/MIX secondari (64–72), MOD/WIDTH e controlli minori
sotto i 56. Margini 20, gutter 20, griglia 8. Sfondo: mascotte gum 180×200 in basso a destra del display
al 12% di opacità, 6 stelle sparse con seed fisso.

## 7. Asset

| File | Formato | Dimensione | Contenuto | Dove |
|---|---|---|---|---|
| `gum_mascot.svg` | SVG | 180×200 | blob-ciunga con un occhio, ombra dura, contorno ink 4 | display, 12% opacità |
| `echo_ghost.svg` | SVG | 64×64 | fantasmino-eco con bocca a "o" | tap nel display, tinto a runtime (`extra`) |
| `bolt.svg` | SVG | 28×48 | fulmine, solo ink | meter, LED clip |
| `star.svg` | SVG | 24×24 | stella 5 punte | footer, sfondo |
| `goo_drip.svg` | SVG | 160×32 | colatura con goccia | bordo inferiore SPACE |
| `halftone_tile.png` | PNG | 128×128 | retino 45° seamless | pannelli, sfondo |
| `grain_tile.png` | PNG | 128×128 | rumore monocromatico | overlay fondo |
| `badge_blank.svg` | SVG | 120×36 | badge avvertenza **senza testo** | top bar, testo a runtime |

Nessun testo dentro gli asset. Le etichette sono `juce::Label`/`g.drawText`.

## 8. Implementazione JUCE

- `EchoGumLookAndFeel : juce::LookAndFeel_V4` — override: `drawRotarySlider`, `drawComboBox`,
  `drawToggleButton`, `drawButtonBackground`, `drawButtonText`, `drawLabel`, `getTypefaceForFont`.
- Display: `TapDisplay : juce::Component` con `Timer` a 30 Hz; `Path` di tracce e fantasmi preallocati
  nel costruttore; scanline disegnata come nel riferimento TEXTURES.
- Sfondo (mascotte 12% + stelle + halftone + grana) in cache `juce::Image`, ricostruito solo in `resized()`.
- Asset: SVG via `juce::Drawable::createFromSVG` (`gum_mascot`, `echo_ghost`, `bolt`, `star`,
  `goo_drip`, `badge_blank`) dentro `juce_add_binary_data`; PNG solo per halftone e grana.
- Parametri (8): `SliderAttachment` ×6 (TIME, FEEDBACK, TONE, MOD, WIDTH, MIX), `ComboBoxAttachment` ×1
  (DIVISION), `ButtonAttachment` ×1 (PING-PONG, booleano). LED SYNC è un indicatore letto dal BPM host,
  non un parametro: nessun attachment, altrimenti i parametri diventano 9.
- Regole generali di resa (font `juce::FontOptions`, rotazione del disegno e non del `Component`,
  hit target 40×40, APVTS) → skill di processo, § tecnica.

## 9. I 3 segni distintivi

1. La manopola TIME con un occhio solo: è il "personaggio" del plugin già a 2 metri di distanza.
2. I fantasmi-eco arancioni che si allungano nel display a ogni ripetizione.
3. Il pulsante PING-PONG ruotato che si accende rosa e trasla come un adesivo premuto.

## 10. Cosa non è stato verificato

- Nessun render: i contrasti in tabella sono calcolati, non misurati su monitor calibrato.
- Ingombro reale di *Bungee* su "ECHO GUM" a 28 px (da controllare dopo l'installazione del font).
- Comportamento a 125%/150% di scala Windows: le coordinate sono @1x.
