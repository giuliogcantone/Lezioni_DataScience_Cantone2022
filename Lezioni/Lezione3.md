Maneggiare il formato tabellare
================

# Il formato tibble si può maneggiare con poche funzioni fondamentali

-   `filter`: Restringe la tabella a solo certe righe che rispettano una
    condizione
-   `select`: Seleziona solo certe colonne
-   `pull`: Estrae i soli dati di una colonna, lasciando perdere i
    metadati (ad esempio, il nome della variabile incolonnata).
-   `mutate`: aggiunge o sostituisce una colonna, in funzione di una o
    più colonne pre-esistenti (una versione alternativa è `transmute`)
-   `group_by` e `summarise`: applica una funzione sommario a tutta la
    tabella oppure, in combinazione con `group_by`, fornisce l’indice
    sommario per dei gruppi individuati.
-   I ‘joins’ servono a prendere una o più colonne da una tabella ed
    innestarle in un altra secondo un criterio di corrispondenza
    rispetto a una o più colonne i comune tra le due tabelle.
-   Gli `anti_join` servono a filtrare via valori da una tabella in
    corrispondenza di valori di una o più colonne in comune tra le due
    tabelle. L’anti-join è una sorta di filtro avanzato tra tabelle, in
    cui una tabella ne nega una seconda.
-   `pivot_longer` e `pivot_wider` servono a ristrutturare tabelle
    trasformando colonne in valori e vice-versa. (Operazione considerata
    piuttosto tortuosa)

## Filtrare e selezionare i dati

``` r
Dati <- readxl::read_excel( "base_dati_CICCHITELLI_excel/Soddisfazione del paziente.xls")

Dati %>% filter(Età < 30) -> Giovani
Giovani
```

    ## # A tibble: 10 x 4
    ##    Soddisfazione   Età `Indice di gravità malattia` `Indice di ansietà`
    ##            <dbl> <dbl>                        <dbl>               <dbl>
    ##  1            89    28                           43                 1.8
    ##  2            77    29                           50                 2.1
    ##  3            89    29                           48                 2.4
    ##  4            88    29                           46                 1.9
    ##  5            77    29                           52                 2.3
    ##  6            86    23                           41                 1.8
    ##  7            63    25                           49                 2  
    ##  8            82    29                           48                 2.5
    ##  9            83    22                           51                 2  
    ## 10            92    28                           46                 1.8

``` r
Giovani %>% select(Soddisfazione, `Indice di ansietà`)
```

    ## # A tibble: 10 x 2
    ##    Soddisfazione `Indice di ansietà`
    ##            <dbl>               <dbl>
    ##  1            89                 1.8
    ##  2            77                 2.1
    ##  3            89                 2.4
    ##  4            88                 1.9
    ##  5            77                 2.3
    ##  6            86                 1.8
    ##  7            63                 2  
    ##  8            82                 2.5
    ##  9            83                 2  
    ## 10            92                 1.8

``` r
Giovani %>% pull(Soddisfazione)
```

    ##  [1] 89 77 89 88 77 86 63 82 83 92

## Mutate

Mutate è forse il comando più ricco e potente, vediamolo subito in
azione.

``` r
tibble(Valore_1 = c(10,12,14),
       Valore_2 = c(3,5,0)) %>%
  mutate(Somma = Valore_1 + Valore_2,
         Differenza = Valore_1 - Valore_2)
```

    ## # A tibble: 3 x 4
    ##   Valore_1 Valore_2 Somma Differenza
    ##      <dbl>    <dbl> <dbl>      <dbl>
    ## 1       10        3    13          7
    ## 2       12        5    17          7
    ## 3       14        0    14         14

``` r
# Mutate si può usare sia con argomenti "mobili" come nel caso sopra, sia con argomenti a valore fisso. Questo è utile per calcolare proporzioni.

tibble(Valore = sample.int(20,10)) %>%
  mutate(SOMMA = sum(Valore),
         Percentuale = Valore/SOMMA) %>%
  mutate_if(is.numeric,round,3)
```

    ## # A tibble: 10 x 3
    ##    Valore SOMMA Percentuale
    ##     <dbl> <dbl>       <dbl>
    ##  1      8    88       0.091
    ##  2      9    88       0.102
    ##  3      3    88       0.034
    ##  4     10    88       0.114
    ##  5      4    88       0.045
    ##  6     17    88       0.193
    ##  7     19    88       0.216
    ##  8     15    88       0.17 
    ##  9      1    88       0.011
    ## 10      2    88       0.023

`mutate` è un comando molto flessibile perché *tende* a funzionare sia
con mutazioni fisse, sia con mutazioni dinamiche parallele.

|                                                                                                       |
|-------------------------------------------------------------------------------------------------------|
| mutazione dinamica parallela: riguardate le tabelle sopra.                                            |
| `SOMMA` è una variabile dinamica il cui valore cambia al cambiare di altre due variabili incolonnate. |

## Dai valori continui ai valori discreti ordinati (variabili ordinali)

`mutate` in combinazione con le funzioni `cut_`.

Le funzioni `cut_` restituiscono sempre dei `factor`, cioé variabili
ordinali. Questo è utile per la visualizzazione, per esempio per
ordinare automaticamente le legende dei grafici.

``` r
Test_ingresso <- readxl::read_excel("base_dati_CICCHITELLI_excel/Test d'ingresso.xls")

Test_ingresso %>% mutate(
  Classe_voto_test = `Test d'ingresso` %>% as.numeric %>% cut_interval(3)
)
```

    ## # A tibble: 118 x 3
    ##    `Test d'ingresso` `Valutazione fine primo anno` Classe_voto_test
    ##    <chr>                                     <dbl> <fct>           
    ##  1 21                                         3.90 [15,21.7]       
    ##  2 28                                         3.78 (21.7,28.3]     
    ##  3 22                                         2.54 (21.7,28.3]     
    ##  4 21                                         3.03 [15,21.7]       
    ##  5 31                                         3.86 (28.3,35]       
    ##  6 32                                         2.96 (28.3,35]       
    ##  7 27                                         3.96 (21.7,28.3]     
    ##  8 26                                         3.18 (21.7,28.3]     
    ##  9 24                                         3.31 (21.7,28.3]     
    ## 10 30                                         3.54 (28.3,35]       
    ## # ... with 108 more rows

``` r
Test_ingresso %>% mutate(
  Classe_voto_test = `Test d'ingresso` %>% as.numeric %>% cut_interval(3,labels = c("Basso","Medio","Alto"))
) -> Test_ingresso

Test_ingresso
```

    ## # A tibble: 118 x 3
    ##    `Test d'ingresso` `Valutazione fine primo anno` Classe_voto_test
    ##    <chr>                                     <dbl> <fct>           
    ##  1 21                                         3.90 Basso           
    ##  2 28                                         3.78 Medio           
    ##  3 22                                         2.54 Medio           
    ##  4 21                                         3.03 Basso           
    ##  5 31                                         3.86 Alto            
    ##  6 32                                         2.96 Alto            
    ##  7 27                                         3.96 Medio           
    ##  8 26                                         3.18 Medio           
    ##  9 24                                         3.31 Medio           
    ## 10 30                                         3.54 Alto            
    ## # ... with 108 more rows

## Statistiche sommario e gruppi

``` r
Test_ingresso %>% group_by(`Test d'ingresso`) %>%
  summarise(Media_voto_finale = mean(`Valutazione fine primo anno`),
            n = n())
```

    ## # A tibble: 23 x 3
    ##    `Test d'ingresso` Media_voto_finale     n
    ##    <chr>                         <dbl> <int>
    ##  1 15                             2        1
    ##  2 16                             2.53     3
    ##  3 18                             2.53     7
    ##  4 19                             3.17     3
    ##  5 20                             2.74     9
    ##  6 21                             3.04     7
    ##  7 22                             2.85     4
    ##  8 23                             3.21     5
    ##  9 24                             3.09    12
    ## 10 25                             3.08    10
    ## # ... with 13 more rows

``` r
# n() è una funzione speciale che funziona solo dentro summarize.
# Conta il numero di osservazioni, come nrow()

Test_ingresso %>% group_by(Classe_voto_test) %>%
  summarise(Media_voto_finale = mean(`Valutazione fine primo anno`),
            n = n())
```

    ## # A tibble: 4 x 3
    ##   Classe_voto_test Media_voto_finale     n
    ##   <fct>                        <dbl> <int>
    ## 1 Basso                         2.76    30
    ## 2 Medio                         3.16    61
    ## 3 Alto                          3.38    23
    ## 4 <NA>                         NA        4

**Domanda**: La tabella sommario rispetta il dogma tidyverse? Sì? No?
Perché?

### Un trucco per fare “mutate condizionali” su statistiche di gruppo

Usare `group_by` insieme a `mutate`…

``` r
Test_ingresso %>%
  group_by(Classe_voto_test) %>%
  mutate(Deviazione =
           `Valutazione fine primo anno` -
           mean(`Valutazione fine primo anno`)
  ) %>% select(Classe_voto_test, Deviazione) %>%
  arrange(Classe_voto_test) %>% View()
```

Questo codice si può capire meglio riprodotto con dati reali

``` r
tibble(Nome = c(Giulio,...,...),
       Genere = c(M,...),
       Altezza = (180,...)) %>%
  group_by(Genere) %>%
  mutate(Deviazione_ragionata =
           Altezza - mean(Altezza))
```

# Joins

L’idea del Join è in verità più semplice di quanto sembri:

``` r
tibble(Cognome = c("Rossi", "Verdi","Rossi","Esposito"),
       Nome = c("Mario","Giovanni","Carla","Carmela"),
       Età = c(54,22,50,38)) -> Utenti

tibble(Famiglia = c("Rossi","Verdi","Esposito"),
       Civico = c("1","2","3")) -> Case

Utenti
```

    ## # A tibble: 4 x 3
    ##   Cognome  Nome       Età
    ##   <chr>    <chr>    <dbl>
    ## 1 Rossi    Mario       54
    ## 2 Verdi    Giovanni    22
    ## 3 Rossi    Carla       50
    ## 4 Esposito Carmela     38

``` r
Case
```

    ## # A tibble: 3 x 2
    ##   Famiglia Civico
    ##   <chr>    <chr> 
    ## 1 Rossi    1     
    ## 2 Verdi    2     
    ## 3 Esposito 3

``` r
full_join(Utenti,Case %>% rename(Cognome = Famiglia),
          by="Cognome")
```

    ## # A tibble: 4 x 4
    ##   Cognome  Nome       Età Civico
    ##   <chr>    <chr>    <dbl> <chr> 
    ## 1 Rossi    Mario       54 1     
    ## 2 Verdi    Giovanni    22 2     
    ## 3 Rossi    Carla       50 1     
    ## 4 Esposito Carmela     38 3

# Anti-join, un filtro avanzato, utile nelle analisi testuali

Il miglior modo di capire l’anti-join è introdurre un pacchetto avanzato
per l’analisi testuale, `tidytext`. Tidytext prende un testo e lo
trasforma in una `tibble`. Possiamo scaricare testi storici grazie al
pacchetto `gutenbergr`.

``` r
pacman::p_load("tidytext")
pacman::p_load("gutenbergr")

gutenberg_metadata %>%
  group_by(language) %>%
  count()
```

    ## # A tibble: 103 x 2
    ## # Groups:   language [103]
    ##    language     n
    ##    <chr>    <int>
    ##  1 af           4
    ##  2 ale/en       1
    ##  3 ang/de       1
    ##  4 ang/en       3
    ##  5 ar           1
    ##  6 arp          2
    ##  7 bg           6
    ##  8 bgi/es       1
    ##  9 br           1
    ## 10 ca          28
    ## # ... with 93 more rows

``` r
gutenberg_metadata %>%
  filter(language == "it",
         title %>% str_detect("Sicil")
         )
```

    ## # A tibble: 7 x 8
    ##   gutenberg_id title    author gutenberg_autho~ language gutenberg_books~ rights
    ##          <int> <chr>    <chr>             <int> <chr>    <chr>            <chr> 
    ## 1        22506 "Le tre~ Sangi~            25368 it       IT Romanzi       Publi~
    ## 2        29409 "La gue~ Amari~            33895 it       IT Storia        Publi~
    ## 3        30984 "Gli av~ Colaj~            34935 it       IT Scienze poli~ Publi~
    ## 4        42649 "Avveni~ Pitrè~            39005 it       IT Folklore      Publi~
    ## 5        46887 "Storia~ Amari~            33895 it       IT Storia        Publi~
    ## 6        46888 "Storia~ Amari~            33895 it       IT Storia        Publi~
    ## 7        47114 "La gue~ Amari~            33895 it       IT Storia        Publi~
    ## # ... with 1 more variable: has_text <lgl>

``` r
gutenberg_metadata %>%
  filter(language == "it",
         title %>% str_detect("Sicil")
         ) %>%
           View()
```

``` r
gutenberg_download(30984) -> Sicilia

Sicilia[199,]
```

    ## # A tibble: 1 x 2
    ##   gutenberg_id text                                                             
    ##          <int> <chr>                                                            
    ## 1        30984 "sagrific\xee non sono mai troppi. E poi, i balzelli hanno l'ale~

``` r
Sicilia[201,]
```

    ## # A tibble: 1 x 2
    ##   gutenberg_id text                                                             
    ##          <int> <chr>                                                            
    ## 1        30984 "muore, peggio per lui. Ci\xf2 che saranno codeste riforme possi~

``` r
Sicilia %>%
  tidytext::unnest_tokens(word,text) -> Sicilia_t

Sicilia_t
```

    ## # A tibble: 129,331 x 2
    ##    gutenberg_id word       
    ##           <int> <chr>      
    ##  1        30984 d.r        
    ##  2        30984 napoleone  
    ##  3        30984 colajanni  
    ##  4        30984 _deputato  
    ##  5        30984 al         
    ##  6        30984 parlamento_
    ##  7        30984 gli        
    ##  8        30984 avvenimenti
    ##  9        30984 di         
    ## 10        30984 sicilia    
    ## # ... with 129,321 more rows

``` r
Sicilia_t %>%
  group_by(word) %>%
  count() %>% arrange(-n)
```

    ## # A tibble: 18,664 x 2
    ## # Groups:   word [18,664]
    ##    word      n
    ##    <chr> <int>
    ##  1 e      5000
    ##  2 di     4543
    ##  3 che    3500
    ##  4 la     2534
    ##  5 il     2364
    ##  6 in     2030
    ##  7 si     1719
    ##  8 non    1699
    ##  9 a      1565
    ## 10 del    1522
    ## # ... with 18,654 more rows

``` r
Sicilia_t %>%
  anti_join(get_stopwords("it")) %>%
  group_by(word) %>%
  count() %>% arrange(-n)
```

    ## # A tibble: 18,465 x 2
    ## # Groups:   word [18,465]
    ##    word         n
    ##    <chr>    <int>
    ##  1 pi         664
    ##  2 sicilia    437
    ##  3 governo    313
    ##  4 perch      307
    ##  5 stato      303
    ##  6 generale   227
    ##  7 quando     199
    ##  8 de         185
    ##  9 altri      184
    ## 10 quali      180
    ## # ... with 18,455 more rows

# Campionamento sul popolazioni finite (sorteggio da una lista di records)

In alcuni casi vogliamo sorteggiare a caso un certo numero di elementi
da una lista di records.

``` r
# Introduciamo un pacchetto abbastanza scherzoso che genera a caso delle identità fittizie
pacman::p_load(tidyverse)
pacman::p_load(randomNames)

randomNames(100, gender = c(rep(0,44),
                           rep(1,56)),
            return.complete.data = T) %>%
  as_tibble() -> Elenco

Elenco
```

    ## # A tibble: 100 x 4
    ##    gender ethnicity first_name last_name       
    ##     <dbl>     <int> <chr>      <chr>           
    ##  1      0         1 Deven      Oster           
    ##  2      0         4 Fernando   Hernandez Torres
    ##  3      0         4 Isaiah     Lazo            
    ##  4      0         1 Hunter     White           
    ##  5      0         2 Nitesh     Mcnew           
    ##  6      0         6 Thaaqib    el-Kamali       
    ##  7      0         3 Devante    Carter          
    ##  8      0         1 Kyle       Mullins         
    ##  9      0         6 Faatih     el-Salik        
    ## 10      0         6 Aadam      el-Kazi         
    ## # ... with 90 more rows

``` r
Elenco %>% slice_sample(n = 10)
```

    ## # A tibble: 10 x 4
    ##    gender ethnicity first_name last_name       
    ##     <dbl>     <int> <chr>      <chr>           
    ##  1      1         6 Shaahida   el-Emami        
    ##  2      0         6 Aadil      el-Hashmi       
    ##  3      1         3 Lianna     Pona            
    ##  4      1         5 Alexis     Fisk            
    ##  5      1         4 Maria      Mendez          
    ##  6      0         2 Kenneth    Runyan          
    ##  7      1         6 Zuhriyaa   al-Syed         
    ##  8      0         4 Fernando   Hernandez Torres
    ##  9      1         1 Tilane     Kuebler         
    ## 10      1         1 Destiny    Lewis

``` r
Elenco %>% slice_sample(prop = .5)
```

    ## # A tibble: 50 x 4
    ##    gender ethnicity first_name last_name
    ##     <dbl>     <int> <chr>      <chr>    
    ##  1      0         6 Thaaqib    el-Kamali
    ##  2      1         4 Janae      Vigil    
    ##  3      1         4 Brooke     Trejo    
    ##  4      0         6 Nu'maan    el-Rayes 
    ##  5      1         6 Sajiyya    el-Abu   
    ##  6      0         2 Mitchell   Tran     
    ##  7      1         3 Morgan     Brooks   
    ##  8      0         2 James      Baird    
    ##  9      1         6 Shaahida   el-Emami 
    ## 10      0         6 Ismad      al-Moradi
    ## # ... with 40 more rows

``` r
# Adesso vogliamo campionare solo 2 uomini e 8 donne, si chiama sovracampionamento. operazione utile per contrastare l'attrito demoscopico.


Elenco %>% group_by(gender) %>%
  slice_sample(n = c(10))
```

    ## # A tibble: 20 x 4
    ## # Groups:   gender [2]
    ##    gender ethnicity first_name   last_name       
    ##     <dbl>     <int> <chr>        <chr>           
    ##  1      0         6 Ismad        al-Moradi       
    ##  2      0         2 Sebastian    Vierra          
    ##  3      0         5 Kit          Brame           
    ##  4      0         4 Isaiah       Lazo            
    ##  5      0         6 Nu'maan      el-Rayes        
    ##  6      0         4 Fernando     Hernandez Torres
    ##  7      0         4 Jesus        Puga            
    ##  8      0         6 Abdul Hameed al-Jamil        
    ##  9      0         1 Dakota       Lovato          
    ## 10      0         5 Jason        Temmer          
    ## 11      1         4 Janae        Vigil           
    ## 12      1         6 Sajaa        al-Fahmy        
    ## 13      1         1 Jamie        Coakley         
    ## 14      1         5 Alexis       Fisk            
    ## 15      1         3 Thezlanikka  Reed            
    ## 16      1         1 Shelby       Elden           
    ## 17      1         6 Rasheeqa     el-Ramin        
    ## 18      1         6 Husniyya     al-Allam        
    ## 19      1         1 Anay         Jones           
    ## 20      1         4 Jennifer     Paredes-Rubio

``` r
#Questo funziona?
# La soluzione si troverà nella Lezione 5!
```

# Pivoting

Pivot su Tidyverse significa una cosa un po’ diversa da “pivot” su
Excel. In concreto, la tabella pivot di Excel è l’equivalente della
tabella sommario su Tidyverse.

Il pivoting su Tydiverse serve a trasformare una classe di valori in una
tabella.

Il pivoting non è particolarmente essenziale nell’introduzione a R
Tiduyverse, ma rimane una skill importante per un Data Scientist.
Recentemente è uscita una [ottima
guida](https://r4ds.hadley.nz/data-tidy.html) da parte del creatore/capo
designer di Tidyverse.
