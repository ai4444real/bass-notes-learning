# 🎸 Bass Notes Learning

Applicazione mobile-first per l'apprendimento delle note sul basso, realizzata come single-file HTML app.

## 📋 Descrizione

Questa è una web app ottimizzata per dispositivi mobile che può essere aperta direttamente dal browser del telefono senza necessità di server. Tutto il codice (HTML, CSS, JavaScript) è contenuto in un unico file per facilitarne l'uso standalone.

## 🚀 Come Usare

1. **Sul telefono**:
   - Scarica il file `index.html`
   - Aprilo con qualsiasi browser (Chrome, Firefox, Safari)
   - L'app funzionerà offline

2. **Sul computer**:
   - Fai doppio click su `index.html`
   - Oppure apri il file con il browser

## 📁 Struttura del Progetto

```
bass-notes-learning/
├── index.html          # File principale (contiene tutto)
└── README.md          # Questa documentazione
```

## 🏗️ Architettura del File index.html

Il file è organizzato in sezioni ben definite per facilitare future modifiche o separazioni:

### 1. Sezione CSS (linee ~14-100)
Contiene tutti gli stili dell'applicazione:
- **Reset e base**: Configurazione iniziale di margini, padding, box-sizing
- **Layout principale**: Gradient background, container centrato
- **Componenti**:
  - `.container`: Box bianco principale con shadow
  - `.counter`: Display grande del contatore
  - `.btn`: Stile dei bottoni con hover effects
- **Responsive**: Media query per schermi sotto 480px

### 2. Sezione HTML (linee ~105-125)
Struttura del contenuto:
- Container principale
- Titolo e sottotitolo
- Area interattiva con counter e bottoni
- Info footer

### 3. Sezione JavaScript (linee ~130-220)
Logica dell'applicazione organizzata in:

#### Variabili Globali
- `count`: Valore del contatore

#### Funzioni Utility
- `updateDisplay()`: Aggiorna il DOM e anima il counter

#### Funzioni Principali
- `incrementCounter()`: Aumenta il contatore di 1
- `decrementCounter()`: Diminuisce il contatore di 1
- `resetCounter()`: Riporta il contatore a 0

#### Inizializzazione
- `window.onload`: Setup iniziale dell'app

#### Event Listeners
- Gestione tastiera (Spazio, Backspace, Esc)

## 🎮 Funzionalità Demo

L'app di esempio include:
- **Counter interattivo**: Incrementa, decrementa, reset
- **Animazioni**: Effetti visivi sui bottoni e sul counter
- **Controlli tastiera**:
  - `Spazio`: Incrementa
  - `Backspace`: Decrementa
  - `Esc`: Reset
- **Design responsive**: Ottimizzato per mobile e desktop
- **Console logging**: Tutti gli eventi sono loggati per debug

## 🛠️ Stack Tecnologico

- **HTML5**: Struttura semantica
- **CSS3**: Styling moderno con flexbox, gradients, transitions
- **JavaScript Vanilla**: Nessuna dipendenza esterna

## 🔮 Sviluppo Futuro

Quando il progetto crescerà, sarà facile separare il file in:
- `styles.css`: Tutta la sezione `<style>`
- `script.js`: Tutta la sezione `<script>`
- `index.html`: Solo il markup HTML con link esterni

## 📝 Note di Sviluppo

### Pattern Consolidato
```
creare → testare → verificare → pulire
```

### Best Practices
- Tutti i cambiamenti vanno committati sul branch `main`
- Ogni sezione è ben commentata
- Codice JavaScript documentato con JSDoc style
- Design mobile-first

## 📦 Version Control

Repository GitHub: [https://github.com/ai4444real/bass-notes-learning](https://github.com/ai4444real/bass-notes-learning)

## 📄 Licenza

Progetto personale per apprendimento

---

**Versione**: 1.0.0
**Ultimo aggiornamento**: 2025-12-11
**Compatibilità**: Tutti i browser moderni (Chrome 90+, Firefox 88+, Safari 14+)
