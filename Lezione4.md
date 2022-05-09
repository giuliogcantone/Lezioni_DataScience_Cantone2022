Visualizzazione Grafica
================

# Introduzione al concetto di “plot”.

Un grafico costruito partendo da dati viene comunemente chiamato plot.

Gli stessi dati possono essere rappresentati con tipologie diverse di
plot.

Quando si decide di presentare dati con un grafico, servono due
competenze:

-   Competenze tecniche per realizzare il plot in tutti i suoi dettagli
-   Competenze di comunicaziome per scegliere il plot giusto, i colori
    giusti etc.

### Quickplot

Quando Tidyverse è caricato, vale sempre la pena consultare la funzione
`qplot`. Questa funzione interpreta i dati immessi come argomento e
rappresenta un plot che secondo R è quello più appropriato, secondo un
layout grafico standard. Di solito, R non è capace di capire
correttamente come vorremmo rappresentare i dati, però il quick plot ci
dà la sua prospettiva sulla natura dei dati a disposizione.

``` r
rnorm(1000,25,5) %>% qplot()
```

![](Lezione4_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

|                                                                                   |
|-----------------------------------------------------------------------------------|
| **SE USATE WINDOWS, SCARICATE IL PACCHETTO “CAIRO”**                              |
| A lezione vi spiegherò come settarlo per migliorare molto la qualità dei grafici. |

# La Grammatica della Grafica

Il comando cardine per plottare su Tidyverse è `ggplot`. `ggplot` usa
una sintassi abbastanza diverso da tutti gli altri comandi di R e
Tidyverse, ed è facile confondersi. La sintassi `ggplot` è ispirata ai
programmi di grafica vettoriale (grafica commerciale) e costruiscono il
grafico “layer per layer”.

Combinata con la pipeline, la forma tipica di un codice per plottare dei
dati è:

``` r
Tabella %>% ggplot()+
  tipo_di_grafico(aes(asse_x = ...,
                      asse_y = ...,
                      fill/colore = ...,),
                  tratteggio = ...,
                  colore_della_linea = "colore",
                  altro = ...
  ) +
  ylab("Nome asse y")+
  xlab("Nome asse x")+
  theme(base_size = "...")+
  theme_test() +
  altro()
```

In verità diversi dettagli possono essere ordinati a `ggplot` in diversi
momenti della pipeline. La parola chiave, su cui è facile confondersi, è
`aes`. `aes` indica a `ggplot` da dove deve andare a prendere i valori
da rappresentare. Questi valori `aes` possono essere forniti anche come
argomento di ggplot(), anche se i risultati non sono del tutto
equivalenti sul piano tecnico, perchè…

-   se inserisco `aes` dentro `ggplot(aes(x=...,y=...))`, sto ordinando
    al programma di partire da uno “sfondo” che già contiene degli assi
    indicizzati (da dove a dove partono e finiscono gli assi) ai valori
    che sto indicando.
-   se inserisco `aes` dentro il tipo di grafico, è molto probabile che
    dovrò aggiungere una indicazione specifica per gli assi; però i
    valori non stanno indicizzando il layer sfondo, ma un layer
    ulteriore, che è il layer della figura geometrica. Questo mi
    consente di caricare più figure geometriche, per esempio più curve
    su diversi layers, sullo stesso sfondo. Io preferisco inserire i
    valori aes

Siccome la pipeline inizia con `Tabella` (Che può essere qualunque
termine a cui è assegnata una `tibble`), Tidyverse istruirà `ggplot` a
cercare, come termini che costituiranno `x` e `y` (cioé: gli assi), tra
le variabili della `Tabella`.

# Grafici tipici

I grafici a barre ed i grafici di curve di densità, generalmente non
hanno bisogno di un valore per l’asse y (alternativamente, per l’asse x)
perché ci sono delle funzioni interne a `ggplot` che permettono di
“contare” le frequenze con cui ricorrono i valori.

### Grafico a barre

-   Per valori discreti

``` r
Test <- readxl::read_excel("base_dati_CICCHITELLI_excel/Test d'ingresso.xls")

Test %>%
  mutate(`Test d'ingresso` = `Test d'ingresso` %>% as.integer) %>%
  filter(`Test d'ingresso` != 0) %>%
  ggplot() +
    geom_histogram(
      aes(x=`Test d'ingresso`),
      fill="#69b3a2",
      color="#e9ecef",
      alpha=0.9,
      stat = "count"
      ) +
    ggtitle("TITOLO") +
    theme_grey(base_size = 20)
```

![](Lezione4_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

-   Per valori continui

``` r
Tabella <- tibble(Altezze = rnorm(120,179,12))

Tabella %>%
  ggplot() +
    geom_histogram(
      aes(x=Altezze),
      bins = 10
      )
```

![](Lezione4_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Curva di densità

``` r
Tabella %>%
  ggplot() +
    geom_density(
      aes(x=Altezze),
      color = "green",
      size = 3
      ) +
  theme_classic(base_size = 15)
```

![](Lezione4_files/figure-gfm/unnamed-chunk-5-1.png)<!-- --> \#\#\#
Scatterplot bi-dimensionale

``` r
Dati <- readxl::read_excel("base_dati_CICCHITELLI_excel/Dati antropometrici.xls")

Dati %>%
  ggplot(aes(`Peso(kg)`,
               `Altezza (cm)`)) +
  geom_point() -> p1

p1
```

![](Lezione4_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
# notate la posizione di aes in questo caso

# metodo non parametrico
p1 + geom_smooth()
```

![](Lezione4_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
# modello lineare
p1 + geom_smooth(method = lm)
```

![](Lezione4_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

### Densità bi-dimensionale

Mentre `ggplot` provvede già dei buoni strumenti per grafici avanzati,
ci sono dei pacchetti specifici che aiutano la costruzione di plot
speciali seguendo la sintassi di `ggplot`.

La densità bi-dimensionale è un concetto molto più semplice di quanto
pensiate, e graficamente utile per comunicare distribuzioni continue
bi-variate.

``` r
pacman::p_load(ggdensity)

Dati %>%
  ggplot(aes(`Peso(kg)`,
               `Altezza (cm)`)) +
  geom_hdr() -> p2
p2
```

![](Lezione4_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
p2 + geom_smooth()
```

![](Lezione4_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
# commentate questo ultimo grafico
```

## BOXPLOTS E VIOLIN PLOTS

Questi grafici servono a visualizzare l’estensione e la densità tra
gruppi (discreti) e variabili continue:

-   Boxplot

``` r
mpg %>%
  mutate(class = fct_reorder(class, hwy, .fun='median')) %>%
  ggplot( aes(x=reorder(class, hwy), y=hwy, fill=class)) +
  geom_boxplot() +
  xlab("Tipo di autovettura") +
  ylab("Miglia per gallone") +
  theme_test(base_size = 16) +
    theme(legend.position="none")
```

![](Lezione4_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

-   Violin plot

-   Boxplot

``` r
mpg %>%
  mutate(class = fct_reorder(class, hwy, .fun='median')) %>%
  ggplot(aes(x=reorder(class, hwy), y=hwy, fill=class)) +
  geom_violin() +
  xlab("Tipo di autovettura") +
  ylab("Miglia per gallone") +
  theme_test(base_size = 12) +
    theme(legend.position="none")
```

![](Lezione4_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

| **Quando usare i boxplot, quando usare i violins?**                           |
|-------------------------------------------------------------------------------|
| Risposta breve: boxplot per articoli scientifici, violins in ogni altro caso. |