---
layout: post
title:  "Soluzione Cumulative Sum"
categories: post
permalink: /solutions/cumulativesum
visible: 0
---

## Soluzione Cumulative Sum

```ruby
def cumulative_sum(vec)
  # Controlliamo i valori in ingresso della nostra funzione
  # vec deve essere un Array
  # ogni elemento di vec deve essere un Numeric
  # si potrebbe fare in modi più efficienti, ma per adesso va bene così
  raise ArgumentError, "vec deve essere un Array" unless vec.is_a? Array
  vec.each do |i|
    raise ArgumentError, "vec deve contenere Numeric" unless i.is_a? Numeric
  end

  ret = []
  # Ret è il valore che cerrà ritornato
  for i in 0...vec.size
    ret << vec[0]
    # (-1)**1 cambia segno agli elementi dispari
    for j in 1..i
      ret[i] += (-1)**(j) * vec[j]
    end
  end
  return ret
end
```
