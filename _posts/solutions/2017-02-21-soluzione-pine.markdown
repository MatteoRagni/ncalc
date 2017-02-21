---
layout: post
title:  "Soluzione Pine"
categories: post
permalink: /solutions/pine
visible: 0
---

## Soluzione Pine

```ruby
def pine(n)
  # Controlliamo che l'argomento in ingresso sia un numero intero
  raise ArgumentError, "Richiesto un numero in ingresso" unless n.is_a? Fixnum

  # Costruiamo la stringa al contrario: viene più facile anche se meno efficiente
  str = []
  for i in 0...n
    str << " " * i + "*" * ((2 * n - 1) - (2 * i)) + " " * i + "\n"
    # La stringa è formata da:
    #  - i elementi di spazio a sinistra
    #  - per quanto riguarda gli asterischi, sono elementi dispari, che si
    #    raddoppiano ma resi dispari. Ovviamente dobbiamo rimuovere gli spazi
    #    a destra e sinistra
    #  - i elementi di spazio a destra
  end  

  # Ritornimao la stringa (join) dall'Array, che viene prima invertito (reverse)
  return str.reverse.join
end
```
