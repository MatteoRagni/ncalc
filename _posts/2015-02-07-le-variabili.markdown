---
layout: post
title:  "Le variabili"
date:   2015-02-11 16:00:00
categories: post
permalink: /lecture3/
lecture: "Lezione 3"
visible: 1
excerpt: "<p>Argomento di questa lezione saranno i contesti e le variabili. Vedremo le varie tipologie di variabili e come possono essere utilizzate all'interno di uno script. Infine, ci concentreremo sui messaggi di errore e come imparare a leggerli per eseguire in modo efficiente il debug di uno script.</p>"
---

Argomento di questa lezione saranno i contesti e le variabili. Vedremo le varie tipologie di variabili e come possono essere utilizzate all'interno di uno script. Infine, ci concentreremo sui messaggi di errore e come imparare a leggerli per eseguire in modo efficiente il debug di uno script.

* table of contents.
{:toc}

## Contesti in Ruby

I contesti all'interno di uno script `Ruby` sono porzioni di codice racchiuse tra parole chiave `begin ... end`. Sono contesti di codice anche i blocchi (racchiusi tra `do ... end` o tra parentesi graffe) e eventuali cicli (`for`, `while`, etc.) e blocchi di istruzioni condizionali (`if`, `case`, etc.)

In seguito analizzeremo del dettaglio e vedremo una applicazione pratica di tali costrutti del codice.

Possono essere considerate sezioni anche i moduli, le classi e le istruzioni che definiscono una funzione (`def ... end`)

## Le variabili in Ruby

`Ruby` e' un linguaggio di scripting interpretato, nel quale le variabili sono **identificatori privi di tipo e e privi di dimensioni definita**, se non si considerano i limiti di memoria del computer sul quale e' eseguito l'interprete.

Astraendo il concetto, immaginate una variabile come una scatole con una etichetta: la etichetta e' il nome della variabile (_possibilmente univoco_), lo spazio all'interno garantisce di conservare delle informazioni: il _contenuto della variabile_.

> La prima operazione di assegnazione di una variabile si chiama anche **inizializzazione**.

> La operazione di assegnazione prevede la presenza di un operatore di assegnazione (in Ruby `=`), un elemento che puo' contenere un valore (variabile) posto a sinistra dell'operatore di assegnazione, detto **l-value, left-value o left hand side (lhs)**, e una espressione posta a destra dell'operatore di assegnazione, detta **r-value, right-value o right hand side (rhs)**.

#### Scope di una variabile

Argomento particolare e' lo **scope di una variabile**, detta anche visibilita' di una variabile.

Il **contesto** in cui una variabile e' inizializzata ne definisce la visibilita' che tale variabile ha all'interno del codice. Una classe inizializzata in un determinato contesto potrebbe non essere visibile in un altro (quando una variabile non e' visibile non e' possibile accedere al suo contenuto).

### Tipi di variabili

Esistono diverse tipologie di variabili, e il tipo e' riconosciuto sulla base della notazione usata per scrivere la "etichetta". Diamo uno sguardo alle tipologie di variabili:

 * variabili locali
 * costanti
 * variabili globali
 * variabili di istanza di una classe
 * variabili di classe
 * pseudo variabili e variabili predefinite

Concentriamoci sulle prime tre tipologie di variabili, tralasciando la analisi delle altre ad un momento successivo.

#### Variabili locali

Le variabili locali sono le variabili il cui nome comincia per caratteri minuscoli `a-z` o con un underscore `_`. In generale il nome di una variabile locale dovrebbe essere scritto in [**snake_case**][snakecase]. La assegnazione di una variabile locale si effettua utilizzando _l'operatore di assegnazione_ `=`. Le variabili locali possono contenere numeri, stringhe ed in generale istanze di oggetti.

Un po' di esempi sull'utilizzo delle variabili, e alcune semplici operazioni con esse:

Resta evidente che le variabili non sono **tipizzate**, ovvero non e' necessario definire a priori che tipo di valore contengono. Un altra cosa da tenere in considerazione e' che le variabili possono essere ridefinite in qualunque punto del codice, cosi' come dopo aver definito inizialmente la variabile `a = 123` nel prossimo script alla linea 7, la abbiamo ridefinita `a = "pippo"` alla linea 19, senza generare alcun tipo di errore o warning.

Tentare di accedere ad una variabile non inizializzata genera un errore di tipo `NameError`. Spesso, una variabile inizializzata in un determinato contesto, _per motivi di visibilita'_ potrebbe essere considerata non definita dall'interprete.

> In `Ruby` una variabile locale inizializzata e' visibile da tutti i contesti contenuti nel contesto in cui e' stata definita, ma non e' visibile dai contesti che contengono il contesto in cui e' definita.

#### Costanti

Le costanti sono variabili che non possono essere riassegnate una volta inizializzate. La etichetta di una  costante comincia sempre con una lettera maiuscola.

> La classi, che vedremo in seguito, sono sempre delle costanti

> Quanto si cerca di ri-definire il valore di una costante, l'interprete genera un messaggio di avviso (un `Warning`).

#### Esempio di script

> Provate a creare uno script con il codice seguente, e rimuovete i commenti alle linee di codice che generano errore

```ruby
#!/usr/bin/env ruby

# Le seguenti righe sono un esempio di assegnazione di
# valori numerici. Tali valori possono ad esempio essere
# sommati mediante l' operatore +, e il risultato salvato
# in una variabile
a = 123
b = 11

c = a + b
# Possiamo usare puts per visualizzare il contenuto della
# variabile c
puts c

# Stessa assegnazione con una variabile di tipo diverso:
# in questo caso due stringhe sono assegnate alle variabili
# a e b, e concatenate mediante l'operatore di +. Il risultato
# concatenato e' salvato nella variabile c
a = "pippo"
b = "pluto"

c = a + b
# Ancora una volta, stampiamo a schermo il risultato mediante puts
puts c

# L'utilizzo dei doppi apici " o dei singoli apici ' definisce
# una stringa. All'interno degli apici il carattere # non e'
# considerato carattere di commento
a = "12"
b = "45"
c = a + b
puts c

# Attenzione! L'utilizzo di operatori come + con variabili di tipo
# diverso puo' portare alla generazione di un errore! Vediamone
# due casi:
a = "pippo"
b = 12
#c = b + a   # -> TypeError: no implicit conversion of Fixnum into String
#puts c

a = "pippo"
b = 12
#c = a + b   # -> TypeError: no implicit conversion of Fixnum into String
#puts c

# Purtroppo non e' possibile visualizzare gli errori all'interno
# dell'interprete nel browser, per questo le linee che generano un
# errore sono commentate...

Costante = "Questa e' una costante"
puts Costante

# Riassegnare un valore ad una costante genera un messaggio di
# warning.

Costante = "questa linea genera un warning"

```

#### Variabili globali

Le variabili globali sono variabili che cominciano con il carattere `$`. Il termine globali e' in relazione alla loro visibilita': queste variabili sono visibili all'interno di tutto l'ambiente dell'interprete, indipendentemente dal contesto in cui ci si trova. Alcune di queste variabili sono predefinite in automatico dall'interprete all'avvio, come la variabile `$0` che contiene il nome dello script in esecuzione (questa e' anche una variabile _predefinita_)

```ruby
#!/usr/bin/env ruby

# Esempio di variabile globale
$variabile = "Questa e' una variabile globale"
# Esempio di variabile locale
variabile  = "questa e' una variabile locale"

# Esempi di costante
Costante = " mentre "

# Esempio di utilizzo di diverse tipologie di variabili e costanti insieme
puts $variabile + Costante + variabile
```

## Errori

Abbiamo avuto il primo incontro con gli errori in uno degli script precedenti. I messaggi di errore sono una preziosa risorsa nella fase di scrittura di un codice, e saperli leggere e' utile alla rapida risoluzione di eventuali problemi.

Andiamo a vedere due possibili messaggi di errore che si sono presentati nell'arco di questo documento:

#### Errore nell'uso degli operatori

Immaginiamo di eseguire il primo script con nome `test.rb`.

```
test.rb:39:in `+': String can't be coerced into Fixnum (TypeError)
	from test.rb:39:in `<main>'
```

Il messaggio di errore ci fornisce una serie di informazioni molto importanti:

 * Posizione dell'errore nello script: `test.rb:39`.
 Questa stringa ci indica che l'errore si trova nel file `test.rb`, alla linea 39. Il numero di linea tiene conto della presenza di eventuali commenti. Quindi L'errore si trova nella istruzione `c = b + a` della linea 39.
 * Il tipo di errore: `TypeError`
 * La natura dell'errore: `'+': String can't be coerced into Fixnum (TypeError)`. Questo errore ci indica in modo abbastanza chiaro una violazione nell'uso dell'operatore `+`. Alla linea 39, si sta cercando di sommare il tipo `Fixnum` (che identifica un valore numerico) contenuto nella variabile `b`, con il tipo `String`, contenuto nella variabile `a`. Questo ovviamente non e' possibile.

 In modo del tutto equivalente, commentando la linea 39, si ottiene:
 ```
test.rb:44:in `+': no implicit conversion of Fixnum into String (TypeError)
	from test.rb:44:in `<main>
```

Questa volta il messaggio e' alla linea 44 del file `test.rb`. A tentativo di assegnazione invertito, otteniamo un tipo di errore invertito. Questa volta l'interprete riporta la sua incapacita' di trasformare (in modo implicito, ovvero senza una istruzione specifica) un numero intero in una stringa. Anche se l'interprete e' in grado di trasformare `123 → "123"`, l'errore e' generato per garantire la **coerenza nel codice**.

La struttura dei messaggi di errore e' coerente tra le diverse tipologie di errore.

#### Avviso nella ridefinizione delle costanti

Se andassimo a ridefinire una costante, otteniamo il seguente messaggio di avviso:

```
test.rb:57: warning: already initialized constant Costante
test.rb:51: warning: previous definition of Costante was here
```

Il messaggio di avviso e' autoesplicativo: La costante `Costante` sta subendo una ridefinizione alla linea 57, mentre era gia' stata inizializzata alla linea 51. Attenzione la ridefinizione di una costante, per motivi di coerenza porta alla variazione del contenuto della costante. Ad esempio:

```ruby
#!/usr/bin/env ruby
# Attenzione, questo codice non puo' essere eseguito dall'interprete
# browser.

Costante = 1
puts "Costante vale: " + Costante
Costante = 2
puts "Costante vale: " + Costante

```

[snakecase]: http://en.wikipedia.org/wiki/Snake_case
