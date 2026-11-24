# Prompt — solo il blocco stile

Il prompt di progetto (ruolo, ancore, direzioni, layout, asset, consegna in `design-brief.md`) è quello
della skill di processo (`plugin-visual-design`). Qui c'è **solo** il pezzo che va aggiunto per ottenere
questa estetica. Non riscrivere il prompt da capo: incolla il blocco.

---

## 1. BLOCCO STILE (da incollare in qualsiasi prompt di progetto)

```
Estetica: acid cartoon / sticker bomb / fanzine fotocopiata.
- Inchiostro nero #0B0B0B su ogni forma, 3–4 px (5–6 px sul bordo dei pannelli), giunzioni tonde.
- Colore piatto, nessun gradiente. Un solo fondo shock, pannelli crema, max 2 accenti dominanti,
  proporzione 60/30/10.
- Ombre sempre dure e offsettate (4,5), mai sfocate. Una sola lucentezza bianca 28% per forma.
- Forme a bolla/pillola, radius 10–18 px, pulsanti e badge ruotati 2–6°.
- Texture: halftone 8–15% e grana xerox 8–12% solo sotto etichette e numeri.
- Anatomia cartoon (occhi, denti, cuore, goo) solo su 1–2 controlli eroe.
- Icone disegnate a mano, nessuna emoji, nessun logo o personaggio esistente copiato.
- Testo funzionale sempre vivo (mai dentro le immagini), contrasto ≥ 4.5:1.

Deve sembrare un adesivo incollato su un poster; NON un render 3D, NON una UI minimal, NON glassmorphism.
Per palette, dimensioni e stati usa i pack e le specifiche di acid-cartoon-ui.
```

---

## 2. Solo estetica (restyling di una UI già esistente)

```
Questa UI esiste già e struttura/parametri sono fissi: [elenco controlli + dimensioni].
Ridisegnala in stile acid cartoon / sticker bomb senza toccare il layout:
dammi 1 palette con hex e ruoli, 1 set di regole contorno/ombra/texture, le specifiche dei
componenti già presenti con stati, e il piano di resa in un LookAndFeel JUCE custom.
Max 2 pagine, solo il layer visivo.
```

---

## 3. Varianti (una riga da aggiungere al blocco)

| Serve | Aggiungi |
|---|---|
| Più fumetto, meno poster | `Prevalenza di inchiostro: contorni 5–6 px, tratteggio incrociato sulle ombre.` |
| Più fotocopia | `Grana xerox 12%, nero non perfetto, fuori registro dei riempimenti ±1 px.` |
| Più giocattolo | `Forme bombate, proporzioni 1.4×, lucentezze più grandi, viti a vista.` |
| Sessione lunga, leggibilità | `Accenti solo su stato; pannelli crema al 45% della superficie; testo ink 12 px minimo.` |
| Finestra piccola (≤ 620×380) | `Un solo elemento eroe, 8 controlli max, il resto in due pannelli.` |
| Pack scuro/fotocopia | `Pack D: fondo collage desaturato, scanline sui display, verde fosforo per le tracce.` |
