# 🔐 Entropy Toolkit

> Cerimonia Multi-Sorgente di Generazione Entropia Autoprodotta

Guida completa per generare **seed crittografici ad alta entropia** utilizzando multiple sorgenti indipendenti in ambiente **air-gapped**.

---

## 🎯 Principi Non Negoziabili

| Principio | Descrizione |
|-----------|-------------|
| ✓ Sistema live verificato ISO | Hash e firma controllati da fonti multiple |
| ✓ Air-gapped completo | Nessuna connessione Wi-Fi/Ethernet/USB |
| ✓ Nessuna persistenza | Spegnimento senza salvare su HD |
| ✓ Sorgenti indipendenti | Distruzione dei materiali intermedi |
| ✓ Lavoro solitario | O con persone di fiducia assoluta |

---

## 📋 1. Preparazione (giorni prima)

### 1.1 Ambiente Software

```bash
# Download ISO ufficiale
Scaricare ISO ufficiale Ubuntu MATE (o distro live minimal fidata)

# Verifica integrità
Verificare SHA256 e firma GPG da fonti multiple

# Preparazione chiavette
Scrivere ISO su chiavetta dedicata (dd o equivalente)
Su seconda chiavetta: HTML + script estrazione revisionati

# Verifica dei file di verifica non-IID (repository ea-non-iid-verifica, tag v1.1.0-beta1)
Pagina HTML:  b1c981676bed8fad83242d5b92dcff528408c7d744ec98442084c4bb70dfe8eb
Script Python: c19937184793c6df5ebd3c1c5bb3bf1ae619752ac561335a03529ccca7cf4c57
```

**⚠️ Importante:** Nulla da rete, tutto verificato offline.

### 1.2 Materiali Fisici

- 🪙 Moneta equilibrata - da 2 euro, nasce bilanciata.
- 🎲 Dadi a 6 facce di qualità + 8 numeri della tombola/bingo
- 📷 Fotocamera RAW (non compresso, o lossless se necessario)
- 📸 Due o + scatti a otturatore chiuso, stesse impostazioni(dark frame)
- 📝 Carta e penna per appunti temporanei
- 🔒 Terza sorgente indipendente controllata (radio FM o microfono in raw)
- 🔒 Quarta sorgente indipendente controllata (csv da sensori del telefono)
---

## 🖥️ 2. Avvio dell'Ambiente Sicuro

1. Spegnere PC; staccare dischi non necessari
2. Boot da chiavetta ISO verificata (Live/Try without installing)
3. **Disattivare rete immediatamente:**
   - Airplane mode
   - `nmcli radio all off`
   - Cavo staccato
4. Verificare sessione live; evitare montaggio in scrittura HD interno
5. Non connettersi a NTP; regolazione orario solo manuale e grossolana

---

## 🌱 3. Generazione Sorgenti di Entropia

Eseguire in **ordini e momenti separati**. Mantenere flussi distinti fino alla concatenazione.

### 3.A — Sorgente Fotografica (HTML)

```
1. Copiare RAW e dark frame in sessione live
2. Aprire HTML locale nel browser della distro
3. Confermare dichiarazione di unicità file
4. Attivare dark-frame mode se disponibile
5. Usare rilevamento automatico blocco dati
6. Preferire RAW non compresso
7. Attivare LSB e DIFF
8. Attivare "Seleziona i migliori bit" con maxBits coerente
9. Eseguire estrazione
```

**Controlli post-estrazione:**
- Stima post-dipendenza vs i.i.d.
- Bias
- Runs
- Match lag-1

**Output:** `.bin` su supporto temporaneo o RAM
**Annotare su carta:**
- Bit validi
- Remainder
- Stima post-dipendenza

### 3.B — Sorgente Moneta

```
• Eseguire centinaia di lanci (se possibile)
• Registrare sistematicamente: Testa=1, Croce=0
• Procedura fissa predecisa (altezza, superficie)
• Scarto lanci ambigui secondo regola prefissata
• NESSUNA correzione a posteriori
```

### 3.C — Sorgente Dadi

```
• Dadi a 6 facce
• Mappatura che non sprechi entropia
• Esempio: scartare 5 e 6 e usare 1–4
• Registrare senza selezione a posteriori
```

### 3.D — Altra Sorgente Indipendente

```
• Processo fisico sotto controllo diretto
• Registrazione integrale
• Indipendente dalle altre sorgenti
```

### 3.E — Verifica Non-IID di Ogni Flusso (primo filtro)

Ogni flusso grezzo, prima della concatenazione, va verificato con lo strumento **ea-non-iid-verifica** (repository e tag v1.1.0-beta1 su GitHub). Lo strumento stima la min-entropia dei dati con i dieci stimatori dello standard NIST SP 800-90B per sorgenti non-IID.

~~
- Un file per flusso, byte grezzi, 8 bit per simbolo (o il formato annotato prima)
- Almeno 1.000.000 di simboli per la validazione NIST; con meno campioni la stima è un'indicazione, non una validazione
- Annotare sul foglio: valore per bit finale, stimatore che dà il minimo, H_bitstring (valore intermedio), soglia usata
- Conservare il rapporto di verifica; il file estratto (.bin) non si conserva
~~

**Valore per bit.** Con 8 bit per simbolo, il valore per bit è quello finale del programma NIST `ea_non_iid`: min(H_original, 8 × H_bitstring) / 8. Il valore intermedio H_bitstring si annota a parte, come valore per bit del solo bitstring.

**Soglia.** Il valore ideale è **1,00 bit per bit**: entropia piena. È un riferimento, non una soglia vincolante. Chi conduce la cerimonia sceglie la soglia prima di iniziare, tra 0,90 e 1,00, la annota e la applica a tutti i flussi nello stesso modo. Non si cambia a posteriori per far passare un flusso.

**Limite osservato.** Su 1.000.000 di byte di `/dev/urandom` il valore per bit finale è 0,829801, con H_bitstring 0,935706. Con questo file il valore ideale 1,00 non viene raggiunto, quindi un flusso può risultare non utilizzabile anche se la sorgente è buona. Il verdetto va letto con questo limite.

**Il verdetto dello strumento** (utilizzabile / non utilizzabile) dipende dalla soglia impostata e non è una decisione automatica. Un flusso sotto la soglia scelta va annotato con il valore reale, e la decisione di includerlo o meno resta a chi conduce la cerimonia, documentata.

**Limiti.** Lo strumento misura la prevedibilità dei dati che riceve, non la sorgente fisica. Non certifica né la sorgente né il seed. Non sostituisce i controlli della sezione 8.
---

## 🔗 4. Concatenazione

1. Portare tutte le sequenze grezze in ambiente live
2. Concatenare in ordine fisso predeciso:
   ```
   Foto → Moneta → Dadi → Altra sorgente
   ```
3. **Non riordinare** in base ai dati osservati
4. Lavorare su sequenze di bit o byte in modo coerente
5. ⚠️ Non inserire timestamp, nomi file, metadati nel flusso

---

## 🎲 5. Estrazione di Casualità (fuori dall'HTML)

### 5.1 — von Neumann (Debiasing a Coppie) (DISMESSO)

```
Su sorgenti sbilanciate o sul flusso concatenato:
  • Scartare coppie uguali (00, 11)
  • 01 → 0
  • 10 → 1

Nota: Può essere sostituito con Peres
```

### 5.2 — Peres (Iterativo) (SOSTITUISCE IN TUTTO VON NEUMANN)

```
Piu efficente di Von Neumann
Secondo implementazione verificata
```

### 5.3 — Toeplitz Hashing

```
1. Generare matrice Toeplitz da sorgente indipendente ulteriore
2. Non riusare i bit in estrazione
3. Dimensionare input/output conservativamente
4. Output << Entropia minima input
5. Implementazione corta, letta riga per riga
```

**Obiettivo:** Stringa finale di lunghezza pari (o superiore con margine) al richiesto.

---

## 🔑 6. Derivazione del Seed Finale

Sulla stringa estratta applicare **unica condensazione crittografica robusta:**

- **SHA-256/SHA-512**, oppure
- **HKDF-SHA256/SHA512** (con info/context fissi e non secret)

### Opzione: Mnemonic BIP39 (non consigliato)

```
1. Prendere bit necessari (128 o 256) + checksum BIP39
2. Usare tool offline fidata o implementazione minimale verificata
3. Trascrivere mnemonic a mano su supporto duraturo
   (metallo/carta qualità) in momento controllato

⚠️ Non fotografare, non digitare su dispositivi connessi, non inviare
```

---

## 🗑️ 7. Distruzione e Chiusura

### Sovrascrivere/cancellare tutti file intermedi:
- RAW
- `.bin`
- Sequenze
- Matrici
- Appunti digitali

### Distruggere fisicamente:
- Appunti cartacei della cerimonia

### Spegnere PC senza salvare la sessione

### Conservare solo:
- ✓ Backup seed/mnemonic in luoghi sicuri e ridondanti
- ✓ Eventualmente verbale cartaceo della procedura (senza valori)

---

## ✅ 8. Controlli di Sanità

### Prima della cerimonia
```
→ Eseguire prova completa con dati fittizi sulla stessa live
→ Distruggere tutto dopo il test
```

### Durante
```
→ Se sorgente mostra bias evidente: scartarla e ripeterla
→ Non "aggiustare" i dati
→ Verificare ogni flusso con lo strumento non-IID (sezione 3.E) e annotare il valore per bit
```

### Dopo
```
→ Verificare che mnemonic produca indirizzi attesi
→ Usare wallet offline in modalità sola lettura
→ Non esporre seed a dispositivi non fidati
```

---

## ❌ 9. Cosa NON Fare

| ❌ | Motivo |
|----|----|
| Non usare PC con HD installato | Rischi di persistenza |
| Non restare collegati in rete | Air-gap compromesso |
| Non riusare stessi RAW/dadi/matrice | Indipendenza violata |
| Non affidare tutto al solo Toeplitz | Punto di fallimento singolo |
| Non conservare file grezzi | Superficie d'attacco |
| Non generare e usare subito online | Macchina potenzialmente infetta |

---

## 🔄 10. Flusso Riepilogativo

```
ISO verificata → live air-gapped
      ↓
RAW unici + dark frame → HTML → bit grezzi
Moneta (procedura fissa)
Dadi (procedura fissa)
Altra sorgente indipendente
      ↓
Verifica non-IID per flusso (primo filtro, sezione 3.E)
      ↓
Concatenazione (ordine fisso predeciso)
      ↓
Peres → Toeplitz (matrice da sorgente diversa)
      ↓
Hash / HKDF → seed
      ↓
Trascrizione + distruzione intermedi + spegnimento live
```

---

## 📊 11. Stima di Robustezza (relativa)

**Benchmark:** Hardware wallet di buona qualità usato correttamente = **100**

| Scenario | Voto |
|----------|------|
| Solo HTML, browser normale, file unici                                                       | ~32   |
| HTML + moneta + dadi + altre + Peres/Toeplitz + hmac/hkdf + ISO live verificata              | 64/68 |
| Come sopra + estrattori e procedura formalmente verificate / multi-persona                   | 70–75 |
| **Hardware wallet di riferimento**                                                           |**100**|

### 📝 Considerazioni

Con questa procedura il **punto debole si sposta** dall'HTML alla qualità complessiva della cerimonia:

- ✓ Indipendenza delle sorgenti
- ✓ Correttezza degli estrattori
- ✓ Disciplina operativa

Restano **differenze strutturali** rispetto a hardware wallet dedicato:
- Isolamento fisico
- Superficie d'attacco
- Collaudo complessivo

---

## ⚖️ Disclaimer

> **Documento destinato a scopo educativo ad uso personale offline.**
>
> **Nessuna garanzia di idoneità a generazione di chiavi per fondi di elevato valore senza ulteriori controlli indipendenti.**
>
> Lo strumento di verifica non-IID citato nella sezione 3.E non certifica sorgenti né seed.

---

**Lingua:** Italiano
**Status:** ⚠️ Educational Only
