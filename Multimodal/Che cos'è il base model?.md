# Che cos'è il base model?


L'approccio standard (base model) al riconoscimento vocale continuo di un
ampio vocabolario presuppone un semplice modello probabilistico di produzione
vocale.  
  
Una sequenza di parole specificata, **W** , produce una sequenza di
osservazione acustica **Y** , con probabilità **P(W,Y).**  L'obiettivo è
decodificare la stringa di parole, in base alla sequenza di osservazione
acustica, in modo che la stringa decodificata abbia la Maximum a Posteriori
**(MAP)  **probability.

