---
layout: post
title:  "Blocchi, File, Errori"
date:   2015-04-20 10:00:00
categories: post
permalink: /lecture7/
lecture: "Lezione 7"
visible: 1
excerpt: "<p>Riprendiamo i blocchi e vediamo il loro utilizzo in modo leggermente più approfondito. Esploriamo la classe <b>File</b>, per leggere e scrivere i risultati dei nostri algoritmi. Introduciamo il problema della programmazione robusta, con la classe delle <b>Exceptions</b>.</p>"
---

Riprendiamo i blocchi e vediamo il loro utilizzo in modo leggermente più approfondito. Esploriamo la classe `File`, per leggere e scrivere i risultati dei nostri algoritmi. Introduciamo il problema della programmazione robusta, con la classe delle `Exceptions`.

* table of contents.
{:toc}

## I blocchi (versione per adulti)

Non è la prima volta che incontriamo i **blocchi** lungo la nostra strada. I blocchi sono segmenti di codice racchiuso tra parentesi o graffe o tra le keyword `do ... end`, che possono essere associati al principio di _fornire all'utente la possibilità di personalizzare funzioni complesse_. Alcuni esempi possono essere:

 * l'attraversamento degli `Array`
 * scrittura/lettura di dati detro i file
 * particolari tipi di cicli
 * fornire funzionalità personalizzate di vario tipo
 * etc.

### La classe `Proc`
Le linee di codice, se scritte in modo intelligente, possono essere inserite tra parentesi e salvate sotto forma di variabile. La variabile conterrà un blocco di codice che risulta essere un oggetto di tipo `Proc`. Facciamo un esempio tipico. Supponiamo di avere un programma che tira un dado, che deve essere reso in quache modo internazionale, ovvero sia in grado di gestire una interfaccia a schermo in lingue diverse (ad esempio inglese e italiano):

```ruby
#!/usr/bin/env ruby

# Configurazioni
LANG = "IT"

# Interfaccia
# number contiene le informazioni sul lancio del dado
number = 0
# continue è true se dobbiamo effettuare un altro lancio
continue = true

case LANG
when "IT"
	interface = Proc.new {
    puts "Il risultato è: #{number}. Provare ancora? [S/N]"
	  input = gets.chomp
    input == "S"
  }
when "EN"
  interface = Proc.new {
    puts "The result is: #{number}. Try again? [Y/N]"
	  input = gets.chomp
    input == "Y"
  }
end

while continue
	number = Random.rand(1..6)
	continue = interface.call
end
```

Il codice qua sopra non è semplicissimo, ma vediamo di analizzarlo. In primo luogo definiamo nelle configurazioni che tipo di interfaccia vogliamo, se in italiano **"IT"** o in inglese **"EN"**. Scelta la lingua di riferimento, viene dichiarata una variabile di tipo `Proc` che si chiama `interface`, che rappresenta l'interfaccia tra programma e utente. Le due interfacce a livello implementativo sono uguali (stampano a schermo il risultato, comparano l'input dell'utente con una lettera, al fine di ritornare vero se l'utente vuole continuare, falso se non vuole continuare). La differenza risiede nelle stringhe utilizzate all'interno di questi metodi.

Nella esecuzione del programma (ciclo `while`), la esecuzione continua fintanto che la nostra `interface` continua a ritornare il valore `true`. Per eseguire effettivamente il contenuto della `Proc` dobbiamo utilizzare il metodo `call`, che ne esegue il contenuto.

### La keyword `yield`
Cambiamo punto di vista e pensiamo ad una funzione che debba essere personalizzata, partendo dall'esempio abbastanza semplice dell'attraversamento di un `Array`, come viene effettuato dal metodo `each`. Proviamo ad implementare una nostra versione di `each` e metterla a confronto con quella di Ruby:

```ruby
ary = (1..10).to_a.shuffle

# Utilizzo del blocco EACH
# con do |...| ... end
ary.each do |elemento|
  puts "Elemento = #{elemento}"
end

# con { |...| ... }
ary.each { |elemento|
  puts "Elemento = #{elemento}"
}

# utilizzo del blocco EACH_WITH_INDEX
ary.each_with_index { |elemento, indice|
  puts "Elemento[#{indice}] = #{elemento}"
}

# Costruire una nostra funzione each
def mio_each(ary)
  for i in 0...ary.size
    yield ary[i]
  end
end

# Costruire una nostra funzione each with index
def mio_each_with_index(ary)
  for i in 0...ary.size
    yield ary[i], i
  end
end

# Usare le nostre funzioni
mio_each(ary) do |e|
  puts "Elemento = #{e}"
end

mio_each_with_index(ary) do |e, i|
  puts "Elemento[#{i}] = #{e}"
end
```

Nella funzione `mio_each` appare la keyword `yield`. Tale keyword rapresenta il punto nella funzione in cui si entrerà nel blocco definito dall'utente, per eseguire le linee di codiece defintio dall'utente (in questo caso la stampa a schermo del contenuto della variabile). Argomento della keyword, le variabli che rientreranno nel blocco tra le "pipe" (quindi l'elemento dell'Array).

Possiamo utilizzare `yield` anche per farci ritornare un valore dall'utente (che come nell'esempio di `interface` è rappresentato dall'ultimo valore valutato dalle parentesi graffe, una comparazione che ritorna `true` o `false`). Un esempio classico è l'utilizzo dei blocchi come metodo per implementare un integratore!

Supponiamo di avere una funzione qualsiasi, $$f(x)$$, da integrare nell'intervallo $$[a,b]$$. La formula di integrazione può essere approssimata come una somma di area di trapezi (integratore a trapezi: datevi una occhiata alla teoria del corso) nella forma:

$$
\int_{a}^{b}{f(x)dx} \approx \dfrac{1}{2} ~\Delta x~ \sum_{s=0}^{n-1}{f(s\Delta x + a) + f((s+1) \Delta x + a)}
$$

dove $$\Delta x = (b-a)/n$$. Nulla di più semplice implementarlo in Ruby!

```ruby
# Integratore con metodo trapezi

def integratore(a, b, n)

  delta = (b - a)/(n.to_f)
  # F rappresenta la primitiva
  primitive_F = 0.0

  for s in 0...n do
    # calcoliamo f_A = f(s*Delta x + a)
    f_A = yield(s*delta + a)
    # calcoliamo f_B = f((s + 1)*Delta X + a)
    f_B = yield((s + 1)*delta + a)

    dF = 0.5 * (f_A + f_B) * delta
    primitive_F += dF
  end

  return primitive_F
end


# Calcoliamo la integrazione con il
# nostro integratore
risultato = integratore(0,(Math::PI/6.0),1000) { |x|
  # Scriviamo qui la funzione integranda
  Math::E**(Math::sin(x))*((Math::cos(x))**2 - Math::sin(x))
}

puts "Risultato della integrazione: #{risultato}"


# => Risultato della integrazione: 0.4278344470997674
```

L'integrazione numerica presenta sempre un errore. Con il nostro integratore numerico, la integrazione ci ritorna come risultato: `0.4278344470997674`. Se provassimo ad integrare analiticamente la funzione $$e^{\sin(x)}\left(\cos^2 x - \sin x \right)$$:

$$
\int_{0}^{\frac{\pi}{6}}{e^{\sin(x)}\left(\cos^2 x - \sin x \right)~dx} = \left.\cos(x) e^{\sin x}\right\rfloor_{0}^{\frac{\pi}{6}} = \dfrac{\sqrt{3~e}}{2} - 1
$$

che vale $$\approx 0.427834504186071253$$. Stiamo quindi integrando con un errore dello $$1.33\cdot10^{-5} \%\%$$.

> Esercizio difficilissimo: provate ad implementare un vostro integratore a step adattativo!

#### Ottimizzazione dell'integratore

Andando a farsi due conti in più, l'ottimizzatore che abbiamo scritto può essere estremamente ottimizzato facendo uso di alcuni semplici trucchetti: partendo dalla sommatoria che abbiamo definito in precedenza:

$$
\begin{array}{rcl}
\int_{a}^{b}{f(x)~dx} & \approx & \sum_{s=0}^{n-1}{\dfrac{1}{2} \left(f(x_{s}) + f((x_{s+1})\right) \Delta x} \\
& = & \dfrac{1}{2} \Delta x \sum_{s=0}^{n-1}{f(x_{s}) + f(x_{s+1})} \\
\end{array}
$$

per $$x_s = \Delta x~s + a$$; espandendo la sommatoria, si ha:

$$
\begin{array}{rcl}
\sum_{s=0}^{n-1}{f(x_{s}) + f(x_{s+1})} & = & (f(x_0) + f(x_1)) + (f(x_1) + f(x_2)) + \dots + \\
 & & + (f(x_{n-2} + f(x_{n-1})) + (f(x_{n-1}) + f(x_n)) \\
& = & f(x_0) + f(x_n) + \sum_{s=1}^{n-1}{2f(x_s)} \\
& = & f(a) + f(b) + 2 \sum_{s=1}^{n-1}{f(x_s)}
\end{array}
$$

Quindi possiamo ridurre il calcolo dell'integrale a:

$$
\int_{a}^{b}{f(x)~dx} = \left(\dfrac{1}{2}\left( f(a) + f(b) \right) + \sum_{s=1}^{n-1}{f(x_s)} \right) \Delta x
$$

che è molto efficiente dal punto di vista dell'implementazione:

```ruby
def integratore(a, b, n)

  delta = (b - a)/(n.to_f)
  # F rappresenta la primitiva
  primitive_F = 0.0

  primitive_F += 0.5 * yield(a)
  primitive_F += 0.5 * yield(b)

  for s in 1...n do
    # calcoliamo f(x_s)
    primitive_F += yield(s*delta + a)
  end

  return primitive_F * delta
end

risultato = integratore(0,(Math::PI/6.0),1000) { |x|
  # Scriviamo qui la funzione integranda
  Math::E**(Math::sin(x))*((Math::cos(x))**2 - Math::sin(x))
}

puts "Risultato della integrazione: #{risultato}"
# => Risultato della integrazione: 0.4278344470997673
```

## I File
I file, la loro lettura e la loro scrittura, sono solitamente un concetto ostico per i neofiti della programmazione. Molto spesso non ci si approccia al file con il giusto spirito. L'utilizzo dei file da parte di un programma è solitamente molto diverso rispetto a quello di una persona. Pensate ad un file di testo, lo aprite con il vostro editor e usate il mouse per portarvi esattamente nella posizione che volete.

Per un programma non è così. Il file è un **flusso** o **stream** di dati che si attraversa. Non esiste una posizione assoluta, ma solo una posizione relativa all'inizio del file. Ruby mette a disposizione delle funzioni di alto livello per la gestione di File, che per nostra comodità sono visti come sequenza di righe (quindi stringhe interrotte dal carattere nuova linea `\n`).

Uno dei tipi più famosi di file risulta essere il CSV (o a volte TSV, che significa COMMA/TAB SEPARATED VALUE). Questo tipo di file è utilizzato per memorizzare tabelle di dati. Le singole righe sono separate dal carattere di fine riga `\n`, mentre le singole colonne sono separate dalla virgola (comma) `,` a dal carattere di tabulazione `\t`. Ancora oggi risulta essere uno degli standard de facto come formato di salvataggio di dati semplici, a causa della sua facile leggibilità e altissima compatibilità.

Nei File dobbiamo tenere in considerazione 3 cose:

 * attributi di accesso al file (in lettura, scritture, o lettura e scrittura?)
 * encoding esterno del file
 * encoding interno del file

Abbiamo visto nella primissima lezione che cosa sono gli attributi di un file. Anche durante la apertura di un file in Ruby, dobbiamo specificare in che modo vogliamo accedere a tale file. Per quanto riguarda l'encoding, vi basti sapere che tutti i caratteri diversi dai 256 caratteri fondamentali della tabella ASCII (cercatela su Google se non sapete cos'è), sono espressi per mezzo di codici. La codifica di tale codice è chiamata encoding. Se un vostro collega russo vi invia un file creato sul suo computer che ha un determinato encoding, probabilmente è una buona idea specificare come encoding esterno quello relativo al sistema del vostro collega, mentre come coding interno quello relativo al vostro sistema, in modo tale da leggere correttamente il file. Se leggete file creati sullo stesso sistema, potrete essere abbastanza sicuri di non dover specificare l'encoding.

### Aprire un file

Ipotizziamo di avere un file `file.txt` nella stessa directory del nostro script. Ovviamente, siccome nel vostro browser non esiste questo file **i prossimi TRY ME non possono assolutamente funzionare**. Ogni volta che si apre un file, bisogna ricordarsi di chiuderlo prima di temrinare la esecuzione di uno script, oppure utilizzare una funzione che lo apra e lo chiuda al posto nostro (un blocco!)

Una volta aperto il file in lettura, vogliamo leggere i dati (`Float`) che contiene, separati da una tabulazione. Lo possiamo fare con pochissime righe di codice:

```ruby
#!/usr/bin/env ruby

# Aprire un file "file.txt" per leggerlo
# solamente (attributo "r")
file = File.open("file.txt", "r")
# a questo punto la variabile file
# contiene un oggetto che punta direttamente
# a file.txt

# linea per linea? il blocco each_line
data = []
file.each_line_ do |line|
  # line è una stringa che contiene
  # i caratteri contenuti nel file. Da notare
  # possiamo scorrere il file in una unica
  # direzione (non sempre vero...)

  # usiamo su line i metodi delle stringhe
  # per suddividere tutti gli elementi della
  # linea che sono separati dal carattere tab
  line_data = line.split("\t")
  # usiamo map! per convertire tutti gli elementi
  # della linea da String a Float
  line_data.map! { |e| e.to_f }

  # a questo punto line_data contiene tutti float,
  # possiamo accodarlo in data
  data << line_data
end

# Arrivati qui, data sarà un Array
# di dimensione pari al numero di linee
# del file, ogni elemento di data è un Array
# che contiene i dati contenuti sulla linea.

# dobbiamo ricordarci di chiudere il file!
# catastrofe e perdita di dati a chi si dimentica!
file.close

```

Possiamo anche evitare di aprire e chiudere il file, e lasciarlo fare alla libreria, utilizzando `open` come se fosse un blocco (**questo metodo è da preferirsi in quanto più robusto, al fine di proteggere i dati contenuti nei File**)

```ruby
#!/usr/bin/env ruby

data = []

File.open("file.txt", "r") { |file|
  file.each_line { |line|
    line_data = line.split("\t")
    line_data.map! { |e| e.to_f }
    data << line_data
  }
} # <- qui il file viene automaticamente chiuso dal
  #    metodo open
```

Un metodo di livello ancora superiore permette di racchiudere **apertura e iterazione tra le linee** del file in un colpo solo:

```ruby
#!/usr/bin/env ruby

data []

File.foreach("file.txt", "r") { |line|
  line_data = line.split("\t")
  line_data.map! { |e| e.to_f }
  data << line_data
}
```

Altri metodi interessanti per la lettera nei file? A bizzeffe! Controllate la [documentazione][rubyfile]!

### Creare un file

> Non chiudere un file dopo averci scritto dati dentro, nella quasi totalità dei casi, porta alla completa perdita dei dati.

Per aprire un file in scrittura, utilizziamo l'attributo di accesso `"w"` al posto di `"r"`. La classe mette a disposizione un paio di metodi molto comodi di una istanza di oggetto File:

 * `puts`: inserisce una riga di testo e la termina con il carattere di nuova linea
 * `print`: inserisce dei dati nel file senza aggiungere un carattere di fine linea

Per vedere come funzionano, immaginiamo di avere ancora la nostra variabile `data` costruita come `Array` di `Array` di dati, e vogliamo scriverlo in un file:

```ruby
#!/usr/bin/env ruby

data # <- consideratelo un Array di Array
     #    contenente dati da scrivere in un file

File.open("nuovo_file.txt", "w") { |file|
  data.each { |line_data|
    line_data.each { |el|
      file.print "#{el}\t"
    }
    file.puts # <- lo usiamo per scrivere "\n"
  }
} # <- chiusura automatica del file

```

> Cosa succede se "nuovo_file.txt" non esiste nel sistema? Se l'utente che sta eseguendo lo script ha i privilegi necessari per scrivere, viene creato un nuovo file nel filesystem.

## Errori

Con l'introduzione dei file abbiamo dovuto specificare che non chiudere correttamente un file dopo la sua apertura può portare alla perdita irreversibile di dati. Ma può accadere che durante la esecuzione di un programma qualcosa vada storto! Dobbiamo scrivere il nostro codice in modo tale che sia **robusto**, ovvero sia in grado di gestire la sua esecuzione anche in occasione di errori.

### Raise

Quando l'interprete identifica un errore, esegue un `raise` di un errore, specificando la natura dell'errore e nel limite del possibile un messaggio che possa aiutare il programmatore a capire quale è stato l'errore.

### Rescue

In molti casi è necessario gestire tale errore, cercando di recuperare il recuperabile: questo è il caso della keyword `rescue`. Il codice che segue `rescue` è eseguito quando un errore viene sollevato dall'interprete.

### Ensure

In alcuni casi, nostante i vari tentativi di recupero, non è possibile recuperare da tali errori. Ancora non è tutto perduto. Dopo la keyword `ensure` possiamo inserire del codice che verrà eseguito nonostante sia stato generato un errore non recuperabile. Queste linee sono fondamentali per tentare di salvare i risultati dei nostri calcoli fino al punto in cui è stato generato l'errore, e devono essere utilizzati per routine estremamente robuste che sicuramente andranno a buon fine (come ad esempio la chiusura di un file che avevamo aperto, al fine di salvare i dati e non perderli).

### Esempio pratico

#### Sollevare errori!

Supponiamo di scrivere una funzione che esegue una divisione. La funzione deve generare un errore se i due valori inseriti non sono numeri, e se il divisore è nullo:

```ruby

def dividi(dividendo, divisore)
  # Controllo sugli argomenti in ingresso
  raise ArgumentError, "Il dividendo deve essere un numero" if not dividendo.is_a?(Numeric)
  raise ArgumentError, "Il divisore deve essere un numero" if not divisore.is_a?(Numeric)

  # Controllo che il divisore sia diverso da zero
  raise RuntimeError, "Il divisore deve essere diverso da zero" if divisore == 0

  return dividendo/divisore
end
```

Da notare l'introduzione di due tipi diversi di errore:

 * `ArgumentError`: l'errore è sul tipo di argomento passato alla funzione
 * `RuntimeError`: gli argomenti sono corretti, ma quello che contiene uno degli argomenti andrà a generare un errore

Gli errori sono innalzati dall'interprete se e solo se l'`if` postfisso ritorna `true`. Se nessun errore viene generato, la funzione continua con la sua esecuzione classica.

#### Recuperare errori

Proviamo a recuperare l'errore divisione per zero. Molto spesso è sufficiente approssimare il risultato aggiungendo al divisore un $$\epsilon \approx 0$$ per poter continuare con la esecuzione. Recuperiamo la esecuzione con la keyword `rescue`, e poi riproviamo con `retry`:

```ruby

def dividi(dividendo, divisore)
  # Controllo sugli argomenti in ingresso
  raise ArgumentError, "Il dividendo deve essere un numero" if not dividendo.is_a?(Numeric)
  raise ArgumentError, "Il divisore deve essere un numero" if not divisore.is_a?(Numeric)

  # Controllo che il divisore sia diverso da zero
  raise RuntimeError, "Il divisore deve essere diverso da zero" if divisore == 0

  return dividendo/divisore
rescue RuntimeError
  if divisore == 0 then
    divisore += 10**(-15) # il nostro epsilon
    retry                 # riprova ad eseguire la funzione dall'inizio, con
                          # divisore modificato
  end
end
```

#### Assicurare gli errori

Cosa succede se nonstante l'errore dobbiamo comunque assicurarci la esecuzione di alcune righe di codice? Dobbiamo assolutamente inserire `ensure` a fine funzione. Questa porzione di codice è eseguita **sempre**, sia che sia stato lancato un errore, che non lo sia stato lanciato.

```ruby

def dividi(dividendo, divisore)
  # Controllo sugli argomenti in ingresso
  raise ArgumentError, "Il dividendo deve essere un numero" if not dividendo.is_a?(Numeric)
  raise ArgumentError, "Il divisore deve essere un numero" if not divisore.is_a?(Numeric)

  # Controllo che il divisore sia diverso da zero
  raise RuntimeError, "Il divisore deve essere diverso da zero" if divisore == 0

  return dividendo/divisore
rescue RuntimeError
  if divisore == 0 then
    divisore += 10**(-15) # il nostro epsilon
    retry                 # riprova ad eseguire la funzione dall'inizio, con
                          # divisore modificato
  end
ensure
  puts "Righe che devono essere eseguite assolutamente vanno inserite qui!"
end
```

[rubyfile]: http://ruby-doc.org/core-2.2.0/File.html
