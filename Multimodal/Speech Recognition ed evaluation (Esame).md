# Speech Recognition ed evaluation (Esame)


Il riconoscimento vocale, o speech recognition, è un processo attraverso il
quale un computer o un dispositivo tecnologico interpreta e converte il
parlato umano in testo scritto.  
  
È il processo di conversione di un segnale vocale in una sequenza di parole,
per mezzo di un algoritmo  
  
Terminologia:  
• **Utterance  **(espressione): Quando l'utente dice qualcosa, questo è noto
come  
un'espressione. Un'espressione è qualsiasi flusso di discorso tra due periodi
di silenzio. Le  
espressioni vengono inviate al motore vocale per essere elaborate.
Un’espressione può  
essere una singola parola o una frase.  
Il silenzio, nel riconoscimento vocale, è importante quasi quanto ciò che
viene detto,  
perché il silenzio delinea l'inizio e la fine di un'espressione.  
• **Pronunciations** : Il motore di riconoscimento vocale utilizza tutti i
tipi di dati, modelli  
statistici e algoritmi per convertire l'input vocale in testo.  
Un'informazione che il motore di riconoscimento vocale utilizza per elaborare
una parola è  
la sua pronuncia, che rappresenta come il motore di riconoscimento vocale
pensa che  
dovrebbe suonare una parola. Le parole possono avere più pronunce ad esse
associate. Ad  
esempio, la parola "the" ha almeno due pronunce nella lingua inglese degli
Stati Uniti:  
"thee" e "thuh".  
• **Grammars** : Bisogna specificare le parole e le frasi che gli utenti
possono dire in  
un'applicazione. Queste parole e frasi vengono definite nel motore di
riconoscimento  
vocale e vengono utilizzate nel processo di riconoscimento. Le grammatiche
definiscono il  
dominio, o contesto, all'interno del quale funziona il motore di
riconoscimento. Il motore  
confronta l'espressione corrente con le parole e le frasi nelle grammatiche
attive. Se  
l'utente dice qualcosa che non è nella grammatica, il motore vocale non sarà
in grado di  
decifrarlo correttamente.  
• **Accuracy** : La precisione è in genere una misura quantitativa delle
prestazioni di un sistema  
di riconoscimento vocale e può essere calcolata in diversi modi. Probabilmente
la misura  
più importante dell'accuratezza è se si è verificato il risultato finale
desiderato.  
  
Abbiamo un gran numero di condizioni su cui basarci per l’evaluation del
sistema:  
• **Speaker dependence vs. independence:**  
  
• **Isolated, discontinuos or continuos speech:**  
o _discorso isolato_ : significa singole parole;  
o _discorso discontinuo:_  significa frasi complete in cui le parole sono
separate  
artificialmente dal silenzio;  
o _discorso continuo:  _significa frasi pronunciate in modo naturale.  
Il riconoscimento vocale isolato e discontinuo è relativamente facile perché i
confini delle  
parole sono rilevabili e le parole tendono ad essere pronunciate in modo
netto.  
• **Read vs. spontaneous speech:**  I sistemi possono essere valutati in base
al discorso che  
viene letto da script preparati o al discorso pronunciato spontaneamente.  
Il discorso spontaneo è molto più difficile, perché tende ad essere condito da
disfluenze  
come "uh" e "um", false partenze, frasi incomplete, balbuzie, tosse e risate;
e inoltre, il  
vocabolario è essenzialmente illimitato; quindi, il sistema deve essere in
grado di gestire in  
modo intelligente parole sconosciute (ad esempio, rilevando e segnalando la
loro presenza  
e aggiungendole al vocabolario, che potrebbe richiedere una certa interazione
con  
l'utente).  
•**  Adverse conditions:** Le prestazioni di un sistema possono anche essere
degradate da una  
serie di condizioni avverse, come:  
o rumore ambientale (es. rumore in un'auto o in una fabbrica);  
o distorsioni acustiche (es. echi, acustica ambientale); o microfoni diversi;  
o banda di frequenza limitata (nella trasmissione telefonica);  
o modo di parlare alterato (gridare, piagnucolare, parlare velocemente, ecc.).

