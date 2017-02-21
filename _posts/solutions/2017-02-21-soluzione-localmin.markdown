---
layout: post
title:  "Soluzione Minimi Locali"
categories: post
permalink: /solutions/localmin
visible: 0
---

## Soluzione Minimi Locali

```ruby
def local_min(vec)
  # Per prima cosa controlliamo gli input
  raise ArgumentError, "vec deve essere un Array" unless vec.is_a? Array
  vec.each do |i|
    raise ArgumentError, "vec deve contenere Numeric" unless i.is_a? Numeric
  end

  # Costruiamo l'hash da ritornare e l'indice del minimo
  r = {}
  idx = 0

  # Iteriamo dall'inizio + 1 dell'Array fino alla fine - 1, dove
  # possiamo veramente valutare la posizione dei minimi
  for i in 1...(vec.size - 1)
    if vec[i] < vec[i-1] and vec[i] < vec[i+1] # condizione di minimo
      idx += 1
      r[idx] = vec[(i-1)..(i+1)]
    end
  end
  # Ritorniamo il risultato
  return r
end
```
