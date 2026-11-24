---
name: acid-cartoon-ui
description: Modulo estetico "acid cartoon / sticker bomb / xerox punk" per UI di plugin audio: DNA dello stile, palette con hex, forme, texture halftone/goo, tipografia, anatomia cartoon, anti-pattern e resa dei componenti. Si innesta al posto di scheda stile + palette + componenti di una skill di processo (es. plugin-visual-design). Usa quando l'utente chiede colori accesi, contorni neri spessi, cartoonesco, sticker, fumetto/fanzine.
---

# Acid Cartoon UI — modulo estetico

Questa skill **non è un processo**: è il layer visivo. Non estrae ancore, non propone direzioni,
non decide il layout, non scrive il brief: quello è compito della skill di processo
(`plugin-visual-design` o equivalente).

Qui c'è solo ciò che rende un'interfaccia "acid cartoon", con numeri implementabili:
scheda stile, palette, forme, texture, tipografia, resa dei componenti, anti-pattern, checklist.

Regola numero zero: **lo stile è un sistema di vincoli, non un collage di citazioni**. Un elemento che
non rispetta i token non è "più ricco": è rumore.

---

## 1. DNA — le 7 ossa dello stile

| # | Osso | Come si riconosce |
|---|---|---|
| 1 | **Inchiostro nero spesso** | ogni forma ha contorno nero pieno 3–6 px, mai sottile, mai grigio, mai soft |
| 2 | **Colore piatto saturo** | riempimenti senza gradienti; 3–4 tinte accese che si scontrano di proposito |
| 3 | **Cartone** | forme a bolla/pillola, proporzioni esagerate, anatomia improbabile (occhi, denti, cuori, lingue) |
| 4 | **Stampato male** | halftone, grana xerox, bordi irregolari, leggero fuori registro |
| 5 | **Sticker bomb** | elementi ritagliati con bordo bianco + bordo nero, sovrapposti e ruotati di 3–12° |
| 6 | **Energia disegnata** | fulmini, scintille "+", gocce di goo, stelle: il suono si vede |
| 7 | **Cattivo gusto controllato** | volutamente eccessivo, mai casuale; la leggibilità viene prima della decorazione |

Deve sembrare **un adesivo incollato su un poster**, NON un render 3D, NON una UI minimal di design
system, NON glassmorphism.

---

## 2. Colori

### 2.1 Ruoli

| Ruolo | Funzione | Regola |
|---|---|---|
| **ink** | contorni, testo, ombre dure | `#0B0B0B`, mai nero puro `#000` (stampa più calda) |
| **bg** | un solo colore shock per schermata | 40–60% della superficie, saturo, senza gradiente |
| **panel** | superficie dei controlli | crema/bianco sporco: serve a far leggere le etichette |
| **a1** | accento primario | manopola eroe, valore attivo |
| **a2** | accento secondario | archi valore, meter, badge |
| **a3** | terzo accento | hover, anelli, scintille |
| **extra** | goo, decorazione | uno solo per schermata |
| **alert** | clip, bypass, errore | mai decorativo |

Proporzione **60% bg / 30% panel / 10% accenti**. Oltre il 15% di accenti la UI diventa un muro di neon
e i controlli spariscono.

### 2.2 Contrasto (non negoziabile)

- Testo funzionale: ink su crema, oppure ink su giallo/ciano. Mai bianco su giallo o ciano.
- Accento su accento sempre separato da inchiostro (contorno o gap).
- Etichette e valori ≥ 4.5:1. Il colore acceso indica **stato**, non decorazione.

### 2.3 Pack pronti (dettaglio in `references/PALETTES.md`)

| Pack | Carattere | bg | a1 | a2 | a3 |
|---|---|---|---|---|---|
| A MAGENTA MELTDOWN | il più vicino alle reference: pelle verde, fulmini gialli, goo rosa | `#FF1B8D` | `#7CE01B` | `#FFE81C` | `#23D7F2` |
| B CYAN STICKER RIOT | poster da muro, meno acido | `#14CFE0` | `#FF2E97` | `#FFE20A` | `#6BE01A` |
| C TOXIC LEMON | massima energia, richiede disciplina | `#FFE400` | `#9B2BE8` | `#00C2A8` | `#FF2E97` |
| D XEROX ZINE | fotocopia + collage, grana obbligatoria | collage | `#FF2E97` | `#FFE400` | ink invertito |

Un pack per prodotto; al massimo una tinta presa in prestito (diventa `extra`).

---

## 3. Forme e linee

- Raggi 10–18 px sui pannelli, pillola (999) su pulsanti e badge. Nessuno spigolo vivo.
- Contorno 3 px su elementi piccoli, 4 px su manopole/pulsanti, 5–6 px sul bordo esterno dei pannelli.
- Il contorno può tremare di ±0.5 px: due passate sfalsate, mai "vettoriale perfetto".
- **Ombra dura** offset (4,5), stesso inchiostro, nessuna sfocatura. È l'ombra che fa "adesivo".
- Una sola lucentezza bianca 25–30% in alto a sinistra.
- Anatomia cartoon (occhi a puntino, X, denti, cuore, lingua) solo su 1–2 controlli "eroe".

---

## 4. Texture

| Texture | Dove | Come |
|---|---|---|
| Halftone | pannelli grandi, sfondo, badge | retino 45°, passo 4–6 px, opacità 8–15% |
| Grana xerox | overlay fondo | tile di rumore 128 px, 8–12% |
| Scanline | display | 1 px ink ogni 3 px, 10% |
| Brush/marker | dentro i riempimenti piatti | pennellate irregolari ±10% luminosità, mai gradienti |
| Goo | separatori, bordi pannello | gocce con gocciolina appesa, `extra` + contorno ink |
| Fulmine | meter, livelli, indicatori | zigzag 3–5 segmenti, doppio contorno ink + accento |
| Stelle / "+" | riempitivo tra i controlli | 5 punte, 24 px, opacità 60–80%, seed fisso |

Le texture **non passano mai sopra un'etichetta o un valore**: sotto sì, sopra no.

Generazione (SVG, tile, procedurale in JUCE): `references/TEXTURES.md`.

---

## 5. Tipografia

- 2 famiglie massimo, licenza dichiarata (SIL OFL preferibile).
- **Display** hand-lettered/poster: *Bungee*, *Shrikhand*, *Permanent Marker* → solo nome plugin e titoli.
- **Etichette** sans condensato bold: *Archivo*, *Barlow Condensed*, *Rubik* → tutti i parametri.
- Titolo 22–28 px · sezione 10–11 px uppercase tracking +0.08em · etichetta 11 px · valore 10 px tabellare.
- Il wordmark può ruotare di −3° con sottolineatura a slash colorato.
- Mai testo dentro PNG/SVG. Mai emoji come icone: le icone sono disegnate, con contorno ink.

---

## 6. Gerarchia e densità

- 1 elemento eroe (il doppio degli altri), 3–6 secondari, il resto piccolo e silenzioso.
- Massimo 12 controlli interattivi per pannello.
- Griglia 8/16/24, margini 16–20; hit target ≥ 40×40 px anche con disegno da 28 px.
- Sfondo collage dietro i controlli al 12–18% di opacità, o coperto dai pannelli crema.

---

## 7. Resa dei componenti

Qui solo **come appare** ogni controllo nello stile; specifiche px, stati completi e codice in
`references/COMPONENTS.md`.

- **Manopola**: capsula cartoon con indicatore a cuneo ink, arco valore doppio (ink 10 px sotto,
  accento 6 px sopra), una lucentezza. Ruota, non si inclina. Hero 96 / standard 64 / mini 40 px.
- **Pulsante**: pillola ruotata −2°, bordo bianco 3 + ink 3, testo ink bold; premuto scende di (2,2) e
  perde l'ombra (feedback fisico da adesivo).
- **Toggle/LED**: gemma o badge con ✓/✕ disegnati; off a ink 40% con tratteggio.
- **Slider**: binario a pillola ink, cursore a capsula `a2`, riempimento accento con contorno.
- **Pannello**: crema, ink 3, radius 14, ombra (5,6), titolo come **tag adesivo ruotato −6°**,
  halftone 10% in un solo angolo.
- **Display**: finestra ink, linea accento 2 px, scanline 10%, angoli arrotondati.
- **Meter/clip**: fulmine che si riempie; al clip diventa `alert` e lampeggia a 2 Hz.
- **Badge/wordmark**: badge tipo avvertenza con testo **inventato**, wordmark display con sottolineatura.

---

## 8. Cosa NON è (anti-pattern)

| Sbagliato | Perché |
|---|---|
| 5–6 neon alla stessa intensità | nessuna gerarchia, l'occhio non trova i controlli |
| Contorni 1 px o grigi | sembra un bug di rendering, non un cartone |
| Gradienti morbidi, blur, glass | annulla l'effetto stampa/adesivo |
| Ombre sfocate | l'ombra dura è l'identità dello stile |
| Faccina su ogni manopola | rumore: l'anatomia va su 1–2 controlli eroe |
| Emoji o icone stock | rompe l'unità del disegno |
| Halftone sopra etichette e numeri | illeggibilità |
| Copiare "Parental Advisory", loghi o personaggi esistenti | marchi e copyright: si cita lo spirito, non il logo |
| Testo dentro PNG/SVG | sfocato a @2x, non traducibile |
| Collage di sfondo alla saturazione della UI | i controlli scompaiono |

---

## 9. Come si innesta

1. La skill di processo produce ancore, 3 direzioni, layout, asset e consegna.
2. Questa skill fornisce i blocchi **scheda stile + palette + componenti** da inserire in quel brief,
   scelti con l'utente o dichiarando l'assunzione (`references/PALETTES.md`, `references/COMPONENTS.md`).
3. Se non è disponibile una skill di processo: ancore e tre direzioni restano necessarie, ma sono
   definite là, non qui — non riscriverle in questo file.
4. Se l'utente vuole solo la pelle: usa il blocco "solo estetica" in `references/PROMPTS.md`.

---

## 10. Checklist di autoverifica (solo estetica)

1. Un solo fondo shock, un solo pannello chiaro, ≤ 2 accenti dominanti.
2. Ogni forma ha contorno ink ≥ 3 px.
3. Ogni ombra è dura e offsettata, nessun blur.
4. Testo funzionale ≥ 4.5:1, nessun bianco su giallo/ciano.
5. Halftone/grana solo sotto il testo, opacità ≤ 15%.
6. Un elemento eroe evidente; anatomia cartoon su ≤ 2 controlli.
7. Almeno 3 elementi sticker (bordo bianco + ink, ruotati), nessuno sopra un'etichetta.
8. Icone disegnate, nessuna emoji, nessun logo di terzi copiato.
9. Componenti in px @1x con variante @2x e hit target ≥ 40 px.
10. Il brief dice cosa NON deve sembrare e come ottenerlo.

---

## 11. Nota legale

Lo stile cita sottoculture (skate, fanzine, sticker art, cartoon underground) senza riprodurre opere,
personaggi, loghi o badge altrui: nomi, mascotte e badge vanno inventati. Font e asset: licenza
dichiarata nel brief.
