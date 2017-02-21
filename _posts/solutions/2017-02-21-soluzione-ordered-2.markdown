---
layout: post
title:  "Soluzione Ordered (b)"
categories: post
permalink: /solutions/ordered/b
visible: 0
---

## Soluzione Ordered (b)

```ruby
def ordered(vec)
  # Controlliamo l'input
  # Potrebbe essere fatto in modo più efficiente, inserendo il secondo
  # raise nel for e quindi attraversando l'Array una volta sola per
  # eseguire tutte le operazioni
  raise ArgumentError, "vec deve essere Array" unless vec.is_a? Array
  vec.each do |i|
    raise ArgumentError, "vec deve contenere Numeric" unless i.is_a? Numeric
  end

  # Eseguiamo se il vettore ha più di un elemento
  if vec.size >= 2
    # Inizializzazione delle condizioni possibili
    str_cres, nor_cres, str_decr, nor_decr = true, true, true, true
    for i in 1...vec.size
      if vec[i] > vec[i-1]
        # Non è DECRESCENTE
        str_decr = false
        nor_decr = false
      elsif vec[i] < vec[i-1]
        # Non è CRESCENTE
        str_cres = false
        nor_cres = false
      else
        # Non è STRETTAMENTE crescente/decrescente
        str_decr = false
        str_cres = false      
      end
    end

    return  2 if str_cres
    return -2 if str_decr
    return  1 if nor_cres
    return -1 if nor_decr
  end
  # Non è ordinato o ha meno di 2 elementi
  return 0
end
```
