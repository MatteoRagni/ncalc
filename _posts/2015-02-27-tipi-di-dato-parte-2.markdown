---
layout: post
title:  "Tipo di dato: String, Symbol e Hash"
date:   2015-02-27 10:00:00
categories: post
permalink: /lecture6c/
lecture: "Lezione 6 (parte 2)"
visible: 1
excerpt: "<p>Scopriamo la classe <b>String</b>. In seguito passeremo alla analisi del tipo <b>Hash</b>, una sorta di array ordinato per mezzo di chiavi piuttosto che per mezzo di un indice numerico. Nell'arco della lezione citiamo la classe <b>Symbol</b></p>"
---

Scopriamo la classe **String**. In seguito passeremo alla analisi del tipo **Hash**, una sorta di array ordinato per mezzo di chiavi piuttosto che per mezzo di un indice numerico. Nell'arco della lezione citiamo la classe **Symbol**

* table of contents.
{:toc}

## String

La classe delle stringhe è una classe molto simile alla classe Array. Entrambe rappresentano un vettore di elementi ordinato, ma nel caso della classe String, questo vettore contiene unicamente caratteri. La manipolazione di stringhe e la loro gestione è molto utile a livello di generazione di output e interfaccia uomo macchina, ma anche per moltissime altre applicazioni, quali la codificazione dei dati o la autenticazione.

Un esempio classico è l'hostname e il sistema DNS. L'hostname è il nome che si dà ad un computer, sotto forma di stringa, i cui elementi (domini di livello) sono separati da punti. L'hostname non è altro che una codifica dell'indirizzo IP di un computer in un nome che sia facilmente ricordabile. Il compito dei server DNS (come quelli di Google) è mantenere aggiornata una tabella che associ ad ogni indirizzo IP un hostname univoco, in modo tale che, quando digitate nel browser ad esempio `unitn.bitbucket.org`, in realtà vi state collegando all'indirizzo IP `131.103.20.167` (decisamente più difficile da ricordare).

Esistono tre modi (molti di più in realtà, ma vediamo i primi tre intanto...) per costruire una stringa:

```ruby
#!/usr/bin/env ruby

stringa_1 = String.new("Costruita nel modo classico - scomodo")
stringa_2 = 'Stringa ad apice singolo'
stringa_3 = "Stringa ad apice doppio!"

puts stringa_1
puts stringa_2
puts stringa_3

puts "Interpolazione"

stringa_4 = 'singolo apice: 2 + 2 = #{2 + 2}'
stringa_5 = "doppio apice: 2 + 2 = #{2 + 2}"

puts stringa_4
puts stringa_5
```

### Interpolazione e formato

La differenza tra la stringa costruita ad apice singolo e quella costruita ad apice doppio risiede tutta nella **interpolazione**, ovver nella possibilità di inserire dei costrutti (`#{ ... }`), che fanno capire all'interprete che il contenuto deve essere valutato e sostituito con una rappresentazione a stringa (abbimao già parlato della interpolazione [qui][interp]). Quindi riassumendo:

 * **singoli apici** `' ... '` sono utilizzati per costruire stringhe statiche, che non interpolano il contenuto di `#{}`
 * **doppi apici** `" ... "` sono utilizzatiper costruire stringhe dinamiche che interpolano il contenuto di `#{}`

#### Il formato

Per formato si intende lo stile con il quale un numero/dato deve essere stampato a schermo. Esiste una vera e propria sintassi per definire il formato, e Ruby ha una sintassi del tutto compatibile a quella del C. In generale il formato si esplicita nel modo seguente:

```
"stringa formato" % [lista, di, variabili]
```

con una sintassi uguale a quella del Python, la stringa di formato, tra apici singoli o doppi è specificata a sinistra del carattere `%`, mentre la lista di variabili che dovranno essere sostituite devono essere separate da una virgola. Questa sintassi **può (deve) essere usata all'interno delle parentesi graffe della interpolazione**. La sintassi che definisce il formato è (per quello che serve a noi) la seguente:

 * **numeri interi**: `%d`. Se si volesse specificare la dimensione del campo: `%Xd` con X numero intero dimensione del campo. Scrivendo `%0Xd` i caratteri del campo non usati sono riempiti di zeri.
 * **numeri floating point**: `%f`. Segue le specifiche di campo degli interi. Se si volesse specificare il numero di cifre dopo la virgola: `%.Yf` con Y numero intero.
 * **numeri in notazione scientifica**: `%e` segue le specifiche dei numeri floating point (i.e. `%X.Ye`)
 * **sequenze di caratteri**: `%s`

Un esempio d'uso potrebbe essere il seguente:

```ruby
#!/usr/bin/env ruby
# Questo script non è supportato dall'interprete nel
# browser! Provatelo con un interprete vero!

integer        = 98765
floating_point = 1.2345
stringa        = "hello!"

formato = ("%s
  \t questo è intero: %10d
  \t questo è floating: %2.2f
  \t questo è scientifico: %3.3e" % [stringa, integer,
                      floating_point, floating_point])

puts formato

```

Nella stringa di formato abbiamo usato alcuni caratteri particolari, detti **caratteri di escaping**. Questi caratteri sostituiscono alcune funzioni particolari, ad esempio:

 * `\t`: inserisce un carattere di tabulazione (quello che è chiamato di solito _il tasto tab_)
 * `\n`: inserisce un carattere di fine linea (quello che solitamente si inserisce con il _tasto invio o return_)

Esistono altri [caratteri di escape][escape] che coprono una serie molto ampia di task, anche se ormai hanno in parte perso il loro valore (erano nati ai tempi delle schede perforate e delle macchine da scrivere!).

### Metodi di string

Anche String, come Array, ha una quantità enorme di metodi utili che permettono di svolgere rapidamente molti task complicati. Ovviamente, non possiamo elencare tutti i metodi della classe: cerchiamo alora qualche trucco per vedere rapidamente, anche durante l'esame, quali sono i metodi a disposizione dell'interprete. Usiamo un metodo della classe **Objects** e un metodo della classe **Array**:

```ruby
#!/usr/bin/env ruby

String.methods.sort.each{ |method|
  puts method
}

# methods: restituisce un Array di metodi
# sort: ordina l'Array

# quello che otteniamo è una stampa a schermo
# di tutti i metodi. Vale per tutte le Classi
# e tutte le istanze di classe.

```

Alcuni metodi che citiamo:

 * `str.length`: ritorna il numero di caratteri in una stringa
 * `str.downcase`: trasforma tutti i caratteri di una stringa in caratteri minuscoli
 * `str.upcase`: trasforma tutti i caratteri di una stringa in caratteri maiuscoli
 * `str1 + str2` e `str1 << str2`: concatena due stringhe. La prima non effettua assegnazione, la seconda effettua assegnazione su `str1`
 * `str.to_i`: trasforma la stringa in un intero
 * `str.to_f`: trasforma la stringa in un floating point

```ruby
#!/usr/bin/env ruby

str1 = "StringaInCamelCase"
str2 = "stringa_in_snake_case"

puts "Lunghezza stringa:"
puts "str1 -> #{str1.length}"
puts "str2 -> #{str2.length}"

# downcase e upcase, seza assegnazione
puts "Stringa downcase: #{str1.downcase}"
puts "Stringa upcase: #{str2.upcase}"

# Concatenazione senza assegnamento
puts "concateno: #{str1 + str2}"

# Concatenazione con assegnamento
str1 << str2
puts "concatenata: #{str1}"

# to floating point e to integer
puts (5.1 + "1.2".to_f)
puts (2 + "2".to_i)

# Ultimo trucchetto! Stringa per numero intero!
puts "Ciao" * 5

```

A questo punto, non dovete far altro che divertirvi con le stringhe!

## Symbols e Hash

### Symbols

Il concetto di simbolo è qualcosa che disorienta i più. Noi non cercheremo l'approccio formale nella spiegazione del concetto di dimbolo, cercheremo di mantenerci piuttosto sull'approccio di chi i simboli li deve usare, e usare in modo rapido e utile.

**Riconoscere un simbolo** è abbastanza semplice. Solitamente i **simboli sono una seria di caratteri preceduti da `:`**. Quando nella serie di caratteri che identifica il simbolo ci sono degli spazi, la stringa di caratteri che identifica il simbolo è racchiuso tra apici singoli o apici doppi. In generale:

```
:simbolo
:"questo è un simbolo"
:'anche questo'
```

A livello di codice, al'atto della programmazione, è possibile scrivere direttamente un simbolo: `:simbolo`. Quando si vuole definire un simbolo durante l'esecuzione di un programma è necessario utilizzare il metodo **definito nella classe String** (quindi non lo trovate in altre classi) `str.to_sym`. Questo metodo trasforma direttamente la stringa, in un simbolo.

**I simboli sono immutabili**, perchè all'atto pratico, la prima volta che vengono invocati, l'interprete provvede ad assegnargli un **numero intero che li identifica in modo univoco**, come una specie di ID. **Tralasciando eventuali parallelismi con altri linguaggi di programmazione, e come sono implementati in Ruby i simboli** (argomenti che possono interessare ai veterani della programmazione ruby, e non a noi _burbe spelacchiate_) ci limitiamo ad affermare che:

> **I simboli sono degli elementi del linguaggio di programmazione Ruby che hanno sia una rappresentazione in stringa (preceduta dal carattere `:`) che una rappresentazione numerica (intera) assegnata automaticamente dall'interprete (`__id__`)

```ruby
#!/usr/bin/env ruby

# Cercare di eseguire una assegnazione
# in un simbolo si traduce in un errore
# L'interprete ha già assegnato qualcosa
# al simbolo

#:simbolo = "pippo"


# è possibile assegnare ad una variabile un simbolo,
# ed è una cosa che capita molto spesso!
pippo = :simbolo
# o anche trasformare una stringa in un simbolo
pippo = "simbolo".to_sym
puts pippo

puts :simbolo
puts :simbolo.to_s

# in una precedente versione del linguaggio
# era possibile vedere che numero era stato assegnato
# al simbolo mediante
#
# puts :simbolo.to_i
#
# adesso non è più possibile, ma si può sempre visualizzare
# l'ID, che è comune a tutti gli oggetti di ruby
puts :simbolo.__id__

```

I simboli hanno un valore estremamente importante nella programmazione in Ruby. Possono essere utilizzati per rappresentare metodi di classe, variabili, etc. Noi li utilizzeremo come **chiavi per accedere agli elementi degli Hash**.

### Hash

Gli Hash, a volte chiamati anche Dizionari (se siete programmatori Python avete capito di cosa stiamo parlando) sono dei **contenitori non-ordinati** di dati.

Come gli Array, possono contenere diversi elementi al loro interno, che possono essere acceduti per mezzo di un indice.

A differenza degli Array, **gli elementi contenuti all'interno degli Hash** non sono ordinati e identificati per mezzo di un indicie a valore crescente, ma **sono identificati per mezzo di chiavi (keys) univoche**. Solitamente le chiavi utilizzate negli Hash, per motivi puramente prestazionali, sono dei simboli (potrebbero essere anche stringhe).

Proviamo a costruire un Hash che descrive il "contatto" di una persona: nome, cognome, numero di telefono e indirizzo mail:

```ruby
#!/usr/bin/env ruby

persona = {
  :nome    => "Mario",
  :cognome => "Rossi",
  :telefono => "+39 02 123987",
  :mail => "mario.rossi@mail.com"
}

puts "#{persona[:nome]} #{persona[:cognome]}"
puts "- tel: #{persona[:telefono]}"
puts "- mail: #{persona[:mail]}"

```

Così come per una Array, per accedere ad un elemento usavamo le `[ ]` dentro le quali specificavamo l'indice, adesso usiamo nuovamente le `[ ]` e mettiamo al loro interno la chiave. Diventa molto più facile definire strutture complesse, nelle quali accedere senza dover ricordarsi a memoria la posizione di ogni elemento, ma semplicemtne la chiave.

Possiamo mettere insieme la potenza delle due classi, Array e Hash, per costruire un prototipo di agenda personalizzata (scrivendo un paio di funzioni ad hoc, e sfruttando un blocco di codice ;) ):

```ruby
#!/usr/bin/env ruby

# funzione stampa_indirizzo
# input:
#  persona: hash che specifica una persona
#           con il campo :indirizzo
#  stringa: stringa contenente tutto l'indirizzo,
#           pronta per essere stampata
# Genera una stringa contenente l'indirizzo da stampare
# dato l'hash di una persona in ingresso. Se di una persona
# non esiste la chiave :indirizzo, ritorna una stringa vuota
def stampa_indirizzo(persona)
  # Se esiste la chiave :indirizzo...
  if persona[:indirizzo] then
    # ci facciamo una piccola scorciatoia ;)
    e = persona[:indirizzo]
    stringa = "#{e[:via]}, #{e[:numero]}\n#{e[:citta]} (#{e[:prov]}), #{e[:cap]}\n#{e[:stato]}"
  else
    stringa = "Sconosciuto"
  end
  return stringa
end

# funzione stampa_persona
# input:
#  persona: hash che specifica una persona
#  stringa: stringa contenente tutte le informazioni,
#           pronta per essere stampata
# Genera una stringa contenente tutti i dati di una persona,
# pronta per essere stampata
def stampa_persona(persona)
  stringa = ""
  # Stampiamo un bel header formattato!
  stringa << "#{persona[:nome]} #{persona[:cognome]} "
  stringa << "*" * (40 - (persona[:nome].length + persona[:cognome].length + 2))
  stringa << "\n"

  # Se esiste il numero di telefono lo stampiamo
  stringa << "* Tel:  "
  if persona[:tel] then
    stringa << "#{persona[:tel]}\n"
  else
    stringa << "Sconosciuto\n"
  end

  # Se esiste l'indirizzo mail lo stampiamo
  stringa << "* Mail: "
  if persona[:mail] then
    stringa << "#{persona[:mail]}\n"
  else
    stringa << "Sconosciuto\n"
  end

  stringa << "* Indirizzo:\n"
  stringa << stampa_indirizzo(persona)

  # Concludiamo con un bel footer!
  stringa << "\n"
  stringa << "*" * 40
end

# Definiamo la nostra rubrica
rubrica = [{
   :nome    => "Carlo",
   :cognome => "Rossi",
   :tel     => 1231231230,
   :mail    => 'carlo.rossi@mail.it',
   :indirizzo => {
     :via    => "Cavour",
     :numero => "10",
     :citta  => "Trento",
     :cap    => "38122",
     :prov   => "TN",
     :stato  => "Italia"
   }},
  {
   :nome    => "Stefan",
   :cognome => "Benz",
   :mail    => 'ste123@mail.de'
   },
  {
   :nome    => "Maria",
   :cognome => "Callas",
   :tel     => 444001231,
   :mail    => 'callas@mail.com'
  }
]

# Non necessariamente la nostra rubrica deve essere completa
# di tutti i campi.... di qualcuno non conosciamo
# l'indirizzo, mentre di altri sappiamo tutto. Vediamo
# vome visualizzare tutte queste informazioni!

# Questo è il codice principale del programma (main)
# si occupa della stampa a schermo di tutte le info
# di tutte le persone in rubrica

rubrica.each { |pers|
  puts stampa_persona pers
  puts
}
```

> Un esercizio **difficilissimo**: provate ad aggiungere qualche persona all'elenco, e scrivete un metodo che sia in grado di ordinare in modo crescente le persone all'interno dell'elenco, e poi stampare a schermo la rubrica ordinata.

[aryclass]: http://ruby-doc.org//core-2.2.0/Array.html
[interp]: /ncalc/lecture2/#la-interpolazione-delle-stringhe
[escape]: http://it.wikipedia.org/wiki/Carattere_di_controllo
