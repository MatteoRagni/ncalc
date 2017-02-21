---
layout: post
title:  "I primi passi in Ruby"
date:   2015-02-10 16:00:00
categories: post
permalink: /lecture2/
lecture: "Lezione 2"
visible: 1
excerpt: "<p>Creiamo il nostro primo script e rendiamolo eseguibile. Prima di continuare, cerchiamo di capire anche l'importanza dello stile nella scrittura del codice.</p>"
---

Creiamo il nostro primo script e rendiamolo eseguibile. Prima di continuare, cerchiamo di capire anche l'importanza dello stile nella scrittura del codice.

* table of contents.
{:toc}

## Hello, World!

Creiamo un primo script, molto classico. Apriamo l'editor di testo (`Accessori → Editor`) e scriviamo al suo interno:

```ruby
puts "Hello, World!"
```

e salviamo il file in `/home/$USER/Develop/ex_1.rb`. Probabilmente sara' necessario creare la directory `Develop` nella vostra `$HOME`.

Apriamo un terminale e proviamo ad eseguire questo script.

```bash
$ cd $HOME/Develop
$ ruby ex_1.rb
```

A schermo dovrebbe apparire la scritta **Hello, World!**. Vuol dire che il primo script funziona! A questo punto iniziamo ad utilizzarlo come base per future evoluzioni.

### Rendere lo script eseguibile

Rendere uno script eseguibile significa aggiungere delle informazioni e modificare i suoi attributi in modo tale che il sistema sia in grado di eseguirlo in maniera autonoma.

In pratica:

 * istruire il sistema su quale interprete utilizzare
 * istruire il sistema del fatto che il nostro script puo' essere interpretato.

**Il primo step si completa definendo la cosidetta [shebang][shebang]**, una istruzione formattata che deve essere inserita nella primissima riga dello script. Modifichiamo `ex_1.rb` come segue:

```ruby
#!/usr/bin/env ruby

puts "Hello, World!"
```

con la riga `#!/usr/bin/env ruby` stiamo informando il sistema di avviare l'interprete ruby ogni volta che si esegue lo script.

**Abbiamo visto nella [lezione precedente][lecture1] come rendere lo script eseguibile**, utilizzando il terminale:

```bash
$ chmod +x ex_1.rb
```

Siamo pronti a provare il nostro script eseguibile, digitando nel terminale:

```bash
$ ./ex_1.rb
```

> Dobbiamo mettere sempre mettere un riferimento di path per i nostri script. In questo caso, trovandoci nella directory che lo contiene, abbiamo usato `./`. Senza la path il sistema risponderebbe con un triste: `command not found`.

### La funzione `puts` e `print`

`puts` e' una funzione che **stampa a schermo il suo argomento** e va a capo.

E' _**convenzione del linguaggio**_, quando si chiama una funzione con un solo argomento, non racchiudere tale argomento tra parentesi tonde (come avviene invece con funzioni con piu' argomenti). Sarebbe comunque lecito scrivere:

```ruby
#!/usr/bin/env ruby

puts("Hello, World!")
```

Equivalente di `puts` e' la funzione `print`, che stampa a schermo il proprio argomento, ma _non_ aggiunge il carattere di fine linea. Per ottenere uno script equivalente utilizzando questa funzione:

```ruby
#!/usr/bin/env ruby

print "Hello, World!\n"

# \n rappresenta il carattere di fine linea
```

#### La interpolazione delle stringhe

Nome difficile per concetto semplice. Le funzioni `puts` e `print` sfruttano una proprietà delle stringhe chiamata interpolazione per poter inserire delle variabii all'interno delle stringhe che andranno a stampare. La interpolazione si effettua utilizzando la sintassi `#{ ... }` sostituendo ai puntino una espressione qualsiasi in linguaggio Ruby. Utilizzeremo questo metodo più vote in diversi script. In questo modo è possibile costruire delle stringhe formattate a nostro piacere.

> Solo le stringhe tra doppi apici `" ... "` supportano la interpolazione. Le stringhe tra appici singoli `' ... '` non eseguono questa operazione. A livello di efficienza nella programmazione del proprio codice, se non è necessario utilizzare la interpolazione, si dovrebbe fare uso di stringhe a singoli apici, al fine di incrementare la efficienza in esecuzione.

> È possibile formattare numeri, utilizzando la [notazione di formato del codice `C`][formato]. La notazione in ruby è: `'format' % var`, ad esempio: `var = 1.2345678; puts '%.2f' % var`, molto simile a quella del python. **Nulla vieta di mettere la stringa di formato dentro una interpolazione!**

### I commenti

I commenti sono una parte fondamentale del codice, che vi permettono di "prendere appunti" al fine di descrivere a livello funzionale il vostro codice. L'interprete ignora i commenti e quindi **non hanno alcun peso dal punto di vista computazionale**, ma un **altissimo peso dal punto di vista operativo**.

La presenza di commenti facilita lo sviluppo (soprattutto di codici complessi) e permettono ad altri programmatori di capire rapidamente quali sono gli obbiettivi dell'algoritmo che avete scritto.

In `Ruby` esistono due tipi di commenti:

 * **commenti a linea singola**: tutto quello che si trova dopo il carattere `#` e' considerato commento e ignorato dall'interprete.  _Fa eccezione_ la presenza di questo carattere in una **stringa**
 * **commenti a linea multipla**: sono commenti che sono contenuti tra le parole chiave `=begin` e `=end`, che devono trovarsi a inizio riga. Questa tipologia di commento dovrebbe essere utilizzata solo all'inizio dello script.

```ruby
#!/usr/bin/env ruby

# questo e' un commento a linea singola

puts "Hello, World!" # altro commento
puts "# non e' un commento"

=begin

questo
e
un
commento

puts "non posso essere stampato"

=end

puts "ok?"
```

## Lo stile

Concludiamo questa prima lezione parlando di un argomento tanto leggero quanto importante: **stile e indentazione nella programmazione**. Imparare a scrivere un codice formattato correttamente riduce in modo sostanzioso i tempi di sviluppo, aumentando la leggibilita' del codice, rendendo chiaro anche a colpo d'occhio come sara' eseguito il codice.

Ecco alcune regole di stile:

 * _usate due spazi per la indentazione dei blocchi_ (soft-indent)
 * _non usate `;` alla fine dei comandi_; come corollario _cercate di inserire una espressione per linea_.
 * _limitate le linee a 80 caratteri_
 * _omettete le parentesi in funzioni che non hanno argomenti_ e _non usare parentesi per funzioni a singolo argomento_
 * _utilizzate gli spazi attorno gli operatori, dopo virgole, punti e virgola e `{}`_; come eccezione, l'operatore elevamento a potenza `**` e gli operatori unari.
 * _Evitate i commenti `=begin/=end`_, se non nella prefazione dello script.

In generale:

#### E' IMPERATIVO ESSERE ORDINATI E SEGUIRE LO STILE VISTO A LEZIONE

[shebang]: http://en.wikipedia.org/wiki/Shebang_%28Unix%29
[lecture1]: /lecture1/
[formato]: http://it.wikipedia.org/wiki/Format_string
