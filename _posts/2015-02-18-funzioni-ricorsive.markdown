---
layout: post
title:  "Ricorsione, condizione, cicli"
date:   2015-02-18 14:00:00
categories: post
permalink: /lecture5/
lecture: "Lezione 5"
visible: 1
excerpt: "<p>In questa lezione andiamo a vedere un utilizzo avanzato delle funzioni, approfondire le istruzioni condizionali e imparare ad utilizzare i cicli classici. Nella ultima parte della lezione metteremo insieme queste conoscenze per scrivere uno script che sia in grado di eseguire la operazione di fattoriale.</p>"
---

In questa lezione andiamo a vedere un utilizzo avanzato delle funzioni, approfondire le istruzioni condizionali e imparare ad utilizzare i cicli classici. Nella ultima parte della lezione metteremo insieme queste conoscenze per scrivere uno script che sia in grado di eseguire la operazione di fattoriale.

* table of contents.
{:toc}

## Funzioni ricorsive

Prima di partire con questo argomento, è necessario aver ben chiaro il sognificato di funzione, come utilizzarla e come scriverla (bene). Nel caso questo non sia chiaro, vi consiglio caldamente di rivedere la lezione precedente, nella quale abbiamo introdotto le funzioni e gli operatori.

Una funzione è detta ricorsiva quando è in grado di **richiamare se stessa**. Affinchè questo sia possibile (ed abbia anche un senso logico), le funzioni ricorsive sono caratterizzate da questi tre elementi peculiari:

 1. una struttura condizionale che determini il flusso di esecuzione della funzione
 2. una istruzione che richiama la funzione stessa in uno dei rami della istruzione condizionale
 3. una istruzione che ritorna un valore ed esce dalla funzione ricorsiva nell'altro ramo della istruzione condizionale
 
Tenendo a mente queste tre caratteristiche, diventa facile costruire una funzione ricorsiva.

### Il fattoriale

La funzione ricorsiva di elezione nell'abito della disciplna informatica è la _funzione fattoriale_ $$n!$$. Nel caso non fosse noto la funzione fattoriale e' definita come segue:

$$
n! = 1\cdot2\cdot3...\cdot(n-2)\cdot(n-1)\cdot n
$$

con $$n\in\mathbb{N}^{+}$$. Appare abbastanza evidente dala definizione precedente:

$$
n! = n\cdot(n-1)!
$$

e inoltre possiamo identificare una identità limite:

$$
1! = 1
$$

Tiriamo alcune conclusioni:

 * il fattoriale di un numero e' sempre uguale al prodotto del numero per il fattoriale dello stesso numero decrementato di 1.
 * il fattoriale di 1 è sempre 1.
 
e usiamo tali conclusioni per definire una funzione fattoriale in Ruby, sostenendo che:
 
 1. la istruzione condizionale controlla che `n` sia maggiore di 1
 2. quando la condizione è vera ritorna `n` moltiplicato al fattoriale di `n - 1`
 3. quando la istruzione è falsa, e quindi `n == 1`, allore ritorna 1

```ruby
#!/usr/bin/env ruby

# Funzione fattoriale
# input
#  n - numero intero positivo di cui effettuare n!
# return
#  fn - fattoriale di n
def fattoriale(n)
  # 1. Istruzione condizionale
  if n > 1 then
    # 2. chiamata ricorsiva
    return n * fattoriale(n - 1)
  else
    # 3. uscita dalla chiamata ricorsiva
    return 1
  end
end

# proviamo la funzione...
n = 10
puts "#{n}! = #{fattoriale(n)}"
```

Sicuramente la ppresenza di due istruzioni `return` può essere fuorviante (_ma come?? una funzione ritorna due volte?_) ma in verità la risposta si trova nella presenza della istruzione condizionale `if`. Come vedremo più avanti, il costrutto condizionale inibisce completamente la esecuzione del codice, quindi solamente un `return` è attivato nell'arco di chiamata di una funzione.

Indaghiamo un pò più a fondo per cercare di capire con precisione che cosa sta succedendo durante una chiamata ricorsiva... dove entriamo? con che valori? e cosa abbiamo in uscita? Possiamo rispondere a queste domande utilizzando quello che abbiamo visto fino ad ora, sfruttando la funzione `puts`.

Utilizziamo anche il prossimo esempio per introdurre un nuovo concetto delle funzioni: la **inizializzazione automatica degli argomenti**.

```ruby
# funzione fatt
# input
#  n - numero intero di cui eseguire n!
#  i - indicatore iterazione
# return
#  res - fattoriale di n
# calcola il fattoriale con una chiamata ricorsiva
# ad ogni chiamata, inserisce un indice di 
# ricorsione, ovvero indica quante chiamate
# ci sono state prima della attuale
def fatt(n, i=0)
  puts ("-" * i) + "#{i}: Entra fatt(#{n})" 
  res = 1 
  res = n * fatt(n-1, i+1) if n > 1 
  puts ("-" * i) + "#{i}: Esce fatt(#{n}) = #{res}" 
  return res 
end
 
n  = 10 
fn = fatt(n) 
puts "Fattoriale #{n} = #{fn}\n"
```

Spieghiamo questo codice linea per linea:

 * La definizione della funzione questa volta esegue una inizializzazione automatica. Se la chiamata alla funzione (come alla linea 20) è effettuata senza specificare l'argomento `i`, allora a `i` è inizializzato automaticamente al valore 0.
 * Le chiamate stampano quando la funzione entra alla linea 12 (inserendo un numero di spazi bianchi pari all'indice di ricorsione `i`) e quando la funzione esce alla linea 15, subito prima di ritornare il valore.
 * Se `n == 1`, la funzione ritorna 1, altrimenti ritorna `n * fatt(n - 1, i + 1)`, passando quindi l'indice di ricorsione (alla linea 14), incrementato di 1.
 
Provate ora ad inserire il codice in uno script e vedere che cosa succede. A questo punto, dovrebbe essere chiaro anche a livello grafico come operano le funzioni ricorsive!
 
## Le istruzioni condizionali e i cicli

Abbiamo potuto constatare come un elemento semplice come `if` possa essere utilizzato per ottenere comportamente molto interessanti, come nel fattoriale. Questo non è l'unico costrutto condizionale che ci viene messo a disposizione dalla sintassi di Ruby. Possiamo distinguere due categorie principali di istruzioni per controllare il flusso di esecuzione del nostro programma:

 * **costruzioni condizionali**: diramano la esecuzione del programma (eseguono certe istruzioni invece di altre) sulla base di una condizione logica (`true` o `false`).
 * **cicli**: eseguono molte volte una data sequenza di codice fino a soddisfare una determinata condizione logica
 
Andiamo a vedere nel dettaglio queste due famiglie di istruzioni.

### Istruzioni condizionali

Le istruzioni condizionali **diramano la esecuzione del codice sulla base di una espressione più o meno complessa che rappresenta una scelta logica**. Esistono molteplici forme di espressioni, in generale costruite facendo uso degli operatori di comparazione definiti nella lezione precedente.

#### `if...then...end`

La prima forma che andiamo a vedere per prima è la più semplice. Traducendo in italiano la logica del costrutto

```
if condizione then
  # execute
end

se la condizione è vera allora
  esegui questo codice
```

Anche se praticamente auto-esplicativo, è necessario porre l'accento sul fatto che il codice che verrà eseguito se la condizione risulta vera è quello racchiuso tra le keyworkd `then` e `end`. Queste due keyword indicano all'interprete dove comincia e dove termina il codice soggetto a controllo condizionale. 

> Mai scambiare l'ultimo `end` come uscita dalla esecuzione del programma (che si effettua con `exit`)

#### `if...then...else...end`

Forma leggermente più complessa della precedente, permette di eseguire del codice alternativo nel caso la condizione risulti falsa. Anche in questo caso possiamo vedere una traduzione in linguaggio naturale del costrutto condizionale:

```
if condizione then
  # execute this
else
  # execute that
end

se la condizione è vera allora
  esegui questo codice
altrimenti
  esegui questo codice alternativo
```


#### Operatore ternario

L'operatore ternario, comune a moltissimi linguaggi di programmazione, è una forma contratta per la espressione di un costrutto condizionale. La sintassi è la seguente:

```
risultato = (condizione) ? (esegue se true) : (esegue se false)
```

Possiamo vedere direttamente una applicazione di tale forma contratta alla funzione fattoriale precedente, fornendone una versione più compatta:

```ruby
#!/usr/bin/env ruby

# Funzione fattoriale
# input
#  n - numero intero positivo di cui effettuare n!
# return
#  fn - fattoriale di n
def fattoriale(n)
  # 1. Istruzione condizionale
  if n > 1 then
    # 2. chiamata ricorsiva
    return n * fattoriale(n - 1)
  else
    # 3. uscita dalla chiamata ricorsiva
    return 1
  end
end

# Funzione fattoriale2
# input
#  n - numero intero positivo di cui effettuare n!
# return
#  fn - fattoriale di n
# esegue il fattoriale sfruttando 
# l'operatore ternario
def fattoriale2(n)
  #      if      then                     else
  return ( n > 1 ? n * fattoriale2(n - 1) : 1 )
end

# proviamo le funzioni...
n = 10
puts "!#{n} = #{fattoriale(n)} = #{fattoriale2(n)}"
```

#### `if` postfisso e `unless`

Avrete ormai notato che la trasformazione da codice Ruby a lingua parlata è relativamente semplice (soprattutto se comparato con altri linguaggi). Questo perchè nella definizione della sintassi si è posto come obbiettivo quello di **mantenersi nei limiti del possibile vicini al linguaggio parlato**. Per fare ciò, sono stati introdotte alcune keyword peculiari di questo linguaggio: parliamo dell'`if` postfisso e dell'`until`.

L'`if` postfisso è una istruzione condizionale posta alla fine di una riga di codice (post-fissa) in grado di inibirne la esecuzione. In linguaggio naturale:

```
codice_da_eseguire if condizione

codice_da_eseguire se la condizione è vera 
```

Questo costrutto è del tutto equivalente ad un `if ... then ... end`:

```ruby
#!/usr/bin/env ruby

condizione = true

puts "la condizione è vera" if condizione

if condizione then
  puts "la condizione è vera"
end
```

In alternativa ad `if` mette a disposizione la keyword `unless` che effattua la valutazione di un codice solo se la condizione risulta essere falsa.

```
unless condizione then
  # codice da eseguire
end

se condizione è falsa allora
  codice da eseguire
```

`unless` può essere usato come postfisso, insieme ad `else`, etc.

#### `if ... then ... elsif ... else ... end`

Cosa succede quando ci sono diversi casi da prendere in considerazione (ad esempio comparando un valore con diversi riferimenti)? Abbiamo la possibilità di utilizzare la keyword `elsif`, per effettuare una ulteriore comparazione. Si possono inserire un numero indefinito di `elsif`, sulla base di quante comparazioni siano necessari:

```
if condizione == termine_1 then
  # codice da eseguire 1
elsif condizione == termine_2 then
  # codice da eseguire 2
elsif condizione == termine_3 then
  # codice da eseguire 3
else
  # codice da eseguire 4
end

se condizione è uguale a termine_1 allora
  esegui codice 1
altrimenti se condizione è uguale a termine_2 allora
  esegui codice 2
altrimenti se condizione è uguale a termine_3 allora
  esegui codice 3
altrimenti
  esegui codice 4 
```

L'utilizzo di questa tipologia può semplificarci molto la vita, come nel caso di questa definizione a tratti:

```ruby
#!/usr/bin/env ruby
# Copyright - Bertolazzi, Bort - 2014
# si, questa l'ho copiata. u.u

# funzione funz
# input
#  x - valore numerico
# return
#  y - output della funzione a tratti
# Esempio con if nidificati
def funz(x)
  if x <= 1 then
    return 1
  else
    if x <= 2 then
      return 2
    else
      if x <= 4 then
        return 3
      else
        if x <= 6 then
          return 4
        else
          if x <= 8 then
            return 5
          else
            return 6
          end
        end
      end
    end
  end
end

# funzione funz2
# input
#  x - valore numerico
# return
#  y - output della funzione a tratti
# Esempio con elsif
def funz2(x)
  if x <= 1 then
    return 1
  elsif x <= 2 then
    return 2
  elsif x <= 4 then
    return 3
  elsif x <= 6 then
    return 4
  elsif x <= 8 then
    return 5
  else
    return 6
  end
end
# un attimino meglio, no? :)
 
# testiamo le due funzioni...
x = 3
puts "x = #{x}, funz(x) = #{funz(x)}, funz2(x) = #{funz2(x)}"
```

#### `case ... when`

Questa è una alternativa a `elseif` quando si effettuano comparazioni di uguaglianza:

```
case condizione
  when termine_1
    # esegui codice 1
  when termine_2
    # esegui codice 2
  when termine_3
    # esegui codice 3
  else
    # esegui codice 4
end

quando la codizione
  è uguale a termine_1 allora
    esegui codice 1
  è uguale a termine_2 allora
    esegui codice 2
  è uguale a termine_3 allora
    esegui codice 3
  altrimenti
	esegui codice 4
```

Poichè `case` ritorna l'ultimo valore valutato è possibile utilizzarlo per effettuare delle assegnazioni. Proviamo a ridefinire l'esempio precedente:

```ruby
#!/usr/bin/env ruby

# funzione funz3
# input
#  x - valore numerico
# return
#  y - output della funzione a tratti
# Esempio con case
def funz3(x)
  return case
    when (x <= 1) 
	  1
	when (x <= 2) 
	  2
	when (x <= 4) 
	  3
	when (x <= 6) 
	  4
	when (x <= 8) 
	  5
	else 
	  6
  end
end

x = 3
puts "x = #{x}, funz(x) = #{funz3(x)}"
```

Che funziona perchè il valore ritornato è la prima condizione vera trovata dall'interprete.
### Cicli iterativi

Un ciclo è una sequenza di istruzioni eseguita in maniera ripetitiva fino al verificarsi di una determinata condizione. Quando tale condizione si verifica, l'interprete esce dal ciclo e continua con la esecuzione delle linee successive dello script.

Nei nostri script potremo trovare tipicamente due tipologie di ciclo:
 
 * cicli definiti a livello di sintassi
 * cicli come metodi di particolari tipologie di variabili (più precisamente metodi di _istanze di classi_), come `Array` o `Range`

Affrontiamo adesso la prima tipologia di cicli.

#### `while` e `until`

Tipico di quasi tutti i linguaggi di programmazione, il ciclo `while` esegue una determinata sequenza di istruzioni fino a quando una determinata condizione da vera diventa falsa. Il cambio logico provoca la uscita dal ciclo. Rendiamo in linguaggio naturale il funzionamento del ciclo:

```
while condizione
  # esegui questo
end
# continua

fino a quando condizione rimane vera
  esegui questo
se condizione diventa falsa
continua
```

Il ciclo `until` opera esattamente allo stesso modo, ma con il principio logico invertito. Il ciclo continua ad essere eseguito fino a quando la condizione da falsa diventa vera.


```
until condizione
  # esegui questo
end
# continua

fino a quando condizione rimane falsa
  esegui questo
se condizione diventa vera
continua
```

#### `for`

Il ciclo `for` è un tipo di ciclo basato su una **variabile contatore** che cambia ad ogni iterazione del ciclo. La struttura di for permette di definire anche gli estremi e il passo entro cui la variabile contatore cambia. Questo è un tipico esempio in cui gli estremi sono indicati facendo uso di un **operatore di range**:

```
for contatore in inizio..fine
  # esegui codice dipendente da contatore
end

per contatore che va da inizio a fine
  esegui questo in funzione di contatore
```

#### Modificare i cicli

Esistono due keyword, comune ai cicli sopra elencati, che permettono di modificare la esecuzione del ciclo (soprattutto insieme a costrutti condizionali come l'`if` postfisso):

 * `next`: permette di interrompere l'iterazione di ciclo attuale e passare alla iterazione successiva.
 * `break`: rompe il ciclo immediatamente e ne esce, evitando di eseguire ulteriori iterazioni.
 
Facciamo un paio di esempi che sfruttano il ciclo `for` e queste due keyword:

```ruby
#!/usr/bin/env ruby

for i in 1..10
  next if i == 5
  break if i == 8
  puts "iterazione = #{i}"
end
```

#### Fattoriale e cicli

Possiamo usare i cicli per costruire una funzione fattoriale che non sia ricorsiva.

> Come esercizio, provate a costruire la funzione fattoriale utilizzando il ciclo `for` e gli operatori di range.
