# Palette pack — acid cartoon

Ogni pack è un sistema chiuso: `ink`, `bg`, `panel`, `a1`, `a2`, `a3`, `extra`, `alert`.
Nomi token pensati per essere usati anche come costanti C++ (`Colours::bg`, `Colours::a1`, …).

Regola trasversale: **un pack per plugin**, al massimo 1 tinta presa in prestito da un altro pack
(diventa `extra`). Non mescolare due pack alla pari.

---

## Pack A — MAGENTA MELTDOWN
Il più vicino alle reference: fondo magenta shock, pelle verde acido, fulmini gialli, goo rosa.

| Token | Hex | Uso |
|---|---|---|
| `ink` | `#0B0B0B` | contorni, testo, ombre dure |
| `bg` | `#FF1B8D` | fondo finestra |
| `panel` | `#FFF3D4` | pannelli, aree controllo |
| `a1` | `#7CE01B` | manopola eroe, valore attivo |
| `a2` | `#FFE81C` | archi valore, meter, badge |
| `a3` | `#23D7F2` | hover, anelli, scintille |
| `extra` | `#FF7DC0` | goo, decorazione |
| `alert` | `#E3122B` | clip, bypass, errore |

Contrasti utili: ink/panel 16.8:1 · ink/a2 15.9:1 · ink/a3 10.4:1 · ink/a1 11.2:1.
Mai bianco su `a2` o su `a3`.

---

## Pack B — CYAN STICKER RIOT
Fondo ciano pieno, sticker rosa/rosso/giallo: più "poster da muro", meno "acido".

| Token | Hex | Uso |
|---|---|---|
| `ink` | `#0B0B0B` | contorni, testo |
| `bg` | `#14CFE0` | fondo finestra |
| `panel` | `#FFF6E0` | pannelli |
| `a1` | `#FF2E97` | accento primario |
| `a2` | `#FFE20A` | accento secondario |
| `a3` | `#6BE01A` | stato attivo |
| `extra` | `#FF6A1A` | goo/arancio bruciato |
| `alert` | `#D81228` | clip |

Contrasti: ink/panel 17.1:1 · ink/a2 15.4:1 · ink/a1 4.9:1 (usare ink, non bianco).

---

## Pack C — TOXIC LEMON
Fondo giallo limone: massima energia, richiede disciplina (il giallo perdona poco).

| Token | Hex | Uso |
|---|---|---|
| `ink` | `#0B0B0B` | contorni, testo |
| `bg` | `#FFE400` | fondo |
| `panel` | `#FFFFFF` | pannelli (bianco pieno per far respirare) |
| `a1` | `#9B2BE8` | viola uva, accento primario |
| `a2` | `#00C2A8` | verde acqua, accento secondario |
| `a3` | `#FF2E97` | evidenza |
| `extra` | `#FF6A1A` | goo |
| `alert` | `#E3122B` | clip |

Contrasti: ink/a1 7.4:1 · ink/a2 8.1:1 · ink/bg 15.9:1.
Il bianco puro va usato **solo** come pannello e bordo sticker, mai come testo su giallo.

---

## Pack D — XEROX ZINE
Fotocopia: fondo collage fotografico, inchiostro nero, due accenti. Per prodotti "underground".

| Token | Hex | Uso |
|---|---|---|
| `ink` | `#0B0B0B` | contorni, testo |
| `bg` | collage (foto desaturata + magenta `#FF2E97` in `Multiply`) | fondo |
| `panel` | `#F4EFE2` | pannelli carta |
| `a1` | `#FF2E97` | accento primario |
| `a2` | `#FFE400` | accento secondario |
| `a3` | `#0B0B0B` | "accento" negativo: stati in nero pieno invertito |
| `extra` | `#B9FF3C` | verde fosforo per display |
| `alert` | `#E3122B` | clip |

Grana xerox obbligatoria 10–12%. Se la grana non c'è, il pack non funziona.

---

## Combinazioni sconsigliate

| Combinazione | Problema |
|---|---|
| A + C | due fondi shock: la finestra non ha un centro |
| giallo limone + bianco come testo | illeggibile |
| verde acido su ciano | ~1.2:1, vibrazione dolorosa |
| magenta su rosso sangue | si confondono a 1 m di distanza |
| 3 accenti + `extra` + `alert` tutti visibili insieme | 5 colori accesi = nessuna gerarchia |

## Derivati ammessi (senza rompere il sistema)

- `panel` schiarito del 6% per hover di pannello.
- `a1` al 30% per alone/halo (solo dietro, mai sopra testo).
- `ink` al 40% per stati disabled, sempre accompagnato da tratteggio diagonale.
- `bg` scurito del 10% per la fascia top bar (crea profondità senza gradienti).
