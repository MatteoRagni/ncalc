---
layout: post
title:  "Soluzione Ordered (c)"
categories: post
permalink: /solutions/ordered/c
visible: 0
---

## Soluzione Ordered (c)

```ruby
def ordered(a)
  # Valutiamo che l'ingresso sia valido
  # per valutare che contenga tutti numeri non usiamo il
  # metodo più efficiente, ma il più semplice
  raise ArgumentError, "a deve essere un Array" unless a.is_a? Array
  a.each do |z|
    raise ArgumentError, "a deve contenere Numeric" unless z.is_a? Numeric
  end

  # Usiamo una soluzione che non è la più efficiente. Salviamo tutte le
  # sequenze crescenti, poi le mettiamo in un hash, valutandone la dimensione
  b = []
  c = [a[0]]
  for i in 1...a.size
    if a[i] > c[-1]
      c << a[i]
    else
      b << c.dup
      c = [a[i]]
    end
  end
  b << c.dup

  # A questo punto c non ci serve più. b è un array di array che sono
  # strettamente decrescenti, contiene anche elementi di dimensione 1
  r = {}
  b.each do |e|
    next if e.size == 1 # scartiamo le dimensioni 1
    r[e.size] = [] unless r.keys.include? e.size # creo la chiave
                                                  # se manca
    r[e.size] << e
  end

  return r
end
```
