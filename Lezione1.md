Formati e strutture dati elementari su R
================

# Formati e Documenti

Con la parola “Formati” ci riferiamo alla estensione (es, `.txt`) dei
documenti (files) con cui lavoriamo. Questo può creare un po’ di
confusione col concetto di “formato tabellare”, che di fatto è una
“struttura dati” comune a più formati informatici nella Data Science.

Ci sono due formati di files comunemente usati su R.

## Lo Script

Per aprire un nuovo “Script”. In alto a sinistra, andate su “Files”, poi
su “New Files”, ed infine “R Script”. Potete anche premere
`CTRL + Shift + N`.

Lo script altro non è che un file di testo in cui annotate i comandi per
lanciarli uno per uno, oppure in sequenza.

Per lanciare un comando dentro uno script bisogna posizionare il cursore
del testo all’inizio del comando e poi premere `Invio + ctrl`. Premere
Invio da solo manda a capo il testo.

Provate a scrivere questo comando in uno script:

    print("Ciao a tutti, come va?")

e poi lanciatelo con `Invio + ctrl`.

|                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `print` è un comando che ordina a R di trasportare **il risultato** di una certa operazione in console. Per esempio, `2+2` è una operazione di somma. Che succede se si lancia `print(2+2)`?                       |
| R è ottimizzato in maniera tale che moltissimi comandi hanno un “print” implicito del loro risultato in console. Per esempio, se scrivete solo `2+2` in uno script e lo lanciate, cosa vedete apparire in console? |
| Questo perchè R *interpreta* il vostro comando, non esegue sempre e solo ciecamente gli ordini.                                                                                                                    |

Adesso lanciate `print("2+2")`. Cosa è cambiato? In questa lezione
impareremo a disambiguare le operazioni per ottenere sempre il risultato
desiderato.

------------------------------------------------------------------------

Generalmente, non vorrete mai lanciare uno script per intero.

|                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Questo non è Python! Su Python c’è la (brutta) tendenza a lanciare gli script per intero. Questa pratica non aiuta affatto chi è alle prime armi perché non permette di individuare quale pezzetto del codice è sbagliato. |

## Il Markdown

Il Markdown è un formato che interpreta un codice testuale testo e lo
traduce in HTML, così da renderlo pubblicabile come pagina online.

Per esempio, queste lezioni sono scritte in R Markdown, che è una
versione alternativa di Markdwon che permette di eseguire blocchi di
codice (“chunks”) in R, Python ed altri linguaggi.

Per aprire un nuovo file Markdown, seguite la stessa procedura per
aprire uno Script, ma stavolta scegliete R Markdown.

Il Markdown è simile allo script, ma in alto a destra c’è un simbolo con
un più ed una “c”. Se premuto, apre un chunk del linguaggio scelto.
Adesso si può scrivere un codice, ad esempio una sequenza di comandi. In
alto a destra del chunk c’è una freccia verso destra. Premendo la
freccia, il codice sarà eseguito, ma piuttosto che riportare i risultati
in console, li riporterà immediatamente sotto il chunk.

``` r
print("ciao, come state?")
```

    ## [1] "ciao, come state?"

``` r
"tutto bene"
```

    ## [1] "tutto bene"

|                                                                                                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Questo modo di visualizzare i risultati dei comandi è molto simile al metodo di programmazione per Jupyter Notebook, che è molto popolare tra chi programma in Python. |

## Progetti

Una buona pratica è creare dei Progetti di R. Queste sono cartelle del
vostro computer che sono già auto-organizzate in maniera efficiente,
cosicchè se un documento R (Script, Markdown, etc.) salverà un risultato
su un file esterno, questo file esterno si troverà comunque nella
cartella del Progetto.

Il Progetto si apre da File -&gt; New Project. Da qui dovreste anche
potervi connettere a progetti “condivisi” su piattaforme come Github.

# Strutture elementari

## Assegnazione in memoria di un valore ad un termine nel Global Environment (Workplace)

Un valore è una entità simbolica interpretabile da R secondo uno schema
di riferimento tipico. I tre valori più comuni sono:

-   valore logico (**logical**), detto altresì valore binario.
    Rappresenta uno stato di verità (**TRUE**, oppure la singola
    lettera T) oppure di falsità (**FALSE**, oppure F).
-   numeri, divisi tra numeri interi (**integer**) e numeri con la
    virgola (**double**)
-   grammi (**character**), cioé simboli alfanumerici compresi tra `" "`
    oppure `' '`. Questi simboli tendono a formare parole, sigle o frasi
    (**character**)

Altri valori “complessi” possono essere:

-   Le date
-   I livelli delle variabili ordinali (**factor**)

## Assegnazioni, Interrogazioni ed Invocazioni (Chiamate)

La assegnazione è un comando speciale con cui si stabilisce una
relazione per cui un valore o una struttura (per esempio, una tabella)
viene assegnato ad una parola (stavolta senza virgolette).

Il comando dell’Assegnazione è `->` (oppure, `->`).

Per esempio, se voglio assegnare il valore della somma `2+2` alla parola
`quattro`, comanderò:

`2+2 -> quattro`

oppure

`quattro <- 2+2`

Però spesso R *interpreta* anche `=` come un comando di assegnazione.
Spesso la grammatica corretta dipende dal dialetto che stiamo usando, e
solo la pratica ci farà capire il simbolo più appropriato.

``` r
1 -> a
a
```

    ## [1] 1

``` r
"La \"mamma\" è voce del linguaggio familiare e di tono affettuoso, usata perciò di regola come vocativo, o quando si parla della madre con i familiari o gli amici intimi" -> mamma

mamma
```

    ## [1] "La \"mamma\" è voce del linguaggio familiare e di tono affettuoso, usata perciò di regola come vocativo, o quando si parla della madre con i familiari o gli amici intimi"

``` r
(2+2 == 4) -> equazione
(2+3 < 4) -> disequazione
equazione
```

    ## [1] TRUE

``` r
disequazione
```

    ## [1] FALSE

Come abbiamo già visto, quando si scrive il termine e si esegue il
codice (con Invio oppure eseguendo l’intero blocco chunk), viene
eseguito un `print` implicito del termine. Questa operazione viene
chiamata “invocazione” oppure chiamata (call) di un termine.

Nel caso di valori logici è corretto parlare di “Interrogazione”
rispetto ad una proposizione. Le interrogazioni sono concetti utili, per
esempio il comando:

``` r
stringr::str_detect("Roma è la capitale","capitale")
```

    ## [1] TRUE

``` r
stringr::str_detect("Io vivo a Roma","capitale")
```

    ## [1] FALSE

interroga se il gramma “capitale” è contenuto nel gramma “Roma è la
capitale” e poi nel gramma “Io vivo a Roma”.

### Salvare e caricare files

Tutti i termini vengono memorizzati in un file di memoria temporanea che
sarà autodistrutto **SE** non viene salvato. Inoltre, tutti i termini
sono visualizzabili nella finestra “Environments”.

Ci sono diversi modi per salvare questo file di memoria. Il più
immediato è salvare l’intero file in formato `.Rdata` cliccando
sull’iconcina del floppy disk (sapete cosa sia un floppy disk???) nella
finestra Environment. Un modo alternativo più rapido di “salvare il
workspace” è il comando:

``` r
save.image("NOME_DEL_FILE.RData")
```

Vi accorgerete che nella finestra files è spuntato un file `.RData`.

Questi file `.RData` sono solitamente molto leggeri, ma potranno essere
letti (importati) solo da altri computer in cui è installato R. Per
importare / caricare / leggere un file `.RData` salvato, basta cliccare
su quel file nella lista dei files.

Facciamo la prova cancellando il workspace e poi ricaricando la copia
salvata.

Per cancellare il workspace bisgona premere sul simbolino della scopa in
alto rispetto al workspace. Si possono cancellare selettivamente solo
certi files, selezionandone la spunta in modalità Grid (Griglia).

Dopo aver introdotto le **strutture dati**, scopriremo che le tabelle,
che sono la struttura tipica della Statistica Multivariata, possono
essere salvate ed importate in altri formati standard. R ha una grande
capacità di leggere (cioé di “importare”) tanti formati dati.

## I vettori

I vettori sono **insiemi ordinati** di valori della stessa tipologia. I
vettori sono caratterizzati da un comando un po’ insolito, la lettera
“c”, che abbrevia il verbo “concatenate”, ma si può anche usare un
comando che richiama la tipologia dell’insieme per forzare tale
tipologia.

``` r
c(1,2,3) -> vettore_numerico

c("Pippo", "Claudio", "Maria") -> amici

vettore_numerico
```

    ## [1] 1 2 3

``` r
amici
```

    ## [1] "Pippo"   "Claudio" "Maria"

``` r
c(2+2==4,3>5, 3<4) -> Domandina

Domandina
```

    ## [1]  TRUE FALSE  TRUE

``` r
as.integer(Domandina)
```

    ## [1] 1 0 1

``` r
c(1,"mamma","zio")
```

    ## [1] "1"     "mamma" "zio"

### Ordinamento dei vettori

I vettori sono **ordinati**. Ogni valore contenuto in un vettore ha una
posizione e si chiama “elemento”. Per richiamare un elemento in una data
posizione si invoca il vettore seguito dal numero della posizione tra
parentesi quadra:

``` r
amici[2]
```

    ## [1] "Claudio"

``` r
amici[2:3]
```

    ## [1] "Claudio" "Maria"

``` r
amici[c(1,3)]
```

    ## [1] "Pippo" "Maria"

La cosa interessante di questo chunk è che è possibile richiamare più di
un elemento inserendo un vettore **integer** invece di un singolo
numero. Una costruzione intelligente di un **vettore integer** con le
posizioni degli elementi da richiamare può eseguire una ricerca mirata
in un lungo vettore. In questo caso la formula `2:3` comanda: da 2 a 3.

In questo modo è possibile anche fare assegnazioni non banali.

``` r
amici[c(1,3)] -> superamici
```

# Liste, data.frame e tibbles (Tabelle)

I vettori si possono combinare in due tipologie di contenitore:

-   Le liste: sono un contenitore piuttosto flessibile e con pochissimi
    requisiti. Sono maggiormente usate negli aspetti più informatici per
    operazioni di organizzazione interna dei dati. Non saranno
    approfondite in questo corso.
-   Le tabelle: R possiede una struttura base per le tabelle, il
    `data.frame`. Noi però useremo una struttura più raffinata, la
    `tibble`, che fa parte del dialetto “Tidyverse”.

La costruzione di tabelle deve rispettare:

-   Regole di codice informatico, senza le quali R non è capace di
    organizzare la tabella e restituirà un errore.
-   Regole di standard d’uso, che sono rispettate per rendere il lavoro
    più fluido e veloce.

## REGOLE MECCANICHE PER FORMARE UNA TABELLA

Una tabella incrocia un numero positivo di colonne (variabili) con un
certo numero non negativo di righe (osservazioni). L’elemento base della
tabella è **LA COLONNA, NON LA RIGA**.

-   Ogni colonna vede sé stessa come un vettore e ne rispetta le regole.
-   Ogni riga vede sé stessa come una tabella (di una sola riga) e ne
    rispetta le regole.
-   REGOLA IMPORTANTISSIMA: tutte le colonne della tabella devono avere
    lo stesso numero di elementi, cioé devono essere della stessa
    lunghezza. Ogni qual volta che si comanda a R qualcosa che viola
    questa regola, R si rifiuterà di eseguire

|                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Le Liste non seguono queste regole, per questo sono più agili per operazioni interni. Un bravo data scientist usa le liste per preparare i dati, ma poi le converte in tabelle alla fine della fase preparatoria. |

Che succede se nel formare una tabella mi manca una informazione e
quindi sospetto che i miei vettori non saranno della stessa lunghezza?
In questo caso si usa il simbolo `NA`, che significa “missing value”,
ovverosia “informaizone mancante”.

### I comandi per formare una tabella tibble

Le `tibble` si costruiscono per colonne, separate da virgole.

``` r
Tabella1 <- tibble(
  Numeri = c(1,2,3),
  Cognomi = c("Rossi","Verdi","Tomaselli")
)
```

Notate bene che siccome `tibble` fa parte del dialetto Tidyverse, qui
preferisco usare `=` per assegnare il contenuto dei vettori ai nomi
delle colonne.

Ci sono anche molti altri modi di formare una tabella da zero, ma questo
è quello basilare.

Due tabelle possono essere unite (bindate) in per righe:

``` r
rbind(Tabella1,
      tibble(
        Numeri = c(4,NA,6),
        Cognomi = c("Rossi","Verdi","Cantone")
        )
      )
```

    ## # A tibble: 6 x 2
    ##   Numeri Cognomi  
    ##    <dbl> <chr>    
    ## 1      1 Rossi    
    ## 2      2 Verdi    
    ## 3      3 Tomaselli
    ## 4      4 Rossi    
    ## 5     NA Verdi    
    ## 6      6 Cantone

O per colonne:

``` r
cbind(Tabella1,
      tibble(
        Numeri = c(4,NA,6),
        Cognomi = c("Rossi","Verdi","Cantone")
        )
      )
```

    ##   Numeri   Cognomi Numeri Cognomi
    ## 1      1     Rossi      4   Rossi
    ## 2      2     Verdi     NA   Verdi
    ## 3      3 Tomaselli      6 Cantone

Una alternativa forse migliore è semplicemente usare il dialetto
Tidyverse.

``` r
add_row(Tabella1,
        tibble(
          Numeri = c(4,NA,6),
          Cognomi = c("Rossi","Verdi","Cantone")
          )
        )
```

    ## # A tibble: 6 x 2
    ##   Numeri Cognomi  
    ##    <dbl> <chr>    
    ## 1      1 Rossi    
    ## 2      2 Verdi    
    ## 3      3 Tomaselli
    ## 4      4 Rossi    
    ## 5     NA Verdi    
    ## 6      6 Cantone

Ma che succede se ora provo a fare lo stesso per colonne?

``` r
add_column(Tabella1,
           tibble(
             Numeri = c(4,NA,6),
             Cognomi = c("Rossi","Verdi","Cantone")
             )
           )
```

Perchè prima non dava errore?

Useremo un nuovo comando che investiga la tipologia di struttura.

``` r
cbind(Tabella1,
      tibble(
        Numeri = c(4,NA,6),
        Cognomi = c("Rossi","Verdi","Cantone")
        )
      ) %>% class()
```

    ## [1] "data.frame"

|                                                                                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `%>%` è un operatore particolare. Si chiama “Pipe” o “Incanalatore” o “Intubatore” e serve a cambiare la sintassi di R nel dialetto Tydiverse. In questo caso, serve a dichiarare un comando in questa forma: “Bindami queste colonne E POI dimmi la tipologia (class) della struttura risultante”. |

Ebbene, R ha interpretato il comando `cbind` come se dovesse *anche*
cambiare la tipologia di tabella da `tibble` a `data.frame`. Questo
perché le `tibble` **NON AMMETTONO** due colonne con lo stesso nome,
mentre i `data.frame` sì.

## DOGMA DI TIDYVERSE

Questo è un Dogma che viene usato da ogni programmatore “Tidy”:

-   Ogni colonna deve rappresentare una variabile differente.
-   Ogni riga deve rappresentare una osservazione differente.
-   Ogni incrocio di colonna e riga deve assumere un valore *valido* per
    quella colonna, oppure un *valore mancante*/*missing value* (`NA`).
    Se invece il valore **non può esistere**, si usa `NaN`.

## Studio sulle “Tabelle ben formate”

Questa è una generica tabella:

``` r
set.seed(1810)
tibble(Dado_1 = sample(1:6, 30, replace = T),
       Dado_2 = sample(1:6, 30, replace = T))
```

    ## # A tibble: 30 x 2
    ##    Dado_1 Dado_2
    ##     <int>  <int>
    ##  1      2      4
    ##  2      4      6
    ##  3      6      4
    ##  4      3      3
    ##  5      5      5
    ##  6      6      6
    ##  7      2      4
    ##  8      3      5
    ##  9      5      4
    ## 10      2      1
    ## # ... with 20 more rows

|                                                                                                                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| In questa tabella il comando `sample()` campiona, ovverosia, estrae a caso dei numeri come se lanciassimo dei dadi.                                                                                                                                                                                                 |
| Il comando `set.seed()` contenente un numero serve a rendere replicabile in maniera identica proprio quel lancio dei dati, che però non può essere conosciuto a priori. Molti filosofi dell’informazione trovano questo argomento molto interessante e parlando correttamente di “pseudo random number generation”. |

Qual è il problema della tabella qui sotto?

``` r
set.seed(1810)
data.frame(
  Nome.1 = sample(c("Giovanni", "Maria", "Carlo", "Paola"),30, replace = T),
  Dado_1 = sample(1:6, 30, replace = T),
  Nome.2 = sample(c("Giovanni", "Maria", "Carlo", "Paola"),30, replace = T),
  Dado_2 = sample(1:6, 30, replace = T)
       )
```

    ##      Nome.1 Dado_1   Nome.2 Dado_2
    ## 1     Maria      5 Giovanni      3
    ## 2     Paola      2    Maria      3
    ## 3     Maria      2 Giovanni      5
    ## 4     Carlo      3    Maria      5
    ## 5     Paola      1    Paola      6
    ## 6     Carlo      2 Giovanni      1
    ## 7  Giovanni      4    Paola      4
    ## 8     Maria      6    Paola      4
    ## 9     Maria      4 Giovanni      2
    ## 10    Carlo      3 Giovanni      4
    ## 11 Giovanni      5    Carlo      4
    ## 12    Maria      6    Maria      6
    ## 13    Maria      4    Carlo      5
    ## 14    Paola      5    Maria      5
    ## 15 Giovanni      4    Paola      2
    ## 16 Giovanni      1    Carlo      4
    ## 17    Maria      6    Paola      1
    ## 18    Maria      6    Carlo      6
    ## 19    Paola      5    Paola      1
    ## 20 Giovanni      6    Paola      4
    ## 21    Paola      3 Giovanni      4
    ## 22    Maria      4 Giovanni      2
    ## 23    Paola      2    Maria      1
    ## 24 Giovanni      3    Paola      4
    ## 25 Giovanni      3    Carlo      1
    ## 26    Paola      3 Giovanni      6
    ## 27    Carlo      5    Paola      3
    ## 28    Carlo      5    Paola      4
    ## 29    Paola      2    Maria      5
    ## 30    Carlo      4    Paola      6

------------------------------------------------------------------------

Che problemi abbiamo qui?

``` r
set.seed(1810)
data.frame(Nome = c("Giorgio", "Michela", "Laura", "Arancione"),
           "Stato Civile" = c("Sposato con Michela", NA, "Nubile", "Sposato"),
           Età = c(34,28,"venti",20)
)
```

    ##        Nome        Stato.Civile   Età
    ## 1   Giorgio Sposato con Michela    34
    ## 2   Michela                <NA>    28
    ## 3     Laura              Nubile venti
    ## 4 Arancione             Sposato    20

# Salvare ed Importare in formato .csv ed Excel

Un formato standard per salvare le tabelle è il formato .csv Facile da
leggere, ma un po’ pesantuccio.

Per salvare un csv, il comando è:

``` r
nome_della_tabella = tibble(Prova = c(1,2))

write.csv(nome_della_tabella,"LaMiaTabella.csv")
```

Per importare (caricare, leggere) un .csv, si può cliccare sul .csv se
si trova nella cartella del Progetto. Alternativamente si usa
l’interfaccia accessibile da:

Files -&gt; Import Dataset -&gt; From text (readr).

Qui avrete una preview di ciò che state importando e potrete controllare
che R sta interpretando correttamente le tipologie delle colonne della
tabella (dataset). In basso a destra apparirà il codice per ri-eseguire
l’operazione senza usare l’interfaccia.

Il mio consiglio è di copiare quel codice nel vostro documento script o
Markdown.

Questa stessa operazione può essere usata per caricare tabelle da Excel.
Al posto del pacchetto “readr” useremo il pacchetto “readxl”.

``` r
pacman::p_load(readxl)
Laureati <- read_excel("base_dati_CICCHITELLI_excel/Laureati.xls", 
    col_types = c("numeric", "text", "date", 
        "text", "numeric", "numeric", "date", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric"))
```

Per salvare una tabella come files Excel il comando è:

In questo progetto
