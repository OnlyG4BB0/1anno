# Prompt per coding agent: sito anniversario "Ciao amore mio"

## Obiettivo

Realizza un sito web romantico e giocoso, in lingua italiana, da regalare alla mia ragazza (che chiamo "la mia boba") in occasione del **primo anniversario di fidanzamento, il 18 ottobre**. Il sito è una piccola esperienza narrativa in una sola pagina, da scorrere dall'alto verso il basso, con un finale interattivo.

Deve essere un'unica pagina, leggera, che funzioni bene su smartphone (è quasi certamente il dispositivo che userà lei) e che non richieda backend, account o database.

## Stack tecnico

- Un unico file `index.html` con CSS e JavaScript inline. Nessuna dipendenza esterna obbligatoria.
- Vanilla HTML, CSS e JavaScript. Non usare framework, a meno che non sia strettamente necessario.
- Le immagini, se presenti, vanno in una cartella `assets/` con nomi semplici (es. `foto1.jpg`). Il sito deve funzionare anche se la cartella non contiene ancora le foto (mostra un placeholder elegante in quel caso).
- Font: puoi usare Google Fonts con un fallback (es. `Georgia, serif` per i titoli corsivi, `system-ui` per il testo).
- Il codice deve essere pulito, commentato in italiano nei punti chiave e facile da modificare: testi, date e nomi devono stare in costanti in cima allo script, così posso cambiarli senza toccare la logica.

## Configurazione da centralizzare (in cima allo script)

```js
const CONFIG = {
  nomeLei: "Boba",                    // come la chiamo io
  dataAnniversario: "18 ottobre",
  testoLettera: [ /* paragrafi, vedi sezione Lettera */ ],
  destinazione: {
    citta: "Napoli",
    evento: "Napoli Comicon",
    dataEvento: "[DA INSERIRE]",      // es. "aprile 2027"
  },
};
```

## Struttura della pagina (in ordine dall'alto verso il basso)

### 1. Apertura: "Ciao amore mio"

- Schermata a tutto schermo, centrata, sfondo morbido (gradiente caldo da rosa a pesca o tonalità che preferisci, purché romantico).
- Testo grande, in corsivo: **"Ciao amore mio"**.
- Sotto, una piccola indicazione discreta tipo una freccia animata o la scritta "scorri giù ↓".
- Un'animazione d'ingresso delicata (fade-in e leggero movimento verso l'alto). Niente di aggressivo.
- Qualche cuoricino o particella decorativa che fluttua lentamente in sottofondo, leggera sulle prestazioni.

### 2. La lettera

- Appare con un effetto **fade-in e slide-up quando entra nel viewport** (usa `IntersectionObserver`, non eventi di scroll pesanti).
- Il contenuto è una lettera scritta su uno sfondo che somiglia a carta (tonalità crema, bordi leggermente irregolari o ombra morbida, font corsivo o serif).
- Il testo viene letto dalla variabile `CONFIG.testoLettera`. Per ora inserisci questo testo segnaposto, che io sostituirò con il mio:

> Boba, un anno fa non avrei mai immaginato quanto la mia vita potesse cambiare con una sola conversazione. [...] Ogni giorno con te è una piccola scoperta. Grazie per la tua pazienza, per le tue risate e per il modo in cui mi guardi quando pensi che io non me ne accorga. Ti amo, oggi e ogni giorno che verrà.
>
> Con tutto il mio amore, il tuo [NOME]

- Ogni paragrafo appare con un leggero ritardo in sequenza (effetto "scrittura"), oppure tutto insieme se è più semplice da mantenere.
- Imposta un'altezza sufficiente perché la lettera sia leggibile comodamente senza troppo scroll interno.

### 3. Domanda di transizione

- Subito dopo la lettera, con un po' di spazio, appare il testo grande: **"Vuoi sapere il tuo regalo?"**
- Sotto, sempre nello stesso blocco, un bottone "Sì, dai!" che porta lo scroll alla sezione successiva con un'animazione di scorrimento fluida (`scrollIntoView({ behavior: "smooth" })`).
- Il bottone deve essere ben visibile e facile da toccare su mobile.

### 4. Il giochino: "Mi ami?"

Questa è la parte interattiva principale. Deve sembrare un piccolo gioco, con una logica chiara:

- Titolo della sezione: **"Mi ami?"** (oppure una domanda simile).
- Due bottoni: **"Sì"** e **"No"**.

**Comportamento del bottone "No":**
- Quando la persona prova a cliccare o si avvicina con il mouse, oppure tocca il bottone su mobile, il bottone "No" **si sposta in una posizione casuale** all'interno della sezione, con una transizione rapida ma visibile, in modo da essere "inseguito" dal cursore.
- Deve restare sempre dentro i limiti dello schermo (calcola i bounds del contenitore, non farlo uscire dalla viewport, né sovrapporsi in modo da coprire il bottone "Sì").
- Dopo un certo numero di tentativi (ad esempio 3-5), il testo del bottone "No" può cambiare in frasi divertenti tipo "Ci riprovi?", "Non ci credo", "Ma sei sicura?", "Ahah no 😏", e il bottone può diventare più piccolo, sempre senza mai diventare impossibile da notare.
- Il bottone "No" non deve essere cliccabile in modo funzionale: se qualcuno riesce a cliccarlo, può mostrare un messaggio giocoso come "Non si può cliccare, ormai hai detto di sì! 💕" oppure semplicemente far scattare il "sì" in automatico. Scegli la soluzione più divertente e coerente.
- Su mobile, il comportamento deve funzionare anche al tocco (evento `touchstart` o simile), non solo con il mouse.

**Comportamento del bottone "Sì":**
- Rimane fermo, grande e ben visibile.
- Al click mostra una breve animazione di festa (coriandoli, cuori o simili, senza librerie pesanti), poi fa scorrere la pagina verso la sezione successiva.

### 5. Il regalo: due biglietti

- Appare sotto la sezione del giochino, con un'animazione di comparsa.
- Titolo: **"Il tuo regalo"** oppure **"Scegli il tuo biglietto"**.
- Mostra **due biglietti** stilizzati (come biglietti di un evento o di un treno), uno accanto all'altro (in colonna su mobile). Possono avere un leggero effetto hover o di sollevamento.
- Entrambi i biglietti, quando cliccati, fanno partire la stessa rivelazione della destinazione. Non devono portare a pagine diverse.

### 6. La rivelazione: Napoli Comicon

Al click su uno dei due biglietti, la schermata si espande con un'animazione (zoom, fade, o effetto "apertura" del biglietto) e mostra:

- Grande titolo: **"Napoli"**
- Sottotitolo: **"Napoli Comicon"**
- Data: `CONFIG.destinazione.dataEvento`
- Una breve frase tipo: "Ti porto a Napoli, al Comicon, insieme a te. Un anno di noi, e il prossimo sarà ancora più bello."
- Un messaggio finale caldo, tipo "Ti amo, Boba 💕".
- Opzionale: una mappa stilizzata o un'immagine decorativa di Napoli (non usare immagini protette da copyright; se non le hai, usa solo testo e icone/emoji).
- Opzionale ma apprezzato: un piccolo bottone "Rigioca" o "Torna su" per riportare la pagina in cima.

## Requisiti di design

- **Mobile first.** Tutto deve essere leggibile e cliccabile su schermi piccoli (375px di larghezza e oltre).
- **Palette romantica:** rosa, pesca, crema, bordeaux o tonalità vicine. Evita colori troppo freddi o troppo saturi.
- **Tipografia:** titoli in corsivo elegante, testo corrente leggibile (minimo 16px).
- **Animazioni fluide** e non invasive. Rispetta `prefers-reduced-motion`: se l'utente lo ha attivato, disattiva le animazioni decorative.
- **Nessun elemento inutile.** Il sito è breve, deve restare curato e pulito.

## Requisiti tecnici

- Usa `IntersectionObserver` per gli effetti di scroll.
- Usa `requestAnimationFrame` per l'animazione del bottone "No", non `setInterval`.
- Nessun errore in console.
- Testato mentalmente su Chrome e Safari, sia desktop che mobile.
- Il file deve funzionare aprendo semplicemente `index.html` nel browser, senza server.
- Aggiungi un `<meta name="viewport">` corretto e un `<title>` tipo "Per la mia Boba 💕".

## Cosa consegnare

1. `index.html` completo e funzionante.
2. Una cartella `assets/` vuota o con un file README che spiega dove inserire le foto.
3. Un breve README in italiano con:
   - come aprire il sito in locale;
   - dove modificare testo della lettera, nome, data e destinazione (`CONFIG`);
   - come sostituire le foto placeholder.
4. Nel messaggio finale, un riepilogo di cosa è stato implementato e di eventuali scelte fatte autonomamente (per esempio la reazione precisa del bottone "No" o l'effetto dei coriandoli).

## Note finali per l'agente

- Il tono deve essere dolce e divertente, mai fastidioso o aggressivo. Il bottone "No" è uno scherzo tra innamorati, non deve sembrare una trappola frustrante.
- Non inventare fatti sulla relazione: usa solo i testi segnaposto e le variabili in `CONFIG`.
- Se qualcosa del brief è ambiguo, scegli l'opzione più semplice e romantica e documentala nel README.
