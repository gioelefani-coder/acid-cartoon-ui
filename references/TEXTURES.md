# Texture — come si costruiscono

Tutte le texture sono **ripetibili** e **leggere** (un tile piccolo, ripetuto). Mai un PNG 4K.

---

## Halftone

**Cosa**: retino a punti, come la stampa a 4 colori. È il segno che dice "stampato".

- Passo griglia: 4–6 px @1x. Punti a 45° (non in quadrato dritto: deve sembrare ruotato).
- Diametro punto: 1.2–2.2 px, opacità 8–15%.
- Tile seamless: 128×128 px (o 64 per display), colore ink su trasparente.

SVG del tile (sostituibile con generazione procedurale):

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="8" height="8" viewBox="0 0 8 8">
  <circle cx="2" cy="2" r="1.1" fill="#0B0B0B"/>
  <circle cx="6" cy="6" r="1.1" fill="#0B0B0B"/>
</svg>
```

In JUCE si può anche generare a runtime (nessun asset):

```cpp
juce::Image makeHalftoneTile (int size = 8, float dotRadius = 1.1f)
{
    juce::Image tile (juce::Image::ARGB, size, size, true);
    juce::Graphics g (tile);
    g.setColour (juce::Colours::black);
    g.fillEllipse (size * 0.25f, size * 0.25f, dotRadius * 2.0f, dotRadius * 2.0f);
    g.fillEllipse (size * 0.75f, size * 0.75f, dotRadius * 2.0f, dotRadius * 2.0f);
    return tile;
}

// uso: riempimento del pannello, poi il retino in overlay
g.setColour (juce::Colours::black.withAlpha (0.10f));
g.fillTiledImage (makeHalftoneTile(), panelArea, juce::RectanglePlacement::stretchToFit);
```

---

## Grana xerox

- Tile di rumore 128×128, monocromatico, alpha 0–255 casuale ma con densità ~20%.
- Opacità globale 8–12%, blend normale (non `add`: schiarisce troppo).
- Va **sopra** tutto tranne testo e valori, oppure solo sullo sfondo. Scegli uno e sii coerente.
- Quando la grana è attiva, il pack D (Xerox Zine) è obbligatorio; negli altri pack è facoltativa.

---

## Scanline (display)

- 1 px ink ogni 3 px, opacità 10%, solo dentro il rettangolo del display.
- Si disegna dopo la traccia e prima delle etichette.

---

## Goo / drips

- Forma: `juce::Path` con una curva chiusa, 3–5 lobi arrotondati e **una** goccia appesa sotto.
- Riempimento `extra` (rosa goo `#FF7DC0` o arancio), contorno ink 3 px, una lucentezza.
- Usi ammessi: separatore tra sezioni, colatura dal bordo superiore del pannello, "piede" della mascotte.
- Mai come sfondo dietro a un'etichetta: solo su zone vuote o come bordo.

---

## Fulmine (energia, meter)

- Zigzag a 3–5 segmenti, larghezza 14–28 px, spessore tratto 6 px.
- Doppio contorno: ink 8 px sotto, accento 4 px sopra (identico alla manopola).
- Nei meter: il fulmine si riempie dal basso (clip rettangolare) e cambia in `alert` al clip.

---

## Stelle e scintille

- Stelle a 5 punte (SVG 24×24) e "+" a 4 punte, ink o accento, opacità 60–80%.
- Ruotate casualmente ma **con seed fisso** (stessa posizione a ogni apertura).
- Densità: max 1 elemento decorativo ogni 6000 px² di superficie libera.

---

## Bordi "strappati" (opzionale)

- Un lato del pannello con 6–10 dentelli irregolari, come carta strappata.
- Si implementa come `juce::Path` chiuso: costa poco e vale molto nel pack D.
- Alternativa: due passate di contorno offsettate di 0.5 px per simulare l'inchiostro a penna.

---

## Regole di performance

- Ogni tile/immagine si crea **una volta** (statica o membro) e si riusa.
- Sfondo completo (collage + halftone + goo + grana) → cache in `juce::Image` alla dimensione
  corrente; ricostruita solo in `resized()`.
- Nessuna allocazione di `Path`/`Image` dentro `paint()`: prepara i `Path` dei fulmini e delle stelle
  nel costruttore del componente.
