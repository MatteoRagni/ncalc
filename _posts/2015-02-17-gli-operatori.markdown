---
layout: post
title:  "Le funzioni e gli operatori"
date:   2015-02-16 16:00:00
categories: post
permalink: /lecture4/
lecture: "Lezione 4"
visible: 1
excerpt: "<p>Impariamo a definire ed utilizzare le funzioni (o metodi) e introduciamo gli operatori di Ruby. Scopriamo <code class='highlighter-ruby'>if</code> e scriviamo la nostra prima funzione numerica, sfruttando tutte le conoscenze acquisite fino ad ora.</p>"
---

Impariamo a definire ed utilizzare le funzioni (o metodi) e introduciamo gli operatori di Ruby. Scopriamo `if` e scriviamo la nostra prima funzione numerica, sfruttando tutte le conoscenze acquisite fino ad ora.

* table of contents.
{:toc}

## Funzioni

Una funzione, e' un particolare costrutto sintattico che permette di raggruppare diverse righe di codice in una struttura unica che possa essere _richiamata_ piu' volte attraverso il codice. Le funzioni permettono di racchiudere codice che esegue uno specifico algoritmo/sequenza di istruzioni in un punto solo, a vantaggio sia **del tempo di sviluppo di un progetto**, che della **manutenibilita'** del codice.

Ruby e' un linguaggio fortemente **orientato agli oggetti**, quindi solitamente le funzioni sono chiamate **metodi**.

### Definire una funzione
La sintassi per definre una funzione e' la seguente

```ruby
#!/usr/bin/env ruby

# Funzione puts_asterisk
# input:
#   n - intero con numero di punti da scrivere
# returns:
#   ret_string - una stringa
# La funzione stampa una linea di asterischi lunga n elementi
def puts_asterisk(n)
  ret_string = "*" * n
  puts ret_string
  return ret_string
end

# La prossima linea invoca la funzione per 10 asterischi
result = puts_asterisk 10

puts result
```

La definizione di una funzione e' caratterizzata dai seguenti elementi:

 * `def`: questa keyword indica all'interprete che sta iniziando la dichiarazione di una funzione
 * `puts_asterik`: subito dopo `def` e' necessario inserire un **nome** per la funzione che la identifica in modo univoco. Specificare lo stesso nome per due funzioni porta alla sovrascrittura della funzione interpretata prima con quella interpretata successivamente. Come le variabili, anche le funzioni devono sottostare a delle **regole di visibilita'**.
 * `(n)`: gli elementi tra parentesi (in questo caso solo uno, in generale una lista separata da virgole) sono chiamati **argomenti della funzione**, ed agiscono come variabili _inizializzate dalla invocazione della funzione_ e che hanno _visibilita' solo all'interno della funzione_. Se la funzione non accetta argomenti in ingresso si omettono le parentesi.
 * **corpo della funzione**: sono le linee di codice che descrivono le operazioni che la funzione esegue, racchiuse tra le keyword `def` e `end`.
 * `return`: questa peculiare keyword determina quale sara' il valore ritornato dalla funzione (in questo caso e' una stringa).
 * **commento prima della funzione**: questa parte, non necessaria ma fondamentale, e' utile a ricordare che cosa fa la funzione, con una indicazione rapida sia dei valori presi in input e dei valori ritornati in output.

## Operatori in Ruby

Per operatori intendiamo particolari tipi di funzione che hanno un elemento a sinistra e un elemento a destra. Gli operatori eseguono operazioni aritmetico/logiche o di assegnazione tra questi due elementi. L'elemento a sinistra e' detto _l-value_, mentre quello a destra e' detto _r-value_.

$$
l_{value}\,[\mathrm{operator}]\,r_{value}
$$

### Operatori aritmetici

Facciamo una introduzione agli operatori aritmetici, che possono essere utilizzati tra variabili di tipo numerico.

> Gli operatori aritmetici sono definiti per tutte le variabili `Numeric`. Tali operatori funzionano anche nel caso di varibili `Fixnum`, `Float` e `Bignum`, che sono tutte definite a partire della `Numeric`.

| Operatore	| Descrizione																		    |Esempio	|
|:---------:|---------------------------------------------------------------------------------------|:---------:|
|`+`		|**Addizione** - Aggiunge _r-value_ a _l-value_											| `a + b`	|
|`-`		|**Sottrazione** - Sottrae _r-value_ a _l-value_										| `a - b`	|
|`*`		|**Moltiplicazione** - Moltiplica _l-value_ per _r-value_								| `a * b`	|
|`/`		|**Divisione** - Ritorna il risultato della divisione tra _l-value_ e _r-value_			| `b / a` 	|
|`%`		|**Modulo** - Ritorna il resto della divisione intera tra _l-value_ e _r-value_			| `b % a` 	|
|`**`		|**Esponente** - Eleva _l-value_ a _r-value_						 					| `a**b`	|

### Operatori di assegnazione

Gli operatori di assegnazione sono tipologie di operatori aritmetici che effettuano direttamente la assegnazione

| Operatore	| Descrizione																									|Esempio					|
|:---------:|---------------------------------------------------------------------------------------------------------------|:-------------------------:|
|`=`		| **Operatore di assegnazione semplice**																		|	`c = a + b` 			|
|`+=`		| **Aggiungi e Assegna**, aggiunge il valore di _r-value_ a _l-value_ e assegna il risultato a _l-value_		|	`c += a` → `c = c + a` 	|
|`-=`		| **Sottrai e Assegna**, sottrae il valore di _r-value_ a _l-value_ e assegna il risultato a _l-value_			|	`c -= a` → `c = c - a` 	|
|`*=`		| **Moltiplica e Assegna**, moltiplica il valore di _r-value_ a _l-value_ e assegna il risultato a _l-value_	|	`c *= a` → `c = c * a` 	|
|`/=`		| **Dividi e Assegna**, esegue la divisione tra _l-value_ e _r-value_ e assegna il risultato a _l-value_		|	`c /= a` → `c = c / a` 	|
|`%=`		| **Resto e Assegna**, calcola il resto della divisione tra _l-value_ e _r-value_ e la assegna a _l-value_		|	`c %= a` → `c = c % a` 	|
|`**=`		| **Esponente e Assegna**, esegue _l-value_ elevato a _r-value_ e assegna il risultato a _l-value_				|	`c **= a` → `c = c**a`	|

### Operatori di comparazione

Gli operatori di comparazione permettono di comparare il valore a sinistra con il valore a destra, secondo una regola logica. Immaginando `a = 10` e `b = 30`.

| Operatore	| Descrizione																							|Esempio 					|
|:---------:|-------------------------------------------------------------------------------------------------------|:-------------------------:|
|`==`		|Controlla se _l-value_ e' uguale a _r-value_															|`(a == b) → false`			|
|`!=`		|Controlla se _l-value_ e' diverso da _r-value_															|`(a != b) → true` 			|
|`>`		|Controlla se _l-value_ e' maggiore da _r-value_														|`(a > b) → false`			|
|`<`		|Controlla se _l-value_ e' minore da _r-value_															|`(a < b) → true`			|
|`>=`		|Controlla se _l-value_ e' maggiore o uguale da _r-value_												|`(a >= b) → false`			|
|`<=`		|Controlla se _l-value_ e' minore o uguale da _r-value_													|`(a <= b) → true`			|
|`<=>`		|**Spaceship operator**																					|`(a <=> b) → -1`			|

#### Spaceship operator `<=>`

Questo operatore di comparazione e' di tipo molto particolare, in quanto ritorna un valore numerico che copre diversi casi di comparazione:

 * `-1` se _l-value_ e' minore da _r-value_
 * `0` se _l-value_ e' uguale da _r-value_
 * `1` se _l-value_ e' maggiore da _r-value_
 * `nil`se _l-value_ e' diverso da _r-value_ e non esiste una regola per definire quale e' maggiore o minore

> In Ruby questo operatore e' fondamentale, in quanto e' sufficiente definire questo metodo e includere la classe `Comparable` per avere la definizione automatica di tutti gli altri operatori di comparazione. Vedremo nella lezione sule classi che cosa significa tutto questo.

### Operatori logici

Tratti dalla algebra di Boole, gli operatori logici permettono di concatenare diverse affermazioni semplici al fine di ottenere espressioni di maggiore complessita'. Immaginando `a = true` e `b = false`.

|Operatore 		| Algebra di Boole 	| Descrizione 							| Esempio      			|
|:-------------:|:-----------------:|---------------------------------------|:---------------------:|
| `and`, `&&`	| $$ab$$ 			| Ritorna vero se entrambi sono veri 	| `(a and b) → false` 	|
| `or`, `||`  	| $$a+b$$ 			| Ritorna vero se uno dei due e' vero 	| `(a or b) → true` 	|
| `!` 			| $$\neg a$$ 		| Ritorna la negazione 					| `!(b) → true` 		|

> Gli operatori logici **non devono essere scambiati con i bitwise operator**, che sono operatori di natura diversa, facenti parte della algebra di Boole, e aventi come scopo la implementazione formale di tale algebra. Quelli presentati sono invece operatori logici, nati per ottenere espressioni complesse a partire da espressioni semplici, e rispondono in modo particolare ai diversi tipi contenuti negli l-value e r-value.

### Operatori di range

Gli operatori di range permettono di costruire un intervallo tra due valori, uno iniziale e uno finale. Esistono due operatori di range, che differiscono nella inclusione o no del punto finale.

|Operatore 		| Insieme        	| Descrizione 							| Esempio      			|
|:-------------:|:-----------------:|---------------------------------------|:---------------------:|
| `..`	        | $$[a,b]$$ 	    | Costruisce un range con $$a$$ e $$b$$ inclusi 	| `(a..b)` 	|
| `...`  	    | $$[a,b)$$ 		| Costruisce un range con $$a$$ incluso e $$b$$ escluso 	| `(a...b)` 	|

## Usiamo quanto imparato...

... per scrivere una funzione che ritorna le radici (anche complesse) di un polinomio di secondo ordine. Nello scrivere questa funzione introdurremo anche l'argomento della prossima lezione: **le istruzioni condizionali**, particolari construtti sintattici nati per definire il flusso di esecuzione di un codice.

### Introduzione ad `if`

Il costrutto **if**, comune nella maggior parte dei linguaggi di programmazione, sfrutta lo stato di una condizione per decidere quali linee di codice eseguire:

$$
\begin{align}
& \mathrm{if}\,\,(condition\,\mathrm{is}\,true)\,\,\mathrm{then} \\
& \qquad\mathrm{statement}_1\\
& \mathrm{else}\\
& \qquad\mathrm{statement}_2
\end{align}
$$

se la condizione $$contion$$ e' vera, il codice eseguito e' quello contenuto in $$\mathrm{statement}_1$$, altrimenti il codice eseguito e' quello contenuto in $$\mathrm{statement}_2$$.

In Ruby:

```ruby
#!/usr/bin/env ruby

a = 1

if a > 0 then
  puts "a > 0"
else
  puts "a < 0"
end
```

### Radici di un polinomio

Dato un polinomio del secondo ordine:

$$
p(x) = a x^2 + b x + c
$$

univocamente defineito dai tre termini noti $${a,b,c}$$, tale polinomio ha radici complesse nella forma:

$$
[ x_{r,k} + j x_{i,k} : k=1,2 ]
$$

Le parti complesse di tali radici sono nulle se il discriminante $$\delta$$ e' maggiore o uguale a 0, dove con discriminante si intende la espressione:

$$
\delta = b^2 - 4ac
$$

e le soluzioni sono nella forma:

$$
\begin{align}
x_{r} &= & \left\{ \begin{matrix}
 \dfrac{-b\pm\sqrt{\delta}}{2a} &\quad \delta \geq 0\\
 \\
 -\dfrac{b}{2a} &\quad \delta < 0
\end{matrix} \right. \\
\\
x_{i} &= & \left\{ \begin{matrix}
 0 &\quad \delta \geq 0\\
 \\
 \pm\dfrac{\sqrt{\delta}}{2a} &\quad \delta < 0
\end{matrix} \right.
\end{align}
$$

abbiamo tutte le informazioni necessarie per poter implementare una funzione.

#### Implementazione

La funzione radice quadratain Ruby e' `Math.sqrt`.

```ruby
#!/usr/bin/env ruby

# Funzione radici_quadrate
# input
#  a - Float, coefficiente dell'elemento di 2 ordine
#  b - Float, coefficiente dell'elemento di 1 ordine
#  c - Float, termine noto
# return
#  [ radice reale 1, radice immaginaria 1,
#    radice reale 2, radice immaginaria 2 ] - array con le radici
# La funzione calcola le radice di un polinomio, specificati i
# coefficiente e i termini noti.
def radici_quadratica(a,b,c)

  # calcolo discriminante
  delta = b**2 - 4 * a * c

  if delta >= 0 then
    # caso radici reali
    sdelta = Math.sqrt(delta)
    x1r = (-b+sdelta)/(2*a)
    x2r = (-b-sdelta)/(2*a)
    x1i = 0
    x2i = 0
  else
    # caso radici complesse
    sdelta = Math.sqrt(-delta)
    x1r = -b/(2*a)
    x2r = -b/(2*a)
    x1i = sdelta/(2*a)
    x2i = -sdelta/(2*a)
  end

  return [x1r, x1i, x2r, x2i]
end

# Ora che abbiamo implementato la funzione,
# possiamo testarla. Ne approfittiamo per
# vedere come interpolare una stringa per inserire
# eventuali valori numerici
res = radici_quadratica(1,2,3)

puts "Prima radice:"
print "Parte reale      = ", res[0], "\n"
print "Parte imaginaria = ", res[1], "\n"

puts "Seconda radice:"
puts "Parte reale      = #{res[2]}"
puts "Parte imaginaria = #{res[3]}"

```
