---
layout: post
title:  "Soluzione Max Min"
categories: post
permalink: /solutions/maxmin
visible: 0
---

## Soluzione

```ruby
def max_min_soluzione(vec)
  # Per prima cosa controlliamo che l'input sia un Array
  # di tutti numeri interi.
  raise ArgumentError, "l'argomento deve essere un Array" unless vec.is_a? Array
  vec.each do |i|
    raise ArgumentError, "gli elementi dell'Array devono essere Numeric" unless i.is_a? Numeric
  end
  # Questo controllo poteva essere effettuato anche durante il loop dell'algoritmo per
  # aumentarne la efficienza.

  # Inizializziamo l'Hash da ritornare come output
  h = { max: vec[0], min: vec[1] }

  # Continuiamo a esplorare il resto dell'Array
  for i in 2...vec.size
    # Cerchiamo il massimo/minimo negli indici pari/dispari
    if i % 2 == 0
      # assegna un nuovo valore a h[:max] se vec[i] è maggiore di h[:max]
      # sfruttando un operatore ternario che si legge come se fosse:
      #   if h[:max] > vec[i]
      #     h[:max] = h[:max]
      #   else
      #     h[:max] = vec[i]
      #   end
      # oppure
      #   h[:max] = vec[i] if vec[i] > h[:max]
      # Tutti e tre i modi sono corretti.
      h[:max] = (h[:max] > vec[i] ? h[:max] : vec[i])
    else
      h[:min] = (h[:min] < vec[i] ? h[:min] : vec[i])
    end
  end

  return h
end
```
