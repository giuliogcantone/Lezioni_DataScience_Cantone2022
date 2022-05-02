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

# Studio sulle “Tabelle ben formate”

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

Questo è un esempio stupidotto di come un errore di comunicazione di
dati parimenti assolutamente validi vi può fare apparire come dei
*dilettanti*.

------------------------------------------------------------------------

### Principio assoluto della Data Science:

In ogni Tabella “ben formata”:

-   Ogni colonna deve rappresentare una variabile differente.
-   Ogni riga deve rappresentare una osservazione differente.
-   Ogni incrocio di colonna e riga deve assumere un valore *valido* nel
    supporto della variabile incolonnata, oppure un *valore mancante* o
    *missing value* (`NA`). Se invece il valore **non può esistere**, si
    usa `NaN`.

Il supporto è l’insieme dei valori possibili per quella dimensione.
Questo insieme può essere finito o anche infinito e limitato, ma non è
mai illimitato.

Cosa distingue l’infinito dall’illimitato?

-   Con un pianoforte posso suonare infiniti brani, con un numero
    limitato di tasti. (*c**i**t*. Alessandro Baricco)

Esempio di operazione non valida perché travalica i limiti di una
tabella “ben formata”:

``` r
set.seed(1810)
data.frame(Nome = c("Giorgio", "Michela", "Laura"),
           "Stato Civile" = c("Sposato con Michela", NA, "Nubile"),
           Età = c(34,28,"venti")
)
```

    ##      Nome        Stato.Civile   Età
    ## 1 Giorgio Sposato con Michela    34
    ## 2 Michela                <NA>    28
    ## 3   Laura              Nubile venti
