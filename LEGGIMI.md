# DL Consulting — Cinematic Scroll Experience

Sito statico realizzato dal prompt e dalle nove clip fornite. Nessun framework, installazione o compilazione necessaria per eseguirlo.

## Anteprima

Dalla cartella del sito:

```sh
python3 -m http.server 8765 --bind 127.0.0.1
```

Apri http://127.0.0.1:8765/. È necessario un server HTTP: aprire index.html tramite file:// non consente il caricamento del manifest nel canvas.

Il sito non è stato pubblicato su un dominio esterno. L'anteprima locale rimane disponibile mentre il server è attivo.

## Cosa è incluso

- 11 pagine HTML ricostruite, con gli URL originali.
- 9 capitoli su canvas 2D con GSAP 3.12.5, ScrollTrigger 3.12.5 e Lenis 1.1.20, serviti localmente.
- 1.350 frame desktop WebP a 1600×900; 864 frame mobile a 800×450.
- Loader sul buffer iniziale, prefetch vicino al frame corrente, coda con priorità e cache limitata.
- Overlay HTML, navigazione dei capitoli, scroll inverso e modalità debug.
- Raccordo finale: stesso fotogramma sul canvas e sullo sfondo HTML, stessa headline e CTA; dissolvenza del canvas e dei comandi; rilascio del pin senza duplicare la sezione.
- Fallback statico per reduced-motion, risparmio dati se rilevabile, dipendenze/asset iniziali mancanti e pulsante “Versione leggera”.
- Servizi, sei fasi del metodo, portfolio, offerte, confronto, DL Care e contatti.
- Project Builder con validazione, preselezione, riepilogo e gestione degli errori.
- Digital Lab con cambio atmosfera e Rete Hub dimostrativo con filtro delle competenze.

Lo ZIP distribuibile contiene i frame necessari al sito. I nove MP4 originali non vengono scaricati dal browser e sono esclusi dallo ZIP di pubblicazione: sono già nel pacchetto clip.zip fornito. Nella cartella di lavoro locale sono conservati in assets/clips/.

## Contenuti

Essential / Advanced / Signature mantengono i prezzi da 690 / 1.290 / 2.490 €. Impact e Immersive restano alias validi nei link al brief. DL Care conserva 99 / 249 / da 449 € al mese. Nessun risultato commerciale o cliente è stato inventato.

Il portfolio conserva Étera Film, CNC Experience, Yulia Training School, SofiNutricion e Our Forever, con i rispettivi stati. Il link Étera resta quello originale. Le scene del Project Vault sono visualizzazioni illustrative generate, non screenshot dei progetti.

La home prepara un messaggio WhatsApp: l'utente lo rivede prima dell'invio. La pagina contatti invia a Formspree solo quando l'utente preme “Invia il brief”. Nei controlli sono state simulate risposte di successo ed errore: nessun brief è stato spedito. La consegna effettiva alla casella del destinatario non è stata verificata.

## Modificare testi e struttura

- `tools/build_pages.py`: contenuti e generazione delle 11 pagine statiche.
- `css/site.css`: identità visiva e responsive.
- `js/site.js`: navigazione, form, Digital Lab e filtri.
- `js/cinema.js`: motore, preload e raccordo finale.
- `assets/manifest.json`: file, frame, intervalli sorgente, pesi dello scroll e inquadratura mobile.
- `assets/cues.json`: intervalli normalizzati degli overlay.

Esegui `python3 tools/build_pages.py` dopo aver aggiornato i contenuti. Attenzione: questo rigenera anche cues.json dagli intervalli presenti nello script; aggiorna quindi la configurazione sorgente prima di rigenerare.

## Asset e rigenerazione

I video originali sono 1920×1080, 24 fps, 8 secondi ciascuno. I frame sorgente finali selezionati, indicizzati da zero, sono 182, 175, 167, 167, 182, 182, 182, 182, 182.

L'estrazione usa FFmpeg e Pillow. Con i nove MP4 in assets/clips/, esegui:

```sh
python3 tools/extract_frames.py
```

FFmpeg deve essere disponibile nel PATH, oppure indicato dalla variabile FFMPEG. Lo script estrae prima JPEG a 1600 px con qualità 3, poi campiona uniformemente l'intervallo scelto e salva WebP (desktop qualità 74, mobile qualità 68). Il numero di frame non rappresenta la durata dello scroll, configurata separatamente.

Confronto di peso sui frame desktop effettivi: riferimento JPEG 160,3 MB; WebP 79,4 MB. Mobile completo: 15,8 MB. Questi totali non sono caricati all'avvio. Budget adottati: circa 1,8 MB desktop / 0,8 MB mobile all'avvio in questa configurazione; cache di 20 bitmap desktop / 28 mobile, oltre al frame terminale e alle decodifiche in corso.

Le clip 6 e 7 usano un'inquadratura contenuta in verticale per non perdere galleria e tre portali. Le altre scene preservano il soggetto centrale. Il passaggio Clip 3→4 presenta un cambio visivo nei sorgenti ed è raccordato con una breve dissolvenza, senza rigenerare i video.

## Debug e verifiche

Aggiungi `?debug=1` alla home per leggere capitolo, frame, cache e richieste. `?lite=1` attiva direttamente la versione statica.

I rapporti in checks/ documentano i test eseguiti con Chrome su macOS, a 1440×1000 e 390×844, più ridimensionamenti. La visualizzazione mobile è emulata; non è un collaudo su iPhone o Android fisici. Non sono stati collaudati Safari e Firefox.

Le misure di caricamento riportate sono locali, senza un hosting remoto, e non rappresentano Core Web Vitals sul campo. INP e fluidità su dispositivi reali richiedono misurazioni dopo la pubblicazione.

Alcuni MP4 contengono scritte/loghi già generati nel video. Sono stati riposizionati gli overlay per ridurre sovrapposizioni; non è stata eseguita una pulizia/inpainting dei filmati originali.

## Versione 2 — tutto ciò che viene dopo la hero (settembre 2026)

La hero cinematica (9 capitoli su canvas, `js/cinema.js`, `assets/frames/`, `assets/cues.json`) è invariata. Unica modifica: il link "Salta l’esperienza" e lo scroll di fallback puntano ora alla nuova prima sezione `#inizio`.

Riprogettato con riferimento strutturale a linearity.io, nella palette DL (nero, viola → ciano):

- **Home dopo la hero:** galleria di formati che si ricompone attorno al titolo (parola che cambia allo scroll) → nastro competenze → "Raccontalo. Rifiniscilo. Pubblicalo ovunque." con mini-interfacce → confronto "Altri consegnano pagine. Noi, sistemi." → tab per tipo di attività → servizi in bento → carosello portfolio → metodo con linea di avanzamento → fondatore → prezzi con switch Progetto / DL Care → FAQ → CTA finale con modulo WhatsApp → nuovo footer.
- **Pagine interne:** tutte e 10 ricostruite con gli stessi componenti (hero centrata con glow, card in vetro, pulsanti a pillola). URL invariati.
- **File nuovi:** `css/sections.css`, `js/sections.js`, `assets/images/v2/` (ritagli WebP dai fotogrammi dei 9 video, circa 600 KB), `assets/fonts/` (Hanken Grotesk, self-hosted, licenza OFL).
- **`css/site.css`:** conserva solo base, header e hero; le vecchie regole delle sezioni sono state rimosse.
- **Contatti:** email aggiornata a dl.consulting.torino@gmail.com; aggiunto Instagram @dl.consulting.it.
- **Contenuti:** prezzi, pacchetti, metodo, portfolio e stati dei progetti invariati. Nessun cliente, risultato o testimonianza inventati. I progetti senza immagine usano copertine tipografiche astratte.

I rapporti in `checks/` si riferiscono alla versione precedente.

### Foto della galleria iniziale (Unsplash)

Sette card della prima sezione dopo la hero usano foto gratuite da Unsplash (licenza Unsplash: uso commerciale consentito, attribuzione non obbligatoria). File in `assets/images/v2/p-*.webp`, ritagliati e alleggeriti; in CSS ricevono una leggera correzione colore viola (`.v-float--photo`).

- p-torino — Mole Antonelliana di notte · unsplash.com/photos/L6_kV_FWD8o
- p-industria — taglio metallo con scintille · unsplash.com/photos/thdb7o0nLyc
- p-smartphone — mano con smartphone al buio · unsplash.com/photos/sgNc8aY6Z7E
- p-ristorante — interno di ristorante · unsplash.com/photos/EjHiN2KxTO4
- p-alluminio — pezzo in alluminio lavorato · unsplash.com/photos/al2B95qSExQ
- p-scrivania — scrivania notturna con laptop · unsplash.com/photos/wT0oU24OJYU
- p-espresso — macchina espresso · unsplash.com/photos/kLfAST5nqjM

- p-sistema — postazione moderna al buio (card "Ti diamo un sistema") · unsplash.com/photos/PsH9KEzquFA
- p-seg-pmi — laptop in officina (scheda PMI & industria) · unsplash.com/photos/KeLUeVSplNY — sullo schermo è stato inserito un sito dimostrativo di officina CNC (brand inventato, generato in HTML)
- p-seg-pro — laptop con sito web su scrivania (scheda Professionisti) · unsplash.com/photos/RTdvy9izXvw
- p-seg-com — tablet con menu al bar (scheda Commercio & ristorazione) · unsplash.com/photos/pXG2xQii2FE

Le altre tre card (Scena 3D, Esperienze, Scroll experience) restano fotogrammi dei video DL. Per cambiare immagini ed etichette modifica la lista `cards` in `sec_gallery()` dentro `tools/build_pages.py` e rigenera.

### Video delle card servizi (Pexels)

Tre clip gratuite da Pexels (licenza Pexels: uso commerciale consentito), tagliate a 6 secondi, senza audio, in WebM + MP4 (`assets/videos/`, ~1,3 MB in totale per entrambi i formati; il browser ne scarica uno solo). Si caricano solo quando la sezione è visibile, su desktop; su mobile, con risparmio dati o "riduci movimento" resta il fermo immagine (`assets/images/v2/v-*-poster.webp`).

- v-web — laptop con un sito a griglia di immagini · pexels.com/video/7872720
- v-social — smartphone in luce viola · pexels.com/video/9785300
- v-analisi — tablet con grafico di crescita · pexels.com/video/38992894

### Portfolio: concept dimostrativi e copertine

Quattro concept con nomi e attività inventati, segnalati con l'etichetta "Concept" sulle card e con una barra "Concept di DL Consulting · progetto dimostrativo" in ogni pagina (`pagine/concept/`, `noindex`):
- Fumo · Brace contemporanea — `fumo.html`
- Forno Lume · Panetteria & caffè — `forno-lume.html`
- Nodo · Abbigliamento sostenibile — `nodo.html`
- Amaro Collina · Liquore artigianale — `amaro-collina.html`

Copertine in `assets/images/concept/cover-*.webp` (1000×800): per i concept sono screenshot desktop + mobile delle pagine demo; per CNC Experience, Yulia Training School, SofiNutricion e Our Forever sono copertine grafiche (foto d'archivio + nome), non screenshot dei siti: sostituiscile con screenshot reali quando i progetti sono pronti.

Foto Unsplash usate: brace (Q_X0T0E0IyU, 9Qs_9n2oSJo), pane (6dSUrlyg), croissant e caffè (z3em1GBRhvY), moda (K0DxxljcRv0), lino (N_wGDmRL4hQ), erbe (9rTCfL5yGWI), fitness (unsplash.com/photos, id 1541534741688), bowl (IGfIGP5ONV0), tavola evento (pqkn1uIS6jY), CNC (id 1713371398484).
