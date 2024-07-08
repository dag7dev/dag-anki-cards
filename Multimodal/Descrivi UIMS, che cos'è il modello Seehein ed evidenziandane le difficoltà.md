# Descrivi UIMS, che cos'è il modello Seehein ed evidenziandane le difficoltà


Un **UIMS** (User Interface Management System) è un meccanismo che **controlla
la relazione tra la presentazione e le funzionalità** , in altre parole
controlla la relazione tra l’interfaccia e le operazioni che si svolgono
attraverso vari canali (voce, gesti, ecc.). Un UIMS è uno strumento o un
insieme di strumenti che aiuta a specificare, implementare, testare e
mantenere un'interfaccia utente. Esso migliora:  
  
**\- Portabilità** : abilità di usare il sistema su dispositivi differenti,
molto complesso nel caso di interfacce multimodali.  
**\- Ri-usabilità** : riusare le componenti per ridurre le spese.  
**\- Interfacce multiple** : per accedere alle stesse funzionalità. In
interfacce multimodali, le interfacce multiple implicano multipli canali.  
Personalizzazione: per il designer e l’utente, a seconda delle necessità.  
  
Nel modello Seehein, sviluppato negli anni '80 durante un workshop UIMS a
Seehein in Germania, il software è separato in tre parti:

  1. **Presentation component:** definisce il comportamento del sistema percepito e manipolato dall'utente.
  

  2. **Application interfaces component:** fornisce una vista dell'applicazione e gestisce la comunicazione.
  

  3. **Dialogue component:** un mediatore tra l’application interfaces component e la presentation component.
  

  

Dalle tre componenti otteniamo tre tipi di feedback:

  1. **Lexical:** rappresenta il codice per esprimere che il sistema ha capito l'intento dell'utente di spostare il focus dell'azione su un'altra cosa (ad esempio, il movimento del mouse).
  

  2. **Syntactic:** regole sintattiche che devono essere rispettate, come una voce di menu selezionata deve essere evidenziata, o un determinato tasto premuto esegue una determinata azione.
  

  3. **Semantic:** il risultato dell'azione compiuta, come il numero sulla calcolatrice che cambia a seguito di una somma. Il feedback semantico è il più lento, ma in molti casi è necessaria una valutazione semantica più veloce (ad esempio, evidenziare il cestino dei rifiuti sul desktop quando un documento viene spostato nelle vicinanze).
  

  

Due difficoltà principali nel modello Seehein sono:

  1. Quando si cambia un componente di presentazione, la  
la **finestra di dialogo deve essere riscritta** per adattarsi alle sue
caratteristiche  
  

  2. la finestra di dialogo tende a basarsi sulla presentazione e  
**la presentazione deve essere cambiata ogni volta che la finestra di  dialogo
viene modificata**  

  

MA  
  

**Gestendo ogni blocco in maniera indipendente** , possiamo fornire gli
**stessi strati esterni per diverse applicazioni**. Ad esempio, cambiando solo
il dialogue possiamo applicare lo stesso aspetto grafico a un editor di testo
come Word e a un foglio di calcolo come Excel. In questo modo, l'utente non
deve imparare diverse lingue di dialogo per diverse applicazioni, come avviene
nei prodotti Microsoft.

