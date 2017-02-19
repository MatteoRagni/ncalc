---
layout: post
title:  "Introduzione alla Object Oriented Programming"
date:   2015-02-22 23:00:00
categories: post
permalink: /lecture6/
lecture: "Lezione 6 (teorica)"
---

OOP (Object Oriented Programmming): abbiamo raccolto l'insieme degli strumenti
necessari a lanciarci e capire la programmazione orientata agli oggetti. In
questa lezione (per adesso solo teorica) introduciamo alcuni degli elementi
che ci aiuteranno a capire meglio il linguaggio Ruby, un linguaggio
**puramente orientato agli oggetti**.

* table of contents.
{:toc}

## OOP in generale

Ruby è un linguaggio di programmazione **puramente orientato agli oggetti**.
Il paradigma di [programmazione orientato agli
oggetti][http://it.wikipedia.org/wiki/Programmazione_orientata_agli_oggetti],
detto comunemente OOP, prevede una forma di **astrazione** delle strutture di
dati (delle variabili - accettabile anche se non completamente corretto)
chiamate **classi**. Le singole istanze di questi oggetti sono chiamati
**oggetti**.

Un linguaggio è detto orientato agli oggetti quando permette di sfruttare le
proprietà:

 * [incapsulamento][incap] (separazione interfaccia e implementazione)
 * [ereditarietà][ered] (definire nuove classi usando classi già definite)
 * [polimorfismo][polim] (classi diverse possono condividere la stessa interfaccia)

Ruby è un puramente OO perchè tutte le rappresentazioni interne di dati sono
oggetti.

> In `C++` ad esempio, non tutti i dati sono da considerarsi oggetto. Esistono
> tipologie di dato definite staticamente.

## Tutto bello...

... ma non ci ho capito nulla.

Allora facciamo un esempio pratico per spiegare la OOP, tralasciando la
implementazione effettiva di classi e oggetti nei nostri script, per il
momento.

### Pensate **alle radio**

Se avete pensato alle radio, allora state facendo una astrazione di quelli che
sono gli oggetti radio. Tale astrazione d'ora in avanti la chiameremo **classe
delle Radio**. Pensando all'insieme di tutte le radio possono esservi venuti
in mente caratteristiche quali:

 * il colore la dimensione il peso le bande di ricezione disponibili la
 * lunghezza della antenna etc.

che rappresentano tutte le caratteristiche che puo' avere una radio. Tali
caratteristiche sono detti **attributi**.

Si considera come attributo anche lo **stato** attuale della radio generica
come:
 
 * il valore del volume la frequenza di sintonia se è accesa o spenta etc.

Pensando alle radio potrebbero esservi venute in mente le manopoline per
modificare il volume o ri-sintonizzare la radio. State pensando alle
**interfacce** dei **metodi** della classe, dove per **metodi** intendiamo
tutte le operazioni che ci permettono di modificare lo stato di una radio,
come ad esempio:

 * alzare/abbassare il volume modificare la sintonia accendere/spegnere la
 * radio etc.

mentre per **interfaccia** intendiamo gli strumenti per poter effettivamente
agire sui metodi (manopole, interruttori, etc.).

### Pensate ad **una radio in particolare**

Pensate ad una radio in particolare, ad esempio la radio che di solito è nel
garage, da accendere quando si fa qualche lavoretto sulla macchina per tenere
compagnia.

Quella radio è:

 * nera ha dimensioni `20cm x 40cm x 15cm` pesa `1.5kg` riceve in `AM` ed `FM`
 * la antenna è telescopica e lunga `1m` etc.

e potete:

 * alzare/abbassare il volume con uno slider sulla faccia superiore cambiare
 * la sintonia con la manopola sulla faccia destra accenderla/spegnerla
 * portando il volume al minimo e superando un interruttore a fine corse dello
 * slider

e sicome state leggendo questo post, probabilmente quella radio è in stato
spento.

Questa radio è a tutti gli effetti un **oggetto**, o una **istanza della
classe Radio**. A differenza della classe, che è una astrazione che definisce
unicamente come sono fatte in generale le Radio, la istanza ha stato e
attributi ben definiti, e quindi è unica (possono esistere diverse radio -
diverse istanze, ma non saranno quella del garage, o per lo meno non del
vostro).

Se fino ad ora vi è chiaro, andiamo a capire le proprietà della programmazione
ad oggetti, andiamo a vedere alcune caratteristiche quali l'incapsulamento e
l'ereditarietà

### Pensate ai **circuiti dentro le radio**

Poche persone aprono una radio funzionante per vedere che cosa c'è dentro,
anche se tutti si aspettano di trovarsi una qualche forma di circuito
elettrico che definisce la sintonia, un demodulatore che elimina la portante
per mantenere solo il segnale (detto intelligence), un amplificatore che
amplifica il segnale di intelligence, etc...

Più o meno sappiamo della presenza di tutte queste cose in una radio, ma
difficilmente conosciamo nei minimi particolari lo schema effettivo dei
circuiti, che ci spiega come sono implementate le funzioni di:

 * ricezione 
 * demodulazione 
 * amplificazione
 * etc.

Anche questi sono metodi della classe, ma sono **metodi privati** ovvero
metodi che sono all'interno ma non utilizzabili da fuori, se non facendo uso
dei metodi definiti in precedenza,, che permettono in qualche modo di
**accedere** a tali metodi privati (o volendo anche **attributi privati**).

Qui spieghiamo la proprietà di **incapsulamento**, ovvero la possibilità di
definire **attributi e metodi privati** che definiscono lo stato dell'oggetto.
All'utente finale (detto **client**, chi ascolta la radio) non interessa la
effettiva implementazione dei singoli metodi o conoscere eventuali attributi
interni (circuiti, colore dei fili interni, etc.).

Per il **client** sono sufficienti l'interfaccio (manopole, interruttori,
etc.) e gli attributi esposti (valore del volume da 0 a 100, indicatore di
frequenza di sintonia, etc.).

### Pensate **alle Radio-Sveglie**

Se vi è chiaro il post fino a questo punto, allora avrete già intuito che
stiamo pensando ad una **nuova classe**, simile alla classe Radio, con la
quale condivide gli attributi, i metodi e l'interfaccia, e implementa
qualcosina in più, come la visualizzazione dell'ora e la funzionalità di
sveglia. Quindi oltre agli attributi precedenti avremo:
 
 * attributi del display 
 * ora attuale ora di sveglia 
 * stato della sveglia 
 * etc.

metodi nuovi:

 * imposta ora 
 * imposta sveglia 
 * attiva/disattiva sveglia 
 * etc.

senza contare i metodi e gli attributi privati necessari alla implementazione
effettiva della sveglia. Anche l'interfaccio differisce, avendo aumentato il
numero di metodi pubblici messi a disposizione (bottoni per l'ora,
interruttore per attivare la sveglia, il pulsante - per me - fondamentale di
snooze).

Quindi la classe Radio-Sveglie implementa attributi e metodi della classe
Radio. In questo caso, la OOP permette di fare uso della proprietà di
**ereditarietà**, secondo la quale, piuttosto che re-implementare nuovamente
da zero i metodi, questi possono essere ereditati dalla classe Radio. La nuova
classe deve solo definire i metodi e gli attributi che non sono definiti nella
classe dallla quale ha ereditato.

In questo caso la classe Radio-Sveglie è detta **sotto-classe**, mentre la
classe Radio è la **super-classe**.

### La Radio-Sveglia nel garage

Nulla vieta che quella famosa radio nel garage sia in realtà una radio-
sveglia. Qui sta il **polimorfismo (per inclusione)**, ovvero la possibilità
di _utilizzare istanze di una sotto-classe al posto di una super-classe_, in
quanto la sotto classe ha ereditato la stessa interfaccia della super-classe e
l'ha espansa con metodi e attributi nuovi.

Se la super-classe era sufficiente, allora lo è anche la sotto-classe.

## Le classi che ci interessano

A cosa è servita tutta questa pappardella? Bè, tutti i tipi di dato in ruby sono in qualche modo definti mediante l'utilizzo della OOP e delle sue proprietà. Quindi per introdurre i Tipi di Dato che andremo ad utilizzare più di frequente, una conoscenza della terminologia specifica è fondamentale.

Ecco uno schema sui tipi di dato fondamentali:

<div style="width:100%; text-align:center;">
  <img src="../assets/img/classes.svg" style="width:40%" class="thumbsvm">
  <br><i>Struttura delle classi per i tipi di dato fondamentale (semplificato)</i>
</div>

Analizzeremo quindi le sottoclassi di **Numeric**, ovvero la classe dei numeri interi **Fixnum** e la classe dei numeri reali **Float**.

Passeremo poi alla classe degli **Array**, che sono molto comode nel campo della analisi numerica, e la classe del tipo **Stringa**. In seguito passeremo alla analisi del tipo **Hash**, una sorta di array ordinato per mezzo di chiavi piuttosto che per mezzo di un indice numerico.

### Numeric

La definizione di un numero intero si ottiene mediante l'assegnazione ad una variabile di un numero intero (senza virgola). Quella variabile diventa automaticamente una istanza della classe Fixnum, e risponde a tutte le regole della aritmetica tra interi. 

Un numero reale si definisce per mezzo della assegnazione ad una variabile di un numero con valore decimale o in notazione scientifica. Quella variabile diventa una istanza della classe Float, e risponde a tutte le regole della aritmetica tra numeri reali.

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

# ATTENZIONE! NON FIDATEVI DEL RISULTATO DEL BROWSER
# PROVATO IN UN VERO INTERPRETE!!
puts "c (intero) -> #{c_int}"
puts "C (float)  -> #{c_flt}"
```

Non fidatevi del risultato del browser (che è solo un emulatore), ma valutate il codice precedente in un vero interprete Ruby. Vedrete immediatamente come `c_int != c_flt`!! Questo perchè nella divisione tra interi la operazione di divisione continua a riportare come risultato un valore intero (come è giusto che sia).

Nelle prossime lezioni vedremo una introduzione agli altri tipi di dato, e rafforzeremo la conoscenza e l'uso della sintassi.

[incap]: http://it.wikipedia.org/wiki/Programmazione_orientata_agli_oggetti#Incapsulamento
[ered]: http://it.wikipedia.org/wiki/Programmazione_orientata_agli_oggetti#Ereditariet.C3.A0
[polim]: http://it.wikipedia.org/wiki/Programmazione_orientata_agli_oggetti#Polimorfismo