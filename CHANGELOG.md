# Changelog — document

Cronologia delle modifiche ai file di questo repository. Le date sono quelle della pubblicazione.

## 2026-10-04 — procedura operativa: ordine MONETA -> DADO -> PALLINA

- **File modificato:** `procedura operativa` (testo, 11.718 byte, SHA-256 `001e9ce0cec059e89cdbdcb5340bf13b468d3749353d126ca58b1a8f96b9fecb`) diventa di 11.738 byte con SHA-256 `1f42da6f8a88b24a1ea5fc4983152cd5244e1a9bf574975ae4ebfda02ba09ddf`.
- **Cosa cambia:** l'ordine fisso dei turni passa da PALLINA -> DADO -> MONETA a MONETA -> DADO -> PALLINA, per coincidere con il Generatore di bit v2.8 (repository `entropy-bit-generator`). Sezione 3.D: ordine fisso, riga di conversione in bit e variante a blocchi. Sezione 3.E: titolo, intestazione, separatori e righe della griglia di registrazione; la riga d'esempio passa da `11100` a `00111`.
- **Conseguenza:** a parità di lanci la sequenza di bit è diversa da quella ottenuta con l'ordine precedente; i turni registrati con il vecchio ordine vanno convertiti con lo stesso ordine con cui sono stati registrati.
- **Non modificato:** il resto del testo e gli altri file (`README.md`, `entropy-toolkit-guida-rapida (2).pptx`, `LICENSE`).
- Prima di questa voce il repository non aveva un CHANGELOG.
