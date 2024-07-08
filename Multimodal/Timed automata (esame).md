# Timed automata (esame)


Timed automata sono un tipo di automi utilizzati per descrivere sistemi che
evolvono nel tempo. Ogni stato di un timed automaton è associato a un orologio
che tiene traccia del tempo trascorso dall'ingresso nello stato. Le
transizioni tra gli stati possono essere condizionate dall'attivazione di un
orologio, consentendo di modellare comportamenti temporizzati nei sistemi.  
ESTESA  
Più in dettaglio, un automa temporizzato è un automa standard a stati finiti
esteso con una raccolta finita di orologi a valori reali.  
Le transizioni di un automa temporizzato sono etichettate con una guardia (una
condizione sugli orologi), un'azione e un ripristino dell'orologio (un
sottoinsieme di orologi da ripristinare).

L’automa temporizzato composto da:

  * Uno stato di un automa è una coppia composta da un nodo di controllo e un'assegnazione di clock, ovvero l'impostazione corrente degli orologi.
  * Le transizioni sono etichettate con un'azione (se si tratta di un passaggio istantaneo dal nodo corrente a un altro) o un numero reale positivo, cioè un ritardo (se l'automa rimane all'interno di un nodo lasciando passare il tempo).
  * Il tempo di incorporamento consente di modificare lo stato delle entità coinvolte in base aeventi basati sul tempo.  
  
GPT  
  
  
# Automi Temporizzati (Timed Automata)  
  
## Concetto Base  
Un *automa temporizzato* è un tipo di automa a stati finiti che include la
nozione di tempo. È utilizzato per descrivere sistemi che evolvono nel tempo,
come sistemi di controllo, protocolli di comunicazione, ecc.  
  
## Componenti Principali  
  
1\. **Stati e Orologi**:  
   \- Ogni stato dell'automa è associato a uno o più orologi che misurano il
tempo trascorso.  
   \- Gli orologi sono valori reali che aumentano costantemente col passare
del tempo.  
  
2\. **Transizioni**:  
   \- Le transizioni tra stati possono avvenire in due modi:  
     1\. **Azioni istantanee**: Transizioni immediate da uno stato a un altro, etichettate con un'azione.  
     2\. **Ritardi temporali**: L'automa può rimanere in uno stato per un certo intervallo di tempo prima di passare a un altro stato.  
  
3\. **Guardie e Reset degli Orologi**:  
   \- **Guardie**: Condizioni sugli orologi che devono essere soddisfatte per
consentire una transizione. Ad esempio, una transizione può essere permessa
solo se un orologio ha raggiunto un certo valore.  
   \- **Reset degli orologi**: Alcune transizioni possono resettare uno o più
orologi, riportandoli a zero.  
  
## Descrizione Dettagliata  
  
### Stati e Assegnazione di Clock  
\- **Stato**: Una coppia composta da un nodo di controllo (l'attuale posizione
dell'automa) e un'assegnazione di clock (i valori correnti degli orologi).  
\- **Assegnazione di clock**: L'insieme dei valori correnti degli orologi.  
  
### Transizioni  
\- **Etichettatura**:  
  \- Ogni transizione è etichettata con una guardia, un'azione e un possibile
reset degli orologi.  
  \- La guardia è una condizione che deve essere soddisfatta affinché la
transizione avvenga (espressa in termini di valori degli orologi).  
  \- L'azione è un'etichetta che indica l'evento che provoca la transizione.  
  \- Il reset specifica quali orologi devono essere resettati al momento della
transizione.  
  
### Incorporamento del Tempo  
\- Il tempo trascorre continuamente mentre l'automa si trova in uno stato.  
\- Durante questo tempo, gli orologi incrementano i loro valori.  
\- Le transizioni possono essere ritardate fino a quando le condizioni delle
guardie sono soddisfatte.  
  
## Esempio  
Immagina un sistema semaforico con due stati principali: **Verde** e
**Rosso**. Supponiamo di avere un orologio `x` che misura il tempo trascorso
in ogni stato.  
  
\- **Stato Verde**:  
  \- Il sistema inizia in questo stato e il clock `x` inizia a contare da
zero.  
  \- Transizione a Rosso: `x >= 60` (quando `x` raggiunge 60 secondi), reset
`x`.  
  
\- **Stato Rosso**:  
  \- Il sistema rimane in questo stato con `x` che ricomincia a contare.  
  \- Transizione a Verde: `x >= 60` (quando `x` raggiunge 60 secondi), reset
`x`.  
  
## Formalizzazione  
Un automa temporizzato può essere formalizzato come una tupla \\((Q, C,
\Sigma, E, q_0)\\) dove:  
\- \\(Q\\) è l'insieme degli stati.  
\- \\(C\\) è l'insieme finito di orologi.  
\- \\(\Sigma\\) è l'alfabeto delle azioni.  
\- \\(E\\) è l'insieme delle transizioni, dove ogni transizione è una tupla
\\((q, g, a, r, q')\\) con:  
  \- \\(q\\) stato sorgente.  
  \- \\(g\\) guardia (condizione sugli orologi).  
  \- \\(a\\) azione.  
  \- \\(r\\) insieme di orologi da resettare.  
  \- \\(q'\\) stato di destinazione.  
\- \\(q_0\\) è lo stato iniziale.  
  
## Riepilogo  
Un automa temporizzato è un automa a stati finiti esteso con orologi che
tengono traccia del tempo trascorso. Le transizioni tra stati sono
condizionate da guardie sugli orologi e possono comportare azioni immediate o
ritardi temporali, con la possibilità di resettare gli orologi. Questa
struttura permette di modellare comportamenti temporizzati in sistemi
complessi.  

