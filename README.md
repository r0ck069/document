Guida Rapida - Entropy Toolkit
Cerimonia Multi-Sorgente di Generazione Entropia Autoprodotta
Scopo: Generare seed crittografici ad alta entropia utilizzando multiple sorgenti indipendenti in ambiente air-gapped.

0. PRINCIPI NON NEGOZIABILI
✓ Sistema live verificato da ISO (hash/firma controllati)
✓ Nessuna connessione di rete (Wi-Fi/Ethernet disabilitati)
✓ Nessuna persistenza: spegnimento senza salvare su HD
✓ Ogni sorgente indipendente, distruzione dei materiali intermedi
✓ L'HTML è solo una componente; estrazione forte fuori da esso
✓ Lavoro solitario o con persone di fiducia assoluta
1. PREPARAZIONE (giorni prima)
1.1 Ambiente Software
Scaricare ISO ufficiale Ubuntu MATE (o distro live minimal fidata)
Verificare SHA256 e firma GPG da fonti multiple
Scrivere ISO su chiavetta dedicata (dd o equivalente)
Su seconda chiavetta: HTML v1.2 + script di estrazione revisionati (nulla da rete)
1.2 Materiali Fisici
Moneta equilibrata (meglio più monete)
Dadi a 6 facce di qualità
Terza sorgente indipendente controllata
Carta e penna per appunti temporanei
Fotocamera RAW (non compresso, o lossless se necessario)
Due+ dark frame: scatti a otturatore chiuso, stesse impostazioni
2. AVVIO DELL'AMBIENTE SICURO
Spegnere PC; staccare dischi non necessari
Boot da chiavetta ISO verificata (Live/Try without installing)
Disattivare rete immediatamente (airplane mode, nmcli radio all off, cavo staccato)
Verificare sessione live; evitare montaggio in scrittura HD interno
Non connettersi a NTP; regolazione orario solo manuale e grossolana
3. GENERAZIONE SORGENTI DI ENTROPIA
Eseguire in ordini e momenti separati. Mantenere flussi distinti fino alla concatenazione.

3.A Sorgente Fotografica (HTML v1.2)
Copiare RAW e dark frame in sessione live da chiavetta dedicata
Aprire HTML locale nel browser della distro
Confermare dichiarazione di unicità file
Attivare dark-frame mode se disponibile
Usare rilevamento automatico blocco dati (altrimenti offset/lunghezza consapevoli)
Preferire RAW non compresso
Attivare LSB e DIFF; PARITY solo dopo valutazione bit-depth sensore
Attivare "Seleziona i migliori bit" con maxBits coerente
Eseguire estrazione; controllare: stima post-dipendenza vs i.i.d., bias, runs, match lag-1
Salvare output .bin su supporto temporaneo o RAM
Annotare su carta: bit validi, remainder, stima post-dipendenza
Chiudere browser
3.B Moneta
Eseguire centinaia di lanci (se possibile)
Registrare sistematicamente (Testa=1, Croce=0) senza correzioni
Procedura fissa predecisa (altezza, superficie, scarto lanci ambigui secondo regola)
3.C Dadi
Dadi a 6 facce; mappatura che non sprechi entropia
Es.: scartare 6 e usare 1–5, o altri metodi noti
Registrare senza selezione a posteriori
3.D Altra Sorgente Indipendente
Processo fisico sotto controllo diretto
Registrazione integrale
Indipendente dalle altre sorgenti
4. CONCATENAZIONE
Portare tutte le sequenze grezze in ambiente live
Concatenare in ordine fisso predeciso (es: foto → moneta → dadi → altra)
Non riordinare in base ai dati osservati
Lavorare su sequenze di bit o byte in modo coerente
Non inserire timestamp, nomi file, metadati nel flusso di entropia
5. ESTRAZIONE DI CASUALITÀ (fuori dall'HTML)
Ordine consigliato:

5.1 von Neumann (Debiasing a Coppie)
Su sorgenti sbilanciate o sul flusso concatenato
Scartare coppie uguali; 01→0, 10→1 (o regola equivalente fissata prima)
Nota: Può essere sostituito con Peres
5.2 Peres (Iterativo)
Applicare dopo o in alternativa controllata a von Neumann
Secondo implementazione verificata
5.3 Toeplitz Hashing
Generare matrice Toeplitz da sorgente indipendente ulteriore
Non riusare i bit in estrazione
Dimensionare input/output conservativamente
Output nettamente più corto dell'entropia minima stimata dell'input
Implementazione corta, letta riga per riga
Obiettivo: stringa finale di lunghezza pari (o superiore con margine) al richiesto
6. DERIVAZIONE DEL SEED FINALE
Sulla stringa estratta applicare unica condensazione crittografica robusta:

SHA-256/SHA-512, oppure
HKDF-SHA256/SHA512 (con info/context fissi e non secret)
Se serve mnemonic BIP39 (non consigliato):

Prendere bit necessari (128 o 256) + checksum secondo BIP39
Usare tool offline fidata o implementazione minimale verificata
Trascrivere mnemonic a mano su supporto duraturo (metallo/carta qualità) in momento controllato

Non fotografare, non digitare su dispositivi connessi, non inviare

7. DISTRUZIONE E CHIUSURA
Sovrascrivere/cancellare tutti file intermedi:
RAW, .bin, sequenze, matrici, appunti digitali
Distruggere fisicamente gli appunti cartacei della cerimonia
Spegnere PC senza salvare la sessione
Conservare solo:
Backup seed/mnemonic in luoghi sicuri e ridondanti
Eventualmente verbale cartaceo della procedura (senza valori di entropia)
8. CONTROLLI DI SANITÀ
Prima della cerimonia
Eseguire prova completa con dati fittizi sulla stessa live
Distruggere tutto dopo il test
Durante
Se sorgente mostra bias evidente o anomalie: scartarla e ripeterla
Non "aggiustare" i dati
Dopo
Verificare che mnemonic produca indirizzi attesi su wallet offline di sola lettura
Usare altra sessione live o hardware wallet in modalità solo controllo
Non esporre seed a dispositivi non fidati
9. COSA NON FARE
✗ Non usare PC con sistema installato su HD per cerimonia
✗ Non restare collegati in rete
✗ Non riusare stessi RAW, sequenze dadi/moneta, matrice Toeplitz
✗ Non affidare tutto al solo Toeplitz/Peres
✗ Non conservare file grezzi "per sicurezza"
✗ Non generare seed e usarlo subito su macchina online
10. FLUSSO RIEPILOGATIVO
Code
ISO verificata → live air-gapped
      ↓
  RAW unici + dark frame → HTML → bit grezzi
  Moneta (procedura fissa)
  Dadi (procedura fissa)
  Altra sorgente indipendente
      ↓
  Concatenazione (ordine fisso predeciso)
      ↓
  Peres → Toeplitz (matrice da sorgente ancora diversa)
      ↓
  Hash / HKDF → seed
      ↓
  Trascrizione + distruzione intermedi + spegnimento live
11. STIMA DI ROBUSTEZZA (relativa)
Valori indicativi rispetto a hardware wallet di buona qualità usato correttamente = 100

Scenario	Voto
Solo HTML, browser normale, file unici	~32
HTML + moneta + dadi + altra sorgente + von Neumann/Peres/Toeplitz + hmac/hkdf + live ISO verificata	64/68
Come sopra + implementazione estrattori e procedura formalmente verificate / multi-persona	70–75
Hardware wallet di riferimento	100
NOTE FINALI
Con questa procedura il punto debole si sposta dall'HTML alla qualità complessiva della cerimonia:

Indipendenza delle sorgenti
Correttezza degli estrattori
Disciplina operativa
Restano differenze strutturali rispetto a hardware wallet dedicato: isolamento, superficie d'attacco, collaudo complessivo.

Documento destinato a scopo educativo ad uso personale offline. Nessuna garanzia di idoneità a generazione di chiavi per fondi di elevato valore senza ulteriori controlli indipendenti.
