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

___

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

___

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

[Vai alla soluzione]({{ "/solutions/campionato" | relative_url }})

___

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

$$
\begin{array}{cccc}
x_0 = 0 & x_1 = 2 & y_0 = 1 & n = 10
\end{array}
$$

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

[Vai alla soluzione]({{ "/solutions/collatz" | relative_url }})

___

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

[Vai alla soluzione]({{ "/solutions/cornice" | relative_url }})

___

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

[Vai alla soluzione]({{ "/solutions/cumulativesum" | relative_url }})

___

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

[Vai alla soluzione]({{ "/solutions/derivative" | relative_url }})

___

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

[Vai alla soluzione]({{ "/solutions/diffdiv" | relative_url }})

___

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

[Vai alla soluzione]({{ "/solutions/grafo" | relative_url }})

___

## Halley

Scrivere la funzione `halley` che si aspetta 3 argomenti:

 * `x0`: approssimazione iniziale della radice
 * `tol`: tolleranza ammessa
 * `imax`: massimo numero di iterate

ed **un blocco** che restituisce una hash con valore della funzione con le sue prime 2 derivate della quale cechiamo lo zero. Le 3 chiavi sono:

 * `:f`: valore della funzione
 * `:df`: valore della derivata prima della funzione
 * `:ddf`: valore della derivata seconda della funzione

La funzione deve implementare il metodo iterativo di Halley per il calcolo dello zero di una funzione. La funzione restituisce una hash con 3 chiavi:

 * `:solution`: con la soluzione
 * `:iter`: un intero con il conteggio del numero delle iterate fatte
 * `:converged`: `true`/`false` (vero se arrivato a convegenza)

Se $$x_k$$ è la ultima iterata, $$x_{k+1}$$ con il metodo di Halley si calcola con la formula:

$$
x_{k+1} = x_{k} - \dfrac{f(x_k) \, \left.\frac{df}{dx}\right|_{x_k}}{\left.\frac{df}{dx}\right|_{x_k}^2 - \frac{1}{2} \, f(x_k) \, \left.\frac{ {d}^{2}f}{ {dx}^{2} }\right|_{x_k}}
$$

Le iterazioni terminano se si supera `imax` (fallimento) o se $$-\mathrm{tol} \leq f(x_k) \leq \mathrm{tol}$$ (successo)

```ruby
def halley(x0, tol, imax)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/halley" | relative_url }})

___

## Heun

Implementare una funzione esterna `heun`. Consideriamo la ODE:

$$
y′ = f(x,y)
$$

il metodo di Heun prende la forma:

$$
\begin{array}{rcl}
\tilde{y} & = & y_k + h\,f(x_k, y_k) \\
y_{k+1} & = & y_k + \dfrac{1}{2} \left(f(x_{k+1} ,\tilde{y}) + f(x_k, y_k) \right)
\end{array}
$$

La funzione 'heun' deve avere la seguente definizione:

```ruby
heun(x0, x1, y0, npts)
```

 * `x0`: numero che rappresenta l'inizio dell'intervallo di integrazione
 * `x1`: numero che rappresenta la fine dell'intervallo di integrazione
 * `y0`: numero che rappresenta la condizione iniziale
 * `npts`: numero di punti nell'intervallo di integrazione
inoltre
 * **blocco**: funzione (i.e. blocco) di due argomenti $$f(x,y)$$

La funzione `heun` deve restituire una hash con due chiavi:
 * `:x`: array con le ascisse dei punti di integrazione (punti dell'intervallo di integrazione)
 * `:y`: array con il valore dell'integrale per ogni `x`.

**Includere la gestione degli errori per ingressi scorretti**.

Note:

La funzione puo' essere testata sulla ODE:

$$
y' = - y - 3\,x
$$

sapendo che se $$x_0 = 0$$, $$x_1 = 2$$, $$y_0 = 1$$, $$n = 10$$, la soluzione che deve essere
restituita è (a meno di errori numerici):

```ruby
{
  :x => [0, 0.2, 0.4, 0.6, 0.8, 1, 1.2, 1.4, 1.6, 1.8, 2],
  :y => [1, 0.8, 0.52, 0.176, -0.219, -0.655, -1.124,
         -1.619, -2.136, -2.668, -3.215]
}
```

```ruby
def heun(x0, x1, y0, npts)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/heun" | relative_url }})

___

## Lettere (a)

Si scriva una funzione `letters` che dato come argomento una stringa restituisce una stringa contenente le lettere `[a-z]` ordinate e convertite in minuscolo presenti nella stringa:
Ad esempio:
```ruby
puts letters("Pippo !G")
```
risulta in:
```ruby
"giop"
```
mentre:
```ruby
puts letters("Wall ! none")
```
risulta in:
```ruby
"aelnow"
```

```ruby
def letters(msg)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/letters/a" | relative_url }})

___

## Lettere (b)

Si scriva una funzione `letters` che dato come argomento una stringa restituisce una hash le cui chiavi sono le lettere dell'alfabeto contenute nella stringa e il cui valore è il numero delle volte in cui la lettera compare. Minuscole e maiuscole non si devono distinguere. Solo le lettere vanno contate, caratteri speciali e numeri non vanno considerati.

Ad esempio
```ruby
puts letters("Pippo !G")
```
risulta in:
```ruby
{ "g" => 1, "i" => 1, "o" => 1, "p" => 3 }
```
mentre:
```ruby
puts letters("Wall ! none")
```
risulta in:
```ruby
{
  "a" => 1, "e" => 1, "l" => 2,
  "n" => 2, "o" => 1, "w" => 1
}
```

```ruby
def letters(msg)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/letters/b" | relative_url }})

___

## Massimo locale

Scivere la funzione `local_max(vec)` che dato un vettore di numeri calcola le posizioni dei massimi locali cioe' gli indici tali che

$$
v_{i-1} < v_{i} > v_{i+1}
$$

**Implementare un controllo sull'ingresso.**

```ruby
def local_max(vec)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/localmax" | relative_url }})

___

## Minimo Locale


Scivere la funzione `local_min(vec)` che dato un vettore di numeri calcola le posizioni dei minimi locali cioe' gli indici tali che:

$$
v_{i-1} > v_{i} < v_{i+1}
$$

la funzione deve restituire una hash dove la chiave è un **numero** che è il numero crescente del minimo trovato e come valore la triade di valori del minimo locale. Ad esempio dato il vettore

```
[ 1, 2, 3,-1,2, 3, 4, 5, 8, 1, 1, 0, 1]
           ^                      ^
           |                      |
           ------- minimi --------
```           

deve restituire:

```ruby
{
  1 => [ 3, -1, 2 ],
  2 => [ 1, 0, 1 ]
}
```

```ruby
def local_min(vec)
  # conpletare
end
```

[Vai alla soluzione]({{ "/solutions/localmin" | relative_url }})

___

## Max Min

Scivere la funzione `max_min(vec)` che dato un vettore di numeri calcola il massimo degli elementi di indice pari e il minimo degli elementi di indice dispari. Il risultato è restituito in una hash con i campi `:max` e `:min`.

```ruby
def max_min(vec)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/maxmin" | relative_url }})

___

## Minimo Comune Divisore

Scivere la funzione mcd(a,b) che dati due numeri interi a e b
maggiori di 0 calcola il loro massimo comun divisore.

> **Proprieta MCD**: Il massimo comun divisore è il numero di che divide sia $$a$$ che $$b$$. Se un numero $$c$$ divide sia $$a$$ che $$b$$ allora deve dividere anche $$d$$: $$\mathrm{mcd}(a,b) = \mathrm{mcd}(b,a)$$

Per calcolare l'MCD di due numeri potete usare i seguenti algoritmi:

**Algoritmo 1 (ricorsivo):**

```
Se a > b allora:
  se b divide a allora mcd(a,b) = b
  altrimenti mcd(a,b) = mcd(a-b,b)
```

**Algoritmo 2 (iterativo):**

```
Assumiamo a > b
fino a quando il resto di a/b != 0
  a = a - b
  se a < b allora scambio a e b
```

```ruby
def mcd(a, b)
  # controllare
end
```

[Vai alla soluzione]({{ "/solutions/mcd" | relative_url }})

___

## Minimo Comune Multiplo

Scivere la funzione mcm(a,b) che dati due numeri interi a e b
maggiori di 0 calcola il loro minimo comune multiplo.

> **Proprieta MCM**: il minimo comune multiplo è il numero che è divisibile sia per $$a$$ che per $$b$$. Se un numero $$c$$ e' divisibile sia $$a$$ che $$b$$ allora $$c \geq \mathrm{mcm}(a,b)$$.

Questo implica che

$$
\mathrm{mcm}(a,b) = (a\,b)/\mathrm{mcd(a,b)}
$$

dove $$\mathrm{mcd}(a,b)$$ è il massimo comun divisore di $$a$$ e $$b$$.

Per calcolare l'MCD, utile a calcolare l'MCM, di due numeri potete usare i seguenti algoritmi:

**Algoritmo 1 (ricorsivo):**

```
Se a > b allora:
  se b divide a allora mcd(a,b) = b
  altrimenti mcd(a,b) = mcd(a-b,b)
```

**Algoritmo 2 (iterativo):**

```
Assumiamo a > b
fino a quando il resto di a/b != 0
  a = a - b
  se a < b allora scambio a e b
```

```ruby
def mcm(a, b)
  # controllare
end
```

[Vai alla soluzione]({{ "/solutions/mcm" | relative_url }})

___

## Mix

Scrivere la funzione `mix` che dati due vettori costruisce un vettore che alterna gli elementi del primo vettore con quelli del secondo. Ad esempio:

```ruby
mix( [1,2,3], [a,b,c,d,e])
```

restituisce:

```ruby
[1,a,2,b,3,c,d,e]
```

notate che se un vettore è piu lungo dell'altro il vettore risultante contiene in coda solo elementi del vettore piu lungo.

```ruby
def mix(a, b)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/mix" | relative_url }})

___

## Monotone

Si scriva una funzione `monotone` che dato un vettore di interi restituisce un vettore di hash. Ogni elemento del vettore è una hash con le chiavi:

 * `:begin`
 * `:end`

a cui corrisponde un intero che è l'indice iniziale e finale di una successione di interi monotona non decrescente del vettore in ingresso di almeno 3 elmenti.

Ad esempio se il vettore in ingresso è

```
[ 1, 0, 1, 2, 2, 4, 3, 3, 3, 4, 5, 0, -1, 0, -1, 2, 50, 101, 0]
     ^           ^  ^           ^             ^          ^
     1-----------5  6----------10            14---------17
```

il risultato sarà il vettore di hashes:

```ruby
[  
  { :begin => 1, :end => 5 },
  { :begin => 6, :end => 10 },
  { :begin => 14, :end => 17 }  
]
```

L'intervallo deve essere **massimale**, nel senso che `{ :begin => 1, :end => 3 }` è un intervallo **monotono ma è contenuto** in `{ :begin => 1, :end => 5 }`.

```ruby
def monotone(v)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/monotone" | relative_url }})

___

## Morse

Scrivere le funzioni `to_morse` e `from_morse` che convertono da e verso l'alfabeto morse.
L'alfabeto morse è messo in una hash che ha come chiavi le lettere ascii che hanno un codice morse
e come valore la scringa di punti "." e linee "-" dell'alfabeto.

La funzione `to_morse` prende una stringa e la converte nel corrispondente codice morse separato da spazi. Ad esempio

```ruby
to_morse("abc") # ".- -... -.-."
```

le lettere minuscole e maiuscole hanno la stessa codifica morse. Viceversa funzione `from_morse` deve prendere una serie di codici morse separati da spazi e restituire una stringa. Ad esempio

```ruby
from_morse(".- -... -.-.") # "ABC"
```

```ruby
MORSE = {
    "!" => "---.",   "\"" => ".-..-.", "$" => "...-..-", "'" => ".----.",
    "(" => "-.--.",  ")"  => "-.--.-", "+" => ".-.-.",   "," => "--..--",
    "-" => "-....-", "."  => ".-.-.-", "/" => "-..-.",   "0" => "-----",
    "1" => ".----",  "2"  => "..---",  "3" => "...--",   "4" => "....-",  "5" => ".....",
    "6" => "-....",  "7"  => "--...",  "8" => "---..",   "9" => "----.",  ":" => "---...",
    ";" => "-.-.-.", "="  => "-...-",  "?" => "..--..",  "@" => ".--.-.", "A" => ".-",
    "B" => "-...",   "C"  => "-.-.",   "D" => "-..",     "E" => ".",      "F" => "..-.",
    "G" => "--.",    "H"  => "....",   "I" => "..",      "J" => ".---",   "K" => "-.-",
    "L" => ".-..",   "M"  => "--",     "N" => "-.",      "O" => "---",    "P" => ".--.",
    "Q" => "--.-",   "R"  => ".-.",    "S" => "...",     "T" => "-",      "U" => "..-",
    "V" => "...-",   "W"  => ".--",    "X" => "-..-",    "Y" => "-.--",   "Z" => "--..",
    "[" => "-.--.",  "]"  => "-.--.-", "_" => "..--.-",
}

def to_morse(str)
  # completare
end

def from_morse(str)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/morse" | relative_url }})

___

## Newton

Scrivere la funzione newton che si aspetta 3 argomenti:

 * `x0` punto iniziale
 * `maxiter` massimo numero di iterate
 * `tol` tolleranza

ed un blocco che restituisce un vettore con valore della funzione e sua derivata. La funzione deve implementare il metodo di Newton.

Ad esempio per calcolare lo 0 di:

$$
f(x) = x^2 - 2
$$

con $$f'(x) = 2x$$ scriveremo:

```ruby
x0  = 1.0  # punto iniziale
tol = 1e-8  
x = newton( x0, 100, tol ) { |x| [ x**2 - 2.0, 2.0*x ] }
puts x
```

```ruby
def newton(x0, maxiter, tol)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/newton" | relative_url }})

___

## Odd Even

Scrivere la funzione `odd_even(vec)` che dato un vettore di numeri calcola costruisce un vettore con all'inizio gli elementi del vettore di indice dispari e poi gli elementi di indice pari. Ad esempio:

```ruby
odd_even([1, 2, 3, 4, 5, 6])
```
ritorna
```ruby
[2, 4, 6, 1, 3, 5]
```

```ruby
def odd_even(v)
  # completare
end
```
[Vai alla soluzione]({{ "/solutions/oddeven" | relative_url }})

___

## Ordered (a)

Scrivere la funzione `ordered` che dato un array (di numeri) in ingresso cerca i sotto-array strettamente decrescenti cioe le successioni di numeri strettamente decrescenti. Ad esempio 5,2,1 è una successione strettamente decrescente mentre 19, 7, 5, 5, 1 no.

Il risultato va scritto in una array. Ogni elemento dell'array contiene gli array STRETTAMENTE decrescenti dell'array originale nell'ordine in cui sono trovati. Si considera array strettamente decrescente un singolo elemento.

Ad esempio se in input abbiamo:

```
[ 1,  2, 1, 0, 2,  1, 0, 1, -8, 1, 5, 0 ]
  ++  +-----+  +-------+ +----+ ++ +--+  ++ <--- sotto-array strettamente crescenti
```
deve restituire:
```
[ [1], [2,1,0], [2,1,0], [1,-8], [1], [5,0] ]
```
Attenzione ogni elemento del vettore restituito deve essere a sua volta un vettore. Ad esempio:
```
[ 1, [2,1,0], [2,1,0], [1,-8], 1, [5,0] ]
  ^                            ^
  |                            |
  non sono vettori-------------+
```
è sbagliato.

Attenzione gli array nell'array devo essere nell'ordine in cui compaiono nel vettore.

```ruby
def ordered(a)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/ordered/a" | relative_url }})

___

## Ordered (b)

Scrivere la funzione `ordered(vec)` che dato un vettore di numeri restituisce:

 * 2: se il vettore è ordinato in modo **strettamente** crescente cioè `vec[i+1] > vec[i]`
 * 1: se il vettore è ordinato in modo crescente cioè `vec[i+1] >= vec[i]`
 * -1: se il vettore è ordinato in modo **strettamente** decrescente cioè `vec[i+1] < vec[i]`
 * -2: se il vettore è ordinato in modo decrescente cioè `vec[i+1] <= vec[i]`
 * 0: se il vettore non è ordinato o consiste di meno di 2 elementi

```ruby
def ordered(ved)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/ordered/b" | relative_url }})

___

## Ordered (c)

Scrivere la funzione `ordered` che dato un array (di numeri) in ingresso cerca i sotto-array strettamente crescenti cioe contenenti numeri strettamente crescenti.
Il risultato va scritto in una hash le cui chiavi sono numeri $$\geq 2$$. Ad ogni chiave corrisponde un array e ogni elemento dell'array è a sua volta un array che ha tanti elementi quanti il numero della chiave. Questi ultimi array contengono numeri **strettamente** crescenti dell'array originale.

Ad esempio se in input abbiamo:
```
[ 1, 0, 1, 2, 2, 1, 0, 1, -8, 1, 5, 0 ]
     +-----+        +--+  +------+      <--- sotto-array strettamente crescenti
2 -> [ [0, 1] ]
3 -> [ [0, 1, 2], [-8, 1, 5] ]
```
Attenzione gli array negli array della hash devo essere nell'ordine in cui compaiono nel vettore, cioe' chiave 3 non deve contenere:
```
3 -> [ [-8, 1, 5], [0, 1, 2] ]
```
perchè gli array sono invertiti.

```ruby
def ordered(a)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/ordered/c" | relative_url }})

___

## Ovale

Si scriva una funzione `ovale` che dati due argomenti interi positivi, restituisce una stringa che rappresenta un "ovale" stilizzato. Ad esempio:

```ruby
puts quad(4,2)
```

deve risultare in

```
  * * * *
*         *
*         *
  * * * *
```
cioè una SINGOLA stringa che contiene la concatenazione delle stringhe:
```
"  * * * *  " + "\n" +
"*         *" + "\n" +
"*         *" + "\n" +
"  * * * *  " + "\n"
```
cioe'
```
"  * * * *  "\n*         *\n*         *\n  * * * *  \n"
```
attenzione ai caratteri non stampabili, `\n` e spazi

_**Note:** Usate l'operatore `*` per replicare e concatenare le stringhe, ad esempio `"pippo" * 3 = "pippopippopippo"`_

```ruby
def ovale(n, m)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/ovale" | relative_url }})

___

## Pairs

Scrivere la funzione `pairs` che dato un array in ingresso cerca i sotto-array di elementi consecutivi uguali. Il risultato va scritto in una hash le cui chiavi sono numeri >= 2. Ad ogni chiave corrisponde un array e ogni elemento dell'array è a sua volta un array che contiene l'elemento ripetuto.

Ad esempio se in input abbiamo:
```
[ 1, 0, 1, 2, 2, 1, 0, 0, 0, 1, -8, -8, -8, "abc", "abc", 1, 5, 0 ]
           +--+     +-----+     +--------+  +----------+      <--- sotto-array elementi ripetuti
2 -> [ 2, "abc" ]
3 -> [ 0, -8 ]
```
Attenzione gli elementi ripetuti negli array della hash devo essere nell'ordine in cui compaiono nel vettore, cioè la chiave 3 non deve contenere:
```
3 -> [ -8, 0 ]
```
perchè gli elementi sono invertiti.

```ruby
def pairs(a)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/pairs" | relative_url }})

___

## Pangram

Si scriva una funzione "pangram" che dato come argomento una stringa restituisce una valore booleano:

  * `true` se la stringa è un pangram o pangramma
  * `false` se la stringa non è un pangram o pangramma

Un pangramma (o anche pantogramma) deriva dal greco e significa "tutte le lettere": è una frase che contiene tutte le lettere dell'alfabeto. Ad esempio:
```
"Pranzo d’acqua fa volti sghembi"
```
è un pangramma sulle lettere dell'alfabeto italiano.

>**Note:** usare una hash per memorizzare le lettere dalla "a" alla "z" e rimuovere le chiavi man mano che si trovano le lettere nella stringa.

**Esempi di Pangram**

 * `Two driven jocks help fax my big quiz.`
 * `Pack my box with five dozen liquor jugs.`
 * `The five boxing wizards jump quickly.`
 * `Bright vixens jump; dozy fowl quack.`
 * `Jackdaws love my big sphinx of quartz.`
 * `John quickly extemporized five tow bags.`
 * `Waltz, nymph, for quick jigs vex Bud.`
 * `Quick wafting zephyrs vex bold Jim.`
 * `Brown jars prevented the mixture from freezing too quickly.`
 * `Fred specialized in the job of making very quaint wax toys.`
 * `New job: fix Mr Gluck's hazy TV, PDQ`

```ruby
def pangram(msg)
  # controllare
end
```

[Vai alla soluzione]({{ "/solutions/pangram" | relative_url }})

___

## Pine

Si scriva una funzione "pine" che dato come argomento un numero intero positivo restituisce una stringa che rappresenta un "pino" stilizzato. Ad esempio:
```ruby
puts pine(4)
```
deve risultare in
```
   *
  ***
 *****
*******
```
cioè una SINGOLA stringa che contiene la concatenazione delle stringhe:
```
"   *   " + "\n" +
"  ***  " + "\n" +
" ***** " + "\n" +
"*******" + "\n"
```
cioè:
```
"   *   \n  ***  \n ***** \n*******\n"
```

_**Note:** Usate l'operatore `*` per replicare e concatenare le stringhe, ad esempio `"pippo" * 3 = "pippopippopippo"`_

```ruby
def pine(n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/pangram" | relative_url }})

___

## Power

Si scriva una funzione "power" dato un intero $$n > 0$$ costruisce tutti i possibili sottoinsiemi dell'insieme $$\{1,2,...,n\}$$. Ad esempio se $$n = 3$$ abbiamo i sottoinsiemi:

$$
\{\},\, \{1\},\, \{2\},\, \{3\},\, \{1,2\},\, \{2,3\},\, \{1,2,3\}
$$

gli insiemi vengono restituiti in un vettore di vettori dove ogni elemento del vettore è un unsieme rappresentato come un vettore.

Ad esempio:
```ruby
power(2)
```
deve restituire:
```ruby
[[], [1], [2], [1, 2]]
```
mentre
```ruby
power(3)
```
deve restituire
```ruby
[[], [1], [2], [3], [1, 2], [2, 3], [1, 3], [1, 2, 3]]
```

> _**Note:** Se `power(n-1)`` restituisce l'insieme di tutti i possibili sottoinsiemi dell'insieme $$\{1,2,...,n-1\}$$ per ottenere i rimanenti insiemi basta unire alla lista la lista della unione degli insiemi prodotti con l'insieme {n}._

```ruby
def power(n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/power" | relative_url }})

___

## Ricorrenza

Scrivere la funzione `recurr` che si aspetta 3 argomenti:

 * `rec`: vettore di numeri che rappresenta la ricorrenza
 * `ini`: vettore delle condizioni iniziali
 * `n`: intero che rappresenta l'indice dell'$$n$$-esimo valore richiesto della ricorrenza

la funzione restituisce l'$$n$$-esimo elemento della ricorrenza definita dai dati passati. La ricorrenza e' definita come:

$$
y_{k+1} = r_0 \, y_{k} + r_1 \, y_{k-1} + \,...\, + r_{\mathrm{dim}(r)} \, y_{k-{\mathrm{dim}(r)} }
$$

dove $$\mathrm{dim}(r)$$ e' la lunghezza del vettore `rec`. Il dato iniziale è dato dal vettore `ini` cioè

 * $$y_0 =$$ `ini[0]`
 * $$y_1 =$$ `ini[1]`
 * $$...$$
 * $$y_{\mathrm{dim}(r)} =$$ `ini[rec.size - 1]`

la funzione deve restituire un singolo numero reale contenente $$y_n$$.

**Esempio:**

$$
r = [1, 2, 3]
$$

$$
y_\mathrm{init} = [2, 3, 1]
$$

con $$n = 4$$, che corrisponde a:

$$
y_{k+1} = y_{k} + 2 \, y_{k-1} + 3 \, y_{k-2}
$$

quindi calcolando la ricorsione:

$$
y_{3} = 1 \cdot 1 + 2 \cdot 3 + 3 \cdot 2 = 13
$$

e poi

$$
y_{4} = 1 \cdot 13 + 2 \cdot 1 + 3 \cdot  3 = 24
$$

risultato $$y_4 = 24$$.

```ruby
def recurr(rec, ini, n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/recurr" | relative_url }})

___

## Le 8 Regine

> **Nota:** Questo è probabilmente l'esercizio più complesso.

Scrivere la funzione `otto_regine` che  risolve il rompicapo (o problema) delle otto regine. Il problema che consiste nel trovare il modo di posizionare otto regine (pezzo degli scacchi) su una scacchiera `8 x 8` tali che nessuna di esse possa catturarne un'altra, usando i movimenti standard della regina, cioe' due regine non si possono trovare sulla stessa riga colonna o diagonale della scacchiera.

Ad esempio nel caso `4 x 4` (una soluzione) è la seguente.

```
+---+---+---+---+
|   | R |   |   |
+---+---+---+---+
|   |   |   | R |
+---+---+---+---+
| R |   |   |   |
+---+---+---+---+
|   |   | R |   |
+---+---+---+---+
```

la funzione deve restituire un vettore di vettori di interi. Ogni elemento del vettore è un possibile soluzione. Ogni soluzione è un vettore di 8 interi da 0 a 7 che rappresenta la posizione della regina sulla scacchiera. Ad esempio nel problema `4 x 4` la soluzione precedente
si scrive come:

```
[1, 3, 0, 2]
```

 * la prima regina è alla posizione `(0,vec[0]) = 0 riga 1 colonna`
 * la seconda regina è alla posizione `(1,vec[1]) = 1 riga 3 colonna`
 * la terza regina è alla posizione `(2,vec[2]) = 2 riga 0 colonna`
 * la quarta regina è alla posizione `(3,vec[3]) = 3 riga 2 colonna`

```ruby
def otto_regine
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/regine" | relative_url }})

___

## Sequence

Si scriva una funzione `sequence` che dato un vettore di interi restituisce un vettore di hash.
Ogni elemento del vettore è una hash con le chiavi:

 * `:begin`
 * `:end`

a cui corrisponde un intero che è l'indice iniziale e finale di una successione di almeno 3 interi tali che due interi consecutivi differiscono al piu di uno.

Ad esempio se il vettore in ingresso è:

```
[ 1, 0, 1, 2, 2, 4, 3, 3, 3, 4, 5, 0, -10, 0, -1, 0, 50, 101, 0]
 ^           ^  ^              ^          ^      ^
 0-----------4  5-------------10          13-----15
```

il risultato sarà il vettore di hash:

```ruby
[  
  { :begin => 0, :end => 4 },
  { :begin => 5, :end => 10 },
  { :begin => 13, :end => 15 }
]
```

```ruby
def sequence(v)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/sequence" | relative_url }})

___

## Simpson

Scrivere la funzione simpson che si aspetta 3 argomenti

 * `a` sinistra intervallo
 * `b` destra intervallo
 * `n` numero intervalli (grandi)

ed un blocco che restituisce il valore della funzione da integrare. La funzione deve implementare il metodo di Simpson per la approssimazione dell'integrale di $$f(x)$$ nell'intervallo $$[a,b]$$.

```ruby
def simpson(a, b, n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/simpson" | relative_url }})

___

## Stack

Scrivere una classe Ruby che implementa una Pila o Stack. La classe deve inizializzarsi con una pila vuota e avere i seguenti metodi:

 * `push( val )`: aggiunge val alla pila
 * `pop`: rimuove l'elemento in cima alla pila
 * `size`: ritorna il numero di elementi nella pila
 * `top`: restituisce l'elemento in cima alla pila

Ad esempio:

```ruby
st = Stack.new # crea una nuova pila

st.push 12     # aggiunge 12 alla pila che ora contiene [12]
st.push 1      # aggiunge  1 alla pila che ora contiene [12,1]
st.push -3     # aggiunge -3 alla pila che ora contiene [12,1,-3]
st.push 4      # aggiunge  4 alla pila che ora contiene [12,1,-3,4]
st.pop         # rimuve 4 dalla pila che ora contiene [12,1,-3]
st.push 0      # aggiunge  0 alla pila che ora contiene [12,1,-3,0]
puts st.top    # stampa 0 senza modificare la pila
puts st.size   # stampa 4 senza modificare la pila
```

```ruby
class Stack
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/stack" | relative_url }})

___

## Star


Scrivere la funzione `star` che si aspetta 3 argomenti:

 * `x0`: approssimazione iniziale della radice
 * `x1`: seconda approssimazione iniziale della radice
 * `tol`: tolleranza ammessa
 * `imax`: massimo numero di iterate

ed un blocco che restituisce il valore della funzione della quale cechiamo lo zero.

La funzione deve implementare il metodo iterativo **start** per il calcolo dello zero di una funzione. La funzione restituisce una hash con 3 chiavi:

 * `:solution`: con la soluzione
 * `:iter`: un intero con il conteggio del numero delle iterate fatte
 * `:converged`: `true`/`false` (vero se arrivato a convegenza)

Se $$x_0$$, $$x_1$$, $$x_2$$ sono le ultime tre iterate e $$f_0 = f(x_0)$$, $$f_1 = f(x_1)$$, $$f_2 = f(x_2)$$ allora $$x_3$$ con il metodo **star** si calcola con:

$$
x_3 = x_2 - \dfrac{ f_2 }{ d_{2,0} + d_{2,1} - d_{1,0} }
$$

dove

$$
d_{i,j} = \dfrac{ f_i - f_j }{ x_i - x_j }
$$

Il metodo star richiede le ultime 3 approssimazioni della radice mentre all'inizio ne forniamo solo 2. Per far partire il metodo usiamo quindi **un solo** passo del metodo delle secanti:

$$
x_2 = x_1 - \dfrac{ f_1 }{ d_{1,0} }
$$

Le iterate terminano se si supera `imax` (fallimento) o se $$-\mathrm{tol} \leq f(x_k) \leq \mathrm{tol}$$ (successo).

```ruby
def star(x0, x1, tol, imax)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/star" | relative_url }})

___

## Somma e Prodotto

Scivere la funzione `sum_prod(v)` che dato un vettore di numeri calcola la somma e il prodotto di 3 elementi consecutivi e li mette un una hash.
La chiave della hash e' un intero con il numero della i-esima somma/prodotto e valore un vettore con 2 elemementi [somma,prodotto]. Se il vettore non ha un numero di elementi multiplo di 3
la ultima [somma,prodotto] è fatta su 2 o 1 elemento. Ad esempio:

```ruby
sum_prod([1, 2, 3, 4, 5])
```

restituisce:

```ruby
{ 1 => [6, 6], 2 => [9, 20] }
```

**Ad esempio**:

```ruby
sum_prod([1, 2, 3, 4, 5, 0, 1])
```

restituisce:

```ruby
{ 1 => [6,6], 2 => [9,0], 3 => [1,1] }
```

```ruby
def sum_prod(vec)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/sumprod" | relative_url }})

___

## To Hours

Si scriva una funzione `to_hour` che dati 2 argomenti:

 * `h` ora del giorno  (numero tra 0 e 23)
 * `d` giorno del mese (numero tra 1 e 31)
 * `m` numero del mese (numero tra 1 e 12)

controlla che la data sia corretta e la converte in ore dall'inizio dell'anno.

| Mese          | Giorni      |
|---------------|-------------|
|  gennaio      | 31 giorni   |
|  febbraio     | 28 giorni   |
|  marzo        | 31 giorni   |
|  aprile       | 30 giorni   |
|  maggio       | 31 giorni   |
|  giugno       | 30 giorni   |
|  luglio       | 31 giorni   |
|  agosto       | 31 giorni   |
|  settembre    | 30 giorni   |
|  ottobre      | 31 giorni   |
|  novembre     | 30 giorni   |
|  dicembre     | 31 giorni   |

Attenzione che ore 0 del 1 gennaio deve dare 0 ore come risultato.

```ruby
def to_hour(h, d, m)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/tohour" | relative_url }})

___

## Tre ottavi

crivere la funzione `tre_ottavi` che si aspetta 3 argomenti:

 * `a` minimo dell'intervallo
 * `b` massimo dell'intervallo
 * `n` numero intervalli (grandi)

ed un blocco che restituisce il valore della funzione da integrare.  La funzione deve implementare la regola dei 3/8 per la approssimazione dell'integrale di $$f(x)$$ nell'intervallo $$[a,b]$$.

Ad esempio per calcolare

$$
\int_{4}^{12}{\sin(x) \exp(x) dx}
$$

con `tre_ottavi` e 50 intevalli scriveremo:

```ruby
int = tre_ottavi(4, 12, 50) { |x| Math::sin(x) * Math::exp(-x) }
puts int
```

La regola dei 3/8 su un _intervallone_ ha la seguente espressione:

$$
\dfrac{h}{8} \left( f(x_k) + 3 \, f(x_k + h) + 3 \, f(x_k + 2\,h) + f(x_k + 3\,h) \right)
$$

dove $$x_k$$ sono i nodi di interpolazione distanziati del passo $$h$$. Il passo è nella forma:

$$
h = \dfrac{b - a}{3 \, n}
$$

La funzione è passata sotto forma di **blocco**.

```ruby
def tre_ottavi(a, b, n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/treottavi" | relative_url }})

___

## Triangolare

Un numero $$n$$ e' un numero triangolare se esiste un intero $$k$$ tale che:

$$
n = \dfrac{k \, (k - 1)}{2}
$$

scrivere la funzione ruby `triagolare` che accetta un intero e restituisce un booleano `true` se il numero e' triangolare, `falso` altrimenti.

```ruby
def triangolare(n)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/triangolare" | relative_url }})

___

## Triangolo

Si scriva una funzione `classifica` che dati 3 argomenti (numeri) che corrispondono alle lunghezze dei 3 lati di un triangolo ritorna un numero intero con le seguenti regole:

 * -1 se i dati non sono corretti, ad esempio lati 0 o negativi
 * 0  se il triangolo e' scaleno
 * 1  se il triangolo e' isoscele
 * 2  se il triangolo e' equilatero
 * 3  se il triangolo e' rettangolo

attenzione se il triangolo e' sia rettangolo che isoscele vale il numero piu alto cioe' si ritorna 3.

```ruby
def classifica(a, b, c)
  # completare
end
```

[Vai alla soluzione]({{ "/solutions/triangolo" | relative_url }})
