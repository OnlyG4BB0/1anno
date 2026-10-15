# Ciao amore mio — sito anniversario

Piccola esperienza romantica in una sola pagina, per il primo anniversario di fidanzamento (18 ottobre). Pensata soprattutto per lo smartphone.

## Link online

**GitHub Pages:** https://onlyg4bb0.github.io/1anno/

## Come aprire il sito in locale

1. Apri la cartella `1anno` sul computer.
2. Fai doppio clic su `index.html`, oppure aprilo con Chrome / Safari / Edge.
3. Non serve installare nulla né avviare un server.

## Dove modificare i testi

Tutto ciò che è personalizzabile sta nella costante `CONFIG` in cima allo `<script>` di `index.html`:

| Campo | Cosa fa |
|--------|---------|
| `nomeLei` | Come la chiami (es. `"Boba"`) |
| `nomeMio` | Firma della lettera (es. `"il tuo Gabriele"`) |
| `dataAnniversario` | Data mostrata sotto il titolo |
| `testoLettera` | Array di paragrafi della lettera |
| `destinazione.citta` | Titolo grande della rivelazione |
| `destinazione.evento` | Sottotitolo (es. Napoli Comicon) |
| `destinazione.dataEvento` | Data dell’evento |
| `destinazione.frase` | Frase sotto la destinazione |

Non serve toccare la logica del gioco o delle animazioni.

## Foto

Le foto sono già in `assets/` e collegate da `CONFIG.foto`. Vedi `assets/README.md` per sostituirle con le vostre.

## Struttura

- `index.html` — pagina unica (HTML + CSS + JS)
- `assets/` — foto opzionali
- `prompt.md` — brief originale

## Dettagli visuali

- Scrollbar nascosta (lo scroll resta attivo)
- Hero “velvet” con orbs, particelle e titolo a parole staggered
- Lettera in busta con sigillo di cera che si apre allo scroll
- Progress dots laterali per navigare le sezioni
- Biglietti puramente estetici (stessa rivelazione) con foto diverse + foil
- Polaroid sotto la lettera, sigillo fotografico, foto Napoli in rivelazione
- Glow del cursore solo su desktop (`pointer: fine`)
- Rispetta `prefers-reduced-motion`
