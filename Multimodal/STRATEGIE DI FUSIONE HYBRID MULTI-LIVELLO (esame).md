# STRATEGIE DI FUSIONE HYBRID MULTI-LIVELLO (esame)


Nel metodo ibrido multilivello, l'integrazione dei segnali di input è
distribuita tra i livelli di acquisizione, riconoscimento e decisione. Esempi
di metodologie applicate in letteratura includono:

  * **Transduttori a stati finiti**  
  * **Grammatiche multimodali**

1\. **Transduttori a Stati Finiti (FST)**

  * I transduttori a stati finiti (FST) sono **automi** a stati finiti (FSA) in cui ogni **transizione consiste in un simbolo di input e un simbolo di output**.
  * Un FST può essere considerato come un **FSA a 2 nastri** con un nastro di input da cui vengono letti i simboli di input e un nastro di output su cui vengono scritti i simboli di output.  

  * Un dispositivo a stati finiti elabora più flussi di input e combina il loro contenuto in una singola rappresentazione semantica.
  * Per un'interfaccia con n modalità, è necessario un dispositivo a stati finiti che operi su n+1 nastri (n flussi di input + 1 output di interpretazione).

**2\. Grammatiche Multimodali**

  * I risultati di ogni riconoscitore sono considerati come **simboli terminali di una grammatica formale** e, di conseguenza, sono riconosciuti dal parser come una singola frase multimodale.
  * Nella fase di interpretazione, il parser utilizza la specifica della grammatica (regole di produzione) per interpretare la frase.
  * L'input multimodale unico può essere rappresentato utilizzando le strutture di caratteristiche tipizzate (TFS).

  

**  
**

**PRO:**

  * **Somiglianza con il paradigma utilizzato nella comunicazione umana** , in cui il dialogo è considerato un fenomeno linguistico unico.

**CONTRO:**

  * Alta complessità della **disambiguazione** intermodale.

