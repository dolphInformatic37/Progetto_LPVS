# Simulazione di un Sistema RFID utilizzando NuSMV

Questo progetto fornisce un modello di simulazione di un sistema RFID (Radio-Frequency Identification) utilizzando il model checker NuSMV. Il sistema simulato comprende un lettore RFID e tre tag, implementati come moduli interagenti in un ambiente sincrono.

## Utilizzo

### Prerequisiti
Assicurati di avere NuSMV installato sul tuo sistema. Puoi scaricarlo e installarlo da [qui](https://nusmv.fbk.eu/).

### Esecuzione della Simulazione
Per eseguire la simulazione, segui questi passaggi:
1. Assicurati di essere nella directory del progetto.
2. Apri un terminale e digita il comando seguente:
    ```
    NuSMV Collision_RFID.smv
    ```
3. Attendi il completamento dell'esecuzione. Una volta terminata, verranno visualizzati i risultati della simulazione.

## Proprietà Verificate

- Raggiungibilità di almeno uno dei tag nello stato di risposta.
- Raggiungibilità estesa di almeno un tag in risposta, data la risposta di un altro.
- Raggiungibilità condizionata del tag dopo che il lettore raggiunge lo stato di accettazione.
- Etc.

## Licenza

Questo progetto è rilasciato sotto la [licenza MIT](LICENSE).


## Proprietà Verificate

Di seguito sono elencate le proprietà verificate nel modello, insieme al relativo codice NuSMV:

1. **Raggiungibilità di almeno uno dei tag nello stato di risposta:**

```   
CTLSPEC EF (t1.tag_state = responding | t2.tag_state = responding | t3.tag_state = responding)
```

2. **Raggiungibilità estesa di almeno un tag in risposta, data la risposta di un altro:**

```
CTLSPEC EF (t1.tag_state = responding -> (t2.tag_state = waiting_probe | t2.tag_state = randomising_bit) & (t3.tag_state = waiting_probe | t3.tag_state = randomising_bit))
```
```
CTLSPEC EF (t2.tag_state = responding -> (t1.tag_state = waiting_probe | t1.tag_state = randomising_bit) & (t3.tag_state = waiting_probe | t3.tag_state = randomising_bit))
```
```
CTLSPEC EF (t3.tag_state = responding -> (t1.tag_state = waiting_probe | t1.tag_state = randomising_bit) & (t2.tag_state = waiting_probe | t2.tag_state = randomising_bit))
```

3. **Raggiungibilità condizionata del tag dopo che il lettore raggiunge lo stato di accettazione:**

```
CTLSPEC AG (r.reader_state = accepting -> EF (t1.tag_state = waiting_probe))
```

4. **Raggiungibilità estesa:**

```
CTLSPEC EF (r.reader_state = sending -> (t1.tag_state = responding & t2.tag_state = responding & t3.tag_state = responding))
```

5. **Raggiungibilità estesa:**

```
CTLSPEC EF (r.reader_state = sending & (t1.tag_state = responding | t2.tag_state = responding | t3.tag_state = responding))
```

6. **Irraggiungibilità (Safety):**

```
CTLSPEC AG (r.reader_state = sending -> AG !(t1.tag_state = responding | t2.tag_state = responding | t3.tag_state = responding))
```

7. **Irraggiungibilità (Safety):**

```
CTLSPEC AG (t1.tag_state = waiting_probe & t2.tag_state = waiting_probe & t3.tag_state = waiting_probe -> AF (r.reader_state = idle))
```

8. **Fairness Condizionata:**

```
CTLSPEC AG AF (r.reader_state = idle | r.reader_state = sending)
```

9. **Unfairness Condizionata:**

```
CTLSPEC AG !AF (r.reader_state = idle | r.reader_state = sending)
```

10. **Fairness Condizionata:**

 ```
 CTLSPEC AG ((r.reader_state = accepting & t1.tag_state = responding) -> EF (r.reader_state = idle))
 ```

## Licenza

Questo progetto è rilasciato sotto la [licenza MIT](LICENSE).
