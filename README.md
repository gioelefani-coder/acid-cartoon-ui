# acid-cartoon-ui

Modulo estetico per assistenti AI (formato `SKILL.md`) che insegna un linguaggio visivo preciso:
**acid cartoon, sticker bomb, fanzine fotocopiata**, applicato alle interfacce dei plugin audio (e a
qualsiasi UI che debba sembrare un adesivo incollato su un poster).

Non è un processo e non è un template grafico: è il layer visivo, con numeri. Contorni neri 3–6 px,
ombre dure senza blur, palette a 5 ruoli con hex, halftone all'8–15%, anatomia cartoon solo sui
controlli eroe.

## Rapporto con una skill di processo

Questa skill non estrae ancore, non propone direzioni, non decide layout, asset o consegna: quelle
restano alla skill di processo (`plugin-visual-design`, che ha la pipeline completa e il file
`design-brief.md`). `acid-cartoon-ui` fornisce **scheda stile, palette, forma dei componenti, texture,
tipografia e checklist estetica** da inserire in quel brief. Il prompt di progetto non si riscrive:
si aggiunge il blocco stile di `references/PROMPTS.md`.

## Cosa contiene

```
acid-cartoon-ui/
├─ SKILL.md                     dottrina visiva: DNA, colori, forme, texture, tipografia, anti-pattern, checklist
├─ references/
│  ├─ PALETTES.md               4 pack di palette con hex, ruoli, contrasti, combinazioni vietate
│  ├─ COMPONENTS.md             specifiche px + stati dei componenti e codice di resa JUCE
│  ├─ TEXTURES.md               halftone, grana xerox, goo, fulmini, stelle: come si costruiscono
│  └─ PROMPTS.md                blocco stile da incollare nel prompt di progetto + varianti
├─ templates/
│  └─ design-brief.md           annex del solo layer visivo (scheda stile, palette, componenti, vincoli)
└─ examples/
   ├─ design-brief-esempio.md   esempio compatto (plugin inventato "GOO FANG")
   └─ delay-stereo/design-brief.md   prova completa: delay stereo 820×500, 8 parametri
```

## Installazione

**Come skill di progetto (Claude Code / agenti con `skills/`):** copia la cartella in
`.claude/skills/acid-cartoon-ui/` (progetto) o `~/.claude/skills/acid-cartoon-ui/` (globale).
Il nome della cartella deve coincidere con il `name` nel frontmatter di `SKILL.md`.

**Da GitHub:**

```bash
git clone <url-del-repo> acid-cartoon-ui
cp -r acid-cartoon-ui ~/.claude/skills/
```

**In un catalogo di skill dell'app:** carica `SKILL.md` come istruzioni e i file in `references/`
come risorse; `templates/` e `examples/` servono come materiale di consultazione.

## Uso

Chiedi una UI con le dritte:

> Progetta l'interfaccia di GOO FANG, un saturatore VST3. Dritte: acido, masticato, giocoso;
> ispirato a sticker da skate e cartoni underground; deve sembrare un adesivo, non una UI 3D.
> Finestra 780×460, 7 parametri.

Con la skill di processo il flusso resta il suo (ancore, tre direzioni, brief): questa skill fornisce
il pack di palette e le specifiche visive da inserire lì. Il risultato combinato è visibile in
`examples/delay-stereo/design-brief.md`: delay stereo 820×500, 8 parametri, coordinate e stati compresi.

## Regole che la skill impone

- Un solo fondo shock, un solo pannello chiaro, massimo 2 accenti dominanti.
- Ogni forma ha un contorno ink ≥ 3 px; ogni ombra è dura e offsettata.
- Nessuna texture sopra etichette e valori; contrasto ≥ 4.5:1 sul testo funzionale.
- Anatomia cartoon su 1–2 controlli eroe, non su tutti.
- Icone disegnate, niente emoji, nessun logo o personaggio esistente copiato.
- Testo sempre vivo (mai dentro SVG/PNG).

## Licenza

MIT — vedi `LICENSE`. Lo stile cita sottoculture visive (skate, fanzine, cartoon underground) senza
riprodurre opere, personaggi o marchi altrui: badge, mascotte e nomi vanno inventati. I font suggeriti
sono indicati con licenza SIL OFL; verifica la licenza prima della distribuzione commerciale.
