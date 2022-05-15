Comandi di calcolo algebrico, logico-testuale e statistico
================

# Ora definiamo “comando”, e poi definiamo la “pipeline” di Tydiverse

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

NOTA l’uso di `=` per gli ARGOMENTI, NON PER LE ASSEGNAZIONI.

# Operatore PIPE, o INCANALATORE o INTUBATORE

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

-   SOMMA CUMULATIVA

``` r
cumsum(1:10)
```

    ##  [1]  1  3  6 10 15 21 28 36 45 55

``` r
# Nota la definizione come vettore... ma perché qui è richiesto l'ordine???
cumsum(c(1,5,15,66))
```

    ## [1]  1  6 21 87

``` r
# Utile per calcolare le funzioni cumulative in statistica descrittiva
```

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
# Divisioni possibili ed impossibili

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
# potenze
2^8
```

    ## [1] 256

``` r
# Cosa è questo?
2^-1
```

    ## [1] 0.5

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
qualsiasi cosa. A volte l’interpretazione non è affatto immediata:

``` r
!3 > 5
```

    ## [1] TRUE

``` r
(!3 > 5) == !(3>5)
```

    ## [1] TRUE

``` r
(!4 > 5) == !(3>5)
```

    ## [1] TRUE

``` r
# Trovo che qui la logica sia un po' contorta...
```

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

### SOMMA E QUANDIFICATORE = QUANTIFICATORE

Una operazione utile è di applicare la sommatoria al quandificatore,
così da ottenere un “quantificatore”. Quante volte succede questo?

``` r
(c("mamma","papà") %in% c("mamma","papà","figlio")) %>% sum()
```

    ## [1] 2

``` r
# è anche possibile calcolare una frequenza sul numero possibile di volte

c("mamma","papà","figlio") -> famiglia

(c("mamma","papà") %in% famiglia) %>% sum() /
  length(famiglia)
```

    ## [1] 0.6666667

## Condizioni

Una interrogazione può essere valutata come condizione di attivazione di
un risultato condizionato del tipo

**SE** *questa cosa è VERA* **ALLORA** *dammi questo risultato*

``` r
ifelse(1:3 >= 3,"mamma","papà")
```

    ## [1] "papà"  "papà"  "mamma"

|                                                                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ifelse` non è l’unica condizione applicabile. Spesso ricorre il comando `case_when` che significa “nel caso in cui”, che si usa comunemente per condizionare risultati a variabili ordinali (factor). |
| Non sarà trattato in queste lezioni.                                                                                                                                                                   |

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

### Trovare la posizione

``` r
# posizione della sottostringa
str_locate_all("La Mamma è andata al mercato","è")
```

    ## [[1]]
    ##      start end
    ## [1,]    10  10

``` r
# Quando la stringa "pattern" è contenuta nella stringa argomento
str_which(c("La Mamma è andata al mercato",
            "Il Papà è andato al mercato",
            "Mia sorella è andata al mercato"),
          "andata")
```

    ## [1] 1 3

Comando `word()`

``` r
word("La mamma è andata al mercato",4)
```

    ## [1] "andata"

``` r
word("La mamma è andata al mercato",c(1,4))
```

    ## [1] "La"     "andata"

``` r
word("La mamma è andata al mercato",c(1,2,5,6)) %>%
  str_flatten(collapse = " ")
```

    ## [1] "La mamma al mercato"

### Espressioni regolari…

<https://github.com/rstudio/cheatsheets/blob/main/strings.pdf>

# Comandi statistici

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

-   Quantili

``` r
#rnorm genera una quantitò pari al primo argomento di
# numeri casuali da una distribuzione normale di
# media pari al secondo argomento, con deviazione standard
# pari al terzo argomento

quantile(rnorm(1000,10,10),c(.25,.5,.6,.9))
```

    ##       25%       50%       60%       90% 
    ##  2.903127  9.963340 12.450681 22.962643

## Il problema dei missing values nei comandi statistici.

Il comandi statistici hanno un risultato non funzionano correttamente se
rilevano dei missing values nei vettori argomento. Di solito questo di
risolve con un secondo argomento che specifica di omettere i missing
values.

``` r
mean(c(1,2,NA,10,12), na.rm = F)
```

    ## [1] NA

``` r
mean(c(1,2,NA,10,12), na.rm = T)
```

    ## [1] 6.25

``` r
var(c(1,2,NA,10,12))
```

    ## [1] NA

``` r
var(c(1,2,NA,10,12, na.rm = T))
```

    ## [1] NA

# Correlazione e regressione

-   Correlazione

``` r
Dati <- readxl::read_excel( "base_dati_CICCHITELLI_excel/Statura e pulsazioni.xls")


# Correlazioni lineari
cor(Dati$Statura,Dati$Pulsazioni)
```

    ## [1] 0.2182248

``` r
cor(Dati$Pulsazioni,Dati$Statura)
```

    ## [1] 0.2182248

``` r
# Valori NA nelle correlazioni

cor(c(1,5,6,8,NA,10),
    c(103,67,NA,208,110,2204))
```

    ## [1] NA

``` r
cor(c(1,5,6,8,NA,10),
    c(103,67,NA,208,110,2204),
    use = "complete.obs")
```

    ## [1] 0.7075261

``` r
### Correlazioni di Rango (non lineari)

cor(c(1,5,6,8,NA,10),
    c(103,67,NA,208,110,2204),
    use = "complete.obs",
    method = "kendall")
```

    ## [1] 0.6666667

-   Regressione

Tidyverse aiuta moltissimo l’interpretazione e la visualizzazione delle
tabelle di regressione, in particolare per le regressioni multiple. In
questi casi ci faremo coadiuvare da un pacchetto periferico ma molto
simpatico, “broom”.

``` r
pacman::p_load(broom)
Dati <- readxl::read_excel( "base_dati_CICCHITELLI_excel/Soddisfazione del paziente.xls")

Dati %>%
  lm(data = .,
     Soddisfazione ~ Età + `Indice di gravità malattia` + `Indice di ansietà`) %>% tidy()
```

    ## # A tibble: 4 x 5
    ##   term                         estimate std.error statistic  p.value
    ##   <chr>                           <dbl>     <dbl>     <dbl>    <dbl>
    ## 1 (Intercept)                   158.       18.1       8.74  5.26e-11
    ## 2 Età                            -1.14      0.215    -5.31  3.81e- 6
    ## 3 `Indice di gravità malattia`   -0.442     0.492    -0.898 3.74e- 1
    ## 4 `Indice di ansietà`           -13.5       7.10     -1.90  6.47e- 2

``` r
Dati %>%
  lm(data = .,
     Soddisfazione ~ Età + `Indice di gravità malattia` + `Indice di ansietà`) %>%
  tidy() %>%
  mutate_if(is.numeric,round,3)
```

    ## # A tibble: 4 x 5
    ##   term                         estimate std.error statistic p.value
    ##   <chr>                           <dbl>     <dbl>     <dbl>   <dbl>
    ## 1 (Intercept)                   158.       18.1       8.74    0    
    ## 2 Età                            -1.14      0.215    -5.32    0    
    ## 3 `Indice di gravità malattia`   -0.442     0.492    -0.898   0.374
    ## 4 `Indice di ansietà`           -13.5       7.1      -1.90    0.065

``` r
Dati %>%
  lm(data = .,
     scale(Soddisfazione) ~
       scale(Età) +
       scale(`Indice di gravità malattia`) +
       scale(`Indice di ansietà`)
     ) %>%
  tidy() %>%
  mutate_if(is.numeric,round,3) %>%
  select(-statistic)
```

    ## # A tibble: 4 x 4
    ##   term                                estimate std.error p.value
    ##   <chr>                                  <dbl>     <dbl>   <dbl>
    ## 1 (Intercept)                            0         0.086   1    
    ## 2 scale(Età)                            -0.591     0.111   0    
    ## 3 scale(`Indice di gravità malattia`)   -0.111     0.123   0.374
    ## 4 scale(`Indice di ansietà`)            -0.234     0.123   0.065
