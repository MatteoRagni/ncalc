---
layout: post
title:  "Soluzione Monotone"
categories: post
permalink: /solutions/monotone
visible: 0
---

## Soluzione Monotone

```ruby
def monotone(v)
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
  # (unless a == b)
  for i in 1...v.size
    if v[i] >= v[b]
      b = i
    else
      r << { :begin => a, :end => b } unless a == b
      a, b = i, i
    end
  end

  # Ritorniamo il risultato
  return r
end
```
