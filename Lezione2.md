Comandi di calcolo algebrico, logico-testuale e statistico
================

# Definizione di comando ed “pipes” di Tydiverse

Un comando, detto anche “funzione”, è un predicato che, completato con
degli “argomenti” contenuti tra parentesi, fornisce un risultato.

La sintassi tipica del comando è:

`comando(argomento1,argomento2,etc.)`

Nella sintassi tipica, molti argomenti del comando sono applicati di
default. Se si vogliono cambiare queste opzioni di default, la sintassi
estesa del comando è:

    comando(ruolo_di_argomento = argomento1,
            ruolo_di_argomento = argomento2,
            etc.)

Nel dialetto Tidyverse, si incanalano diversi argomenti per volta con
l’operatore `%>%`, quindi la sintassi diventa:

    soggetto %>% comando(argomento_di_1) %>%
                 comando2(argomento_di_2)

L’operatore pipe (intubatore) porta il soggetto del comando
automaticamente come primo argomento del comando. In certi casi si vuole
usare una pipe per l’argomento n-esimo di un comando. In questi casi
bisogna combinare `%>%` con un puntino `.`.

``` r
"mamma" %>% str_detect("La mamma ha comprato il pane",.)
```

    ## [1] TRUE

``` r
"mamma" %>% str_detect("La mamma ha comprato il pane")
```

    ## [1] FALSE

# Operatori algebrici

-   SOMMA

La abbiamo già incontrata col simbolo `+` tra due numeri. Si può anche
sommare un intero vettore numerico.

``` r
sum(1:10)
```

    ## [1] 55

``` r
sum(1,5,15,66)
```

    ## [1] 87

-   SOTTRAZIONE

Abbastanza scontato:

``` r
10 - 2
```

    ## [1] 8

``` r
5 - 8
```

    ## [1] -3

``` r
-2 - 10
```

    ## [1] -12

-   MOLTIPLICAZIONE, DIVISIONE, POTENZA E RADICE

``` r
2*2
```

    ## [1] 4

``` r
10/5
```

    ## [1] 2

``` r
10/3
```

    ## [1] 3.333333

``` r
0/100
```

    ## [1] 0

``` r
100/0
```

    ## [1] Inf

``` r
0/0
```

    ## [1] NaN

``` r
2^8
```

    ## [1] 256

-   LOGARITMI (molto utili)

``` r
#logaritmo naturale

log(10)
```

    ## [1] 2.302585

``` r
#logaritmo in base 2

log2(100)
```

    ## [1] 6.643856

``` r
#logaritmo in base 10

log10(100)
```

    ## [1] 2

``` r
#logaritmo in base "x"

x <- 5

log(19,x)
```

    ## [1] 1.829483

# Operatori logici di interrogazione

Alcuni li abbiamo già visti:

-   Interrogazione di equazione: i due argomenti dell’operatore sono lo
    stesso valore?

-   Interrogazione di negazione: i due argomenti sono diversi?

-   Interrogazione di comparazione: più grande o più piccolo?

``` r
# Occhio al doppio uguale!
4 == 4
```

    ## [1] TRUE

``` r
2*2 == 4
```

    ## [1] TRUE

``` r
2*5 == 4
```

    ## [1] FALSE

``` r
str_length("mamma") == 5
```

    ## [1] TRUE

``` r
length(0:10) == 10
```

    ## [1] FALSE

``` r
# Negazione

3 != 5
```

    ## [1] TRUE

``` r
# Comparazione

3 > 1:10
```

    ##  [1]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
3 >= 1:10
```

    ##  [1]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
5 < 6
```

    ## [1] TRUE

``` r
5 <= 4:6
```

    ## [1] FALSE  TRUE  TRUE

`!` è un simbolo particolare che si usa per negare praticamente
qualsiasi cosa. A volte l’interpretazione non è immediata:

``` r
!3 > 5
```

    ## [1] TRUE

-   “Quandificatore”

L’operatore quandificatore `%in%` è una estensione dell’interrogazione
di equazione e di negazione. Infatti compara un valore o un vettore
contro un altro vettore e restituisce `TRUE` **quando** l’argomento a
sinistra del quandificatore è contenuto \* almeno una volta\* nel
vettore a destra.

``` r
3 %in% 1:10
```

    ## [1] TRUE

``` r
1:10 %in% 3
```

    ##  [1] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
"mamma" %in% "La mamma è a casa"
```

    ## [1] FALSE

``` r
c("mamma","papà") %in% c("mamma","papà","figlio")
```

    ## [1] TRUE TRUE

|                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------|
| Una operazione utile è di applicare la sommatoria al quandificatore, così da ottenere un “quantificatore”. Quante volte succede questo? |
| `r (c("mamma","papà") %in% c("mamma","papà","figlio")) %>% sum()`                                                                       |
| `## [1] 2`                                                                                                                              |
| \`\`\`r \# è anche possibile calcolare una frequenza sul numero possibile di volte                                                      |
| c(“mamma”,“papà”,“figlio”) -&gt; famiglia                                                                                               |
| (c(“mamma”,“papà”) %in% famiglia) %&gt;% sum() / length(famiglia) \`\`\`                                                                |
| `## [1] 0.6666667`                                                                                                                      |

## Condizioni

Una interrogazione può essere valutata come condizione di attivazione di
un risultato condizionato del tipo

**SE** *questa cosa è VERA* **ALLORA** *dammi questo risultato*

``` r
ifelse(1:3 >= 3,"mamma","papà")
```

    ## [1] "papà"  "papà"  "mamma"

|                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ifelse` non è l’unica condizione applicabile. Spesso ricorre il comando `case_when` che significa “nel caso in cui”, che si usa comunemente per condizionare risultati a variabili ordinali (factor) |

### Lunghezze

``` r
length(0:10)
```

    ## [1] 11

``` r
length(tibble(Nomi = c("Pippo","Paperino")))
```

    ## [1] 1

``` r
# Perché la length della tibble è 1 e non 2?

nrow(tibble(Nomi = c("Pippo","Paperino")))
```

    ## [1] 2

``` r
# Contare numero di simboli alfanumerici in una stringa character
str_length("mamma")
```

    ## [1] 5

``` r
# Contare quante volte un simbolo ricorre in una stringa
str_count("mamma","a")
```

    ## [1] 2

``` r
# Contare il numero di parole
str_count("mamma","\\w+")
```

    ## [1] 1

``` r
str_count("La mamma è andata al mercato","\\w+")
```

    ## [1] 6

``` r
# Occhio all'uso degli apostrofi
str_count("L'aria è pulita, qui","\\w+")
```

    ## [1] 5

# Operazioni testuali

La maggior parte delle operazioni testuali in dialetto Tidyverse
iniziano con `str_`. Ce ne sono molte altre, ma queste sono quelle
essenziali.

-   Concatenare stringhe

``` r
str_c("la mamma","è andata","al mercato")
```

    ## [1] "la mammaè andataal mercato"

``` r
x <- 3
str_c("La mamma ha comprato ",x," mele.")
```

    ## [1] "La mamma ha comprato 3 mele."

-   Pulizia

``` r
"La Mam£ma è£ and£ata al merca£to" %>%
  str_remove_all("£")
```

    ## [1] "La Mamma è andata al mercato"

``` r
"    La mamma è   andata al   mercato...  "
```

    ## [1] "    La mamma è   andata al   mercato...  "

``` r
"    La mamma è   andata al   mercato...  " %>% str_squish()
```

    ## [1] "La mamma è andata al mercato..."

Se vi serve una funzione per interagire con le parole, caricate
tidyverse poi iniziate a scrivere `str_` e vedete se trovate quello che
cercate. Vi consiglio di googlare in inglese quello che vi serve,
inserendo la parola “stringr” nella query di ricerca.

# Comandi statistici

I COMANDI SI ESEGUONO SEMPRE SU VETTORI NUMERICI. L’argomento deve
sempre essere correttamente formattato come vettore numerico!

-   Media e mediana

``` r
1:10 %>% mean()
```

    ## [1] 5.5

``` r
c(1,2,3) %>% mean()
```

    ## [1] 2

``` r
c(1,1,2,3,6,8,10) %>% median()
```

    ## [1] 3

``` r
1,2,3 %>% mean()
```

-   Varianza e deviazione standard

``` r
1:100 %>% var()
```

    ## [1] 841.6667

``` r
1:100 %>% sd()
```

    ## [1] 29.01149

``` r
1:100 %>% sd() == (1:100 %>% var()) %>% sqrt()
```

    ## [1] TRUE
