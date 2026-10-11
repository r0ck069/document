# Avanzamento: progetto entropia su Raspberry Pi 5

Registro di lavoro. Non fa parte della guida: è stato spostato dal README il 11/10/2026.

Aggiornato il 24 settembre 2026.

## Piattaforma
- Raspberry Pi 5 (8 GB), microSD 128 GB
- Raspberry Pi OS 64-bit con desktop, Debian 13 "trixie", aarch64
- Il container di test sul NAS usa `debian:bookworm`, quindi compilatore e librerie sono più vecchie di quelle del Pi: i risultati vanno confrontati a parità di file.

## Toolchain compilato sul Pi (in `~/tools`)
- `arcetri/sts` v3.2.7
- `SP800-90B_EntropyAssessment`: `ea_iid`, `ea_non_iid`, `ea_restart`, `ea_conditioning`, `ea_transpose`
- `PractRand` pre0.95 (`RNG_test`)
- Pacchetti apt installati e verificati: gcc, make, git, wget, unzip, xxd, file, sox, python3, dieharder, ent, python3-matplotlib 3.10.1

## Validazione della build (in corso)
- PractRand su 64 MB da `/dev/urandom`: nessuna anomalia in 182 risultati.
- File di prova `test_urandom_1MB.bin` (1 MB da `/dev/urandom`),
  sha256 `32edce6557e97a3702d84aa00fed21e405065f0cf7bea13deee696a8f23700de`.
- `ea_non_iid -v` sul Pi 5: `H_original` 7.276950, `H_bitstring` 0.890793, minimo 7.126346.
  Sono stime prudenti su 1 MB, non vanno lette come misura precisa della sorgente.
- Sul NAS le prime 11 stime coincidono con quelle del Pi; il risultato finale del NAS è ancora da confrontare.

## Da fare
- Prova di `sts` sul Pi.
- Confronto completo (STS e PractRand) sul file Tascam a 6 bit già analizzato sul NAS.
- Annotare gli hash dei commit di `sts` e `SP800-90B_EntropyAssessment` (`git rev-parse HEAD`).
- Portare sul Pi script Python e repo del progetto, poi isolare la macchina (nessuna rete) prima della generazione dei seed.
