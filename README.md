# Simulazione di un Sistema RFID utilizzando NuSMV

Questo progetto fornisce un modello di simulazione di un sistema RFID (Radio-Frequency Identification) utilizzando il model checker NuSMV. Il sistema simulato comprende un lettore RFID e tre tag, implementati come moduli interagenti in un ambiente sincrono.

## Struttura del Progetto

- `main.smv`: Il file principale che definisce il modulo principale e specifica le proprietà da verificare utilizzando la logica temporale di NuSMV.
- `tag.smv`: Il modulo che rappresenta il comportamento di un singolo tag RFID.
- `reader.smv`: Il modulo che rappresenta il comportamento del lettore RFID.
- `tag_behavior.smv`: Il modulo che definisce il comportamento dei tag e la gestione della priorità.

## Utilizzo

1. Assicurati di avere NuSMV installato sul tuo sistema.
2. Esegui la simulazione utilizzando il comando `NuSMV main.smv`.

## Proprietà Verificate

- Raggiungibilità di almeno uno dei tag nello stato di risposta.
- Raggiungibilità estesa di almeno un tag in risposta, data la risposta di un altro.
- Raggiungibilità condizionata del tag dopo che il lettore raggiunge lo stato di accettazione.
- Etc.

## Licenza

Questo progetto è rilasciato sotto la [licenza MIT](LICENSE).
