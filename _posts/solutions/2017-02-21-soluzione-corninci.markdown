---
layout: post
title:  "Soluzione Cornici"
categories: post
permalink: /solutions/cornici
visible: 0
---

## Soluzione Cornici

```ruby
def cornice(r, c)
  # Controlliamo gli input. Facciamolo con un ciclo per fare prima :)
  [r, c].each do |i|
    raise ArgumentError, "Argomento deve essere un intero" unless i.is_a? Fixnum
    raise ArgumentError, "Argomento deve essere >= 2" unless i >= 2
  end

  # Usiamo una shortcut per la creazione di un Array con
  # r righe. Ogni elemento dell'Array è inizializzato con
  # una proc, che crea un sotto-Array (colonne) fatto da una
  # String di c elementi spazio " "
  ary = Array.new(r) { " " * c }

  # Costruiamo la parte superiore e inferiore della cornice.
  # Sono uguali,quindi una volta costruita una non dobbiamo fare altro
  # che copiare quella superiore nello spazio di quella inferiore.
  # Usiamo la moltiplicazione tra un carattere e un intero per la
  # ripetizione di '-':
  # '-' * 5 = '-----'
  ary[0] = ary[-1] = '+' + ('-' * (c - 2)) + '+'

  # Ora sistemiamo tutte le lettere nelle altre righe della matrice,
  # dalla 1 (seconda) alla (r - 1) - 1 (penultima).
  # In questo caso stiamo sfruttando l'accesso ad Array sulle String,
  # per facilitarci il compito
  for i in (1...(r - 1))
    ary[i][0] = ary[i][-1] = '|'
  end

  return ary
end
```
