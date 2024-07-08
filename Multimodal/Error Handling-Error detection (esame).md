# Error Handling/Error detection (esame)


  1. input mancante,
  2. rifiuto di riconoscimento,
  3. il riconoscitore restituisce qualcosa che non può essere interpretato (non ha alcun senso),
  4. il riconoscitore restituisce qualcosa che non è semanticamente coerente,
  5. il riconoscitore restituisce frasi semanticamente ben formate, ma impossibili da soddisfare,
  6. come il punto 5, con l'eccezione che l'impossibilità è dovuta al contesto del dialogo,
  7. il sistema backend non riesce a soddisfare il comando (ad esempio, connessione al database persa),
  8. correzione degli errori iniziata dall'utente: l'utente può rilevare molti tipi di errori,  
errori di riconoscimento vocale che non risultano in nessuno dei tipi di
errore sopra menzionati e che non possono essere identificati dai punteggi di
riconoscimento e dallo stato del dialogo, possono essere rilevati solo
dall'utente,

Il progettista del sistema deve assicurarsi che l'utente possa individuare e
correggere ogni possibile errore che può verificarsi, e anche che l'utente
sappia come correggerli.

