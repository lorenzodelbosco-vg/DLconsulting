# Pubblicare DL Consulting su GitHub Pages

## Prima di pubblicare (obbligatorio)
1. Quando hai la partita IVA, in `tools/build_pages.py` completa `PIVA` (compare in automatico nel footer e nella privacy)
   - `TITOLARE`, `SEDE` se vuoi cambiarli
   - `SITE_URL` → l'indirizzo definitivo (per ora `https://lorenzodelbosco-vg.github.io/DLconsulting/`)
2. Rigenera le pagine: `python3 tools/build_pages.py`
3. Fai controllare `pagine/privacy.html` a un consulente.
4. Prova il brief di `pagine/contatti.html` con un invio reale e verifica che arrivi a dl.consulting.torino@gmail.com (Formspree: al primo invio chiede di confermare l'email).

## Pubblicazione (repository `DLconsulting`)
1. Installa GitHub Desktop (desktop.github.com) e accedi con l'account lorenzodelbosco-vg.
2. File → Clone repository → scegli `DLconsulting` → Clone.
3. Apri la cartella clonata (Repository → Show in Finder) e copiaci dentro **tutto il contenuto** di `DLconsulting-da-caricare` (anche il file nascosto `.nojekyll`: nel Finder premi Cmd+Shift+. per vederlo).
4. In GitHub Desktop scrivi un messaggio (es. "Sito DL Consulting v2"), premi **Commit to main**, poi **Push origin**. Il caricamento di ~95 MB richiede qualche minuto.
5. Su github.com → repository DLconsulting → Settings → Pages → Source: "Deploy from a branch", branch `main`, cartella `/ (root)` → Save.
6. Dopo 1–3 minuti il sito è su https://lorenzodelbosco-vg.github.io/DLconsulting/

## Dominio personalizzato (quando lo compri)
1. Compra il dominio (es. dlconsulting.it) da un registrar italiano.
2. Nei DNS del dominio aggiungi:
   - 4 record **A** per `@` → 185.199.108.153 · 185.199.109.153 · 185.199.110.153 · 185.199.111.153
   - 1 record **CNAME** per `www` → `lorenzodelbosco-vg.github.io`
   (con il dominio il sito passa dalla sottocartella /DLconsulting/ alla radice: aggiorna `SITE_URL` e rigenera)
3. In GitHub → Settings → Pages → Custom domain: scrivi `www.dlconsulting.it`, salva, poi attiva "Enforce HTTPS".
4. Cambia `SITE_URL` in `tools/build_pages.py`, rigenera e ricarica i file.

## Dopo la pubblicazione
- Google Search Console: aggiungi il sito e invia `sitemap.xml`.
- Scheda Google Business Profile per Torino.
- Controlla l'anteprima dei link su WhatsApp/LinkedIn (usa l'immagine `assets/images/og-image.jpg`).
- Test su iPhone (Safari) e Android reali.
