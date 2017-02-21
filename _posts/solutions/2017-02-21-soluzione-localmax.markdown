---
layout: post
title:  "Soluzione Massimo Locale"
categories: post
permalink: /solutions/localmax
visible: 0
---

## Soluzione Massimo Locale

```ruby
def local_max(vec)
  # Per prima cosa controlliamo che l'input sia un Array
  # di tutti numeri interi.
  raise ArgumentError, "l'argomento deve essere un Array" unless vec.is_a? Array
  vec.each do |i|
    raise ArgumentError, "gli elementi dell'Array devono essere Numeric" unless i.is_a? Numeric
  end
  # Questo controllo poteva essere effettuato anche durante il loop dell'algoritmo per
  # aumentarne la efficienza.

  # Costruiamo un vettore vuoto nel quale salveremo i nostri indici
  # ei massimi locali
  mx = []
  # I massimi locali possono trovarsi solo tra gli elementi in indice
  # 1 e la fine del vettore meno 1 elemento (ovvero non controlliamo
  # gli elementi del vettore vec[0] e vec[-1])
  for i in 1...(vec.size-1)
    # Aggiungiamo l'elemento all'indice se rispetta entrambe le condizioni
    mx << i if (vec[i] > vec[i-1] and vec[i] > vec[i+1])
  end
  # Ritorniamo i vettori di indice
  return mx
end
```
