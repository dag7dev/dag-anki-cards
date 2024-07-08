# Strategie di fusione basate sul riconoscimento


L'integrazione dei segnali di ingresso a livello di riconoscimento richiede
strutture adeguate per rappresentare questi segnali. Tre tipi principali di
rappresentazioni sono:  
\- **Action Frame**  
\- **Input Frame**  
\- **Slot**  
  
1\. Un **Action Frame** è una struttura che rappresenta un'azione specifica da
eseguire in risposta all'input multimodale: flussi paralleli di dati che
possono essere allineati e segmentati insieme.  
**Ogni flusso rappresenta un tipo di input** (ad esempio, vocale o penna)
unimodale, che viene segmentato e allineato per creare una sequenza di
segmenti di ingresso, chiamati *slot di parametri*.  
\- L'insieme di questi slot forma un **action frame** , che specifica l'azione
da eseguire.  
  
**Esempio**  
\- Sistema di navigazione cartografica: l'utente dice "Quanto è lontano da qui
a là?" mentre disegna una freccia tra due punti sulla mappa.  
  \- Flusso vocale: parole dell'utente.  
  \- Flusso penna: coppia di token `arrow_start` e `arrow_end`.  
  \- *Action frame* risultante: `QueryDistance` con due slot:
`QueryDistanceSource` e `QueryDistanceDestination`.  
  
2\. Gli **Input Frame**  memorizzano gli output dei moduli di interpretazione
visiva e uditiva utilizzando vettori di input.  
  
\- **Modulo visivo**  
  \- Traccia le caratteristiche dei dati video tramite segmentazione e
algoritmi di tracciamento del movimento, mettendole in un vettore di input  
  
\- **Modulo uditivo** :  
  \- Funziona in modo simile, applicato ai dati audio.  
\- L'integrazione delle modalità visiva e uditiva avviene **attraverso
strutture come gli Hidden-Markov-Model (HMM)**  e le Probabilistic
Independence Networks (PIN).  
  
3\. Negli **slot** , le informazioni dall'input multimodale vengono archiviate
in un **buffer**.  
  
Il linguaggio di comando dell'applicazione è codificato in unità semantiche
chiamate **frame**.  
  
Esempio  
\- Comando "sposta la finestra":  
  \- Due slot identificati: `oggetto` (per specificare l'oggetto) e `dove`
(per specificare la posizione finale).  
\- Il buffer degli slot viene continuamente monitorato.  
  \- Quando un frame è completo (cioè contiene informazioni sufficienti),
l'agente di fusione lo invia per l'esecuzione.  
  
\---  
  
1\. **Action Frame**  
   \- Allinea e segmenta i flussi di input unimodali.  
   \- Crea una sequenza di segmenti (slot di parametri) che formano un frame
d'azione specifico.  
  
2\. **Input Frame**  
   \- Memorizza le caratteristiche dei dati visivi e uditivi in vettori di
input.  
   \- Integra le modalità tramite modelli probabilistici.  
  
3\. **Slots**  
   \- Archivia le informazioni dell'input in uno slot buffer.  
   \- Riempie i frame di comando che, una volta completi, vengono eseguiti.

