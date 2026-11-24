# Componenti — specifiche e implementazione

Tutte le misure sono **px a scala 1×**; a @2× si moltiplica tutto per 2 (o si disegna in coordinate
logiche e si lascia scalare il `Component`). Ogni componente elenca colori, stati e note di rendering.

Helper trasversale (da mettere una volta nel LookAndFeel):

```cpp
void hardShadow (juce::Graphics& g, juce::Rectangle<float> r, float radius,
                 juce::Point<float> offset = { 4.0f, 5.0f })
{
    g.setColour (ink);
    g.fillRoundedRectangle (r.translated (offset.x, offset.y), radius);
}
```

---

## 1. Manopola

| Variante | Diametro | Uso |
|---|---|---|
| Hero | 96 px | 1 per schermata (cutoff, drive, mix) |
| Standard | 64 px | la maggior parte dei parametri |
| Mini | 40 px | parametri secondari, hit target portato a 40×40 |

**Struttura (dall'indietro):**
1. ombra dura: cerchio ink, offset (4,5)
2. anello esterno: `a3` pieno, contorno ink 4 px
3. corpo: `a1` pieno, contorno ink 4 px, inset 6 px dall'anello
4. arco valore: sotto-traccia ink 10 px, sopra `a2` 6 px, da −135° a +135°, cappucci tondi
5. indicatore: cuneo ink, base 7 px, dal centro al bordo del corpo
6. lucentezza: ellisse bianca 28% in alto a sinistra (raggio 0.34×)
7. opzionale (solo hero): 2 occhi a puntino + sopracciglia ink → pareidolia

**Stati:**

| Stato | Cambiamento |
|---|---|
| idle | come sopra |
| hover | anello `a3` +1 px, alone `a3` 20% dietro (raggio +6) |
| drag | corpo scala 1.03, ombra offset (2,3) — sembra premuto |
| modulato | arco valore tratteggiato 4/3 e punto `a2` sul valore modulato |
| bypass | desaturato 50%, tratteggio diagonale ink 25% sopra |
| disabled | ink 40%, nessun alone |

---

## 2. Pulsante sticker

- Altezza 44 px, padding orizzontale 16, radius pillola, **rotazione −2°** (mai 0°).
- Bordo: bianco 3 px + ink 3 px esterno (effetto die-cut). Ombra dura (3,4).
- Testo ink bold 12 px uppercase, tracking +0.06em.
- Icona opzionale a sinistra 16×16, sempre con contorno ink.

| Stato | Cambiamento |
|---|---|
| hover | riempimento +8% luminosità, ombra (4,5) |
| premuto | trasla (2,2), ombra rimossa, bordo ink 4 |
| attivo/on | riempimento `a1`, testo ink, badge ✓ |
| disabled | ink 40%, tratteggio diagonale, nessuna ombra |
| focus (tastiera) | outline `a3` 2 px a 3 px di distanza, oltre il bordo |

---

## 3. Toggle / LED

- 40×40, forma a gemma (esagono arrotondato) o badge quadrato ruotato 4°.
- ON: `a1` pieno + ✓ ink spesso 4 px. OFF: `panel` + ✕ ink 40% + tratteggio.
- Cambio di stato con "pop" 1.15 → 1.00 in 90 ms (solo se l'host non è in modalità a basso consumo).

---

## 4. Slider verticale / orizzontale

- Lunghezza 128 px (verticale), spessore binario 14 px, radius pillola.
- Binario: `panel` con contorno ink 3; riempimento `a1` con contorno ink 3 (stessa geometria, clip).
- Cursore: capsula 28×44 (verticale) / 44×28 (orizzontale), `a2`, contorno ink 4, ombra dura (3,4),
  una lucentezza, indicatore ink 6×18 al centro.
- Ticks: tacche ink 2×6 ogni 10%, etichette solo agli estremi.

---

## 5. Pannello / sezione

- Riempimento `panel`, contorno ink 3 px, radius 14, ombra dura (5,6).
- **Titolo = tag adesivo** ruotato −6°, appoggiato sul bordo superiore sinistro, offset (−6,−10):
  pillola `a3` (o `a2`), bordo bianco 2 + ink 2, testo ink 10 px uppercase bold.
- Halftone `ink` 10% nel solo angolo in alto a destra (maschera rettangolare, non su tutto il pannello).
- Facoltativo: 2 viti/bulloni ink 6 px agli angoli opposti (fa "hardware", non "web").

---

## 6. Menu a tendina

- Altezza 36, radius pillola, `panel`, ink 3, ombra (3,4).
- Freccia = fulmine disegnato con `juce::Path` (3 segmenti), ink pieno, 12×10.
- Popup: `panel`, ink 3, radius 12, voci 26 px, hover `a3` 35%, voce selezionata `a1` + testo ink.
- Popup **non** ruotato: la rotazione è solo decorativa, mai su testi lunghi o liste.

---

## 7. Display (waveform / ADSR / meter)

- Finestra `ink` pieno, radius 12, bordo `panel` 3 px esterno + ink 2.
- Traccia: `a1` 2 px, oppure `extra` fosforo nei pack scuri (D).
- Overlay: scanline ink 10%, halftone 6%, angolo "REC" con pallino `alert` 6 px.
- Griglia: ink 25%, 4 divisioni, mai sopra la traccia.
- Etichette dentro il display: **testo JUCE** (mai baked), 10 px, `panel` 80%.

---

## 8. Badge / wordmark

- Badge tipo "avvertenza": rettangolo `panel`, ink 2, doppio filetto interno, testo ink 8–9 px
  uppercase, **contenuto inventato** (mai "Parental Advisory" o loghi reali).
- Wordmark: display font, ink pieno, sottolineatura `a2` 6 px ruotata −1°, ombra dura (3,4).
- Mascotte: 1 sola, 120–220 px, PNG/SVG @2x con contorno ink, mai sopra un controllo.

---

## Mapping JUCE

Base: `juce::LookAndFeel_V4` con override mirati. Nessun ridisegno da zero del framework.

| Override | Dove |
|---|---|
| `drawRotarySlider` | §1 |
| `drawLinearSlider` | §4 |
| `drawButtonBackground` / `drawButtonText` | §2 |
| `drawToggleButton` | §3 |
| `drawComboBox` / `positionComboBoxText` | §6 |
| `drawPopupMenuBackground` / `drawPopupMenuItem` | §6 |
| `drawLabel` | etichette, tracking e colore ink |
| `getTypefaceForFont` | display vs etichette |
| `drawDocumentWindowTitleBar` | top bar (se finestra non nativa) |

### Scheletro del LookAndFeel

```cpp
class AcidLookAndFeel : public juce::LookAndFeel_V4
{
public:
    // token della palette, uno per ruolo
    juce::Colour ink   { 0xFF0B0B0B }, bg { 0xFFFF1B8D }, panel { 0xFFFFF3D4 };
    juce::Colour a1    { 0xFF7CE01B }, a2 { 0xFFFFE81C }, a3 { 0xFF23D7F2 };
    juce::Colour extra { 0xFFFF7DC0 }, alert { 0xFFE3122B };

    void drawRotarySlider (juce::Graphics& g, int x, int y, int w, int h,
                           float pos, float startAngle, float endAngle,
                           juce::Slider& s) override
    {
        auto b = juce::Rectangle<float> ((float) x, (float) y, (float) w, (float) h)
                     .reduced (3.0f);
        auto r = juce::jmin (b.getWidth(), b.getHeight()) * 0.5f;
        auto c = b.getCentre();
        auto angle = startAngle + pos * (endAngle - startAngle);

        // 1. ombra dura
        g.setColour (ink);
        g.fillEllipse (juce::Rectangle<float> (r * 2.0f, r * 2.0f)
                           .withCentre (c.translated (4.0f, 5.0f)));

        // 2. anello
        auto ring = juce::Rectangle<float> (r * 2.0f, r * 2.0f).withCentre (c);
        g.setColour (a3); g.fillEllipse (ring);
        g.setColour (ink); g.drawEllipse (ring, 4.0f);

        // 3. corpo
        auto body = ring.reduced (6.0f);
        g.setColour (a1); g.fillEllipse (body);
        g.setColour (ink); g.drawEllipse (body, 4.0f);

        // 4. arco valore (doppio tratto)
        juce::Path arc;
        arc.addCentredArc (c.x, c.y, r - 8.0f, r - 8.0f, 0.0f,
                           startAngle, angle, true);
        g.setColour (ink);   g.strokePath (arc, juce::PathStrokeType (10.0f,
                                   juce::PathStrokeType::curved,
                                   juce::PathStrokeType::rounded));
        g.setColour (a2);    g.strokePath (arc, juce::PathStrokeType (6.0f,
                                   juce::PathStrokeType::curved,
                                   juce::PathStrokeType::rounded));

        // 5. indicatore a cuneo
        juce::Path wedge;
        const auto wBase = 7.0f, rIn = body.getWidth() * 0.18f, rOut = body.getWidth() * 0.46f;
        wedge.addTriangle (-wBase * 0.5f, -rIn,  wBase * 0.5f, -rIn,  0.0f, -rOut);
        g.setColour (ink);
        g.fillPath (wedge, juce::AffineTransform::rotation (angle).translated (c));

        // 6. lucentezza
        g.setColour (juce::Colours::white.withAlpha (0.28f));
        g.fillEllipse (juce::Rectangle<float> (r * 1.1f, r * 0.8f)
                           .withCentre (c.translated (r * -0.32f, r * -0.34f)));
    }
};
```

### Regole di resa (solo ciò che riguarda lo stile)

- **Rotazione** (pulsanti sticker): `g.saveState(); g.addTransform (juce::AffineTransform::rotation (
  juce::degreesToRadians (-2.0f), cx, cy)); … g.restoreState();` — ruota il *disegno*, mai il
  `Component` (rompe hit test e layout).
- **Inchiostro**: `PathStrokeType` sempre con giunzioni `rounded`; per il jitter usare due passate
  sfalsate di 0.5 px, non un blur.
- **Texture**: halftone e grana come `juce::Image` tiled con `fillTiledImage`; mai generate in `paint()`.
- **Asset**: SVG per mascotte, fulmini, stelle, goo, badge (colore applicato a runtime); PNG solo per
  halftone e grana. Niente JPEG per i contorni netti. Formati e bundling: vedi la skill di processo.
- **Sfondo**: collage + halftone + grana in cache `juce::Image`, ricostruita solo in `resized()`;
  `paint()` disegna solo controlli e ombre.
- **Qualità**: `g.setImageResamplingQuality (juce::Graphics::highResamplingQuality)` prima di
  disegnare immagini scalate.
- **Accessibilità**: hit target ≥ 40×40 anche per i controlli mini; contrasto delle etichette
  verificato sul pannello, non sullo sfondo collage.

Font, APVTS/attachment, bundling degli asset e struttura del tema: regole generali nella skill di
processo (`plugin-visual-design`, step tecnico). Qui non si ripetono.
