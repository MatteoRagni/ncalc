---
layout: post
title:  "Prima di cominciare..."
date:   2015-02-07 15:40:50
categories: post
permalink: /lecture1/
lecture: "Lezione 1"
---

... con `Ruby`, dobbiamo prendere confidenza con quelli che sono gli strumenti che utilizzeremo per sviluppare i nostri algoritmi. In questo post parleremo della console e dell'interprete `irb`, che ci accompagneranno nell'arco di questo corso.

* table of contents.
{:toc}

## Questo blog...

... contiene parte di quello che verra' detto a lezione. Non abbiamo tempo di fornire tutto qui, essendo una completa perdita di tempo. Su internet troverete tantissime guide e riferimenti che sono sicuramente piu' completi e formali di quanto possiate trovare qui dentro. Nelle pagine saranno presentati alcuni degli script, e avete la possibilita' (**limitata**) di eseguirli all'interno del browser.

Alcuni riferimenti consigliabili sono:

#### Ruby (in italiano)

 * [Imparare a Programmare in Ruby][ita1]: questo sito contiene un corso online completo per imparare Ruby. Se non bastano le lezioni e le esercitazioni, o comunque qualche concetto è sfuggito questo sito è l'ideale per coprire le lacune. (Fortemente consigliato).
 * [Ruby in Venti Minuti][ita2]: Se partite da 0 non imparare a programmare in 20 minuti. In ogni caso sono ottimi 20 minuti o più da spendere.
 * [Ruby User Guide][ita3]: traduzione italiana da scaricare localmente. Manuale del linguaggio con una panoramica su tutte le sue caratteristiche. Manuale tradotto da: Gianluigi Spagnuolo, Cristiano Macaluso, Massimo Arnaudo, Gabriele Renzi.

#### Ruby (in inglese)

Il punto di riferimento del linguaggio rimane la [**documentazione ufficiale del linguaggio Ruby**][docu] (in inglese), che vi invito a consultare (e ad imparare a consultare).

 * [Ruby Essentials][eng1]: Un ottimo libro online.
 * [The Bastards Book of Ruby][eng2]: Libro on line per imparare Ruby. Non adatto per un neofita ma ottimo come riferimento o per che conosce altri linguaggi di programmazione.
 * [Imparare Ruby in modo interativo][eng3]: serie di lezioni online per imparare Ruby.
 * [Mr. Neighborly's Humble Little Ruby Book][eng4]: Un libro sul linguaggio Ruby.
 * [Little Book Of Ruby][eng5]: Semplice e un po datato sebbene abbastanza approfondito mini-libro sul linguaggio Ruby.
 * [Corso interativo di codecademy][eng6]: Fatto molto bene ma più adatto a chi sa già programmare in qualche altro linguaggio.

#### Linux

 * [Tutorial di base GNU/Linux][linux] con introduzione alla bash e il sistema Linux in generale
 * [Guida avanzata alla scripting bash][bash]: per imparare tutti i segreti dello scripting nella bash (l'interprete tipico di un terminale Linux)

## Il teminale

Il terminale e' uno strumento di altissima utilita', lo useremo per creare file, navigare tra le directory ed eseguire i file `.rb` che conterranno gli script `Ruby`.

Imparare ad utilizzare questo strumento puo' velocizzare il vostro lavoro ordinario. Per motivi di praticita', ci concentriamo sulla console di un sistema `Unix`, in particolare `Linux Ubuntu`, distribuzione installata nelle postazioni di laboratorio.

Potete aprire un terminale tramite il menu `Accessori → Terminale`. Vi si presentera' una schermata attraverso la quale inserire i comandi.
La linea di inserimento (**linea di comando**, preceduta dal **prompt dei comandi**) contiene alcune informazioni utili, se si sanno leggere. Potreste trovare ad esempio:

```
nome.cognome@hostname:~$
```

Ci sono almeno quattro informazioni molto importanti nel **prompt**:

 * `nome.cognome`: rappresenta il nome utente, per gli sbadati... Tale nome e' salvato all'interno della _variabile_ `$USER`, che troveremo qualche volta nei posts.
 * `hostname`: e' il nome del computer dal quale stato lavorando
 * `~`: e' la directory all'interno della quale ci troviamo. Il carattere `~` e' una abbreviazione per la **home**, la directory ppersonale di ogni utente. Solitamente questa si trova nella directory `/home/nome.cognome`, ma oltre la abbreviazione vista prima e' possibile utilizzare la _variabile_ `$HOME`.
 * `$`: siete un utente con privilegi normali (non siete il magnifico e potentissimo `root`, il quale avrebbe il carattere `#`), quindi _non_ potete fare modifiche al sistema che richiedano privilegi di amministratore.


> I comandi sono **case-sensitive**. Fate attenzione a Maiuscole e minuscole.
>
> Anche gli spazi possono essere problematici, quindi cercate di utilizzare nomi per i file e per le directory senza spazi.

> All'interno dei posts, la linea di comando e' preceduta dal carattere:
>
> * `$`: quando sono comandi da inserire come **utente normale**
> * `#`: quando sono comandi da inserire come **super-utente** (richiede privilegi di amministratore, che voi non avete nei computer di laboratorio, per ovvie ragioni).
>
> questi caratteri **non devono essere digitati**, ma li troverete gia' a schermo, e vi aiuteranno a capire con che tipo di utente state lavorando.



I comandi che utilizzeremo sono:

 * `cd`: per cambiare directory
 * `ls`: per visualizzare cosa c'e' all'interno di una directory.
 * `cp` e `mv`: per copiare o muovere un file (praticamente copia e taglia dell'interfaccia).
 * `rm`: per rimuovere un file (o una directory).
 * `chmod`: per cambiare gli attributi di un file, ad esempio renderlo eseguibile.
 * `cat`: per visualizzare il contenuto di un file.
 * `man`: per visualizzare il manuale d'uso di un comando o di un programma.
 * `pwd`: stampa a schermo la directory corrente.

### `cd`: change directory

Ci permette di spostarci da una directory all'altra (le directory sono assimilabili alle _cartelle_ dei sistemi operativi _Windows_). La sintassi del comando e' molto semplice:

```bash
$ cd /home/$USER/Documents/Books
```

Il primo (e unico) argomento rapppresenta la posizione della directory in cui ci vogliamo spostare. Le directory hanno una struttura ad albero, e ogni nodo e' identificato dal carattere `/`.

Nel comando precedente ci siamo spostati dalla directory in cui ci trovavamo alla directory `/home/$USER/Documents`. Questo tipo di spostamento e' detto a **path assoluta**, perche' comincia dalla radice dell'albero, che e' il primo `/` all'inizio della path.

Esistono spostamenti di tipo relativo, ovvero aventi come base di spostamento la directory nella quale ci troviamo. Se ad esempio ci troviamo nella directory `/home/$USER` e volessimo spostarci nella directory `/home/$USER/Documents/Books` con uno spostamento relativo potremmo usare il comando:
```bash
$ cd Documents/Books
```
Fate caso alla assenza della `/` a sinistra della path: questo indica alla console che stiamo effettuando uno spostamento relativo.

Esistono due directory particolari, che troviamo definite ovunque nell'albero delle directory:

 * la directory corrente `.`
 * la directory precedente `..`

Se ci troviamo nella directory `/home/$USER/Documents/Books` e vogliamo andare nella directory `/home/$USER/Documents` mediante uno spostamento relativo, possiamo utilizzare il comando:
```bash
$ cd ..
```

> Il comando `cd` senza argomenti effettua sempre uno spostamento nella directory `/home/$USER`, ovvero vi riporta sempre a casa...

> Non potete spostarvi in tutte le directory a vostro piacimento! Ad esempio non potete andare dentro le _home_ di altri utenti.

### `ls`: list

Mostra la lista dei file e delle directory contenuti nella directory specificata come argomento (o nella directory corrente, come nell'esempio qui sotto).

```bash
$ ls
```

### `cp` e `mv`: copy e move

Sono comandi molto simili, e a livello logico l'equivalente di copia e incolla della interfaccia grafica di ogni moderno sistema operativo:
```bash
$ cp origine.txt /home/$USER/Documents/destinazione.txt
```
esegue la copia di un file, `origine.txt`, presente nella directory corrente (specificato mediante una _path relativa_) nella posizione `/home/$USER/Documents/destinazione.txt` (quindi specificato mediante path assoluta). Ovviamente, il nuovo file copiato avra' come nome `destinazione.txt`.

Per poter copiare intere directory e' necessiaro utilizzare la opzione `-r`

```bash
$ mv origine.txt /home/$USER/Documents/destinazione.txt
```
sposta `origine.txt`, presente nella directory corrente (specificato mediante una _path relativa_) nella posizione `/home/$USER/Documents/destinazione.txt` (quindi specificato mediante path assoluta). Ovviamente, il nuovo file avra' come nome `destinazione.txt`.

Per poter spostare intere directory e' necessiaro utilizzare la opzione `-r`, ad esempio

```bash
$ mv -r $HOME/origine $HOME/destinazione
```

> `mv` puo' essere utilizzato anche per rinominare i file, ad esempio: `mv old.rb new.rb`.

> Per copiare o spostare file/directory

### `rm`: remove

`rm` rimuove un file, sempre che l'utente abbia i permessi per poterlo fare. Per poter rimuovere intere directory e tutto il loro contenuto e' necessario usare la opzione `-rf`.

Ad esempio per rimuovere la directory `bad_directory`:
```bash
$ rm -rf ./bad_directory
```

### `chmod`: change mode

Questo comando ci servira' per rendere i nostri script **eseguibili**, ad esempio:
```bash
$ chmod +x primo_script.rb
```
In questo modo potremmo avviare direttamente lo script (se correttamente scritto) senza doverlo specificare come argomento dell'interprete `Ruby`.

Non approfondiamo ulteriormente lo scopo del comando `chmod`.

### `man`: manual

Uno dei comandi piu' importanti della lista. Specificare `man` seguito da un comando (o da un programma) apre una pagina del manuale, nel quale e' spiegato, in modo dettagliato:

 * sintassi del comando
 * opzioni e loro utilizzo
 * eventuali comandi correlati e o posizione dei file di configurazione

La maggior parte dei comandi espone delle flag specifiche per ottenere un aiuto rapido (e piu' conciso del manuale), specificando `-h` e `--help`. Ad esempio:
```bash
$ rm -h
```
stampa a schermo una descrizione e l'uso del comando remove.

### L'interprete interattivo di Ruby `irb`

Il pacchetto di installazione di `Ruby` mette a disposizione un interprete interattivo. L'inserimento del codice avviene una riga alla volta, e l'interprete restituisce a schermo la rappresentazione interna di tale inserimento. Per avviarlo:
```bash
$ irb
```
il prompt dovrebbe cambiare in:
```bash
irb(main):001:1>
```


[ita1]: http://corsorubyonrails.com/imparare-a-programmare/
[ita2]: https://www.ruby-lang.org/it/documentation/quickstart/
[ita3]: http://ruby-it.org/rug_it.zip
[eng1]: http://www.techotopia.com/index.php/Ruby_Essentials
[eng2]: http://ruby.bastardsbook.com/
[eng3]: http://tryruby.org/levels/1/challenges/0
[eng4]: http://www.humblelittlerubybook.com/book/hlrb.pdf
[eng5]: http://www.sapphiresteel.com/IMG/pdf/LittleBookOfRuby.pdf
[eng6]: http://www.codecademy.com/tracks/ruby
[linux1]: https://www.debian.org/doc/manuals/debian-reference/ch01.it.html
[bash]: http://www.pluto.it/files/ildp/guide/abs/
[docu]: http://www.ruby-doc.org/
