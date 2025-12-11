# Specifiche Tecniche - Bass Notes Learning

## 🎯 Obiettivo Principale

Creare un'app mobile per imparare a tradurre le note musicali sul pentagramma (chiave di basso) in posizioni fisiche sulla tastiera del basso elettrico (fretting) e viceversa.

---

## 📝 Convenzioni e Definizioni FONDAMENTALI

### Notazione delle Note vs Fretting

**IMPORTANTE**: Questa distinzione è CRITICA e non va MAI dimenticata!

- **MAIUSCOLO = Nota Musicale**
  - Esempio: `A3` = La all'ottava 3
  - Formato: `[Lettera][Numero Ottava]`
  - Es: A2, C3, E4, G2

- **minuscolo = Fretting (posizione fisica)**
  - Esempio: `a3` = corda A, terzo fret
  - Formato: `[corda][numero_fret]`
  - Es: e0, a5, d7, g12

### Accordatura Standard del Basso

```
Corda 4 (più grave):  E  (Mi)
Corda 3:             A  (La)
Corda 2:             D  (Re)
Corda 1 (più acuta):  G  (Sol)
```

Notazione: **E A D G** (dalla grave all'acuta)

### Sistemi di Notazione delle Note

L'app deve supportare entrambi i sistemi:

| Lettere | Solfeggio Italiano |
|---------|-------------------|
| A       | La                |
| B       | Si                |
| C       | Do                |
| D       | Re                |
| E       | Mi                |
| F       | Fa                |
| G       | Sol               |

**Priorità**: Imparare prima le lettere, poi aggiungere il solfeggio italiano come feature extra.

---

## 🎸 Caratteristiche del Basso

### Note Duplicate
**IMPORTANTE**: La stessa nota musicale può essere suonata in più posizioni diverse sulla tastiera.

Esempio: La nota `E3` può essere suonata come:
- `e0` (corda E a vuoto)
- `a5` (corda A, quinto fret)
- `d10` (corda D, decimo fret)
- `g15` (corda G, quindicesimo fret)

Tutte e quattro sono corrette ma suonano leggermente diverse (timbro).

---

## 📊 Fasi di Sviluppo

### FASE 1 - Esercizi Base (Priorità ALTA)

#### Esercizio Tipo 1: Nota → Fretting
**Flusso**:
1. App mostra una nota sul pentagramma (chiave di basso)
2. Utente inserisce il fretting corrispondente (es: `a3`)
3. App valida la risposta
4. Feedback: ✓ punto guadagnato / ✗ zero punti
5. Mostra tutte le posizioni alternative corrette

**Esempio**:
```
Domanda: [Immagine nota C sul pentagramma]
Risposta utente: "a3"
Risultato: ✓ Corretto! (+1 punto)
          Alternative: e8, d13, g18
```

#### Esercizio Tipo 2: Fretting → Nota
**Flusso**:
1. App mostra un fretting (es: `d5`)
2. Utente inserisce la nota corrispondente
3. Risposta base: solo lettera (es: `G`)
4. Risposta completa: con ottava (es: `G2`) → punti bonus
5. Feedback con punteggio

**Sistema punteggio**:
- Solo lettera corretta: 1 punto
- Lettera + ottava corretta: 2 punti
- Risposta sbagliata: 0 punti

**Esempio**:
```
Domanda: Che nota è "d5"?
Risposta base: "G" → ✓ 1 punto
Risposta completa: "G2" → ✓✓ 2 punti
```

---

### FASE 2 - Fretboard Interattiva (Priorità MEDIA)

#### Feature: Visualizzazione Tastiera
**Componente**: Rappresentazione grafica interattiva della tastiera del basso

**Funzionalità**:
- Click su un fret → mostra info:
  - Nota: `C2`
  - Fretting: `a3`
  - Nome italiano: `Do 2`
- Evidenziazione visiva della posizione
- Markers per i fret (punti sul 3°, 5°, 7°, 9°, 12°, ecc.)

#### Esercizio Tipo 3: Nota → Click Fretboard
**Flusso**:
1. App mostra nota sul pentagramma
2. Utente clicca sulla fretboard
3. Validazione immediata con feedback visivo
4. Mostra tutte le posizioni corrette

#### Esercizio Tipo 4: Fretting Evidenziato → Nota
**Flusso**:
1. App evidenzia una posizione sulla fretboard
2. Utente inserisce la nota
3. Validazione con punteggio (come Tipo 2)

---

### FASE 3 - Sequenze e Pattern (Priorità BASSA)

#### Feature: Sequenze Multiple
**Obiettivo**: Imparare scale, riff, e sequenze di note

**Visualizzazione**:
- Note sul pentagramma in sequenza
- Indici numerici (1, 2, 3...) per l'ordine
- Possibilità di visualizzare sulla fretboard

**Esercizi**:

**Tipo 5: Scale**
```
Domanda: "Suona la scala di E minore"
Risposta: Sequenza di click sulla fretboard
Validazione: Controlla ordine e note
```

**Tipo 6: Riff Famosi**
```
Esempio: "Seven Nation Army" intro
Mostra: Pentagramma con 4-5 note numerate
Utente: Riproduce sulla fretboard nell'ordine
```

---

## 🎨 Design e UX

### Requisiti Mobile-First
- Touch-friendly (pulsanti grandi, interazioni semplici)
- Orientamento portrait preferito
- Responsive per diverse dimensioni
- Funzionamento offline

### Sistema di Gamification
- Contatore punti
- Streak di risposte consecutive corrette
- Statistiche (% risposte corrette, note più difficili)
- Livelli di difficoltà (opzionale)

---

## 🔧 Decisioni Tecniche PRESE ✓

### 1. Visualizzazione del Pentagramma ✓
**DECISIONE**: SVG/Canvas dinamico con libreria **VexFlow**

**Vantaggi**:
- Rendering professionale e preciso
- Tutto dinamico, niente immagini da gestire
- Flessibilità totale per note, chiavi, accidenti
- Libreria ben documentata e mantenuta
- Dimensione: ~100KB (accettabile per le funzionalità)

**Implementazione**:
- Usare VexFlow per rendering pentagramma in chiave di basso
- Container SVG responsivo per mobile
- Note generate programmaticamente

### 2. Estensione della Tastiera ✓
**DECISIONE**: **20 fret**

**Range coperto**:
- Corda E: da E1 (e0) a E4 (e20)
- Corda A: da A1 (a0) a A4 (a20)
- Corda D: da D2 (d0) a D5 (d20)
- Corda G: da G2 (g0) a G5 (g20)

Range totale: circa 3.5 ottave (E1 - G5)

Standard sufficiente per coprire tutte le note comuni. Espandibile a 24 fret in futuro se necessario.

### 3. Input Utente ✓
**DECISIONE**: **Tastiera virtuale custom**

**Fase 1 - MVP**:
- Bottoni touch-friendly per corde: [e] [a] [d] [g]
- Numpad 0-20 per i fret
- Bottoni per note: [A] [B] [C] [D] [E] [F] [G]
- Numpad 1-5 per le ottave
- Bottone [Conferma] per inviare risposta
- Bottone [Reset] per ricominciare input

**Fase 2**:
- Aggiungere click diretto sulla fretboard interattiva come input alternativo

**Vantaggi**:
- Zero errori di battitura
- Perfetto per touch mobile
- UI chiara e intuitiva
- Feedback visivo immediato

---

## 📋 Priorità di Implementazione

### Milestone 1 - MVP (Minimum Viable Product) 🎯
**Obiettivo**: App funzionante con esercizi base

**Componenti core**:
- [ ] Integrazione VexFlow per pentagramma (chiave di basso)
- [ ] Data structure: mappatura note ↔ fretting (20 fret)
- [ ] Tastiera virtuale custom per input
- [ ] Esercizio Tipo 1: Nota → Fretting
- [ ] Esercizio Tipo 2: Fretting → Nota
- [ ] Sistema punteggio base con feedback visivo
- [ ] Mostra posizioni alternative corrette
- [ ] UI mobile-first responsive
- [ ] Range: tutte le note naturali (no diesis/bemolle) su 20 fret

**Stima complessità**: Media-Alta (nuovo sistema input + VexFlow)

### Milestone 2 - Enhanced 🎨
**Obiettivo**: Migliorare UX e aggiungere interattività visiva

- [ ] Fretboard interattiva completa (visualizzazione grafica)
- [ ] Click su fret → mostra nota + fretting
- [ ] Esercizio Tipo 3: Nota → Click Fretboard
- [ ] Esercizio Tipo 4: Fretting evidenziato → Nota
- [ ] Sistema statistiche (% corrette, streak, note difficili)
- [ ] Modalità selezione esercizio (menu)
- [ ] Animazioni e transizioni migliorate
- [ ] Sound feedback (opzionale)

**Stima complessità**: Media (grafica fretboard + interazioni)

### Milestone 3 - Advanced 🚀
**Obiettivo**: Features avanzate per apprendimento completo

- [ ] Sequenze multiple (2-8 note)
- [ ] Scale predefinite (E minore, A maggiore, ecc.)
- [ ] Riff famosi (database small)
- [ ] Visualizzazione sequenze su pentagramma + fretboard
- [ ] Solfeggio italiano (Do, Re, Mi...) come opzione
- [ ] Livelli di difficoltà (facile/medio/difficile)
- [ ] Modalità pratica libera (esplora senza score)
- [ ] Accidenti: diesis e bemolle
- [ ] Esporta/importa progressi (localStorage)

**Stima complessità**: Alta (molte features)

---

## 🎼 Note Tecniche Musicali

### Chiave di Basso
Il pentagramma deve usare la **chiave di basso** (o chiave di Fa):
- Symbol: 𝄢
- Le note sono più basse rispetto alla chiave di violino
- Standard per strumenti gravi (basso, tuba, trombone, ecc.)

### Accidenti (Da implementare in futuro?)
- Diesis (#): alza la nota di un semitono
- Bemolle (♭): abbassa la nota di un semitono
- Bequadro (♮): annulla diesis/bemolle

**Fase 1**: Solo note naturali (niente accidenti)
**Fase N**: Aggiungere diesis e bemolli

---

## 📦 File di Output

### Struttura Dati Suggerita

```javascript
// Mapping note → fretting
const notesToFretting = {
  "E1": ["e0"],
  "F1": ["e1"],
  "G1": ["e3"],
  "A1": ["e5", "a0"],
  "C2": ["e8", "a3"],
  // ... etc
};

// Mapping fretting → nota
const frettingToNote = {
  "e0": "E1",
  "e1": "F1",
  "a3": "C2",
  // ... etc
};

// Info fretboard
const fretboard = {
  strings: ["E", "A", "D", "G"],
  frets: 20,
  tuning: {
    E: "E1",
    A: "A1",
    D: "D2",
    G: "G2"
  }
};
```

---

## 🎬 Prossimi Passi

### Pronto per partire con Milestone 1 - MVP

**Piano di implementazione**:
1. Creare struttura dati note ↔ fretting
2. Integrare VexFlow per rendering pentagramma
3. Costruire tastiera virtuale custom
4. Implementare logica esercizio Tipo 1
5. Implementare logica esercizio Tipo 2
6. Sistema punteggio e feedback
7. Testing e refinement

---

**Versione**: 2.0
**Data**: 2025-12-11
**Status**: ✅ Decisioni prese, pronto per implementazione
