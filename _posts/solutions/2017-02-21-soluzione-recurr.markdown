---
layout: post
title:  "Soluzione Ricorrenza"
categories: post
permalink: /solutions/recurr
visible: 0
---

## Soluzione Ricorrenze

```ruby
def recurr( rec, ini, n )
  # Analizziamo i dati in ingresso. Rec, così come
  # ini è un Array di Numeric, quindi li possiamo analizzare
  # assieme (si potrebbe fare in modo più efficiente, ma per
  # ora facciamo così). n deve essere un Fixnum
  [rec, ini].each do |z|
    raise ArgumentError, "deve essere un Array" unless z.is_a? Array
    z.each { |k| raise ArgumentError, "deve contenere Numeric" unless k.is_a? Numeric }
  end
  raise ArgumentError, "deve essere un Fixnum" unless n.is_a? Fixnum
  # Dobbiamo sollevare un errore anche se la dimensione
  # del vettore di ricorrenza e di inizializzazione sono diverse.
  # Se fossero diverse infatti, ci sarebbe una incongruenza sulla
  # inizializzazione.
  raise ArgumentError, "rec e ini sono di dimensione diversa" unless rec.size == ini.size

  # Completato il check sui dati in ingresso andiamo
  # a costruire la nostra ricorrenza
  y = ini.dup
  q = y.size - 1

  # Questa parte di codice non fa altro che mimare quanto
  # scritto nelle istruzioni
  while q < n
    y[q+1] = 0
    # Questo ciclo for è come una sommatoria:
    # y[q+1] = rec[0] * y[q-0] + ... + rec[rec.size-1] * y[q-rec.size-1]
    for i in 0...rec.size
      y[q+1] += rec[i] * y[q-i]
    end
    # Aggiorniamo la dimensione di q
    q += 1
  end

  # Ritorniamo l'ultimo valore della ricorrenza.
  return y[-1]    
end
```
