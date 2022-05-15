Formati e strutture dati elementari su R
================

# Formati e Documenti

Formato: è l’estensione (es, `.txt`) dei documenti (files) con cui
lavoriamo.

I formati possono conservare:

-   `codice`
-   `dati`, es. risultati

|                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------|
| Avete capito la differenza tra codice e dati?                                                                                   |
| Il codice fa agire il computer secondo dei `comandi`. I `dati` sono le informazioni di input ed output (risultati) dei comandi. |

-   Esistono tanti formati per *conservare dati*
-   Essenzialmente ci sono due formati di files per *conservare codice*
    su R.

# Conservare Codice

## Lo Script è un tipo di formato per conservare CODICE

Per aprire un nuovo “Script”: - In alto a sinistra, andate su “Files”, -
Poi su “New Files”, - Infine “R Script”.

Potete anche premere `CTRL + Shift + N`.

Lo script altro non è che un file di testo in cui annotate i comandi per
lanciarli uno per uno, oppure in sequenza.

Per lanciare un comando dentro uno script bisogna posizionare il cursore
del testo all’inizio del comando e poi premere `Invio + ctrl`. Provate a
scrivere questo comando in uno script:

    print("Ciao a tutti, come va?")

e poi lanciatelo con `Invio + ctrl`.

|                                                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `print` è un comando che ordina a R di trasportare **il risultato** di una certa operazione in **console**. Per esempio, `2+2` è una operazione di somma. Che succede se si lancia `print(2+2)`?                   |
| R è ottimizzato in maniera tale che moltissimi comandi hanno un “print” implicito del loro risultato in console. Per esempio, se scrivete solo `2+2` in uno script e lo lanciate, cosa vedete apparire in console? |
| Questo perchè R *interpreta* il vostro comando, non esegue sempre e solo ciecamente gli ordini.                                                                                                                    |

Adesso lanciate `print("2+2")`. Cosa è cambiato? In queste lezioni
impareremo a **disambiguare** le operazioni per ottenere il risultato
desiderato.

------------------------------------------------------------------------

Generalmente, non vorrete mai lanciare uno script per intero.

------------------------------------------------------------------------

Questo non è Python! Su Python c’è la (brutta) tendenza a lanciare gli
script per intero. Questa pratica non aiuta affatto chi è alle prime
armi perché non permette di individuare quale pezzetto del codice è
sbagliato.

------------------------------------------------------------------------

## Il Markdown

Il Markdown è un un altro formato per conservare CODICE. Si considera un
formato comodo per la didattica perché può interpretare il codice e
tradurlo in HTML, così da renderlo pubblicabile come pagina online.

|                                                                                                                                                                                             |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Per esempio, queste lezioni sono scritte in *R Markdown*, che è una versione alternativa di Markdwon che permette di eseguire blocchi di codice (“chunks”) in R, Python ed altri linguaggi. |

Per aprire un nuovo file Markdown, seguite la stessa procedura per
aprire uno Script, ma stavolta scegliete R Markdown.

Il Markdown è simile allo script, ma in alto a destra c’è un simbolo con
un più ed una “c”. Se premuto, apre un *chunk* del linguaggio scelto.
Adesso si può scrivere un codice dentro il chunk, ad esempio una
sequenza di comandi. In alto a destra del chunk c’è una freccia verso
destra. Premendo la freccia, il codice dentro il chunk sarà eseguito.

Non troverete i risultati in console, ma immediatamente sotto il chunk.

``` r
# ricordatevi che spesso (NON SEMPRE) il print() è pleonastico
print("ciao, come state?")
```

    ## [1] "ciao, come state?"

``` r
"tutto bene"
```

    ## [1] "tutto bene"

``` r
# In qualunque contesto, potete annotare del testo che non sarà eseguito antecedendo la riga col simbolo `#`
```

|                                                                                                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Questo modo di visualizzare i risultati dei comandi è molto simile al metodo di programmazione per Jupyter Notebook, che è molto popolare tra chi programma in Python. |

# Conservare dati in files

## Progetti

Una buona pratica è creare dei Progetti di R. Queste sono cartelle del
vostro computer che sono già auto-organizzate cosicchè se un documento R
(Script, Markdown, etc.) salverà un risultato su un file esterno, questo
file esterno si troverà comunque nella cartella del Progetto.

Il Progetto si apre da File -&gt; New Project. Da qui dovreste anche
potervi connettere a progetti “condivisi” su piattaforme come Github.

### Lavorare con Markdown e progetti

Se la cartella del Markdown è in una sottocartella della cartella
progetto e la cartella in cui conservate i files dati salvati o da
importare sta su una sottocartella diversa, R non riuscirà a torvare i
files da caricare. In questo caso, dovete:

-   andare nelle opzioni globali di R Studio
-   andare su R Markdown
-   Cambiare “Evaluate chunks in directory” da “Document” a “Project.”

# Prima di conservare dati bisogna organizzare i dati in strutture di classificazione e poi assegnarli ad un “oggetto” (che è un nome)

## Assegnazione in memoria di un valore ad un oggetto nel Global Environment (Workplace)

Un valore è una entità simbolica interpretabile da R secondo uno schema
di riferimento tipico. Il valore informatico è strettamente legato al
concetto di valore statistico, a volte riferito anche come “modalità
della variabile”. Qui a noi interessa capire quali sono le classi di
valore tipiche.

|                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------|
| Vi ricordate la classificazione delle unità di misurazione che si studia in Statistica ed anche in Metodologia della Ricerca Sociale? |
| \- Logico binario                                                                                                                     |
| \- Nominale                                                                                                                           |
| \- Ordinale                                                                                                                           |
| \- Continua                                                                                                                           |

Le tre classi di valore più comuni su R sono:

-   valore logico (**logical**), detto altresì valore binario.
    Rappresenta uno stato di verità (**TRUE**, oppure la singola
    lettera T) oppure di falsità (**FALSE**, oppure F).
-   numeri, divisi tra numeri interi (**integer**) e numeri con la
    virgola (**double**).
-   stringhe (**character**), cioé simboli alfanumerici compresi tra
    `" "` oppure `' '`. Questi simboli tendono a formare parole, sigle o
    frasi.

Esempi di altri valori possono essere:

-   Le date
-   I livelli delle variabili ordinali (**factor**)

## Assegnazioni, Interrogazioni ed Invocazioni (Chiamate)

La assegnazione è un comando speciale con cui si stabilisce una
relazione per cui un valore o una struttura (per esempio, una tabella)
viene assegnato ad una parola (stavolta senza virgolette).

Il comando dell’Assegnazione è `->` (oppure, `->`).

|                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Il comando di assegnazione va scritto e poi eseguito. Il comando non è attivo finché non è stato eseguito. Il risultato del comando di assegnazione NON si vede in console, ma modificherà qualcosa nel workplace (enviroment). |

Per esempio, se voglio assegnare il valore della somma `2+2` alla parola
`quattro`, comanderò:

`2+2 -> quattro`

oppure

`quattro <- 2+2`

Però spesso R *interpreta* anche `=` come un comando di assegnazione.
Spesso la grammatica corretta dipende dal dialetto che stiamo usando. La
pratica ci farà capire quale sia il simbolo più appropriato.

``` r
1 -> a
a
```

    ## [1] 1

``` r
## Assegnazione di un testo ad un oggetto

"La \"mamma\" è voce del linguaggio familiare e di tono affettuoso, usata perciò di regola come vocativo, o quando si parla della madre con i familiari o gli amici intimi" -> mamma

mamma
```

    ## [1] "La \"mamma\" è voce del linguaggio familiare e di tono affettuoso, usata perciò di regola come vocativo, o quando si parla della madre con i familiari o gli amici intimi"

``` r
## Questa è una interrogazione, che da per risultato un valore logico binario di vero / falso
(2+2 == 4) -> equaz
(2+3 < 4) -> disequaz
equaz
```

    ## [1] TRUE

``` r
disequaz
```

    ## [1] FALSE

Come abbiamo già visto, **quando si scrive il termine dell’oggetto** e
si esegue il codice, viene eseguito un `print` implicito dell’oggetto.
Questa operazione viene chiamata “invocazione” oppure chiamata (call) di
un oggetto, vedremo nelle prossime lezioni" che è utile “concatenerare”
una chiamata ad una vista con:

`oggetto %>% View()`

|                                            |
|--------------------------------------------|
| Comando utile quando si lavora con scripts |

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

interroga se la stringa “capitale” è contenuto nella stringa “Roma è la
capitale” e poi nel gramma “Io vivo a Roma”.

## Salvare e caricare files dati

Tutti i termini vengono memorizzati in un file di memoria temporanea che
sarà autodistrutto **SE** non viene salvato.

Inoltre, tutti i termini sono visualizzabili nella finestra
“Environments”, che noi chiamiamo workspace.

|                              |
|------------------------------|
| QUINDI                       |
| BISOGNA                      |
| RICORDARSI                   |
| DI SALVARE I DATI DI LAVORO! |
| (Oltre al codice)            |

# Files .Rdata, cosa sono?

Ci sono diversi modi per salvare il workspace come unico file di
memoria. Questo salva TUTTI gli oggetti. Il più immediato è salvare
l’intero file in formato `.Rdata` cliccando sull’iconcina del floppy
disk (sapete cosa sia un floppy disk???) nella finestra Environment. Un
modo alternativo più rapido di “salvare il workspace” è il comando:

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

### Alternative a salvare l’intero workspace come .Rdata

Dopo aver introdotto le **strutture dati**, scopriremo che le
**tabelle**, che sono la struttura tipica della *Statistica
Multivariata*, possono essere salvate ed importate in altri formati. R
ha una grande capacità di leggere (cioé di “importare”) tanti formati
dati.

# I vettori

I vettori sono **insiemi ordinati** di valori della stessa classe.

I vettori sono caratterizzati da essere chiamati da comando un po’
insolito, la lettera “c”, che abbrevia il verbo “concatenate”. Il
comando `c()` interpeta da sé la classe del vettore. In alternativa, si
possono usare comandi che esplicitano la classe del vettore, che di
solito iniziano con `as.`

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
# Domandina è un vettore di risultati di interrogazioni binarie...

c(2+2==4,3>5, 3<4) -> Domandina

Domandina
```

    ## [1]  TRUE FALSE  TRUE

``` r
# Quando il comando as.integer() viene usato per forzare dei numeri su valori logico-binari, la Verità assume valore numerico 1, e la Falsità assume valore numerico 0.

as.integer(Domandina)
```

    ## [1] 1 0 1

``` r
# DOMANDA PER IL PUBBLICO, CHE CLASSE HA IL PROSSIMO VETTORE?
c(1,"mamma","zio")
```

    ## [1] "1"     "mamma" "zio"

## Ordinamento dei vettori

I vettori sono **ordinati**. Ogni valore contenuto in un vettore ha una
posizione e si chiama “elemento”. Per richiamare un elemento in una data
posizione si invoca il vettore seguito dal numero della posizione tra
parentesi quadra:

``` r
amici[2]
```

    ## [1] "Claudio"

``` r
# I due punti indicano progressione senza buchi "da... a..."
amici[2:3]
```

    ## [1] "Claudio" "Maria"

``` r
# Notate la differenza col prossimo comando
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

superamici
```

    ## [1] "Pippo" "Maria"

``` r
superamici[2]
```

    ## [1] "Maria"

Siccome un vettore ha un certo numero di elementi, può essere utile
voler contare quanti elementi ci sono in un vettore. Questo si può fare
col comand0 `length()`

``` r
amici %>% length()
```

    ## [1] 3

``` r
length(amici)
```

    ## [1] 3

# Liste, data.frame e tibbles (Tabelle)

Due o più vettori si possono combinare in due strutture contenitori:

-   Le liste: sono un contenitore piuttosto flessibile e con pochissimi
    requisiti. Sono maggiormente usate negli aspetti più informatici per
    operazioni di organizzazione interna dei dati. Non saranno
    approfondite in questo corso.
-   Le tabelle: R possiede una struttura base per le tabelle, il
    `data.frame`. Noi però useremo una struttura più raffinata, la
    `tibble`, che fa parte del dialetto “Tidyverse”.

La costruzione di tabelle deve rispettare:

-   Regole di codice informatico, senza le quali R non è capace di
    organizzare la tabella, e restituirà un errore.
-   Regole di standard d’uso, che sono rispettate per rendere il lavoro
    più fluido ed interpretabile LATO UMANO.

## REGOLE MECCANICHE PER OPERARE CON LE TABELLE

Una tabella incrocia un numero positivo di colonne (variabili) con un
certo numero non negativo di righe (osservazioni). In R, l’elemento
fondamentale della tabella è **LA COLONNA, NON LA RIGA**.

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

### Il concetto di nullità

Che succede se nel formare una tabella mi manca una informazione e
quindi sospetto che i miei vettori non saranno della stessa lunghezza?
In questo caso si usa il simbolo `NA`, che significa “missing value”,
ovverosia “informaizone mancante”.

|                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Il concetto di nullità infomatica è ben più raffinato, infatti si usa distinguire tra:                                                                                                                                                                                                                                                           |
| Nullità di valore numerico, cioé `0`.                                                                                                                                                                                                                                                                                                            |
| Nullità di informazione, cioé sapere di non sapere `NA`.                                                                                                                                                                                                                                                                                         |
| Nullità di possbilità, cioé sapere che non può esistere `NaN`.                                                                                                                                                                                                                                                                                   |
| Nullificazione di valore, cioé cancellazione dell’informazione errata LATO UMANO `NULL`.                                                                                                                                                                                                                                                         |
| Il Prof. Giuffrida insegna che gran parte dei casini informatici avvengono perché gli impiegati non capiscono la differenza tra i diversi livelli di nullificazione. Spero che un laureato UniCT capisca bene l’importanza di capire la differenza tra diversi gradi di nullità prima di laurearsi, così da non rendersi responsabile di casini. |
| Faremo degli esempi più avanti quando tratteremo delle funzioni statistiche.                                                                                                                                                                                                                                                                     |
| Ricordate, lato macchina non esiste informazione errata, esistono solo comandi impossibili da eseguire. Questo è uno dei problemi informatici della disinformazione, il fatto che le macchine valutano solo la coerenza col loro funzionamento interno e non con la realtà esterna.                                                              |

### I comandi per formare una tabella tibble

Le `tibble` si costruiscono per colonne, separate da virgole.

``` r
#La costruzione di ogni colonna è simile alla costruzione di un vettore, ma qui si usa "=" e non "<-". "<-" lo usiamo per assegnare la struttura della tabella all'oggetto Tabella1.

Tabella1 <- tibble(
  Numeri = c(1,2,3),
  Cognomi = c("Rossi","Verdi","Tomaselli")
)
```

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
mentre i `data.frame` sì. Per quanto suoni strano, noi *vogliamo*
strutture più rigorose!

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
# set.seed serve a rendere i valori casuali ma riproducibili...
# vedrete come nella nota sotto
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

NOTA IMPORTANTISSIMA:

Data la struttura della tabella di cui sopra, si sta implicando che c’è
un processo di *appaiamento* tra osservazioni. Presentare i dati in
questo modo sta implicando che noi non sappiamo perché, ma è importante
che il primo lancio del dado 1 sia paragonato proprio al primo lancio
del dado 2. Vedremo adesso una struttura simile che fa capire il
concetto di appaiamento dei dati.

``` r
tibble(
  Nome_paziente = rep("Anonimo",6),
  Kg_prima_dieta = c(102,88,93,90,92,104),
  Kg_dopo_dieta = c(86,77,89,87,94,98))
```

    ## # A tibble: 6 x 3
    ##   Nome_paziente Kg_prima_dieta Kg_dopo_dieta
    ##   <chr>                  <dbl>         <dbl>
    ## 1 Anonimo                  102            86
    ## 2 Anonimo                   88            77
    ## 3 Anonimo                   93            89
    ## 4 Anonimo                   90            87
    ## 5 Anonimo                   92            94
    ## 6 Anonimo                  104            98

# Tabelle problematiche

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
data.frame(Nome = c("Giorgio", "Michela", "Laura", "Arancione","Kadim"),
           "Stato_Civile" = c("Sposato con Michela", "Vedi sopra", "Nubile", "Sposato",NA),
           Età = c(34,28,"venti",20,32/33)
)
```

    ##        Nome        Stato_Civile              Età
    ## 1   Giorgio Sposato con Michela               34
    ## 2   Michela          Vedi sopra               28
    ## 3     Laura              Nubile            venti
    ## 4 Arancione             Sposato               20
    ## 5     Kadim                <NA> 0.96969696969697

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

Laureati <- read_excel("base_dati_CICCHITELLI_excel/Laureati.xls")

Laureati <- read_excel("base_dati_CICCHITELLI_excel/Laureati.xls", 
    col_types = c("numeric", "text", "date", 
        "text", "numeric", "numeric", "date", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric", "numeric", "numeric", 
        "numeric"))
```

Per salvare una tabella come file Excel il comando è:

``` r
writexl::write_xlsx(nome_della_tabella,"LaMiaTabella.xlsx")
```

|                                                                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| COMANDO IMPORTANTISSIMO Per Visualizzare una tabella (o qualunque altro tipo di struttura) si usa il comando `View()`. La V deve essere maiuscola. Le `tibble` sono piuttosto agevoli da visualizzare, mentre le liste lo sono di meno… |
| Quando si da un `print` (implicito o esplicito) di una tibble, di solito si visualizzano le prime diece osservazioni e le prime colonne.                                                                                                |

### Chiamare elementi delle tabelle

Per chiamare una variable incolonnata, si chiama il numero della colonna
con `tabella[numero_colonna]` oppure si chiama il nome della colonna con
`tabella$nome_colonna`.

``` r
tibble(Nomi = c("Pippo","Paperino"),
       Età = c(30,32)
       ) -> Tabella1

Tabella1$Nomi
```

    ## [1] "Pippo"    "Paperino"

``` r
Tabella1[2]
```

    ## # A tibble: 2 x 1
    ##     Età
    ##   <dbl>
    ## 1    30
    ## 2    32

``` r
#Per chiamare una riga si mette una virgola dopo il numero tra parentesi quadre.

Tabella1[2,]
```

    ## # A tibble: 1 x 2
    ##   Nomi       Età
    ##   <chr>    <dbl>
    ## 1 Paperino    32

**Di solito però le righe sono filtrate con strumenti diversi del
dialetto Tidyverse. In generale in dialetto Tidyverse tutto diventa più
facile da ricordare.**

# Importare database dal web (Anticipazione della Lezione 6)

Tra le funzioni più entuasiamanti di R c’è la possibilità di condividere
database (cioé: insiemi di tabelle) senza mai veramente uscire da R
Studio. Di fatto, tutta la gestione della trasmissione dati viene
gestita da R Studio.

Come esempio, studieremo il pacchetto `owidR`. Che è una API, cioé un
software di interfaccia guidata, con il sito [Our World in
Data](https://ourworldindata.org/).

``` r
pacman::p_load(owidR)

owidR::owid_covid() -> Covid
```

``` r
pacman::p_load(owidR)
owid_search("education") %>% View()
```

``` r
owid("pupil-teacher-ratio-for-primary-education-by-country") -> Education

Education %>% View()
```

``` r
Education %>% filter(entity == "Italy") %>% View()
```

Consiglio personale per la vostra tesi di laurea: scegliete una parola
chiave e guardate come questa si sviluppa nei database di OWID. A quel
punto non fidatevi ciecamente dei database di OWID, ma cercate di capire
quali sono le variabili che ricorrono come legate a quella parola
chiave. Questo funge da una sorta di “studio di letteratura” che vi
permette di capire, storicamente, con che tipo di studi è stata
approcciato il tema che vi interessa.

``` r
owid_search("leisure") %>% View()
```
