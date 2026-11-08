# wine-selector
Il progetto consiste nello sviluppo di un sistema intelligente di raccomandazione dei vini che utilizza l'algoritmo di ottimizzazione Particle Swarm Optimization (PSO) per individuare il vino più adatto in base al cibo, all'occasione e al budget dell'utente. L'obiettivo è applicare tecniche di intelligenza computazionale a un problema concreto: scegliere il vino più appropriato da portare a cena.

# Dataset
I dati vengono acquisiti da un documento Google Sheets accessibile attraverso il seguente link, utilizzato come database dei vini.

[https://docs.google.com/spreadsheets/d/1ula298Ry_2ld8ejwDEPu-BvQDhRk1IrTp0NyckL1USI/export?format=csv](https://docs.google.com/spreadsheets/d/1ula298Ry_2ld8ejwDEPu-BvQDhRk1IrTp0NyckL1USI/edit?usp=sharing)


Per ogni vino vengono considerate sei informazioni: nome, prezzo, acidità, dolcezza, intensità, tannini. 
Le quattro caratteristiche organolettiche hanno valori compresi tra 1 e 5. 

# Pulizia dati
Prima dell'elaborazione, il sistema esegue una fase di preprocessing che comprende:
  * conversione dei valori numerici;
  * gestione dei valori mancanti;
  * eliminazione dei vini privi di nome;
  * eliminazione delle caratteristiche non valide;
  * controllo dei prezzi;
  * arrotondamento dei valori a due decimali.

Per i vini privi di prezzo vengono attualmente assegnati valori simulati compresi tra 5 € e 50 €.

# Scelta dell'utente
Il sistema mette a disposizione sei profili alimentari:
  * grigliata o arrosti di carne
  * pesce al forno e frutti di mare
  * primo piatto al pomodoro e ragù
  * tagliere di formaggi e salumi
  * cena vegana, verdure e risotti
  * pasticceria, dessert e torte

Ogni profilo è rappresentato da un target ideale composto da acidità, intensità, dolcezza e tannini.


L'utente può inoltre selezionare tre tipologie di occasione:
  * Cena formale
  * Cena informale tra amici
  * Cena romantica o occasione speciale

A ogni occasione viene associato un peso che modifica l'influenza del prezzo nella funzione di fitness.

# Fitness
Il sistema utilizza la distanza euclidea per misurare la somiglianza tra le caratteristiche del vino e il profilo alimentare ideale.
La funzione di fitness da massimizzare è:  \Fitness = -\D +(\frac{\prezzo}{\budget}*\peso_prezzo).

Dove:
  * \D rappresenta la distanza euclidea;
  * il prezzo è rapportato al budget massimo;
  * il peso del prezzo dipende dall'occasione selezionata.

Una fitness più vicina allo zero indica una soluzione migliore secondo i criteri definiti.


# PSO
Il progetto implementa l'algoritmo Particle Swarm Optimization, ispirato al comportamento collettivo di gruppi di particelle.
Ogni particella rappresenta una possibile soluzione, identificata dall'indice di un vino nel database.

L'algoritmo utilizza:
  * 20 sciami
  * 30 particelle per sciame
  * 50 iterazioni per sciame
  * peso d'inerzia w=0.7
  * coefficiente cognitivo C1=1.5
  * coefficiente sociale C2=1.5

Le particelle aggiornano la propria posizione considerando la migliore soluzione individuale (Pbest) e quella globale (Gbest).

# Output

Al termine dell'elaborazione il programma restituisce:

  * il miglior vino individuato;
  * il relativo prezzo;
  * il profilo alimentare selezionato;
  * il confronto tra caratteristiche reali e target ideale;
  * il valore della fitness;
  * la percentuale di somiglianza;
  * una classifica dei vini individuati dai diversi sciami.

Il sistema esegue inoltre una ricerca esaustiva su tutti i vini disponibili per individuare il massimo globale della funzione di fitness.

# Utilizzo

Per eseguire il programma è necessario disporre di un ambiente Python con le librerie pandas e numpy installate.

È sufficiente:
  1. Scaricare il file Python del progetto.
  2. Aprirlo con un ambiente di sviluppo Python (ad esempio Visual Studio Code, PyCharm o Jupyter).
  3. Eseguire il programma.




