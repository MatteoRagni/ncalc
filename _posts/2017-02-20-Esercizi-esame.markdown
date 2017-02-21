---
layout: post
title:  "Esercizi"
date:   2017-02-20 10:00:00
categories: post
permalink: /esercizi/
lecture: "Esercizi con soluzione"
visible: 1
excerpt: "<p>In questa pagina trovate una serie di esercizi. Per ogni esercizio è fornita anche la soluzione. Gli esercizi <b>non</b> sono in ordine di difficoltà ma in ordine alfabetico.</p>"
---

In questa pagina trovate una serie di esercizi. Per ogni esercizio è fornita anche la soluzione. Gli esercizi **non** sono in ordine di difficoltà ma in ordine alfabetico.

* table of contents.
{:toc}

## Bolletta


Scrivere la funzione `bolletta` che legge una serie di contatti (telefono, tariffa, tempo) da un file CSV (cioe' ogni riga contiene le stringhe separate da virgola) e fa le operazioni descritte in seguito.

Ogni elemento del file rappresenta una telefonata ad una certa tariffa
per un cereto tempo. Il costo della singola telefonata si calcola con
la formula: `tariffa x tempo`

costruire un vettore di hash dove ogni hash ha 2 campi

 * `:telefono`
 * `:bolletta`

dove `:telefono` e' il numero di telefono associato alla `:bolletta` che e' la somma dei costi delle singole telefonate.

Restituire il vettore di hash delle bollette dove la chiave e' il numero di telefono e il valore e' il costo della bolletta per quel numero. Attenzione i costi e le tariffe sono tutti numeri interi.

Esempio di file:

```
2345,10,12
1111,12,22
2345,10,121
1111,12,21
2345,10,123
```

```ruby
def bolletta(filename)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/bolletta" | relative_url }})

## Campionato

> Esercizio ispirato da:
**Esercizi di programmazione in C, Esercitazioni per il corso di Fondamenti di Informatica**, _Fulvio Corno, Silvia Chiusano_ - Politecnico di Torino – Dipartimento di Automatica e Informatica

Realizzare un programma in grado di calcolare la classifica di un campionato di calcio giocato tra N squadre, numerate consecutivamente a partire da 0.
I risultati delle partite sono memorizzati in un file ASCII il cui nome e' passato come primo argomento alla funzione classifica.

Questo file contiene un risultato per riga nel formato:

```
squadra1,squadra2,goal1,goal2
```

dove `squadra1` e `squadra2` sono stringhe con i nomi delle squadre che si sono incontrate mentre `goal1` e `goal2` sono le reti segnate da ciascuna squadra. Le colonne sono separate da una virgola "`,`".

Il programma deve calcolare e riempire una hash di output. Le chiavi della hash sono stinghe e sono i nomi delle squadre. I valori della hash sono a loro volta delle hash chiave-valore che contengono:

 * `:partite`: numero di partite giocate
 * `:punti`: i punti conseguiti (si ricorda che la vittoria vale tre punti ed il pareggio un punto)
 * `:vinte`: numero di partite vinte
 * `:perse`: numero di partite perse

A titolo di esempio, supponendo che il file `CAMPIONATO.TXT` contenga le seguenti informazioni:

```
ROSSI BIANCHI 1 1
VERDI NERI 1 0
ROSSI NERI 2 0
```

allora la hash risultante deve contenere le seguenti informazioni:

```ruby
{
   'ROSSI'   => {  :partite => 2, :punti => 4, :vinte => 1, :perse => 0 },
   'BIANCHI' => {  :partite => 1, :punti => 1, :vinte => 0, :perse => 0 },
   'NERI'    => {  :partite => 2, :punti => 0, :vinte => 0, :perse => 2 },
   'VERDI'   => {  :partite => 1, :punti => 3, :vinte => 1, :perse => 0 },
}
```

Scriversi un file adeguato per fare il test.

```ruby
def campionato(filename)
  # completare
end
```

[Vai alla soluzione](/solutions/campionato)

## Collatz

Implementare una funzione esterna 'collatz'.
Consideriamo la ODE:

$$
y' = f(x, y)
$$

il metodo di collatz prende la forma:

$$
\begin{array}{rcl}
y\left(k+\dfrac{1}{2}\right) & = & y(k) + \dfrac{h}{2} \, f\left(x(k),y(k)\right) \\
y(k+1) & = & y(k) +h \, f\left(x\left(k+\dfrac{1}{2}\right),y\left(k+\dfrac{1}{2}\right)\right)
\end{array}
$$

La funzione `collatz` deve avere la seguente definizione:
```
collatz(x0, x1, y0, npts)
```

  * `x0`    : numero che rappresenta l'inizio dell'intervallo di integrazione
  * `x1`    : numero che rappresenta la fine dell'intervallo di integrazione
  * `y0`    : numero che rappresenta la condizione iniziale
  * `npts`  : numero di punti nell'intervallo di integrazione
inoltre
  * **blocco**: in aggiunta un blocco con la funzione che richiede 2 argomenti `f(x,y)`

La funzione `collatz` deve restituire una hash con due chiavi:
  * `:x`: array con le ascisse dei punti di integrazione (punti dell'intervallo di
        integrazione)
  * `:y`: array con il valore dell'integrale per ogni `x`.

Includere **la gestione degli errori sulla variabili e il blocco in ingresso**.

La funzione `collatz` puo' essere testata sulla ODE:

$$
y' = - y - 3x
$$

sapendo che se:

 * $x_0 = 0$
 * $x_1 = 2$
 * $y_0 = 1$
 * $n = 10$

la soluzione che deve essere restituita è (a meno di errori numerici):
```ruby
{
  :x=> [0, 0.2, 0.4, 0.6, 0.8, 1, 1.2, 1.4, 1.6, 1.8, 2],
  :y => [1, 0.8, 0.52, 0.176, -0.219, -0.655,
         -1.124, -1.619, -2.136, -2.668, -3.215]
}
```

```ruby
def collatz(x0, x1, y0, npts)
  # completare
end
```

[Vai alla soluzione](/solutions/collatz)

## Cornice

Si scriva una funzione "cornice" che dati 2 argomenti `r` e `c` (numeri interi)
restituisce un vettore di stringhe. Il vettore ha `r` elementi
e ogni elemento ha una stringa con `c` caratteri.
La stampa sei caratteri deve formare una cornice con i caratteri '`+`', '`-`', e '`|`'.
Ad esempio `cornice(4,5)` restituisce un array di 4 stringhe

```
res[0] = '+---+'
res[1] = '|   |'
res[2] = '|   |'
res[3] = '+---+'
```

controllare che w e h devono essere >= 2.

```ruby
def cornice(r, n)
  # completare la funzione
end
```

[Vai alla soluzione](/solutions/cornice)

## Cumulative Sum

Scivere la funzione `cumulative_sum(vec)` che dato un vettore di numeri calcola la somma cumulativa degli elementi di un vettore sommando gli elementi di indice pari e sottraendo gli elementi di indice dispari. Ad esempio:
```ruby
cumulative_sum([1, 2, 3, 4, 5, 6])
```
restituisce:
```
[1, -1, 2, -2, 3, -3]
```
cioè:
 * `1`
 * `1-2`
 * `1-2+3`
 * `1-2+3-4`
 * `1-2+3-4+5`
 * `1-2+3-4+5-6`
Altro esempio:
```ruby
cumulative_sum([1, 2, 3, 4, 5, 0, 1])
```
restituisce:
```
[1, -1, 2, -2, 3, 3, 4]
```

```ruby
def cumulative_sum(vec)
  # completare
end
```

[Vai alla soluzione](/solutions/cumulativesum)

## Derivative

Scrivere la funzione `derivative` che si aspetta 2 argomenti

 * `x`: coordinata x
 * `h`: intervallo approssimazione

ed un blocco che restituisce il valore della funzione della quale vogliamo calcolare le sue derivate. La funzione deve calcolare con differenze finite le derivate prime e seconde
e restituirle in una hash. La hash deve contenere come chiavi:

 * `:central`: derivata prima approssimata con differenze centrate
 * `:forward`: derivata prima approssimata con differenze 'in avanti'
 * `:backward`: derivata prima approssimata con differenze 'all'indietro'
 * `:order2`: derivata prima seconda approssimata con 3 punti

ricordo che:

$$
\begin{array}{lcl}
\dfrac{\Delta_h f}{\Delta x}_{\mathrm{central}}  & = & \dfrac{f(x+h)-f(x-h)}{2 \, h} \\
\\
\dfrac{\Delta_h f}{\Delta x}_{\mathrm{forward}}  & = & \dfrac{f(x+h)-f(x)}{h} \\
\\
\dfrac{\Delta_h f}{\Delta x}_{\mathrm{backward}} & = & \dfrac{f(x)-f(x-h)}{h} \\
\\
\dfrac{\Delta^2_h f}{\Delta x^2}   & = & \dfrac{f(x+h)-2 \, f(x)+f(x-h)}{h^2}
\end{array}
$$

```ruby
def derivative(x, h)
  # completare
end
```

[Vai alla soluzione](/solutions/derivative)

## Differenze Divise

Scrivi la funzione `diffdiv` che prende in ingresso:

 * un vettore di coordinate $$x$$
 * un vettore di coordinate $$y$$

e ritorna la differenza divisa $n$-esima come numero `Float`.

$n$ rappresenta la lunghezza dei due vettori. Nel caso i due vettori non siano della stessa lunghezza, tale funzione deve ritornare `nil`. Attenzione! I numeri in ingresso potrebbero essere interi, non necessariamente `Float`. Questo potrebbe essere un problema?

Ma come si calcola?

I due vettori sono della stessa lunghezza in quanto dovrebbero risultare dalla relazione:

$$
\begin{array}{rcl}
x & = & [ x_0,\,...\,, x_n ] \\
y & = & [ f(x_0),\,...\,, f(x_n) ]
\end{array}
$$

La differenza divisa di ordine 0 risulta essere:

$$
f_0([x_{i}, x_{i+1}]) = \dfrac{f(x_{i+1}) - f(x_i)}{x_{i+1} - x_i}
$$

mentre quelle di ordine successivo:

$$
f_k([x_{i},\,...\,, x_{i+k}]) = \dfrac{
  f_{k-1}([x_{i+1},\,...\,, x_{i+k}]) - f_{k-1}([x_{i},\,...\,, x_{i+k-1}])
}{x_{i+k} - x_{i}}
$$

non è altro che la costruzione di una tabella fatta così:

$$
\begin{array}{ccccc}
x   & f       & f_{0}             & f_{1}                  & f_{2} \\
x_0 & f(x_0)  & -                 & -                      & -     \\
x_1 & f(x_1)  & f_{0}([x_0, x_1]) & -                      & -     \\
x_2 & f(x_2)  & f_{0}([x_1, x_2]) & f_{1}([x_0, x_1, x_2]) & -     \\
x_3 & f(x_3)  & f_{0}([x_2, x_3]) & f_{1}([x_1, x_2, x_3]) & f_{2}([x_0, x_1, x_2, x_3]) \\
... & ... & ... & ... & ...
\end{array}
$$

**Suggerimento**: _Per la soluzione di questo esercizio vi consiglio di usare la
funzione `map`. Cfr. la [documentazione](http://ruby-doc.org/core-2.3.1/Array.html#method-i-map)._

```ruby
def diffdiv(x, y)
  # completare
end
```

[Vai alla soluzione](/solutions/diffdiv)

## Grafo orientato

Scrivere una classe Ruby che implementa una [**Grafo orientato**](https://it.wikipedia.org/wiki/Grafo#Grafi_orientati_e_grafi_semplici).

Un grafo è un insieme $$(V,E)$$ dove $$V$$ è in insieme di simboli detti vertici ed $$E$$ e' un insieme di coppie di vertici (ordinate) che definiscono uno spigolo o edge. Ad esempio se $$v_a$$ e $$v_b$$ sono due vertici e la coppia ordinata $$[v_a,v_b]$$ e' contenuta nell'insieme $$E$$ allora $$e = [v_a,v_b]$$ è un edge che fa parte del grafo.

La classe deve inizializzarsi con una grafo vuoto e avere i seguenti metodi:

 * `add(v0, v1)`:   aggiunge un edge al grafo che va dal vertice v0 a v1, v0 e v1 devono essere delle stringhe. Se un edge è inserito piu di una volta deve essere tenuta una sola copia dell'edge.
 * `get`: restituisce un vettore di hash contenente la lista degli edge. Ogni edge è una hash del tipo `{ :from => v0, :to => v1 }` con `v0` e `v1` stringhe
 * `size`: restituisce il numero di edge del grafo
 * `erase(v0, v1)` rimuove un edge `{ :from => v0, :to => v1 }` se esiste
 * `source_and_sink`: restituisce una hash con 2 chiavi: `:source` e `:sink`. Alla chiave `:source` e `:sink` corrispondono dei vettori di vertici. `:source = [....]` conterrà la lista dei vertici sorgente. `:sink = [....]` conterrà la lista dei vertici pozzo. Un vertice sorgente è un vertice dal quale gli edge sono solo uscenti, mentre un vertice pozzo è un vertice nel quale gli edge sono solo entranti.

Ad esempio:
```ruby
g = Grafo.new # crea una nuova pila

g.add( "a", "b")  # aggiunge l'edge
g.add( "a", "c")  # aggiunge l'edge
g.add( "b", "c")  # aggiunge l'edge
g.add( "c", "a")  # aggiunge l'edge
puts g.getvertex
puts g.get
```

```ruby
class Grafo
  # completare
end
```

[Vai alla soluzione](/solutions/grafo)
