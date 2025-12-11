# Piano di Implementazione - Milestone 1 MVP

## 📋 Checklist Generale

- [ ] Step 1: Struttura dati note ↔ fretting
- [ ] Step 2: Integrazione VexFlow + CDN
- [ ] Step 3: UI base + layout mobile
- [ ] Step 4: Tastiera virtuale custom
- [ ] Step 5: Esercizio Tipo 1 (Nota → Fretting)
- [ ] Step 6: Esercizio Tipo 2 (Fretting → Nota)
- [ ] Step 7: Sistema punteggio e feedback
- [ ] Step 8: Testing e polish
- [ ] Step 9: Documentazione aggiornata
- [ ] Step 10: Commit e push

---

## Step 1: Struttura Dati Note ↔ Fretting

### Obiettivo
Creare la mappatura completa tra note musicali e posizioni sulla tastiera del basso (20 fret).

### Output
```javascript
// Note musicali (solo naturali, no diesis/bemolle)
const NOTES = ['C', 'D', 'E', 'F', 'G', 'A', 'B'];

// Semitoni dalla nota C
const NOTE_OFFSETS = {
  'C': 0, 'D': 2, 'E': 4, 'F': 5,
  'G': 7, 'A': 9, 'B': 11
};

// Accordatura standard (nota assoluta in semitoni da C0)
const TUNING = {
  'e': 28,  // E1
  'a': 33,  // A1
  'd': 38,  // D2
  'g': 43   // G2
};

// Funzioni di conversione
function frettingToNote(fretting) { /* ... */ }
function noteToFrettings(note) { /* ... */ }
```

### Task dettagliate
- [ ] Definire costanti base (NOTE, NOTE_OFFSETS, TUNING)
- [ ] Implementare `frettingToNote(fretting)` → es: "a3" → "C2"
- [ ] Implementare `noteToFrettings(note)` → es: "C2" → ["a3", "e8", ...]
- [ ] Testing console: verificare conversioni sono corrette
- [ ] Generare array di tutte le note possibili (E1 - G5)

---

## Step 2: Integrazione VexFlow

### Obiettivo
Integrare la libreria VexFlow per rendering del pentagramma in chiave di basso.

### Output
- VexFlow caricato da CDN
- Funzione `renderNote(noteName)` che disegna una nota sul pentagramma
- Container SVG responsive

### Task dettagliate
- [ ] Aggiungere CDN VexFlow nel `<head>`:
  ```html
  <script src="https://cdn.jsdelivr.net/npm/vexflow@4.2.2/build/cjs/vexflow.js"></script>
  ```
- [ ] Creare container `<div id="staff-container"></div>`
- [ ] CSS per rendere il container responsive
- [ ] Implementare funzione `renderNote(note, octave)`
- [ ] Testare rendering di note diverse (C2, E1, G3, ecc.)
- [ ] Gestire chiave di basso (bass clef)

### Documentazione VexFlow
- Usare `Vex.Flow.Stave` per il pentagramma
- Usare `Vex.Flow.StaveNote` per le note
- Chiave di basso: `new Vex.Flow.Stave(...).addClef("bass")`

---

## Step 3: UI Base + Layout Mobile

### Obiettivo
Creare il layout principale dell'app, ottimizzato per mobile.

### Componenti UI
```
┌─────────────────────────────┐
│    Bass Notes Learning      │
│         Score: 0            │
├─────────────────────────────┤
│                             │
│   [Pentagramma VexFlow]     │
│                             │
├─────────────────────────────┤
│       Domanda:              │
│   Qual è il fretting?       │
├─────────────────────────────┤
│                             │
│   [Tastiera Virtuale]       │
│                             │
├─────────────────────────────┤
│     [Conferma] [Skip]       │
├─────────────────────────────┤
│      Feedback Area          │
└─────────────────────────────┘
```

### Task dettagliate
- [ ] Header con titolo + score counter
- [ ] Container pentagramma (fisso in alto)
- [ ] Sezione domanda/istruzioni
- [ ] Area tastiera virtuale (placeholder)
- [ ] Bottoni azione (Conferma, Skip, Nuovo)
- [ ] Feedback area (nascosta di default)
- [ ] CSS responsive con breakpoint mobile
- [ ] Testare su dimensioni diverse

---

## Step 4: Tastiera Virtuale Custom

### Obiettivo
Costruire input touch-friendly per fretting e note.

### Design Tastiera Fretting
```
Corde:  [e] [a] [d] [g]

Fret:   [0] [1] [2] [3] [4]
        [5] [6] [7] [8] [9]
        [10][11][12][13][14]
        [15][16][17][18][19][20]

Input corrente: "a3"

        [Reset] [Backspace]
```

### Design Tastiera Note
```
Note:   [A] [B] [C] [D] [E] [F] [G]

Ottava: [1] [2] [3] [4] [5]

Input corrente: "C2"

        [Reset] [Backspace]
```

### Task dettagliate
- [ ] Componente tastiera fretting:
  - [ ] Bottoni corde (e, a, d, g)
  - [ ] Numpad 0-20
  - [ ] Display input corrente
  - [ ] Bottoni Reset/Backspace
- [ ] Componente tastiera note:
  - [ ] Bottoni lettere A-G
  - [ ] Numpad ottave 1-5
  - [ ] Display input corrente
  - [ ] Bottoni Reset/Backspace
- [ ] CSS touch-friendly (min 44x44px)
- [ ] Feedback visivo al click (active state)
- [ ] Gestione stato input (string building)
- [ ] Validazione formato (es: "a3" valido, "a23" no)

---

## Step 5: Esercizio Tipo 1 (Nota → Fretting)

### Flusso Completo
1. App genera nota random (es: "C2")
2. Renderizza nota sul pentagramma con VexFlow
3. Mostra domanda: "Qual è il fretting per questa nota?"
4. Utente inserisce con tastiera virtuale (es: "a3")
5. Utente clicca [Conferma]
6. App valida risposta:
   - Corretto: +1 punto, feedback verde, mostra alternative
   - Sbagliato: 0 punti, feedback rosso, mostra risposta corretta
7. Bottone [Prossima] per continuare

### Task dettagliate
- [ ] Funzione `generateRandomNote()` → es: "C2"
- [ ] Render nota su pentagramma
- [ ] Mostra tastiera fretting
- [ ] Gestione click [Conferma]:
  - [ ] Validazione risposta
  - [ ] Update score
  - [ ] Mostra feedback
  - [ ] Mostra posizioni alternative
- [ ] Bottone [Prossima] → nuovo esercizio
- [ ] Transizioni smooth tra esercizi

---

## Step 6: Esercizio Tipo 2 (Fretting → Nota)

### Flusso Completo
1. App genera fretting random (es: "d5")
2. Mostra fretting grande al centro
3. Mostra domanda: "Che nota è questo fretting?"
4. Utente inserisce nota con tastiera note (es: "G2")
5. Utente clicca [Conferma]
6. App valida risposta:
   - Solo lettera corretta: +1 punto
   - Lettera + ottava corretta: +2 punti
   - Sbagliato: 0 punti
7. Feedback con risposta completa
8. Bottone [Prossima] per continuare

### Task dettagliate
- [ ] Funzione `generateRandomFretting()` → es: "d5"
- [ ] Display fretting grande (tipografia)
- [ ] Mostra tastiera note
- [ ] Gestione click [Conferma]:
  - [ ] Validazione risposta (due livelli)
  - [ ] Update score (1 o 2 punti)
  - [ ] Mostra feedback dettagliato
  - [ ] Mostra nota completa corretta
- [ ] Bottone [Prossima] → nuovo esercizio
- [ ] Opzionale: visualizzare anche sul pentagramma

---

## Step 7: Sistema Punteggio e Feedback

### Features
- Counter punti persistente
- Feedback visivo (verde/rosso)
- Mostra risposte alternative/corrette
- Statistiche base

### Task dettagliate
- [ ] Score counter nell'header
- [ ] Funzione `updateScore(points)` → animazione
- [ ] Feedback component:
  - [ ] Area feedback colorata (verde/rosso)
  - [ ] Icone ✓ / ✗
  - [ ] Messaggio testuale
  - [ ] Mostra alternative (esercizio 1)
  - [ ] Mostra risposta corretta (esercizio 2)
  - [ ] Animazione fade-in
- [ ] Statistiche base:
  - [ ] Totale esercizi
  - [ ] Risposte corrette
  - [ ] Percentuale successo
- [ ] Opzionale: streak counter (risposte consecutive)

---

## Step 8: Testing e Polish

### Test Funzionali
- [ ] Tutti i fretting generano note corrette
- [ ] Tutte le note generano fretting corretti
- [ ] Input tastiera virtuale funziona correttamente
- [ ] Validazione risposte accurata
- [ ] Score aggiornato correttamente
- [ ] Feedback mostrato correttamente

### Test UX
- [ ] App usabile su mobile (touch)
- [ ] Bottoni abbastanza grandi
- [ ] Font leggibili
- [ ] Colori contrastati
- [ ] Transizioni smooth
- [ ] Performance VexFlow ok

### Polish
- [ ] Animazioni piacevoli
- [ ] Messaggio benvenuto iniziale
- [ ] Gestione errori gracefully
- [ ] Loading states se necessario

---

## Step 9: Documentazione

### Aggiornare README.md
- [ ] Screenshot app
- [ ] Spiegazione esercizi
- [ ] Come si usa
- [ ] Architettura codice aggiornata

### Aggiornare SPECS.md
- [ ] Marcare Milestone 1 completato
- [ ] Note su implementazione reale vs piano

### Commenti nel Codice
- [ ] Ogni sezione ben commentata
- [ ] Funzioni documentate
- [ ] Costanti spiegate

---

## Step 10: Commit e Push

### Git Workflow
- [ ] Testare app completa
- [ ] `git add index.html`
- [ ] `git commit -m "Milestone 1: MVP complete - Exercise Type 1 & 2"`
- [ ] `git push origin main`
- [ ] Verificare su GitHub

---

## 🎯 Definizione di "Done" per Milestone 1

L'app è considerata completa quando:

✅ Posso aprire index.html sul telefono
✅ Vedo un pentagramma con una nota (chiave di basso)
✅ Posso inserire un fretting con la tastiera virtuale
✅ Ricevo feedback se è corretto
✅ Il punteggio si aggiorna
✅ Posso fare un nuovo esercizio
✅ Posso fare esercizio Tipo 2 (fretting → nota)
✅ Tutto funziona offline
✅ Tutto funziona su mobile

---

## 📦 Deliverable Finali

- `index.html` - App completa single-file con Milestone 1
- `SPECS.md` - Aggiornato con status Milestone 1
- `README.md` - Aggiornato con istruzioni uso
- `IMPLEMENTATION_PLAN.md` - Questo file, con checklist
- Repository GitHub aggiornato

---

**Ready to start?** 🚀
