# Changelog — document

Cronologia delle modifiche ai file di questo repository. Le date sono quelle della pubblicazione.

## 2026-10-13 — README: sezione 3.E, valore per bit e limite dello strumento (non ancora pubblicata)

- **File modificato:** `README.md` (SHA-256 `46d24cf23fcc88cd34dd850911dcf69f4fdfed6442b4b35c1d02403e9a081374`).
  - Sezione 3.E: il valore per bit è quello finale del programma NIST `ea_non_iid` con 8 bit per simbolo, min(H_original, 8 × H_bitstring) / 8; H_bitstring si annota come valore intermedio.
  - Soglia: 1,00 bit per bit è il riferimento ideale; chi conduce la cerimonia sceglie la soglia tra 0,90 e 1,00 prima di iniziare.
  - Limite osservato: su 1.000.000 di byte di `/dev/urandom` il valore per bit finale è 0,829801, con H_bitstring 0,935706.
  - Requisito di campioni: sotto 1.000.000 simboli la stima è un'indicazione, non una validazione NIST.
- **Nota:** la voce del 2026-10-11 resta come cronologia della versione pubblicata; la presente la aggiorna per la sezione 3.E.
- **Stato:** modifica non ancora committata né pubblicata; la data va confermata alla pubblicazione.

## 2026-10-11 — README: verifica non-IID per flusso; registro spostato

- **File modificato:** `README.md` (SHA-256 `a2402721f381d59fd93a5f97e7bc1ad9a62d9ef4455f1a1e63c5351ef3d44c20`).
  - 1.1: impronte SHA-256 della pagina e dello script di verifica non-IID (repository ea-non-iid-verifica, tag v1.1.0-beta1).
  - Nuova sezione 3.E: verifica non-IID di ogni flusso come primo filtro, prima della concatenazione.
  - Sezione 8 (Durante) e sezione 10 (Flusso riepilogativo): passo di verifica per flusso.
  - Disclaimer: lo strumento non certifica sorgenti né seed.
  - Rimossa la sezione "Avanzamento" (registro di lavoro), spostata in `AVANZAMENTO.md`.
- **File nuovo:** `AVANZAMENTO.md` (SHA-256 `1be77da7d1f6c2e93c38da9369398721088ca565e1d8d9bd4975124b05291974`): registro di lavoro del progetto, spostato dal README con contenuto invariato.
- **Scelta di riferimento:** la soglia 1,00 bit per bit è il valore ideale di riferimento, non vincolante. Chi conduce la cerimonia la fissa prima di iniziare e la applica a tutti i flussi.
- **Non modificato:** `procedura operativa`, `entropy-toolkit-guida-rapida (2).pptx`, `LICENSE`.

## 2026-10-04 — procedura operativa: ordine MONETA -> DADO -> PALLINA

- **File modificato:** `procedura operativa` (testo, 11.718 byte, SHA-256 `001e9ce0cec059e89cdbdcb5340bf13b468d3749353d126ca58b1a8f96b9fecb`) diventa di 11.738 byte con SHA-256 `1f42da6f8a88b24a1ea5fc4983152cd5244e1a9bf574975ae4ebfda02ba09ddf`.
- **Cosa cambia:** l'ordine fisso dei turni passa da PALLINA -> DADO -> MONETA a MONETA -> DADO -> PALLINA, per coincidere con il Generatore di bit v2.8 (repository `entropy-bit-generator`). Sezione 3.D: ordine fisso, riga di conversione in bit e variante a blocchi. Sezione 3.E: titolo, intestazione, separatori e righe della griglia di registrazione; la riga d'esempio passa da `11100` a `00111`.
- **Conseguenza:** a parità di lanci la sequenza di bit è diversa da quella ottenuta con l'ordine precedente; i turni registrati con il vecchio ordine vanno convertiti con lo stesso ordine con cui sono stati registrati.
- **Non modificato:** il resto del testo e gli altri file (`README.md`, `entropy-toolkit-guida-rapida (2).pptx`, `LICENSE`).
- Prima di questa voce il repository non aveva un CHANGELOG.
