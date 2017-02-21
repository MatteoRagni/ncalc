---
layout: post
title:  "Soluzione Grafo"
categories: post
permalink: /solutions/grafo
visible: 0
---

## Soluzione Grafo

```ruby
class Grafo
  def initialize
    # La soluzione più semplice prevede la creazione di una classe
    # che contiene solamente una lista di edges e una lista di vertici
    # Non cerchiamo la soluzione più efficiente ma la soluzione più
    # rapida
    @edges = []
    @vertices = []
  end

  def add(a, b)
    # come sempre per prima cosa controlliamo l'input
    [a, b].each do |v|
      raise ArgumentError, "Vertici sono stringhe" unless v.is_a? String
    end
    # Aggiungiamo i nostri vertici se e solo se la nostra lista
    # li contiene
    [a, b].each do |v|
      @vertices << v unless @vertices.include? v
    end
    # Costruiamo il nostro edge come specificto
    e = {from: a, to: b}
    @edges << e unless @edges.include? e
    # Ritorniamo la istanza alla fine
    return self
  end
  # Gli altri metodi sono estremamente triviali a questo punto
  def get; return @edges; end
  def size; return @edges.size; end
  def getvertex; return @vertices; end

  # L'unico metodo a cui dobbiamo dare un po' di attenzione
  # è il source and sink. Ricostruiamo due Array di from
  # e to partendo dai singoli hash. Poi valutiamo mediante una
  # intersezione dei due set.
  # Una sorgente non rientra nel set di elementi riceventi
  # Un ricevente non rientra nel set di elementi sorgente
  # Aggiungiamo un ulteriore controllo per non avere duplicati
  def source_and_sink
    from, to = [], []

    h = { sources: [], sinks: [] }

    @edges.each do |e|
      from << e[:from]
      to   << e[:to]
    end

    from.each do |f|
      h[:sources] << f unless (to.include?(f) or h[:sources].include?(f))
    end

    to.each do |t|
      h[:sinks] << t unless (from.include?(t) or h[:sinks].include?(t))
    end

    return h
  end
end
```

Esempio d'uso
```ruby
g = Grafo.new # crea una nuova pila

g.add( "a", "b")  # aggiunge l'edge
g.add( "a", "b")  # aggiunge l'edge
g.add( "a", "b")  # aggiunge l'edge
g.add( "a", "b")  # aggiunge l'edge
g.add( "a", "c")  # aggiunge l'edge
g.add( "b", "c")  # aggiunge l'edge
g.add( "c", "b")  # aggiunge l'edge
puts g.getvertex
puts g.get
puts g.source_and_sink
```
