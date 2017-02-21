---
layout: post
title:  "Soluzione Mix"
categories: post
permalink: /solutions/mix
visible: 0
---

## Soluzione Mix

```ruby
def mix(a, b)
  [a, b].each do |z|
    raise ArgumentError, "input devono essere Array" unless z.is_a? Array
  end

  # Valutiamo quale vettore ha lunghezza maggiore
  l = a.size > b.size ? a.size : b.size
  # Vettore risultante
  r = []
  # Aggiungiamo un alemento da a e da b solo se tali
  # elementi all'indice esistono
  for i in 0...l
    r << a[i] if a[i]
    r << b[i] if b[i]
  end
  # Ritorniamo l'Array mixato
  return r
end
```
