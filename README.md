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
```

**⚠️ Importante:** Nulla da rete, tutto verificato offline.

### 1.2 Materiali Fisici

- 🪙 Moneta equilibrata (meglio più monete)
- 🎲 Dadi a 6 facce di qualità
- 📷 Fotocamera RAW (non compresso, o lossless se necessario)
- 📸 Due+ dark frame (scatti a otturatore chiuso, stesse impostazioni)
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
• Esempio: scartare 6 e usare 1–5
• Registrare senza selezione a posteriori
```

### 3.D — Altra Sorgente Indipendente

```
• Processo fisico sotto controllo diretto
• Registrazione integrale
• Indipendente dalle altre sorgenti
```

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

---

**Lingua:** Italiano  
**Status:** ⚠️ Educational Only
