---
layout: post
title:  "Tipo di dato: Numeric e Array"
date:   2015-02-26 10:00:00
categories: post
permalink: /lecture6b/
lecture: "Lezione 6 (parte 1)"
visible: 1
excerpt: "<p>Analizziamo <b>Numeric</b>, ovvero la classe dei numeri interi <b>Fixnum</b> e la classe dei numeri reali <b>Float</b>. Vedremo poi la classe degli <b>Array</b>, che sono molto comode nel campo della analisi numerica.</p>"
---

Analizziamo **Numeric**, ovvero la classe dei numeri interi **Fixnum** e la classe dei numeri reali **Float**. Vedremo poi la classe degli **Array**, che sono molto comode nel campo della analisi numerica.

* table of contents.
{:toc}

## Numeric

La classe **Numeric** è una classe di base che definisce in forma generale i metodi e gli attributi che avranno le sottoclassi di quali **Fixnum**, **Bignum**, e **Float**. È all'interno di questa classe che sono definiti gli operatori di comparazione, così come moltissimi altri metodi utili ad effettuare la manipolazione di oggetti numerici.

Per accedere ai metodi della classe, in Ruby, dato un oggetto, è necessario utilizzare la cosidetta **dot-notation**.

Data una variabile `num`, istanza di un oggetto della classe Numeric, possiamo ricordare una serie di metodi utili:

 * `num.abs`: ritorna il valore assoluto.
 * `num.ceil`: ritorna il numero intero più piccolo possibile che sia maggiore o uguale del numero in `num`.
 * `num.floor`: ritorna il numero intero più grande possibile che sia minore o uguale al numero in `num`.
 * `num.nonzero?`: ritorna `num`se il numero contenuto in `num`è diverso da 0, altrimenti ritorna `nil`.

Un metodo molto importante, che non fa parte realmente della classe Numeric, ma della classe Object, è il metodo `num.to_s`, che trasforma il contenuto di `num`in una stringa (sequenza di caratteri), in modo tale che possa essere assegnato a schermo.

### Fixnum e Bignum

La sottoclasse principe di Numeric è la classe **Fixnum**, che definisce i numeri interi. Possiamo dichiarare una variabile come un Fixnum:

```ruby
num = 5
```

> In **generale**, la definizione di un numero intero si ottiene mediante l'assegnazione ad una variabile di un numero intero (ovvero un numero che non ha specificato il separatore delle cifre decimali, che è rappresentato da un punto). Quella variabile diventa automaticamente una istanza della classe Fixnum, e risponde a tutte le **regole della aritmetica tra interi**.

Il range dei numeri Fixnum si estende fino ad una determinata dimensione, definita dalla configurazione dell'interprete. Quando si sfora questo range, automaticamente l'interprete trasforma il Fixnum in un Bignum, che dal punto di vista del tempo di esecuzione del codice è molto meno efficiente. A livello di interfaccia (**polimorfismo**) le due classi sono del tutto uguali.

Definita la variabile, `num`, questa ha la possibilità di utilizzare i metodi tipici definiti nella classe Fixnum e nella classe Numeric. Per poter accedere ai metodi, ancora una volta faremo uso della **dot-notation**. De sequito un po' di metodi utili:

 * `num.next` e  `num.succ`: ritornano il numero `num + 1`.
 * `num.zero?`: ritorna vero se `num == 0`.
 * `num.odd?`: ritorna vero se il numero è dispari
 * `num.even?`: ritorna vero se il numero
 * `num.to_f`: trasfomra il numero intero in un Float.
 * `num.upto(n)`: esegue il codice che segue `n - num` volte (_è un Block, vedremo negli Array come si usa_).

Nel caso dei numeri interi, **la divisione per zero ritorna un errore**.

### Float

Un numero reale si definisce per mezzo della assegnazione ad una variabile di un numero con valore decimale o in notazione scientifica. Quella variabile diventa una istanza della classe Float, e risponde a tutte le regole della aritmetica tra numeri reali.

```ruby
num    = 1234.56   # Numero reale
num_ns = 1.23456e3 # Notaz. scientifica

# Nella notazione scientifica la
# lettera "e" (o "E") rappresenta
# l'esponente in base 10, quindi il numero
# precedente è in realtà
# 1.23456 * (10**3)

# Proviamo che siano uguali
puts (num == num_ns)
```

Il range della classe Fixnum si estende da $$-\infty$$ a $$+\infty$$. Infatti **nel caso di una divisione per 0, il risultato è** $$\infty$$. Ruby rappresenta l'infinito mediante una costante: `Infinity`. Qualche volta può capitare che operazioni portino a risultati non rappresentabili o che possano essere considerati come non numeri. In quel caso il risultato potrebbe essere **NaN (Not a Number)**.

Vediamo nel pratico questo cosa significa, soprattutto nell'utilizzo della divisione:

```ruby
#!/usr/bin/env ruby

# Aritmetica degli interi
a_int = 12
b_int = 60

c_int = a_int / b_int

# Aritmetica dei float
a_flt = 12.0
b_flt = 60.0

c_flt = a_flt / b_flt

d_flt = 0.0
e_flt = a_flt / d_flt

# ATTENZIONE! NON FIDATEVI DEL RISULTATO DEL BROWSER
# PROVATE LO SCRIPT IN UN VERO INTERPRETE!!
puts "c (intero) -> #{c_int}"
puts "C (float)  -> #{c_flt}"
puts "E (float)  -> #{e_flt}"
```

Non fidatevi del risultato del browser (che è solo un emulatore), ma valutate il codice precedente in un vero interprete Ruby. Vedrete immediatamente come `c_int != c_flt`!! Questo perchè nella divisione tra interi la operazione di divisione continua a riportare come risultato un valore intero (come è giusto che sia).

Alcuni metodi tipici della classe Float sono:

 * `num.infinite?`: ritorna vero se `num == Infinity`
 * `num.round(n)`: ritorna una rappresentazione arrotondata ad `n` cifre significative il numero `num`
 * `num.truncate(n)`: tronca ad `n` cifre dopo il separatore decimale il numero `num`

## Array

Un **Array** è una struttura abbastanza rispetto a quelle che abbiamo appena visto. Un Array può essere visto come un contenitore che contiene una serie di variabili, **ordinate** e raggiungibili per mezzo di un **indice a base** 0.

<div style="width:100%; text-align:center;">
  <img src="http://upload.wikimedia.org/wikipedia/it/d/d4/Vettoremapam.JPG" style="width:25%" class="thumbsvm">
  <br><i>Esempio grafico di Array (tratto da: Wikipedia)</i>
</div>

Un array può essere definito o inizializzato come vuoto, oppure contenente dei valori. In Ruby (e non in moltissimi altri linguaggi), gli Array hanno le seguenti caratteristiche:

 1. i dati contenute nelle singole caselline del vettore non devono essere necessariamente tutti della stessa classe.
 2. l'indice comincia da 0, e si specifica tra parentesi quadre: `ary[index]`
 3. non è necessario definire a priori la **dimensione** dell'Array (ovvero il numero delle caselline dentro le quali possimao inserire dati). La diensione dell'Array può quindi variare dinamicamente.
 4. Gli array possono essere multidimensionali, ovvero un Array può contenere un altro Array. Spesso ci si riferisce a questo tipo di array come Matrici.

Facciamo alcuni esempi di utilizzo, e proviamo direttamente le caratteristiche enunciate:

```ruby
#!/usr/bin/env ruby

# Definizione di un Array vuoto
# esistono 2 modi per definirlo:

ary = Array.new

# oppure

ary = []

# Definizione di un Array popolato
# Testiamo anche la caratteristica 1, 2 e 4:

ary = [ 1, 1.123, [1, 2, 3] ]

puts "Elemento 0: #{ary[0]}"
puts "Elemento 2: #{ary[2]}"
puts "Elemento 2 dell'elemtno 2: #{ary[2][2]}"

# Ridefianiamo l'Array come un vettore di Float

ary = [1.2, 6.43, 5.32, 2.35, 8.96]

# la dimensione di questo Array è:

puts "Prima: #{ary.size}"

# e possiamo inserire un nuovo elemento alla fine
# dell'Array

ary << 1.56

puts "Dopo: #{ary.size}"

# Per accedere rapidamente all'ultimo elemento: indice -1

puts "Ultimo elemento: #{ary[-1]}"

```

Per poter accedere all'ultimo elemento dell'Array molto spesso il metodo più semplice è usare un indice negativo -1.

### Attraversare gli Array

L'attraversmento di un array è una serie struttura di controllo (ciclo `for` o altro) che attravera letteralmente ogni elemento di un Array. Facciamo un esempio di questa tipologia di codice:

```ruby
#!/usr/bin/env ruby

# Attraversare gli array

ary = [1.2, 6.43, 5.32, 2.35, 8.96]
puts "Il vettore ha #{ary.size} elementi"

# Mediante ciclo for

puts "\nMediante For"
for i in (0...ary.size)
  puts "Elemento #{i} -> #{ary[i]}"
end

# Mediante ciclo while o until

puts "\nMediante while"
i = 0
while i < ary.size
  puts "Elemento #{i} -> #{ary[i]}"
  i += 1
end

puts "\nMediante until"
i = 0
until i == ary.size
  puts "Elemento #{i} -> #{ary[i]}"
  i += 1
end

```

### I **Blocks** (versione adatta ai minori)

Esistono dei metodi avanzati per la esecuzione di codice specifico. Tali metodi sono definiti **Blocks**, perchè permettono di eseguire blocchi di codice (compresi tra le parole `do` e `end`), come se fossero una funzione definita localmente. Tali blocchi di codici sono passati come **argomento di una funzione**.

I blocchi sono molto utili, e forse anche una delle features più interessanti del linguaggio Ruby, anche se spesso difficili da comprendere, soprattutto se si è alle rime armi. In questo caso vediamo un blocco (e i suoi 2 modi di scriverlo) che attraversa un array e ci mette a disposizione l'elemento corrente.

Forse, vedere come si scrive e cosa fa ci aiuterà a capire meglio di cosa stiamo parlando:

```ruby
#!/usr/bin/env ruby

ary = [1.2, 6.43, 5.32, 2.35, 8.96]

# Utilizziamo il metodo each che
# prende come argomento un Block che
# esegue delle operazioni sui singoli
# elementi

puts "MODO 1"
ary.each do |ary_element|
  # Funzioni dentro al blocco
  puts "Il doppio di #{ary_element} e\' #{ary_element * 2}"
end

puts "MODO 2"
ary.each { |el|
  # Funzioni dentro al blocco
  puts "Il doppio di #{el} e\' #{el * 2}"
}
```

Il codice dentro al blocco in questo caso ha a disposizione la variabile `ary_element`, e ad ogni ciclo di esecuzione questa variabile cambia e diventa l'elemento successivo nell'Array.
Il codice dentro al blocco stampa a schermo il valore dell'elemento corrente, poi in seguito calcola il doppio e lo stampa a schermo. Le variabili nel blocco, specificate **tra i caratteri `|...|`** e **separati da una virgola** possono avere il nome che desideriamo, non necessariamente devono chiamarsi come nell'esempio!

Esiste un secondo modo, equivalente, che al posto delle keywords `do |variable| ... end` usa le parentesi graffe `{ |variable| ... }`.

> Ricordatevi cosa sono.... si tende ad usarli **spesso**!

### Array e metodi

Esistono decine di metodi per la classe Array, molti dei quali utilissimi. Esistono metodi per ordinarne il contenuto (come `ary.sort`) o metodi per ottenere il massimo o il minimo (`ary.max` e `ary.min`). Vi consiglio caldamente di fare spesso riferimento alla documentazione ufficiale della [classe Array][aryclass]

> Per comodità, alcuni metodi hanno spesso degli **alias**, ovvero possono essere chiamati in più modi diversi, ma eseguono lo stesso codice. Un esempio è il metodo che ritorna la dimensione di un Array: `ary.length == ary.size`

Proviamo ad implementare un paio di metodi della classe giusto per imparare un po' ad utilizzare il linguaggio...

#### Trova il massimo

Troviamo il massimo facendo uso di `while`, di un blocco e poi testiamo il metodo della libreria.

```ruby
#!/usr/bin/env ruby

# inizializza vettore
ary = [4,-2,3,-23,189,46,343,12]

# Trova il massimo di un vettore (while)
l = ary.length # lunghezza dell'Array
m = ary[0]     # valore del primo elemento
i = 1          # indice

# La variabile m contiene il valore massimo
# trovato
while i < l do

  # se il valore ary[i] 'nuovo' è piu grande del
  # valore vecchio m, mi salva questo nuovo
  # valore in m = ary[i]
  m = ary[i] if m < ary[i]

  i = i + 1
end
puts "WHILE - Il massimo è: #{m}"

# Trova il massimo di un vettore (block)
m = ary[0]
ary.each { |el|
  m = el if m < el
}
puts "BLOCK - Il massimo è: #{m}"

# Trova il massimo (metodo classe Array)
puts "Usando metodo Ruby: #{ary.max}"
```

Appare evidente il perchè della esistenza dei blocchi. Il codice richiede molte meno inizializzazioni e molte meno particolarità rispetto al caso precedente. Ovviamente, il metodo più rapido dal punto di vista dello scrittura effettiva di codice, rimane il metodo di classe, che spesso è da preferire in quanto (solitamente) ottimizzato.

_Cosa succede quando chiamiamo il blocco?_ Se potessimo "srotolare" il codice di each al suo interno troveremo qualcosa del genere:

```
funzione each(blocco)
  prendi array
  per i in 0...dimensione(array)
    esegui blocco(array[i])
  fine
fine
```

dove `blocco` è il codice Ruby che noi scriviamo di tra `do ... end`.

#### Bubble Sort

L'algoritmo di ordinamento (_sorting_) buble sort è un metodo iterativo per l'ordinamento di una sequenza di dati. Fondamentalmente ci spostiamo lungo il vettore comparando due a due gli elementi, procedendo in una direzione stabilita. Se il numero a sinistra è maggiore di quella a destra, i due elementi vengono scambiati di posizione.

<div style="width:100%; text-align:center;">
  <img src="http://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif" style="width:30%" class="thumbsvm">
  <br><i>Esempio grafico ddi algoritmo BubbleSort (tratto da: Wikipedia)</i>
</div>

Dopo la prima iterazione il numero massimo si trova sempre in ultima posizione, quindi al ciclo successivo si riducono le iterazioni di una unità. Effettuati un numero di cicli tali da coprire tutto l'Array, il vettore finale risulterà ordinato.

> Ovviamente stiamo ordinando un Array coerente, in cui tutti gli elementi appartengono alla stessa classe (nel nostro caso Numeric).

Una prima implementazione fa uso del ciclo `for`. In seguito ne vediamo un altro con un metodo della classe Fixnum, che accetta un blocco come argomento.

```ruby
#!/usr/bin/env ruby

# inizializza vettore
ary = [4,-2,3,-23,189,46,343,12]

# Attraversiamo tutto l'Array
for l in 1...ary.length do
  # Attraversiamo tutto l'Array fino
  # alla posizione (ary.length - l)
  for i in (0...(ary.length - l))
    # Controlliamo se l'elemento successivo è
    # maggiore
    if ary[i] > ary[i.next]
      # Scambiamo i due elementi
      ary[i], ary[i.next] = ary[i.next], ary[i]    
    end
  end
end

puts "Array ordinato: #{ary}"
```

Il codice appena visto è funzionante, ma cerchiamo di capire meglio cosa fa aumentando l'output prodotto dallo script in modo da capire in modo approfondito la esecuzione effettiva:

```ruby
#!/usr/bin/env ruby

# inizializza vettore
ary = [4,-2,3,-23,189,46,343,12]

# Attraversiamo tutto l'Array
for l in 1...ary.length do
  puts "Ciclo #{l} :: ary = #{ary}"
  puts "-- Sorting ary[0...#{ary.length - l}] = #{ary.slice(0,ary.length-l)}"
  # Attraversiamo tutto l'Array fino
  # alla posizione (ary.length - l)
  for i in (0...(ary.length - l))
    print "---- i = #{i} :: "
    # Controlliamo se l'elemento successivo è
    # maggiore
    if ary[i] > ary[i.next]
      # Scambiamo i due elementi
      print " swapping (ary[#{i}] ⇋ ary[#{i.next}] = #{ary[i]} ⇋ #{ary[i.next]})"
      ary[i], ary[i.next] = ary[i.next], ary[i]
    end
    print "\n"
  end
 end

 puts "Array ordinato: #{ary}"
```

Ad ogni ciclo for attraversiamo un sotto-Array, più piccolo di uno. L'output del programma è abbastanza auto-esplicativo. Il metodo `ary.slice(idx_start, idx_end)` seleziona una sottoparte dell'array.

Possiamo implementarlo utilizzando gli altri metodi messi a disposizione. Ad esempio, il metodo `each` e il metodo `upto`:

```ruby
#!/usr/bin/env ruby

# inizializza vettore
ary = [4,-2,3,-23,189,46,343,12]

1.upto(ary.length) { |l|
  ary.slice(0, ary.length - l).each_index { |i|
    if ary[i] > ary[i.next]
      # Scambiamo i due elementi
      ary[i], ary[i.next] = ary[i.next], ary[i]
    end
  }
}

puts "Array ordinato: #{ary}"
```

[aryclass]: http://ruby-doc.org//core-2.2.0/Array.html
[interp]: /ncalc/lecture2/#la-interpolazione-delle-stringhe
[escape]: http://it.wikipedia.org/wiki/Carattere_di_controllo
