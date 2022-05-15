Introduzione
================

This is the teaching materials repository for:

-   Introduction to Data Science with R Tidyverse for Research

for University of Catania, Department of Political and Social Sciences,
Spring 2022.

------------------------------------------------------------------------

Questo è l’hub del materiale didattico per il seminario:

-   Introduzione alla Data Science con R Tidyverse, per la Ricerca
    Scientifica

per il Dipartimento di Science Politiche e Sociali dell’Università di
Catania, Secondo Semestre 2022.

------------------------------------------------------------------------

# Cos’è la Data Science

Data Science: produzione di valore applicando **pratiche e metodi della
ricerca scientifica** a qualunque tipo di informazione statistica, cioé
i “dati”.

La Data Science usa conoscenze tipiche della **Ricerca Statistica e
della Scienza dell’Informazione**. Per esempio, in questo seminario si
imparerà ad **organizzare i dati secondo degli standard internazionali**
che rendono molto più agevole la comunicazione delle informazioni.

### Perché alla Ricerca Sociale interessa la Data Science?

L’approccio moderno alla Ricerca Sociale prevede che uno studente, a
conclusione di una laurea magistrale, conosca almeno i principi di un
**linguaggio di programmazione scientifica**. Alcuni benefici:

-   La conoscenza di un linguaggio di programmazione scientifica è
    condizione per l’accesso al mondo della ricerca pubblica (Dottorati,
    Collaborazioni Tecniche, etc.) e privata (Ricerche sperimentali su
    comportamenti di consumo…). Tabelle e grafici sono elementi
    essenziali delle pubblicazioni scientifiche.
-   Lo studente apprende i principi della comunicazione “tecnica” in
    ambito privato. In particolare lo studente apprenderà come
    “interrogare” dati tabellari per supportare le proprie proposte.
-   OPINIONE PERSONALE: una società civile necessita di lavoratori della
    pubblica amministrazione (in inglese, public servants…) che hanno
    dimestichezza coi dati. Essi, avendo un accesso privilegiato
    all’informazione, hanno **possibilità ed oneri** di generare e
    diffondere valore in tutto il territorio che amministrano. Che
    pasticcio hanno combinato coi dati gli inglesi quando il Covid è
    arrivato da loro? La Regione Sicilia è stata da meno?
-   Nuove professioni, es. “Data Journalist”…

## Perchè scegliere R Tidyverse come linguaggio di programmazione scientifica per la Ricerca Sociale?

R è un linguaggio di programmazione, ovverosia una *sintassi logica* di
**codici** per impartire ordini ad un computer. Ogni comando produce un
*risultato* oppure un *errore* (cioé: non è eseguito). Un risultato
sbagliato non è un errore, dal punto di vista del computer.

I risultati si organizzano secondo schemi tipici (ad esempio: tabelle).
[Tidyverse](https://www.tidyverse.org/) è un “dialetto” di R che ha
tante buone proprietà:

-   facile
-   veloce
-   usa degli standard quindi…
-   …cresce organicamente: quando qualcuno traduce una tecnica (es.
    network analysis) nel dialetto Tidyverse, non deve reinventare i
    comandi.

Useremo anche una speciale interfaccia per R, che si chiama [R
Studio](https://www.rstudio.com/), e semplifica alcune operazioni di
gestione dei documenti di lavoro.

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CONCETTI FONDAMENTALI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Concetto di “Lato Utente”: Essere umano (utente) e computer (macchina) devono “interfacciarsi”. A volte la richiesta dell’utente è complessa e c’è la necessità di **disambiguare** il codice per permettere alla macchina di comprendere correttamente le istruzioni dell’utente. Nella ricerca sociale è molto importante che il codice con cui il ricercatore esegue operazioni ed analisi sui dati sia facile da capire per altri ricercatori. R Tidyverse è considerato un dialetto facile da valutare e trasparente in quello che fa, quindi adatto alla ricerca scientifica. |
| Concetto di “Lato Macchina”: Nei fatti è la velocità con cui la macchina esegue gli ordini. Nella ricerca sociale tradizionale di solito la velocità delle operazioni è istantanea, ma per problemi avanzati (es. Big Data) il ricercatore deve **ottimizzare il codice** anche per non forzare la macchina a fare più lavoro del necessario.                                                                                                                                                                                                                                       |

# Alternative ad R

`R` non è l’unico software di Data Science per la ricerca sociale. Il
linguaggio più famoso è `Python`, ed una terza alternativa è `Julia`.
Tutti e tre sono **gratuiti**.

`Stata` è un linguaggio di programmazione scientifica per la ricerca
sociale a pagamento. `SPSS` non è un linguaggio ma una interfaccia che
“pre-confeziona” alcune operazioni tipiche e poi le converte in diverse
linguaggi. Infine, probabilmente conoscerete già `Excel`, che è uno
strumento utile per l’immissione dei dati tabellari, ma non per compiere
analisi automatizzate (quindi: veloci, non richiedono molto sforzo).
*Chi mi sa dire perché?*

|                                                                                                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Suggerimento:                                                                                                                                                          |
| Excel funziona su base *continua*… questo è indesiderabile perché è come se deve sempre usare molta più energia del necessario. Buono per operazioni piccole e rapide. |

# Guida all’installazione di tutto il software necessario

-   Prima di tutto, scaricate [l’ultima versione di R per il vostro
    sistema operativo](https://cran.stat.unipd.it/). Finito il download,
    installate il file.
-   Ripetete l’operazione con [R
    Studio](https://www.rstudio.com/products/rstudio/download/)

D’ora in poi, se volete lavorare su R, aprirete sempre R Studio.

## Installare Tidyverse

A questo punto bisogna installare Tidyverse. Ci sono due modi egualmente
validi, ed un terzo metodo che è ancora più comodo, ma richiede di aver
capito i primi due.

-   Metodo 1: aprite R Studio. Il programma è diviso in quattro
    riquadri. Il riquadro in basso a destra ha cinque pagine:
    “Files,”Plots“,”Packages“,”Help" e “Viewer”. Basta cliccare su
    “Packages”. Spunterà una lista di “pacchetti”, che sono contenitori
    di codici. Sotto “Files” apparirà “Install”. Qui bisogna scrivere
    “tidyverse”, spuntare l’opzione per installare pure le sue
    dipendenze e poi cliccare su “Install”.

![Packages](Packages.PNG)

-   Metodo 2: Nello spazio chiamato “Console” (di base, si trova nel
    riquadro in basso a sinistra), scrivete questo codice:
    `install.packages("tidyverse")`, poi premete Invio.

Complimenti! Avete avete lanciato il vostro primo comando a R! Avete
enunciato un “ordine”: *Installa!* ed avete associato un complemento
oggetto: “tidyverse”.

Se tutto è andato a buon fine, R ha eseguito il comando: si è connesso
con Tidyverse ed ha installato il codice aggiutivo per “imparare” il
dialetto di Tidyverse, che in effetti si compone di diversi
sotto-pacchetti che arricchiranno il vostro repertorio con nuovi
comandi.

Prima di capire cosa fa il Metodo 3, bisogna ricordarsi che…

### ANCHE SE UN PACCHETTO È INSTALLATO,

### NON FUNZIONERÀ FINCHÈ NON È ATTIVATO.

### QUANDO CHIUDETE R STUDIO,

### TUTTI I PACCHETTI EXTRA SI DISATTIVANO DA SOLI

Ne consegue che: per lanciare comandi in “dialetto Tydiverse” bisogna
prima attivare “Tidyverse”.

Per attivare Tidyverse, bisogna lanciare il comando:

``` library("tidyverse")```.
Ora siete pronti per il Metodo 3.

* Metodo 3: Installate "pacman". Dovreste esserne capaci da soli. Ora lanciate il comando: ```pacman::p_load("tidyverse")```

---
In questo caso non è stato necessario attivare "pacman", perché abbiamo anteposto `pacman::` al nome del comando. Anteporre il nome del pacchetto e due volte due punti prima di un comando è utile per *disambiguare* il codice.
---

`p_load("nome_del_pacchetto")` fa due cose: se il pacchetto non è installato, lo installa e poi lo attiva, se è già installato, lo attiva e basta. Se il pacchetto è già attivato, pacman non fa niente. Potete chiedere a pacman di attivarvi più pacchetti in un solo comando in questo modo: `p_load("nome_del_pacchetto_1","nome_del_pacchetto_2","nome_del_pacchetto_etcetc")`. Comodo, no?

# A che serve Github?

Github è un sito che funge da deposito di codici ed altro materiale informatico utile. Una cartella di documenti si chiama "Repository". Github viene organizzato secondo il linguaggio "Git", la cui conoscenza non è necessaria per questo seminario.

Idealmente, se a qualcuno di voi interessa imparare come usare Github, vi sarà possibile scaricare tutto il materiale da lezione dentro una cartella del vostro computer usando i comandi di R Studio. Alternativamente dovreste poterli scaricare uno alla volta.

---
Git e Github sono utili nel mondo della ricerca perché consenstono di lavorare in parallelo su documenti informatici complessi, condivisi in un team di ricerca, creando versioni parallele dello stesso progetto e condividendo risorse.

Il linguaggio equivalente per la scrittura di articoli scientifici si chiama LateX
(si pronuncia: LateCh; l'ultima lettera è una Chi greca).
---

# Beneficio didattico di Tidyverse?

Ci sono diversi benefici ad usare Tidyverse invece della sintassi base. L'idea di fondo dietro Tidyverse è che la tabella multivariata deve diventare l'oggetto centrale di ogni operazione per rendere R un linguaggio raffinato per la Data Science. Nel fare questo R "assorbe" caratteristiche da altri linguaggi.

Per esempio, buona parte delle operazioni tabellari sono copiate da SQL, il linguaggio dei database relazionali, mentre le funzioni di automazione di solito si affidano a del "codice nascosto" in C++, che è un altro linguaggio!!!

Il principale beneficio di imparare R subito con Tidyverse è che il codice si presenterà in una forma molto comprensibile, infatti ogni comando sarà intervallato da un simbolo `%>%` che serve a separare le operazioni in blocchettini atomici. Questa riduzione atomica è molto utile per lo studio perché potete isolare operazione per operazione facilmente e capire cosa state facendo per prove e tentativi.

Inoltre, se imparate R Tidyverse è molto probabile che vi verrà facilissimo imparare SQL, dopo.

Un difetto di Tidyverse: tende ad escludere le liste (`list`) dall'uso; mentre specialmente in programmazione avanzata per l'automazione (per esempio, lo scraping), le liste sono molto utile. C'è da dire che la loro sintassi di indicizzazione è cervellotica.

# Risorse

https://www.r-bloggers.com/ è una buona fonte, aggiornata, che consiglio anche di seguire su Twitter.

Io moltissime cose le ho imparate piano piano su questo sito:
https://stackoverflow.com/

Stack Overflow è una sorta di forum che è esclusivamente dedicato a una sola funzione:

- si sceglie un linguaggio informatico
- si mostra un codice che non funziona
- si cerca di spiegare come lo si vorrebbe fare funzionare

A quel punto ci sono degli utenti, di solito davvero molto bravi, che propongono delle soluzioni, e chi fa la domanda sceglie la soluzione che trova migliore. Tutte le persone coinvolte in questo processo, ma soprattutto chi da la risposta migliore, prendono dei "punti". Accumulare punti quantifica la reputazione di quella persona e moltissime persone, soprattutto dal Terzo Mondo, che non possono studiare nelle Università ma sono auto-didatte, mettono la loro reputazione su questo sito nei loro curriculum.

## Libri

Personalmente, non conosco buoni libri dedicati esclusivamente ad R che siano a pagamento. Ne conosco solo di gratuiti, online, pubblicati con una estensione di Markdown che si chiama Bookdown.

Qui una lista eterogenea:

https://www.r-bloggers.com/2022/05/best-books-to-learn-r-programming-2/

Qui una mia selezione personale:

- Libro che copre nel dettaglio gli argomenti delle prime due lezioni:

https://r4ds.had.co.nz/

## Argomenti non coperti dalle lezioni:

- Modeling statistico, molto utile per chi vuole fare ricerca sociologica quantitativa

https://www.tmwr.org/

- Text mining, per chi vuole lavorare su corpus testuali

https://www.tidytextmining.com/

- Ricettario grafico

https://r-graphics.org/

- (Io non lo ho mai completato) questo è considerato il miglior libro per capire sia la statistica multivariata che la programmazione in R di applicazioni Data Science / Artificial Intelligence 

https://www.amazon.com/Introduction-Statistical-Learning-Applications-Statistics/dp/1071614177/ref=sr_1_1?keywords=An+Introduction+to+Statistical+Learning%3A+with+Applications+in+R&qid=1651979932&s=books&sr=1-1

Se voi capite questo qui molto bene siete ad un livello per cui potete già lavorare come data scientist o potete entrare in qualunque dottorato di ricerca, anche uno in Computer Science.


# Struttura delle Lezioni

Il Seminario si compone di 6 Lezioni:

1. Formati e strutture dati elementari su R
2. Comandi di calcolo algebrico, logico-testuale e statistico
3. Maneggiare la struttura tabellare
4. Visualizzazione grafica
5. Principi di automazione dei comandi ed alcune tecniche avanzate di Data Science

Che troverete a [questo link](ciao)

# Esami per studenti di LM-88

Esame per frequentanti:

3 domande a risposta chiusa su:
- Sotto-modulo 1 (formati e strutture)
- Sotto-modulo 2 (calcolo, logica, correlazioni e regressioni)
- Sottomodulo 3 (tibbles etc.)

Esempio di domande d'esame:

---
DOMANDA: Voglio calcolare la media del vettore "Altezze", quali delle seguenti pipelines produrrà un errore?

1. `Altezze %>% mean()`
2. `Altezze %>% c() %>% mean()`
3. `mean(Altezze) %>% c()`
4. `c(mean) %>% Altezze`
---

---
DOMANDA: Cosa descrive il risultato di questa pipeline?


```r
Residenti %>%
  filter(Nazionalità != "Italia") %>%
  group_by(Nazionalità) %>%
  summary(n() / nrow(Residenti))
```

1.  Conta il numero di residenti nel Comune (qui non specificato quale
    Comune) e poi li raggruppa per nazionalità, italiana e non.
2.  Conta quante volte ricorre la nazionalità italiana nel database
    filtrato chiamato “Residenti”.
3.  Raggruppa i "Residenti\` del Comune (qui non specificato quale
    Comune) per nazionalità, e poi li conta in percentuale.
4.  Raggruppa i “Residenti” non italiani per nazionalità, e poi ne conta
    la percentuale sui Residenti.

------------------------------------------------------------------------

Esempi di domande orale:

-   Mi parli della differenza tra codice e dati.
-   Cos’è l’argomento di una funzione informatica?
