# Design brief — GOO FANG

> Esempio compilato con la skill `acid-cartoon-ui`. Plugin inventato: saturatore a due stadi.

## 1. Ancore

| Ancora | Valore |
|---|---|
| Prodotto | GOO FANG — saturatore/distorsore a 2 stadi, VST3 |
| Tipo di suono | sporco, masticato, "cassetta lasciata al sole" |
| 3 aggettivi | acido, masticato, giocoso |
| Riferimenti | sticker da skate anni '90, cartoni underground, fanzine fotocopiate, poster punk |
| Vincoli duri | finestra 780×460, 7 parametri principali, nessun logo aziendale |
| Deve sembrare / NON deve sembrare | un adesivo incollato su un poster / un clone di Serum o una UI 3D |

_(assunzione: nessuna palette di marca, quindi il fondo shock è libero.)_

## 2. Direzioni proposte e scelta

| | Nome | Colore dominante | Forma | Mascotte | Verdetto |
|---|---|---|---|---|---|
| A | Magenta Meltdown | magenta shock `#FF1B8D` | bolle, pillole | mostro verde che morde | **scelta** |
| B | Cyan Riot | ciano `#14CFE0` | adesivi ritagliati | teschio con occhiali | scartata: meno "sporco" |
| C | Toxic Lemon | giallo `#FFE400` | fumetto | lingua con denti | scartata: troppo accecante su 780×460 |

**Scelta: A** — il magenta regge un fondo grande senza far sparire i controlli crema, e il verde acido
della mascotte è già il colore dell'elemento eroe.

## 3. Scheda stile

- **Pack palette**: A — MAGENTA MELTDOWN
- **Contorni**: ink `#0B0B0B`, 4 px su manopole e pulsanti, 3 px su etichette/pillole, 6 px sul bordo
  esterno dei pannelli, giunzioni tonde, jitter ±0.5 px sulle curve grandi
- **Riempimenti**: piatto + 1 lucentezza bianca 28% + 1 ombra dura (4,5)
- **Texture dominante**: halftone 10% sugli angoli dei pannelli, grana xerox 8% sul fondo, scanline 10%
  nei due display
- **Forme**: radius 14 su pannelli, pillole su pulsanti/badge, tag di sezione ruotati −6°, pulsanti −2°
- **Anatomia**: occhi sulla manopola DRIVE (eroe), denti sul bordo superiore del pannello STAGE 2
- **Tipografia**: display *Bungee* (SIL OFL) · etichette *Archivo Bold* (SIL OFL) · 24 / 11 / 10 px

## 4. Palette

| Ruolo | Hex | Uso | Contrasto su |
|---|---|---|---|
| ink | `#0B0B0B` | contorni, testo, ombre | panel 16.8:1 |
| bg | `#FF1B8D` | fondo finestra | — |
| panel | `#FFF3D4` | 3 pannelli + top bar | ink 16.8:1 |
| a1 | `#7CE01B` | DRIVE, manopole attive | ink 11.2:1 |
| a2 | `#FFE81C` | archi valore, meter | ink 15.9:1 |
| a3 | `#23D7F2` | hover, anelli, fulmini | ink 10.4:1 |
| extra | `#FF7DC0` | goo sui bordi, stelle | — |
| alert | `#E3122B` | clip, LED mute | ink 4.6:1 |

60% bg · 30% panel · 10% accenti. Nessun bianco su giallo o ciano.

## 5. Componenti

| Componente | Dimensione @1x | Riempimento | Contorno | Ombra | Stati |
|---|---|---|---|---|---|
| Manopola DRIVE (hero) | 96 px | `a1` | ink 4 + anello `a3` 4 | (4,5) | hover alone `a3` 20%; drag scala 1.03; bypass 50% + tratteggio |
| Manopole standard ×4 | 64 px | `a1` | ink 4 | (4,5) | come sopra, senza occhi |
| Manopola MIX | 64 px | `extra` | ink 4 | (4,5) | arco tratteggiato quando modulata |
| Pulsante sticker ON | 44 px h, −2° | `a2` | bianco 3 + ink 3 | (3,4) | premuto trasla (2,2); on = `a1` + ✓ |
| LED clip | 40×40 gemma | `panel` | ink 3 | (2,3) | off: ✕ ink 40% + tratteggio; on: `alert` + fulmine |
| Slider DRIVE trim | 128 px | `a1` fill | ink 3 | cursore (3,4) | cursore 28×44 `a2` |
| Pannello ×3 | 220×180 | `panel` | ink 3, radius 14 | (5,6) | tag adesivo `a3` ruotato −6° |
| Combo MODE | 36 px h | `panel` | ink 3 | (3,4) | hover `a3` 35%; popup non ruotato |
| Display ×2 | 200×72 | ink | panel 3 + ink 2 | nessuna | scanline 10%, traccia `a1` 2 px |
| Wordmark | 190×28 | — | ink | (3,4) | sottolineatura `a2` 6 px, −1° |

## 6. Layout

- Finestra **780×460**, fissa, variante @2x. Griglia 12 colonne, gutter 16, margini 20.
- `y 0–44`: top bar `panel`, wordmark a sinistra, combo MODE + pulsante ON a destra, bordo ink 6 sotto.
- `y 60–240`: pannello STAGE 1 (x 20–300) con DRIVE eroe + 2 manopole; pannello STAGE 2 (x 320–600)
  con 2 manopole + combo; pannello OUT (x 620–760) con LED clip e MIX.
- `y 260–420`: display waveform (x 20–400) + display curva (x 420–760).
- `y 420–440`: striscia footer con 4 stelle `extra` e versione 10 px.
- Sfondo: collage di sticker (mostro, fulmini, badge "GOO") portato a 14% di opacità dietro i pannelli.

## 7. Asset

| File | Formato | Dimensione | Contenuto | Dove |
|---|---|---|---|---|
| `mascot_fang.svg` | SVG | 220×260 | mostro verde con denti, occhi a X | footer destro, 14% di opacità |
| `bolt.svg` | SVG | 28×48 | fulmine, solo ink (colore a runtime) | meter, LED clip |
| `star.svg` | SVG | 24×24 | stella 5 punte | footer, sparsi |
| `goo_drip.svg` | SVG | 160×40 | colatura con goccia | bordo inferiore pannelli |
| `halftone_tile.png` | PNG | 128×128 | retino 45° seamless | pannelli, sfondo |
| `grain_tile.png` | PNG | 128×128 | rumore monocromatico | overlay fondo |
| `badge_blank.svg` | SVG | 120×40 | badge avvertenza **senza testo** (testo a runtime) | angolo top bar |

Nessun testo dentro gli asset.

## 8. Implementazione JUCE

- `AcidLookAndFeel : juce::LookAndFeel_V4` con override: `drawRotarySlider`, `drawLinearSlider`,
  `drawButtonBackground`, `drawButtonText`, `drawToggleButton`, `drawComboBox`, `drawPopupMenuBackground`,
  `drawPopupMenuItem`, `drawLabel`, `getTypefaceForFont`.
- Coordinate logiche 780×460 con `setResizeLimits`/scala su `@2x`; font con `juce::FontOptions`.
- Mascotte/fulmini/stelle/goo: `juce::Drawable::createFromSVG` + `juce_add_binary_data`; texture in PNG.
- Sfondo (collage + halftone + grana) in cache `juce::Image`, ricostruito solo in `resized()`.
- Display: `Timer` 30 Hz, traccia in `Path` preallocato, scanline in overlay.
- Parametri: `SliderAttachment`×6, `ButtonAttachment`×1 sull'APVTS.

## 9. I 3 segni distintivi

1. La manopola DRIVE con due occhi e arco giallo: è il "personaggio" del plugin.
2. I pannelli con tag adesivo ruotato e goo rosa sul bordo inferiore.
3. Il wordmark GOO FANG sottolineato da uno slash giallo su fondo magenta.

## 10. Cosa non è stato verificato

- Resa a 125% e 150% di scala su Windows.
- Contrasto misurato su monitor calibrato (i valori in tabella sono calcolati, non misurati).
- Ingombro reale dei font display nelle lingue diverse dall'italiano.
