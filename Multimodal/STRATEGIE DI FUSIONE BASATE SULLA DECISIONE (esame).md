# STRATEGIE DI FUSIONE BASATE SULLA DECISIONE (esame)


Nel metodo basato sulle decisioni, i risultati di ogni riconoscitore vengono
interpretati separatamente dai gestori delle decisioni specifici e poi inviati
al sistema di gestione del dialogo che li integra usando procedure di fusione
guidate dal dialogo per ottenere l'interpretazione completa.

Per rappresentare le interpretazioni parziali provenienti dai gestori delle
decisioni e ottenere l'integrazione dei segnali di input a livello di
decisione, possono essere utilizzate diverse strutture come:

  * strutture di caratteristiche tipizzate (Cohen et al., 1997; Johnston, 1998)
  * melting pots (Nigay e Coutaz, 1995)
  * frame semantici (Vo e Wood, 1996; Russ et al., 2005).

1\. **Strutture di Caratteristiche**

  * Una struttura di caratteristiche è composta da coppie di caratteristiche-valore.
  * Il valore di una caratteristica può essere un atomo, una variabile o un'altra struttura di caratteristiche.
  * Quando due strutture di caratteristiche sono unificate, si forma una **struttura composita** contenente **tutte le specifiche delle caratteristiche di ciascuna struttura componente**.
  * Qualsiasi caratteristica comune a entrambe le strutture non deve avere valori in conflitto.

L'unificazione delle strutture di caratteristiche può risultare in un grafo
aciclico diretto (DAG) quando più di un valore utilizza la stessa variabile.

  

Le **Tipizzate  **sono un'estensione dove le strutture di caratteristiche e
gli atomi sono assegnati a tipi gerarchicamente ordinati.

  * La gerarchia rappresenta conoscenze specifiche e indipendenti dal dominio usando relazioni IS-A e IS-PART-OF.
  * L'unificazione delle strutture di caratteristiche tipizzate richiede che le coppie di strutture o atomi siano compatibili in tipo.
  * Il risultato di un'unificazione tipizzata è la struttura o atomo più specifico nella gerarchia dei tipi.
  * Questo metodo è ideale per l'integrazione multimodale perché può combinare input complementari o ridondanti, ma esclude quelli contraddittori.

Esempio

Un comando come "crea linea" può avere caratteristiche come oggetto (linea),
posizione e stile (filo spinato, colore rosso). Se un input parlato come "filo
spinato" si integra con un gesto di linea, esso rappresenta un comando
parzialmente specificato che necessita di ulteriori dettagli come la
posizione, fornita dal disegno dell'utente sullo schermo.

  

**Compensazione Multimodale**

Sia il parlato che i gesti hanno interpretazioni parziali. **L'interpretazione
del parlato richiede che la sua caratteristica di posizione sia di tipo linea,
quindi solo l'unificazione con l'interpretazione del gesto come linea avrà
successo e sarà considerata una valida interpretazione multimodale.** Per
selezionare la migliore interpretazione unificata, vengono associate
probabilità a ciascun input unimodale.

  
  
2\. **Melting Pots**

Un **melting pot** è una **struttura** 2-D con **parti** strutturali generate
dalle azioni di input dell'utente sull'asse verticale e il tempo sull'asse
orizzontale. La fusione avviene nel gestore del dialogo usando una tecnica
basata su agenti. Tre criteri attivano la fusione dei melting pots:

  1. Fusione **microtemporale** : combina informazioni prodotte in parallelo o in intervalli di tempo sovrapposti.
  2. Fusione **macrotemporale** : gestisce input sequenziali o intervalli di tempo non sovrapposti ma appartenenti alla stessa finestra temporale.
  3. Fusione **contestuale** : combina input secondo vincoli contestuali, indipendentemente dai vincoli temporali.

3\. **Frame Semantici**

L'input di ciascuna modalità viene trasformato in un **frame semantico
contenente slot** che specificano i parametri del comando, come l'azione da
eseguire o l'oggetto su cui agire. Questi frame parziali possono essere
incompleti o ambigui e vengono combinati in un frame completo tramite un
algoritmo che seleziona i valori degli slot dai frame parziali per
massimizzare un punteggio combinato.

### Conclusioni sulle Strategie Basate sulle Decisioni

**Vantaggi principali:**

  * **Multitasking** , poiché diversi canali multimodali, riconoscitori e interpreti possono **elaborare input unimodali indipendenti contemporaneamente**.
  * Possibilità di utilizzare riconoscitori e interpreti standard e ben testati per ciascuna modalità.

**Svantaggi principali:**

  * **Complessità elevata nella disambiguazione intermodale** , specialmente con modalità più complesse che richiedono non solo coppie elemento-tempo ma intere strutture per disambiguare l'input multimodale.

