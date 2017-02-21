---
layout: post
title:  "Soluzione Sequenze"
categories: post
permalink: /solutions/sequence
visible: 0
---

## Soluzione Sequence

```ruby
def sequence(v)
  # Controlliamo l'ingresso (anche se in modo non efficiente)
  raise ArgumentError, "v deve essere Array" unless v.is_a? Array
  v.each do |z|
    raise ArgumentError, "v deve contenere Numeric" unless z.is_a? Numeric
  end

  r = []
  a, b = 0, 0

  # Cerchiamo le seuquenze come indicato, ma usando questo
  # metodo, che risulta il più semplice, ci ritroviamo con
  # elementi che hanno :begin e :end uguali. Aggiungiamo
  # quindi una condizione che ci permette di evitare questo problema
  for i in 1...v.size
    if (v[i] - v[b]).abs < 2
      b = i
    else
      r << { :begin => a, :end => b } if (b - a >= 2)
      a, b = i, i
    end
  end

  # Ritorniamo il risultato
  return r
end
```
